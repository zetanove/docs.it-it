---
title: "Code Access Security Basics | Microsoft Docs"
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
  - "security [.NET Framework], code access security"
ms.assetid: 4eaa6535-d9fe-41a1-91d8-b437cfc16921
caps.latest.revision: 21
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 19
---
# Code Access Security Basics
È necessario che tutte le applicazioni basate su Common Language Runtime, ovvero tutte le applicazioni gestite, interagiscano con il relativo sistema di sicurezza. Quando un'applicazione gestita viene caricata, il relativo host concede automaticamente un set di autorizzazioni a tale applicazione. Queste autorizzazioni sono determinate dalle impostazioni di sicurezza locali dell'host o dalla sandbox che contiene l'applicazione. A seconda delle autorizzazioni, l'applicazione viene eseguita correttamente o genera un'eccezione di sicurezza.  
  
 L'host predefinito per le applicazioni desktop consente l'esecuzione del codice in modalità di attendibilità totale. Se pertanto l'applicazione è destinata al desktop, dispone di un set di autorizzazione senza restrizioni. Altri host o sandbox forniscono un set di autorizzazioni limitato per le applicazioni. Poiché il set di autorizzazioni può essere diverso da host a host, è necessario progettare l'applicazione in modo che usi solo le autorizzazioni consentite dall'host di destinazione.  
  
 È necessario avere familiarità con i concetti attinenti alla sicurezza dall'accesso di codice, illustrati di seguito, per poter scrivere applicazioni efficienti basate su Common Language Runtime:  
  
-   **Codice indipendente dai tipi**: il codice indipendente dai tipi è codice che accede ai tipi solo con modalità ben definite e consentite. Dato un riferimento a un oggetto valido, ad esempio, il codice indipendente dai tipi può accedere solo a offset fissi corrispondenti ai membri di campo effettivi. Se tuttavia il codice accede alla memoria a offset arbitrari esterni all'intervallo di memoria appartenente ai campi dell'oggetto esposti in modo pubblico, non sarà indipendente dai tipi. Per consentire al codice di usufruire dei vantaggi della sicurezza per l'accesso al codice, è necessario usare un compilatore che generi codice indipendente dai tipi verificabile. Per altre informazioni, vedere la sezione [Scrittura di codice indipendente dai tipi verificabile](#typesafe_code) più avanti in questo argomento.  
  
-   **Sintassi imperativa e sintassi dichiarativa**: codice basato su Common Language Runtime che può interagire con il sistema di sicurezza richiedendo autorizzazioni, imponendo che i chiamanti dispongano di autorizzazioni specifiche ed eseguendo l'override di alcune impostazioni di sicurezza, purché dotato dei sufficienti privilegi. Per interagire a livello di codice con il sistema di sicurezza di .NET Framework, è necessario usare due forme differenti di sintassi: la sintassi dichiarativa e la sintassi imperativa. Le chiamate dichiarative sono eseguite mediante l'impiego di attributi, le chiamate imperative mediante l'uso di nuove istanze di classi all'interno del codice. Alcune chiamate possono essere eseguite solo in modo imperativo, altre solo in modo dichiarativo e altre ancora in nessun modo.  
  
