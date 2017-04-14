---
title: "Securing Wrapper Code | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "security [.NET Framework], wrapper code"
  - "wrapper code, securing"
  - "secure coding, wrapper code"
  - "code security, wrapper code"
ms.assetid: 1df6c516-5bba-48bd-b450-1070e04b7389
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Securing Wrapper Code
Il codice wrapper, soprattutto dove il wrapper ha un'attendibilità più elevata del codice che lo usa, può creare una combinazione univoca di punti di debolezza nella sicurezza. Tutte le operazioni eseguite per conto di un chiamante, in cui le autorizzazioni limitate del chiamante non sono incluse nel controllo di sicurezza appropriato, sono un potenziale punto di debolezza da sfruttare.  
  
 Non abilitare mai tramite il wrapper nulla che il chiamante non possa abilitare manualmente. L'esecuzione di operazioni con un controllo di sicurezza limitato comporta un grave rischio, al contrario di una richiesta di percorso stack completo. Con i controlli dei livelli singoli, se si interpone il codice wrapper tra il vero chiamante e l'elemento API in questione, il controllo di sicurezza potrebbe facilmente avere esito positivo quando non dovrebbe, indebolendo in tal modo la sicurezza.  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta. Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
## Delegati  
 La sicurezza dei delegati è diversa a seconda della versione di .NET Framework.  Questa sezione descrive i diversi comportamenti dei delegati e le relative considerazioni sulla sicurezza.  
  
### Nelle versioni 1.0 e 1.1 di .NET Framework  
 Le versioni 1.0 e 1.1 di .NET Framework eseguono le seguenti azioni di sicurezza su un creatore del delegato e un chiamante del delegato.  
  
-   Quando viene creato un delegato, le richieste di collegamento sicurezza per il metodo destinazione delegato vengono eseguite sul set di concessioni del creatore del delegato.  Se si verifica un errore nell'azione di sicurezza, viene generata un'eccezione <xref:System.Security.SecurityException>.  
  
-   Quando il delegato viene richiamato, vengono eseguite le eventuali richieste di sicurezza esistenti per il chiamante del delegato.  
  
 Quando il codice accetta un <xref:System.Delegate> da un codice considerato meno attendibile che potrebbe chiamarlo, assicurarsi di non consentire al codice considerato meno attendibile di eseguire l'escalation delle autorizzazioni. Se si accetta un delegato e lo si usa in un secondo momento, il codice che ha creato il delegato non è nello stack di chiamate e le autorizzazioni non verranno testate se il codice dentro o sotto il delegato tenta di eseguire un'operazione protetta. Se il proprio codice e il codice del chiamante hanno privilegi più elevati di quelli del creatore, il creatore può orchestrare il percorso di chiamate senza far parte dello stack di chiamate.  
  
### Nelle versioni 2.0 e successive di .NET Framework  
 Diversamente dalle versioni precedenti, la versione 2.0 di .NET Framework esegue l'azione di sicurezza sul creatore del delegato quando il delegato viene creato e chiamato.  
  
-   Quando viene creato un delegato, le richieste di collegamento sicurezza per il metodo destinazione delegato vengono eseguite sul set di concessioni del creatore del delegato.  Se si verifica un errore nell'azione di sicurezza, viene generata un'eccezione <xref:System.Security.SecurityException>.  
  
-   Anche il set di concessioni del creatore del delegato viene acquisito durante la creazione del delegato e archiviato con il delegato.  
  
-   Quando il delegato viene richiamato, il set di concessioni acquisito del creatore del delegato viene prima confrontato con eventuali richieste nel contesto corrente se il creatore e il chiamante del delegato appartengono ad assembly diversi.  Vengono poi eseguite eventuali richieste di sicurezza esistenti per il chiamante del delegato.  
  
