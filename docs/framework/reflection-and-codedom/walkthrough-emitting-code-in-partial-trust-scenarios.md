---
title: "Walkthrough: Emitting Code in Partial Trust Scenarios | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "reflection emit, anonymously hosted dynamic methods"
  - "partial trust, reflection"
  - "partial trust, emitting dynamic methods"
  - "reflection emit, partial trust scenarios"
  - "anonymously hosted dynamic methods [.NET Framework]"
  - "emitting dynamic assemblies,partial trust scenarios"
  - "reflection emit, dynamic methods"
  - "dynamic methods"
ms.assetid: c45be261-2a9d-4c4e-9bd6-27f0931b7d25
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Walkthrough: Emitting Code in Partial Trust Scenarios
Reflection emit utilizza le stesse API impostate in attendibilità totale o parziale, ma alcune funzionalità richiedono autorizzazioni speciali per il codice parzialmente attendibile.  Inoltre, reflection emit presenta una funzionalità, metodi dinamici ospitati anonimamente, progettati per essere utilizzati in scenari di attendibilità parziale e dagli assembly SecurityTransparent.  
  
> [!NOTE]
>  Prima di [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)], l'emissione di codice richiedeva <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  Questa autorizzazione è inclusa per impostazione predefinita nei set di autorizzazioni denominati `FullTrust` e `Intranet`, ma non nel set di autorizzazioni `Internet`.  Di conseguenza, una libreria può essere utilizzata con attendibilità parziale solo se dispone dell'attributo <xref:System.Security.SecurityCriticalAttribute> ed esegue un metodo <xref:System.Security.PermissionSet.Assert%2A> per <xref:System.Security.Permissions.ReflectionPermissionFlag>.  Tali librerie richiedono un'accurata revisione della sicurezza perché eventuali errori nel codice potrebbero comportare problemi di sicurezza.  [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] consente l'emissione di codice in scenari di attendibilità parziale senza alcuna richiesta di sicurezza, in quanto la generazione di codice non è, per sua natura, un'operazione privilegiata.  In altre parole, il codice generato dispone delle stesse autorizzazioni dell'assembly di emissione.  Questo consente alle librerie che generano il codice di essere security transparent ed elimina la necessità di asserire <xref:System.Security.Permissions.ReflectionPermissionFlag>, in modo tale che la scrittura di una libreria protetta non richieda una revisione della sicurezza così approfondita.  
  
 In questa procedura dettagliata vengono illustrate le attività seguenti:  
  