-   **Librerie di classi sicure**: una libreria di classi protetta usa richieste di sicurezza per garantire che i relativi chiamanti dispongano dell'autorizzazione di accesso alle risorse da essa esposte. Una libreria di classi protetta potrebbe ad esempio usare un metodo per la creazione di file mediante il quale si impone che i chiamanti dispongano di specifiche autorizzazioni per creare file. In .NET Framework sono disponibili librerie di classi protette. È necessario conoscere esattamente le autorizzazioni necessarie per l'accesso a ognuna delle librerie usate dal codice. Per altre informazioni, vedere la sezione [Uso di librerie di classi protette](#secure_library) più avanti in questo argomento.  
  
-   **Codice trasparente**: A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], oltre a identificare autorizzazioni specifiche è necessario determinare se il codice deve essere eseguito come SecurityTransparent. Il codice SecurityTransparent non può chiamare tipi o membri identificati come SecurityCritical. Questa regola si applica sia alle applicazioni completamente attendibili che a quelle parzialmente attendibili. Per altre informazioni, vedere [Security\-Transparent Code](../../../docs/framework/misc/security-transparent-code.md).  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta. Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
<a name="typesafe_code"></a>   
## Scrittura di codice indipendente dai tipi verificabile  
 Durante la compilazione JIT viene eseguito un processo di verifica, in base al quale il codice viene esaminato, per provare a determinare se è indipendente dai tipi. Il codice che a seguito della verifica è riconosciuto indipendente dai tipi viene definito *codice indipendente dai tipi verificabile*. Esiste, infatti, codice che pur essendo indipendente dai tipi non è indipendente dai tipi verificabile, a causa delle limitazioni del processo di verifica o del compilatore. Non tutti i linguaggi sono indipendenti dai tipi e alcuni compilatori di linguaggio, quali Microsoft Visual C\+\+, non sono in grado di generare codice gestito indipendente dai tipi verificabile. Per stabilire se il compilatore di linguaggio usato è in grado di generare codice indipendente dai tipi verificabile, consultare la documentazione del compilatore. Se il compilatore di linguaggio usato genera codice indipendente dai tipi verificabile solo se si evitano determinati costrutti di linguaggio, è possibile usare lo [strumento PEVerify](../../../docs/framework/tools/peverify-exe-peverify-tool.md) per determinare se il codice è indipendente dai tipi verificabile.  
  
 È tuttavia possibile tentare l'esecuzione di codice non indipendente dai tipi verificabile, se i criteri di sicurezza consentono al codice di evitare la verifica. Poiché l'indipendenza dai tipi è tuttavia una componente essenziale del meccanismo di isolamento degli assembly nell'ambiente di esecuzione, non è possibile applicare la sicurezza in maniera affidabile se il codice viola le regole dell'indipendenza dai tipi. In base all'impostazione predefinita, l'esecuzione del codice non indipendente dai tipi è consentita solo se il codice ha origine nel computer locale. È quindi necessario che il codice mobile sia indipendente dai tipi.  
  
<a name="secure_library"></a>   
## Uso di librerie di classi protette  
 Se il codice richiede e ottiene le autorizzazioni richieste dalla libreria di classi, sarà autorizzato ad accedere alla libreria e le risorse esposte dalla libreria saranno protette dall'accesso non autorizzato. Se il codice non dispone delle autorizzazioni appropriate, non sarà consentito l'accesso alla libreria di classi e il codice dannoso non potrà usare il codice dell'utente per accedere indirettamente alle risorse protette. Altro codice che chiama il codice deve essere autorizzato ad accedere alla raccolta. In caso contrario, sarà limitata anche l'esecuzione del codice.  
  
 La sicurezza per l'accesso al codice non elimina la possibilità di errori umani nella scrittura del codice. Tuttavia, se l'applicazione usa le librerie di classi protette per accedere alle risorse protette, il rischio di problemi relativi alla sicurezza del codice applicazione risulta ridotto dall'accurato controllo cui sono sottoposte le librerie di classi.  
  