## Richieste di collegamento e wrapper  
 Un particolare caso di protezione con richieste di collegamento è stato rafforzato nell'infrastruttura di sicurezza, ma è ancora una possibile fonte di vulnerabilità nel codice.  
  
 Se un codice completamente attendibile chiama una proprietà, un evento o un metodo protetto da un oggetto [LinkDemand](../../../docs/framework/misc/link-demands.md), la chiamata ha esito positivo se il controllo dell'autorizzazione **LinkDemand** per il chiamante viene soddisfatto. Inoltre, se il codice completamente attendibile espone una classe che accetta il nome di una proprietà e chiama la funzione di accesso **get** usando la reflection, la chiamata alla funzione di accesso **get** ha esito positivo anche se il codice utente non dispone del diritto di accesso a questa proprietà. Questo accade perché **LinkDemand** controlla solo il chiamante immediato, che è il codice completamente attendibile. In pratica, il codice completamente attendibile effettua una chiamata con privilegi per conto del codice utente senza verificare che il codice utente disponga del diritto per eseguire la chiamata.  
  
 Per evitare tali problemi di sicurezza, Common Language Runtime estende il controllo a una richiesta di percorso stack completo per tutte le chiamate indirette a un metodo, un costruttore, una proprietà o un evento protetto da **LinkDemand**. Questa protezione comporta costi in termini di prestazioni e richiede modifiche alla semantica del controllo di sicurezza. La richiesta di percorso stack completo potrebbe non riuscire se viene superato il più rapido controllo di un solo livello.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], il codice parzialmente attendibile è stato ridefinito come codice Transparent. Il modello di trasparenza crea una barriera tra il codice autorizzato a eseguire operazioni privilegiate \(codice Critical\), ad esempio chiamare codice nativo, e il codice che non dispone di tale autorizzazione \(codice Transparent\). La trasparenza sostituisce l'uso di <xref:System.Security.Permissions.SecurityAction> per l'attendibilità totale per poter identificare il codice completamente attendibile con <xref:System.Security.SecurityCriticalAttribute>. Per altre informazioni su questa e altre modifiche, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
## Wrapper di caricamento assembly  
 Diversi metodi usati per caricare il codice gestito, tra cui <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>, caricano gli assembly con l'evidenza del chiamante. Se si esegue il wrapping di uno di questi metodi, il sistema di sicurezza potrebbe usare le autorizzazioni del codice, invece delle autorizzazioni del chiamante del wrapper, per caricare gli assembly. Non è consigliabile consentire al codice considerato meno attendibile di caricare codice a cui sono state concesse autorizzazioni più elevate di quelle del chiamante del wrapper.  
  
 In questo modo il codice con attendibilità totale o con un'attendibilità considerevolmente maggiore di quella di un potenziale chiamante \(incluso un chiamante con livello di autorizzazioni per Internet\) potrebbe indebolire la sicurezza. Se il codice dispone di un metodo pubblico che accetta una matrice di byte e la passa ad **Assembly.Load**, creando così un assembly per conto del chiamante, potrebbe violare la sicurezza.  
  
 Questo problema si verifica con gli elementi API seguenti:  
  
-   <xref:System.AppDomain.DefineDynamicAssembly%2A?displayProperty=fullName>  
  
-   <xref:System.AppDomain.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>  
  
-   <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>  
  
## Demand e LinkDemand  
 La sicurezza dichiarativa offre due tipi di controlli di sicurezza che, pur essendo simili, eseguono verifiche molto diverse. È importante conoscerli entrambi perché la scelta sbagliata potrebbe indebolire la sicurezza o provocare una riduzione delle prestazioni.  
  
 La sicurezza dichiarativa offre i controlli di sicurezza seguenti:  
  
-   <xref:System.Security.Permissions.SecurityAction> specifica il percorso di chiamate nello stack di sicurezza dall'accesso al codice. Tutti i chiamanti nello stack devono disporre dell'identità o dell'autorizzazione specificata per poter passare.**Demand** viene eseguito a ogni chiamata perché lo stack potrebbe contenere chiamanti diversi. Se si chiama un metodo più volte, questo controllo di sicurezza viene eseguito ogni volta.**Demand** è una valida protezione contro gli attacchi luring, perché consente di rilevare il codice non autorizzato che cerca di passare.  
  