-   [Configurazione di una sandbox semplice per il test di codice parzialmente attendibile](#Setting_up).  
  
    > [!IMPORTANT]
    >  Si tratta di un modo semplice per sperimentare il codice in un contesto di attendibilità parziale.  Per eseguire codice realmente proveniente da percorsi non attendibili, vedere [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
-   [Esecuzione di codice nei domini applicazione parzialmente attendibili](#Running_code).  
  
-   [Utilizzo di metodi dinamici ospitati anonimamente per generare ed eseguire codice in attendibilità parziale](#Using_methods).  
  
 Per ulteriori informazioni sulla generazione di codice in scenari di attendibilità parziale, vedere [Security Issues in Reflection Emit](../../../docs/framework/reflection-and-codedom/security-issues-in-reflection-emit.md).  
  
 Per un elenco completo del codice illustrato in queste procedure, vedere la [sezione Esempio](#Example) alla fine di questa procedura dettagliata.  
  
<a name="Setting_up"></a>   
## Impostazione di percorsi parzialmente attendibili  
 Nelle due procedure descritte di seguito viene illustrato come configurare percorsi dai quali sia possibile eseguire il test di codice con attendibilità parziale.  
  
-   Nella prima procedura viene descritto come creare un dominio applicazione sandbox nel quale vengono concesse al codice autorizzazioni Internet.  
  
-   Nella seconda procedura viene descritto come aggiungere <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> a un dominio applicazione parzialmente attendibile per consentire l'accesso ai dati privati negli assembly di pari o inferiore attendibilità.  
  
### Creazione di domini dell'applicazione mediante sandbox  
 Per creare un dominio applicazione nel quale gli assembly siano in esecuzione con attendibilità parziale è necessario specificare l'insieme di autorizzazioni da concedere agli assembly utilizzando l'overload di metodo [AppDomain.CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=fullName>.  Il modo più semplice per specificare la concessione è recuperare una concessione denominata dai criteri di sicurezza.  
  
 Nella procedura descritta di seguito viene creato un dominio applicazione mediante sandbox che esegue il codice con attendibilità parziale, per testare scenari in cui il codice generato può accedere solo a membri pubblici di tipi pubblici.  In una procedura successiva viene mostrato come aggiungere <xref:System.Security.Permissions.ReflectionPermissionFlag>, per testare scenari in cui il codice generato può accedere a tipi e membri non pubblici in assembly che dispongono di autorizzazioni uguali o inferiori.  
  
##### Per creare un dominio applicazione con attendibilità parziale  
  
1.  Creare un set di autorizzazioni da concedere agli assembly nel dominio applicazione sandbox.  In questo caso, viene utilizzato il set di autorizzazioni dell'area Internet.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#2)]
     [!code-vb[HowToEmitCodeInPartialTrust#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#2)]  
  
2.  Creare un oggetto <xref:System.AppDomainSetup> per inizializzare il dominio applicazione con un percorso dell'applicazione.  
  
    > [!IMPORTANT]
    >  Per semplificare, in questo esempio di codice viene utilizzata la cartella corrente.  Per eseguire codice realmente proveniente da Internet, utilizzare una cartella separata per il codice non attendibile, come descritto in [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#3)]
     [!code-vb[HowToEmitCodeInPartialTrust#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#3)]  
  
3.  Creare il dominio applicazione, specificando le informazioni di configurazione del dominio e il set di concessioni per tutti gli assembly eseguiti nel dominio.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#5)]
     [!code-vb[HowToEmitCodeInPartialTrust#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#5)]  
  
     L'ultimo parametro dell'overload del metodo [AppDomain.CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=fullName> consente di specificare un insieme di assembly che devono essere concessi in attendibilità totale, invece della concessione del dominio applicazione.  Non è necessario specificare gli assembly [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] utilizzati dall'applicazione, perché si trovano nella Global Assembly Cache.  Gli assembly della Global Assembly Cache sono sempre completamente attendibili.  È possibile utilizzare questo parametro per specificare assembly con nome non sicuro che non si trovano nella Global Assembly Cache.  
  
### Aggiunta di RestrictedMemberAccess ai domini creati mediante sandbox  
 Le applicazioni host possono consentire a metodi dinamici ospitati anonimamente di accedere ai dati privati in assembly con livelli di attendibilità uguali o inferiori al livello di attendibilità dell'assembly che genera il codice.  Per attivare la possibilità limitata di ignorare i controlli di visibilità Just\-In\-Time \(JIT\) l'applicazione host aggiunge un oggetto <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> \(RMA\) alla concessione.  
  
 Ad esempio, un host potrebbe concedere alle applicazioni Internet autorizzazioni Internet più RMA, in modo che un'applicazione Internet possa generare codice che accede a dati privati nei propri assembly.  Poiché l'accesso è limitato agli assembly di attendibilità uguale o inferiore, un'applicazione Internet non può accedere a membri di assembly di attendibilità totale ad esempio gli assembly di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
> [!NOTE]
>  Per impedire l'aumento dei privilegi, quando vengono costruiti i metodi dinamici ospitati anonimamente, vengono incluse le informazioni sullo stack per l'assembly che genera.  Quando viene chiamato il metodo, vengono verificate le informazioni sullo stack.  Pertanto, un metodo dinamico ospitato anonimamente richiamato da codice di attendibilità totale è ancora limitato al livello di attendibilità dell'assembly che genera.  
  
##### Per creare un dominio applicazione con attendibilità parziale più RMA  
  
1.  Creare un nuovo oggetto <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag> \(RMA\) e utilizzare il metodo <xref:System.Security.PermissionSet.SetPermission%2A?displayProperty=fullName> per aggiungere l'autorizzazione al set di concessioni.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#7)]
     [!code-vb[HowToEmitCodeInPartialTrust#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#7)]  
  
     Il metodo <xref:System.Security.PermissionSet.AddPermission%2A> consente di aggiungere l'autorizzazione alla concessione, se non è già inclusa.  Se l'autorizzazione è già inclusa nella concessione, i flag specificati vengono aggiunti all'autorizzazione esistente.  
  
    > [!NOTE]
    >  RMA è una funzionalità di metodi dinamici ospitati anonimamente.  Quando i metodi dinamici comuni ignorano i controlli di visibilità JIT, il codice emesso richiede attendibilità totale.  
  
2.  Creare il dominio applicazione specificando le informazioni di configurazione del dominio e il set di concessioni.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#8)]
     [!code-vb[HowToEmitCodeInPartialTrust#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#8)]  
  
<a name="Running_code"></a>   
## Esecuzione di codice nei domini applicazione creati mediante sandbox  
 Nella procedura descritta di seguito viene illustrato come definire una classe utilizzando metodi eseguibili in un dominio applicazione, come creare un'istanza della classe nel dominio e come eseguire i relativi metodi.  
  
#### Per definire ed eseguire un metodo in un dominio applicazione  
  
1.  Definire una classe che deriva da <xref:System.MarshalByRefObject>.  In tal modo sarà possibile creare istanze della classe negli altri domini applicazione e fare chiamate al metodo attraverso limiti del dominio applicazione.  In questo esempio la classe è denominata `Worker`.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#10)]
     [!code-vb[HowToEmitCodeInPartialTrust#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#10)]  
  
2.  Definire un metodo pubblico che contiene il codice da eseguire.  In questo esempio, il codice genera un semplice metodo dinamico, crea un delegato per eseguire il metodo e richiama il delegato.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#11)]
     [!code-vb[HowToEmitCodeInPartialTrust#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#11)]  
  
3.  Nel programma principale, ottenere il nome visualizzato dell'assembly.  Questo nome viene utilizzato quando si creano istanze della classe `Worker` nel dominio applicazione creato mediante sandbox.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#14)]
     [!code-vb[HowToEmitCodeInPartialTrust#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#14)]  
  
4.  Nel programma principale, creare un dominio applicazione mediante sandbox, come descritto nella [prima procedura](#Setting_up) di questa procedura dettagliata.  Non è necessario aggiungere autorizzazioni al set di autorizzazioni `Internet` impostato, perché il metodo `SimpleEmitDemo` utilizza solo metodi pubblici.  
  
5.  Nel programma principale, creare un'istanza della classe `Worker` nel dominio applicazione creato mediante sandbox.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#12)]
     [!code-vb[HowToEmitCodeInPartialTrust#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#12)]  
  
     Il metodo <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> crea l'oggetto nel dominio applicazione di destinazione e restituisce un proxy che può essere utilizzato per chiamare le proprietà e i metodi dell'oggetto.  
  
    > [!NOTE]
    >  Se questo codice viene utilizzato in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], è necessario modificare il nome della classe per includere lo spazio dei nomi.  Per impostazione predefinita, lo spazio dei nomi rappresenta il nome del progetto.  Ad esempio, se il progetto è "PartialTrust", il nome della classe deve essere "PartialTrust.Worker".  
  
6.  Aggiungere codice per chiamare il metodo `SimpleEmitDemo`.  La chiamata viene sottoposta a marshalling attraverso il limite del dominio applicazione e il codice viene eseguito nel dominio applicazione creato mediante sandbox.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#13)]
     [!code-vb[HowToEmitCodeInPartialTrust#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#13)]  
  
<a name="Using_methods"></a>   
## Utilizzo di metodi dinamici ospitati anonimamente  
 I metodi dinamici ospitati anonimamente sono associati a un assembly trasparente fornito dal sistema.  Il codice in essi contenuto è quindi trasparente.  I metodi dinamici comuni, per contro, devono essere associati a un modulo esistente \(specificato direttamente o derivato da un tipo associato\) e assumono il livello di sicurezza da tale modulo.  
  
> [!NOTE]
>  L'unico modo per associare un metodo dinamico all'assembly che fornisce hosting anonimo è utilizzare i costruttori descritti nella procedura riportata di seguito.  Non è possibile specificare in modo esplicito un modulo nell'assembly di hosting anonimo.  
  
 I metodi dinamici comuni hanno accesso ai membri interni del modulo ai quali sono associati, o ai membri privati del tipo a cui sono associati.  I metodi dinamici ospitati anonimamente sono isolati da codice diverso, pertanto non hanno accesso ai dati privati.  Tuttavia, hanno una possibilità limitata di ignorare i controlli di visibilità JIT per accedere ai dati privati.  Questa possibilità è limitata agli assembly con livelli di attendibilità uguali o inferiori al livello di attendibilità dell'assembly che genera il codice.  
  
 Per impedire l'aumento dei privilegi, quando vengono costruiti i metodi dinamici ospitati anonimamente, vengono incluse le informazioni sullo stack per l'assembly che genera.  Quando viene chiamato il metodo, vengono verificate le informazioni sullo stack.  Un metodo dinamico ospitato anonimamente richiamato da codice di attendibilità totale è ancora limitato al livello di attendibilità dell'assembly che lo ha generato.  
  
#### Per utilizzare metodi dinamici ospitati anonimamente  
  
-   Creare un metodo dinamico ospitato anonimamente utilizzando un costruttore che non specifica un modulo o un tipo associato.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#15)]
     [!code-vb[HowToEmitCodeInPartialTrust#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#15)]  
  
     Se un metodo dinamico ospitato anonimamente utilizza solo tipi e metodi pubblici, non richiede accesso limitato al membro e non deve ignorare i controlli di visibilità di JIT.  
  
     Per generare un metodo dinamico non sono necessarie autorizzazioni speciali, ma il codice generato richiede le autorizzazioni obbligatorie per i tipi e i metodi che utilizza.  Ad esempio, se il codice generato chiama un metodo che accede a un file, richiede <xref:System.Security.Permissions.FileIOPermission>.  Se il livello di attendibilità non include tale autorizzazione, viene generata un'eccezione di sicurezza quando il codice generato viene eseguito.  Il codice illustrato genera un metodo dinamico che utilizza solo il metodo <xref:System.Console.WriteLine%2A?displayProperty=fullName>.  Pertanto, il codice può essere eseguito da percorsi parzialmente attendibili.  
  
-   In alternativa, creare un metodo dinamico ospitato anonimamente con possibilità limitata di ignorare i controlli di visibilità JIT, utilizzando il costruttore [DynamicMethod\(String, Type, Type\<xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%2CSystem.Boolean%29> e specificando `true` per il parametro `restrictedSkipVisibility`.  
  
     [!code-csharp[HowToEmitCodeInPartialTrust#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#16)]
     [!code-vb[HowToEmitCodeInPartialTrust#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#16)]  
  
     La limitazione consiste nel fatto che il metodo dinamico ospitato anonimamente può accedere ai dati privati solo in assembly con livelli di attendibilità uguali o inferiori al livello di attendibilità dell'assembly che genera il codice.  Ad esempio, se il metodo dinamico viene eseguito con attendibilità Internet, può accedere ai dati privati in altri assembly eseguiti anch'essi con attendibilità Internet, ma non ai dati privati in assembly di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Gli assembly di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] vengono installati nella Global Assembly Cache e sono sempre completamente attendibili.  
  
     I metodi dinamici ospitati anonimamente possono utilizzare questa possibilità limitata per ignorare i controlli di visibilità JIT solo se l'applicazione host concede autorizzazioni <xref:System.Security.Permissions.ReflectionPermission> con il flag <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName>.  La richiesta di questa autorizzazione viene fatta quando viene richiamato il metodo.  
  
    > [!NOTE]
    >  Quando viene costruito un metodo dinamico, vengono incluse le informazioni dello stack di chiamate dell'assembly che lo genera.  Pertanto, la richiesta viene fatta per le autorizzazioni dell'assembly che genera anziché per l'assembly che richiama il metodo.  In tal modo si evita che il codice generato venga eseguito con autorizzazioni elevate.  
  
     Nell'[esempio di codice completo](#Example) alla fine di questa procedura dettagliata vengono illustrati l'utilizzo e le limitazioni di accesso al membro.  La classe `Worker` include un metodo che può creare metodi dinamici ospitati anonimamente con o senza la possibilità limitata di ignorare controlli di visibilità. Nell'esempio viene illustrato il risultato dell'esecuzione di tale metodo in domini applicazione con livelli di attendibilità diversi.  
  
    > [!NOTE]
    >  La possibilità limitata di ignorare i controlli di visibilità è una funzionalità di metodi dinamici ospitati anonimamente.  Quando i metodi dinamici comuni ignorano i controlli di visibilità JIT, richiedono la concessione dell'attendibilità totale.  
  
<a name="Example"></a>   
## Esempio  
  
### Descrizione  
 Nell'esempio di codice riportato di seguito viene illustrato l'utilizzo del flag <xref:System.Security.Permissions.ReflectionPermissionFlag> per consentire ai metodi dinamici ospitati anonimamente di ignorare i controlli di visibilità JIT, ma solo quando il membro di destinazione è a un livello di attendibilità uguale o inferiore a quello dell'assembly che genera il codice.  
  
 Nell'esempio viene definita una classe `Worker` di cui può essere effettuato il marshalling attraverso limiti del dominio applicazione.  La classe ha due overload di metodi `AccessPrivateMethod` che generano ed eseguono metodi dinamici.  Il primo overload genera un metodo dinamico che chiama il metodo privato `PrivateMethod` della classe `Worker` e può generare il metodo dinamico con o senza controlli di visibilità JIT.  Il secondo overload genera un metodo dinamico che accede alla proprietà `internal` \(proprietà`Friend` in Visual Basic\) della classe <xref:System.String>.  
  
 Nell'esempio viene utilizzato un metodo di supporto per creare un set di concessioni limitato alle autorizzazioni `Internet`, quindi viene creato un dominio applicazione utilizzando l'overload del metodo [AppDomain.CreateDomain\(String, Evidence, AppDomainSetup, PermissionSet, StrongName\<xref:System.AppDomain.CreateDomain%28System.String%2CSystem.Security.Policy.Evidence%2CSystem.AppDomainSetup%2CSystem.Security.PermissionSet%2CSystem.Security.Policy.StrongName%5B%5D%29?displayProperty=fullName> per specificare che tutto il codice eseguito nel dominio utilizza questo set di concessioni.  Nell'esempio viene creata un'istanza della classe `Worker` nel dominio applicazione e viene eseguito il metodo `AccessPrivateMethod` due volte.  
  
-   La prima volta che viene eseguito il metodo `AccessPrivateMethod` vengono applicati i controlli di visibilità JIT.  Il metodo dinamico ha esito negativo quando viene richiamato, perché i controlli di visibilità JIT gli impediscono di accedere al metodo privato.  
  
-   La seconda volta che viene eseguito il metodo `AccessPrivateMethod` i controlli di visibilità JIT vengono ignorati.  Il metodo dinamico ha esito negativo quando viene compilato, perché la concessione `Internet` non è sufficiente per ignorare i controlli di visibilità.  
  
 Nell'esempio, <xref:System.Security.Permissions.ReflectionPermission> con <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> viene aggiunto al set di concessioni.  Nell'esempio viene creato quindi un secondo dominio, specificando che tutto il codice eseguito nel dominio possiede le autorizzazioni del nuovo set.  Nell'esempio viene creata un'istanza della classe `Worker` nel nuovo dominio applicazione e vengono eseguiti entrambi gli overload del metodo `AccessPrivateMethod`.  
  
-   Viene eseguito il primo overload del metodo `AccessPrivateMethod` e i controlli di visibilità JIT vengono ignorati.  Il metodo dinamico compila ed esegue correttamente, perché l'assembly che genera il codice corrisponde all'assembly che contiene il metodo privato.  Pertanto, i livelli di attendibilità sono uguali.  Se l'applicazione che contiene la classe `Worker` ha molti assembly, lo stesso processo riuscirebbe per uno qualsiasi di tali assembly, perché sarebbero tutti allo stesso livello di attendibilità.  
  
-   Viene eseguito il secondo overload del metodo `AccessPrivateMethod` e i controlli di visibilità JIT vengono di nuovo ignorati.  Questa volta il metodo dinamico ha esito negativo quando viene compilato, perché tenta di accedere alla proprietà `internal` `FirstChar` della classe <xref:System.String>.  L'assembly che contiene la classe <xref:System.String> è totalmente attendibile.  Pertanto dispone di un livello di attendibilità superiore a quello dell'assembly che genera il codice.  
  
 Nel confronto viene illustrato come <xref:System.Security.Permissions.ReflectionPermissionFlag?displayProperty=fullName> consente a codice parzialmente attendibile di ignorare i controlli di visibilità per altro codice parzialmente attendibile senza compromettere la sicurezza del codice attendibile.  
  
### Codice  
 [!code-csharp[HowToEmitCodeInPartialTrust#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/cs/source.cs#1)]
 [!code-vb[HowToEmitCodeInPartialTrust#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEmitCodeInPartialTrust/vb/source.vb#1)]  
  
## Compilazione del codice  
  
-   Se si compila questo esempio di codice in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], è necessario modificare il nome della classe per includere lo spazio dei nomi quando la si passa al metodo <xref:System.AppDomain.CreateInstanceAndUnwrap%2A>.  Per impostazione predefinita, lo spazio dei nomi rappresenta il nome del progetto.  Ad esempio, se il progetto è "PartialTrust", il nome della classe deve essere "PartialTrust.Worker".  
  
## Vedere anche  
 [Security Issues in Reflection Emit](../../../docs/framework/reflection-and-codedom/security-issues-in-reflection-emit.md)   
 [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md)