## Sicurezza dichiarativa  
 La sintassi di sicurezza dichiarativa usa gli [attributi](../../../docs/standard/attributes/index.md) per inserire informazioni di sicurezza nei [metadati](../../../docs/standard/metadata-and-self-describing-components.md) del proprio codice. Gli attributi possono essere inseriti a livello di assembly, classe o membro, per indicare il tipo di richiesta, la domanda o l'override che si vuole usare. Le richieste vengono usate in applicazioni destinate a Common Language Runtime per informare il sistema di sicurezza runtime sulle autorizzazioni necessarie o non necessarie per l'applicazione. Le richieste e gli override vengono usati nelle librerie per proteggere le risorse dai chiamanti o per eseguire l'override del comportamento di sicurezza predefinito.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] sono state apportate importanti modifiche al modello di sicurezza e alla terminologia di .NET Framework. Per altre informazioni su queste modifiche, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
 Per usare le chiamate di sicurezza dichiarativa, è necessario inizializzare i dati dello stato dell'oggetto di autorizzazione in modo che rappresenti la forma specifica di autorizzazione necessaria. Ciascuna autorizzazione incorporata dispone di un attributo a cui viene passata un'enumerazione <xref:System.Security.Permissions.SecurityAction> per descrivere il tipo di operazione di protezione che si vuole eseguire. Tuttavia, le autorizzazioni accettano anche i propri parametri esclusivi.  
  
 Nel frammento di codice riportato di seguito viene illustrata la sintassi dichiarativa per richiedere che i chiamanti del codice dispongano di un'autorizzazione personalizzata denominata `MyPermission`. Questa autorizzazione è un'autorizzazione personalizzata ipotetica e non esiste in .NET Framework. In questo esempio viene effettuata la chiamata dichiarativa direttamente prima della definizione di classe, specificando che è necessario applicare l'autorizzazione a livello di classe. L'attributo viene passato una struttura **SecurityAction. Demand** per specificare che i chiamanti devono disporre di questa autorizzazione per l'esecuzione.  
  
```vb  
<MyPermission(SecurityAction.Demand, Unrestricted = True)> Public Class MyClass1 Public Sub New() 'The constructor is protected by the security call. End Sub Public Sub MyMethod() 'This method is protected by the security call. End Sub Public Sub YourMethod() 'This method is protected by the security call. End Sub End Class  
  
```  
  
```csharp  
[MyPermission(SecurityAction.Demand, Unrestricted = true)] public class MyClass { public MyClass() { //The constructor is protected by the security call. } public void MyMethod() { //This method is protected by the security call. } public void YourMethod() { //This method is protected by the security call. } }  
```  
  
## Sicurezza imperativa  
 La sintassi di sicurezza imperativa invia una chiamata di sicurezza mediante la creazione di una nuova istanza dell'oggetto autorizzazione che si vuole richiamare. È possibile usare la sintassi imperativa per eseguire domande e override, ma non richieste.  
  
 Prima di eseguire la chiamata di sicurezza, è necessario inizializzare i dati dello stato dell'oggetto di autorizzazione in modo che rappresenti la forma specifica di autorizzazione necessaria. Ad esempio, quando si crea un oggetto <xref:System.Security.Permissions.FileIOPermission>, è possibile usare il costruttore per inizializzare l'oggetto **FileIOPermission** in modo che rappresenti l'accesso illimitato a tutti i file oppure nessun accesso ai file. In alternativa, è possibile usare un diverso oggetto **FileIOPermission** , passando parametri che indicano il tipo di accesso che l'oggetto deve rappresentare \(ovvero, leggere, aggiungere o scrivere\) e i file che l'oggetto deve proteggere.  
  
 Oltre a usare la sintassi di sicurezza imperativa per richiamare un singolo oggetto di sicurezza, è possibile usarla per inizializzare un gruppo di autorizzazioni in un set di autorizzazioni. Ad esempio, questa tecnica è l'unico modo per eseguire in maniera affidabile le chiamate [assert](../../../docs/framework/misc/using-the-assert-method.md) su più autorizzazioni in un unico metodo. Usare le classi <xref:System.Security.PermissionSet> e <xref:System.Security.NamedPermissionSet> per creare un gruppo di autorizzazioni e quindi chiamare il metodo appropriato per richiamare la chiamata di sicurezza desiderato.  
  
 È possibile usare la sintassi imperativa per eseguire domande e override, ma non richieste. Potrebbe usare la sintassi imperativa per richieste e override anziché la sintassi dichiarativa quando le informazioni necessarie per inizializzare lo stato di autorizzazione diventano note solo in fase di esecuzione. Ad esempio, se si vuole garantire che i chiamanti abbiano l'autorizzazione di lettura di un determinato file, ma non si conosce il nome del file fino al runtime, usare una richiesta imperativa. È anche possibile usare controlli imperativi invece di controlli dichiarativi quando è necessario determinare in fase di esecuzione se contiene una condizione e, in base al risultato del test, eseguire o no una richiesta di sicurezza.  
  
 Nel frammento di codice riportato di seguito viene illustrata la sintassi imperativa per richiedere che i chiamanti del codice abbiano un'autorizzazione personalizzata denominata `MyPermission`. Questa autorizzazione è un'autorizzazione personalizzata ipotetica e non esiste in .NET Framework. Una nuova istanza di `MyPermision` viene creata in `MyMethod` e protegge solo questo metodo con la chiamata di sicurezza.  
  