-   [LinkDemand](../../../docs/framework/misc/link-demands.md) viene eseguito in fase di compilazione JIT e controlla solo il chiamante immediato. Questo controllo di sicurezza non verifica il chiamante del chiamante. Una volta passato questo controllo, non ne vengono eseguiti altri, indipendentemente dal numero di chiamate effettuate dal chiamante. Tuttavia, non esiste nemmeno alcuna protezione contro gli attacchi luring. Con **LinkDemand**, il codice che supera il test e può fare riferimento al codice può potenzialmente provocare problemi di sicurezza consentendo al codice dannoso di chiamare usando il codice autorizzato. Non usare quindi **LinkDemand** a meno che non sia possono evitare completamente tutti i possibili punti di debolezza.  
  
    > [!NOTE]
    >  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], le richieste di collegamento sono state sostituite dall'attributo <xref:System.Security.SecurityCriticalAttribute> negli assembly <xref:System.Security.SecurityRuleSet>.<xref:System.Security.SecurityCriticalAttribute> equivale a una richiesta di collegamento per l'attendibilità totale, ma influisce anche sulle regole di ereditarietà. Per altre informazioni su questa modifica, vedere [Security\-Transparent Code, Level 2](../../../docs/framework/misc/security-transparent-code-level-2.md).  
  
 Le precauzioni aggiuntive necessarie quando si usa **LinkDemand** devono essere programmate singolarmente. Il sistema di sicurezza può offrire un'ulteriore tutela. Ogni errore crea un punto di debolezza per la sicurezza. Tutto il codice autorizzato che usa il codice dell'utente deve essere responsabile dell'implementazione di altre misure di sicurezza tramite l'esecuzione delle operazioni seguenti:  
  
-   Limitare l'accesso del codice chiamante alla classe o all'assembly.  
  
-   Inserire nel codice chiamante gli stessi controlli di sicurezza visualizzati nel codice che viene chiamato e obbligare i chiamanti a fare lo stesso. Ad esempio, se si scrive codice che chiama un metodo protetto con **LinkDemand** per <xref:System.Security.Permissions.SecurityPermission> con il flag <xref:System.Security.Permissions.SecurityPermissionFlag> specificato, il metodo deve eseguire anche il controllo **LinkDemand** \(o **Demand**, che è più affidabile\) per questa autorizzazione. Si verifica un'eccezione se il codice usa il metodo protetto da **LinkDemand** in modo limitato, ma considerato sicuro, dal momento che nel codice esistono altri meccanismi di protezione della sicurezza \(ad esempio, le richieste\). In questo caso eccezionale, il chiamante si assume la responsabilità di indebolire la protezione della sicurezza nel codice sottostante.  
  
-   Garantire che i chiamanti del codice non possano spingere il codice a chiamare il codice protetto per conto loro. In altre parole, i chiamanti non possono obbligare il codice autorizzato a passare parametri specifici al codice protetto o recuperare i risultati da esso.  
  
### Interfacce e richieste di collegamento  
 Se un metodo, una proprietà o un evento virtuale con **LinkDemand** esegue l'override di un metodo della classe base, il metodo della classe base, per avere effetto, deve avere lo stesso **LinkDemand** anche per il metodo di cui viene eseguito l'override. Per il codice dannoso è possibile eseguire nuovamente il cast al tipo di base e chiamare il metodo della classe base. Si noti inoltre che le richieste di collegamento possono essere aggiunte in modo implicito agli assembly che non dispongono dell'attributo a livello di assembly <xref:System.Security.AllowPartiallyTrustedCallersAttribute>.  
  
 È consigliabile proteggere le implementazioni dei metodi con richieste di collegamento quando anche i metodi di interfaccia dispongono di richieste di collegamento. Tenere presente quanto segue sull'uso di richieste di collegamento con interfacce:  
  
-   L'attributo **AllowPartiallyTrustedCallersAttribute** si applica anche alle interfacce.  
  
-   È possibile inserire le richieste di collegamento nelle interfacce per proteggere in modo selettivo alcune interfacce evitando che vengano usate da codice parzialmente attendibile, ad esempio quando si usa l'attributo **AllowPartiallyTrustedCallersAttribute** .  
  
-   Se in un assembly è definita un'interfaccia che non contiene l'attributo **AllowPartiallyTrustedCallersAttribute** , è possibile implementare tale interfaccia in una classe parzialmente attendibile.  
  
-   Se si inserisce un oggetto **LinkDemand** in un metodo pubblico di una classe che implementa un metodo di interfaccia, **LinkDemand** non verrà applicato se poi si esegue il cast all'interfaccia e si chiama il metodo. In questo caso, poiché si è creato il collegamento all'interfaccia, viene tenuto in considerazione solo l'oggetto **LinkDemand** nell'interfaccia .  
  
 Verificare la presenza di problemi di sicurezza negli elementi seguenti:  
  
-   Richieste di collegamento esplicite nei metodi di interfaccia. Assicurarsi che le richieste di collegamento offrano la protezione prevista. Determinare se il codice dannoso può usare un cast per evitare le richieste di collegamento, come descritto in precedenza.  
  
-   Metodi virtuali con richieste di collegamento applicate.  
  
-   Tipi e interfacce implementate. Questi devono usare le richieste di collegamento in modo coerente.  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)