```vb  
Public Class MyClass1 Public Sub New() End Sub Public Sub MyMethod() 'MyPermission is demanded using imperative syntax. Dim Perm As New MyPermission() Perm.Demand() 'This method is protected by the security call. End Sub Public Sub YourMethod() 'YourMethod 'This method is not protected by the security call. End Sub End Class  
  
```  
  
```csharp  
public class MyClass { public MyClass(){ } public void MyMethod() { //MyPermission is demanded using imperative syntax. MyPermission Perm = new MyPermission(); Perm.Demand(); //This method is protected by the security call. } public void YourMethod() { //This method is not protected by the security call. } }  
```  
  
## Uso di classi wrapper gestite  
 È necessario che la maggior parte delle applicazione e dei componenti, fatta eccezione per le librerie protette, non chiami direttamente codice non gestito. Le ragioni sono molteplici. Se il codice chiama direttamente codice non gestito, in molti casi non ne sarà autorizzata l'esecuzione, poiché per chiamare codice nativo è necessario che il codice disponga di un livello di attendibilità elevato. Se i criteri vengono modificati in modo da consentire l'esecuzione di tale applicazione, potrebbe risultarne seriamente indebolita la protezione del sistema e l'applicazione sarebbe libera di eseguire quasi ogni tipo di operazione.  
  
 È inoltre probabile che il codice che dispone dell'autorizzazione per l'accesso a codice sia in grado di effettuare qualsiasi operazione chiamando un'API non gestita. Non è necessario, ad esempio, che un codice autorizzato a chiamare codice non gestito disponga di un oggetto <xref:System.Security.Permissions.FileIOPermission> per accedere a un file. Sarà sufficiente che effettui la chiama diretta a un'API di file non gestita \(Win32\), ignorando l'API di file gestita che richiede **FileIOPermission**. Se il codice gestito è autorizzato a chiamare codice non gestito e lo chiama direttamente, il sistema di protezione non sarà in grado di imporre in maniera affidabile restrizioni di protezione, dal momento che non è possibile imporre tali restrizioni su codice non gestito.  
  
 Se si vuole che l'applicazione esegua un'operazione che richiede l'accesso a codice non gestito, sarà necessario usare, se disponibile, una classe gestita attendibile che esegua il wrapping della funzionalità richiesta. Non creare autonomamente una classe wrapper se ne esiste già una in una libreria di classi protetta. La classe wrapper, a cui è necessario concedere un elevato livello di attendibilità perché le sia consentito chiamare codice non gestito, impone ai chiamanti il possesso delle opportune autorizzazioni. Se si usa una classe wrapper, è necessario che il codice richieda e ottenga esclusivamente le autorizzazioni da essa pretese.  
  
## Vedere anche  
 <xref:System.Security.PermissionSet>   
 <xref:System.Security.Permissions.FileIOPermission>   
 <xref:System.Security.NamedPermissionSet>   
 <xref:System.Security.Permissions.SecurityAction>   
 [Assert](../../../docs/framework/misc/using-the-assert-method.md)   
 [Code Access Security](../../../docs/framework/misc/code-access-security.md)   
 [Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md)   
 [Attributi](../../../docs/standard/attributes/index.md)   
 [Metadati e componenti auto\-descrittivi](../../../docs/standard/metadata-and-self-describing-components.md)