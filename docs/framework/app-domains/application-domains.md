---
title: "Domini applicazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "domini applicazione"
  - "domini applicazione, informazioni"
  - "isolamento dell'applicazione"
  - "codice, processo di verifica"
  - "Common Language Runtime, domini applicazione"
  - "isolamento tra applicazioni"
  - "limiti di processo per l'isolamento"
  - "runtime, domini applicazione"
  - "codice per il test di verifica"
ms.assetid: 113a8bbf-6875-4a72-a49d-ca2d92e19cc8
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Domini applicazione
I sistemi operativi e gli ambienti runtime forniscono solitamente una forma di isolamento tra le applicazioni.  Windows, ad esempio, usa i processi per isolare le applicazioni.  L'isolamento è necessario per garantire che il codice in esecuzione in un'applicazione non interferisca con altre applicazioni non correlate.  
  
 I domini applicazione forniscono un limite di isolamento per sicurezza, affidabilità e controllo delle versioni, nonché per lo scaricamento degli assembly.  I domini applicazione vengono solitamente creati dagli host di runtime, che sono responsabili dell'avvio di Common Language Runtime prima dell'esecuzione di un'applicazione.  
  
 Negli argomenti contenuti in questa sezione della documentazione viene illustrato come usare i domini applicazione per fornire un isolamento tra gli assembly.  
  
 In questa panoramica sono incluse le sezioni seguenti:  
  
-   [Vantaggi dell'isolamento delle applicazioni](#benefits)  
  
-   [Riferimento](#reference)  
  
<a name="benefits"></a>   
## Vantaggi dell'isolamento delle applicazioni  
 L'isolamento delle diverse applicazioni in esecuzione sullo stesso computer è sempre stato basato sui limiti dei processi.  Ciascuna applicazione viene caricata in un processo separato che consente di isolarla dalle altre applicazioni in esecuzione.  
  
 Le applicazioni risultano isolate perché gli indirizzi di memoria sono relativi ai processi. Un puntatore di memoria passato da un processo a un altro non può essere usato in modo significativo nel processo di destinazione.  Inoltre, non è possibile effettuare chiamate dirette tra due processi.  È invece necessario usare un proxy, che fornisce un livello di riferimento indiretto.  
  
 Il codice gestito deve essere sottoposto a verifica prima che sia possibile eseguirlo, a meno che non esista un'apposita autorizzazione dell'amministratore.  Il processo di verifica determina se il codice può tentare di accedere a indirizzi di memoria non validi o eseguire operazioni che potrebbero compromettere il corretto funzionamento del processo in cui è in esecuzione.  Il codice che supera la verifica viene definito come indipendente dai tipi.  La possibilità di verificare che il codice sia indipendente dai tipi consente a Common Language Runtime di fornire un livello di isolamento corrispondente ai limiti del processo, con un'incidenza sulle prestazioni di gran lunga inferiore.  
  
 I domini applicazione forniscono un'unità di elaborazione più protetta e versatile che può essere usata da Common Language Runtime per fornire isolamento tra le applicazioni.  In ogni processo è possibile eseguire più domini applicazione con lo stesso livello di isolamento che si ottiene usando processi separati, ma senza l'overhead derivante dalle chiamate tra processi o dal passaggio tra processi.  La possibilità di eseguire più applicazioni all'interno di un singolo processo incrementa considerevolmente la scalabilità.  
  
 L'isolamento delle applicazioni è importante anche per la sicurezza delle applicazioni stesse.  È possibile, ad esempio, eseguire controlli da diverse applicazioni Web in esecuzione in un singolo processo browser, in modo che i controlli non possano accedere alle risorse e ai dati reciproci.  
  
 L'isolamento fornito dai domini applicazione offre i seguenti vantaggi:  
  
-   Gli errori di un'applicazione non possono influire sulle altre applicazioni.  Poiché il codice indipendente dai tipi non può provocare errori di memoria, l'utilizzo dei domini applicazione assicura che il codice in esecuzione in un dominio non possa influire sulle altre applicazioni nel processo.  
  
-   È possibile arrestare singole applicazioni senza arrestare l'intero processo.  L'utilizzo dei domini applicazione consente di scaricare il codice in esecuzione in una specifica applicazione.  
  
    > [!NOTE]
    >  Non è possibile scaricare singoli assembly o tipi.  È possibile scaricare solo un dominio completo.  
  
-   Il codice in esecuzione in un'applicazione non può accedere direttamente al codice o alle risorse di un'altra applicazione.  Common Language Runtime assicura tale isolamento impedendo le chiamate dirette tra gli oggetti appartenenti a domini applicazione diversi.  Il passaggio di un oggetto da un dominio all'altro avviene tramite copia o usando un proxy.  Se l'oggetto viene copiato, la chiamata all'oggetto è locale.  In altre parole, sia l'oggetto a cui viene fatto riferimento che il chiamante si trovano nello stesso dominio applicazione.  Se si accede all'oggetto tramite un proxy, la chiamata all'oggetto è remota.  In questo caso, l'oggetto a cui viene fatto riferimento e il chiamante si trovano in domini applicazione diversi.  Le chiamate tra domini usano la stessa infrastruttura di chiamata remota delle chiamate tra due processi o tra due computer.  I metadati relativi all'oggetto a cui viene fatto riferimento devono essere pertanto disponibili per entrambi i domini applicazione, affinché il compilatore JIT possa compilare la chiamata in modo corretto.  Se il dominio chiamante non ha accesso ai metadati per l'oggetto chiamato, la compilazione potrebbe avere esito negativo, con un'eccezione di tipo **System.IO.FileNotFound**.  Per maggiori dettagli, vedere [Oggetti remoti](http://msdn.microsoft.com/it-it/515686e6-0a8d-42f7-8188-73abede57c58).  Il meccanismo che stabilisce in che modo è possibile accedere a un oggetto da un dominio diverso è determinato dall'oggetto.  Per altre informazioni, vedere [Classe MarshalByRefObject](frlrfSystemMarshalByRefObjectClassTopic).  
  
-   L'ambito del comportamento del codice viene stabilito dall'applicazione in cui questo è in esecuzione.  In altri termini, il dominio applicazione fornisce impostazioni di configurazione quali i criteri di controllo delle versioni dell'applicazione, la posizione degli assembly remoti a cui questa accede e le informazioni sul percorso degli assembly che vengono caricati nel dominio.  
  
-   Le autorizzazioni concesse al codice possono essere controllate dal dominio applicazione in cui il codice è in esecuzione.  
  
 [Torna all'inizio](#top)  
  
## Domini applicazione e assembly  
 In questa sezione viene illustrata la relazione tra domini applicazione e assembly.  Per eseguire il codice contenuto in un assembly, è necessario innanzitutto caricare l'assembly in un dominio applicazione.  L'esecuzione di un'applicazione tipica implica il caricamento di diversi assembly in un dominio applicazione.  
  
 Il modo in cui viene caricato un assembly determina se il codice con compilazione JIT può essere condiviso da più domini applicazione nel processo e se l'assembly può essere scaricato dal processo.  
  
-   Se un assembly viene caricato come indipendente dal dominio, tutti i domini applicazione che condividono lo stesso insieme di autorizzazioni di sicurezza possono condividere lo stesso codice con compilazione JIT, il che comporta una riduzione della quantità di memoria richiesta dall'applicazione.  L'assembly tuttavia non può mai essere scaricato dal processo.  
  
-   Se non viene caricato come indipendente dal dominio, un assembly deve essere sottoposto a compilazione JIT in ogni dominio applicazione in cui viene caricato.  È tuttavia possibile scaricare l'assembly dal processo scaricando tutti i domini applicazione nei quali è caricato.  
  
 L'host di runtime determina se caricare gli assembly come indipendenti dal dominio nel momento in cui carica il runtime in un processo.  Per le applicazioni gestite, applicare l'attributo <xref:System.LoaderOptimizationAttribute> al metodo del punto di ingresso del processo e specificare un valore dall'enumerazione <xref:System.LoaderOptimization> associata.  Per applicazioni non gestite che ospitano Common Language Runtime, specificare il flag appropriato quando si chiama il metodo [Funzione CorBindToRuntimeEx](../../../ocs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  
  
 Il caricamento di assembly indipendenti dal dominio può avvenire in tre modi:  
  
-   Con l'impostazione <xref:System.LoaderOptimization> non viene caricato alcun assembly come indipendente dal dominio, ad eccezione di Mscorlib, che viene sempre caricato come indipendente dal dominio.  Questa impostazione viene denominata a dominio singolo perché viene usata in genere quando sull'host è in esecuzione una sola applicazione nel processo.  
  
-   Con l'impostazione <xref:System.LoaderOptimization> tutti gli assembly vengono caricati come indipendenti dal dominio.  Usare questa impostazione quando nel processo esistono più domini applicazione che eseguono tutti lo stesso codice.  
  
-   Con l'impostazione <xref:System.LoaderOptimization> vengono caricati come indipendenti dal dominio gli assembly con nome sicuro, purché siano stati installati insieme alle relative dipendenze nella Global Assembly Cache.  Gli altri assembly vengono caricati e sottoposti a compilazione JIT separatamente per ogni dominio applicazione in cui sono stati caricati e possono pertanto essere scaricati dal processo.  Usare questa impostazione se si eseguono più applicazioni nello stesso processo o se si dispone di una combinazione di assembly condivisi da molti domini applicazione e di assembly che devono essere scaricati dal processo.  
  
 Il codice con compilazione JIT non può essere condiviso per gli assembly caricati nel contesto di origine del caricamento usando il metodo <xref:System.Reflection.Assembly.LoadFrom%2A> della classe <xref:System.Reflection.Assembly> né può essere caricato da immagini usando overload del metodo <xref:System.Reflection.Assembly.Load%2A> che specificano matrici di byte.  
  
 Gli assembly compilati nel codice nativo usando il [Ngen.exe \(Native Image Generator\)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) possono essere condivisi tra domini applicazione se sono stati caricati come indipendenti dal dominio la prima volta che sono stati caricati in un processo.  
  
 Il codice con compilazione JIT per l'assembly contenente il punto di ingresso dell'applicazione è condiviso solo se possono essere condivise tutte le dipendenze.  
  
 Un assembly indipendente dal dominio può essere sottoposto a compilazione JIT più di una volta.  Se ad esempio gli insiemi di autorizzazioni di sicurezza di due domini applicazione sono diversi, non possono condividere lo stesso codice con compilazione JIT.  Ciascuna copia dell'assembly con compilazione JIT tuttavia può essere condivisa con altri domini applicazione con lo stesso insieme di autorizzazioni.  
  
 Quando si decide se caricare o meno gli assembly come indipendenti dal dominio, è necessario trovare un compromesso tra la riduzione dell'utilizzo di memoria e altri fattori relativi alle prestazioni.  
  
-   L'accesso a dati e metodi statici è più lento per gli assembly indipendenti dal dominio a causa della necessità di isolare gli assembly.  Ciascun dominio applicazione che accede all'assembly deve disporre di una copia separata dei dati statici, per evitare che i riferimenti agli oggetti contenuti nei campi statici superino i limiti del dominio.  Il runtime contiene la logica aggiuntiva necessaria per indirizzare un chiamante alla copia appropriata del metodo o dei dati statici.  Tale logica aggiuntiva rallenta la chiamata.  
  
-   Tutte le dipendenze di un assembly devono essere individuate e caricate quando l'assembly viene caricato come indipendente dal dominio, poiché una dipendenza che non può essere caricata come indipendente dal dominio impedisce il caricamento dell'assembly come indipendente dal dominio.  
  
## Domini applicazione e thread  
 Il dominio di un'applicazione costituisce un limite di isolamento per sicurezza, controllo delle versioni, affidabilità e scaricamento di codice gestito.  Un thread è il costrutto del sistema operativo usato da Common Language Runtime per eseguire il codice.  In fase di esecuzione, tutto il codice gestito viene caricato in un dominio applicazione ed eseguito da uno o più thread gestiti.  
  
 Non esiste una relazione uno a uno tra domini applicazione e thread.  È possibile eseguire diversi thread nello stesso dominio applicazione contemporaneamente e un particolare thread non è confinato a un singolo dominio applicazione.  I thread possono quindi estendersi oltre i limiti dei domini applicazione. Non viene creato un nuovo thread per ogni dominio applicazione.  
  
 In qualsiasi momento, ogni thread viene eseguito in un dominio applicazione.  In qualsiasi dominio applicazione potrebbero essere in esecuzione zero, uno o più thread.  Il runtime tiene traccia dei thread in esecuzione nei diversi domini applicazione.  In qualsiasi momento è possibile individuare il dominio in cui un thread viene eseguito chiamando il metodo <xref:System.Threading.Thread.GetDomain%2A?displayProperty=fullName>.  
  
### Domini applicazione e impostazioni cultura  
 Le impostazioni cultura, rappresentate da un oggetto <xref:System.Globalization.CultureInfo>, sono associate ai thread.  È possibile ottenere le impostazioni cultura associate al thread attualmente in esecuzione tramite la proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e ottenere o impostare le impostazioni cultura associate al thread attualmente in esecuzione tramite la proprietà <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName>.  Se le impostazioni cultura associate a un thread sono state impostate in modo esplicito tramite la proprietà <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName>, continueranno a essere associate al thread in questione quando da quest'ultimo vengono superati i limiti del dominio applicazione.  In caso contrario, le impostazioni cultura associate al thread in un determinato momento sono determinate dal valore della proprietà <xref:System.Globalization.CultureInfo.DefaultThreadCurrentCulture%2A?displayProperty=fullName> nel dominio applicazione in cui il thread è in esecuzione:  
  
-   Se il valore della proprietà non è `null`, le impostazioni cultura che vengono restituite dalla proprietà sono associate al thread e pertanto restituite dalle proprietà <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.  
  
-   Se il valore della proprietà è `null`, le impostazioni cultura correnti del sistema vengono associate al thread.  
  
## Programmazione con i domini applicazione  
 I domini applicazione vengono solitamente creati e modificati direttamente a livello di codice dagli host di runtime.  Tuttavia, anche un programma applicativo può richiedere talvolta l'utilizzo di domini applicazione.  Un programma applicativo, ad esempio, potrebbe caricare il componente di un'applicazione in un dominio per poter scaricare il dominio e il componente senza dover interrompere l'intera applicazione.  
  
 La [classe AppDomain](frlrfSystemAppDomainClassTopic) rappresenta l'interfaccia che consente di accedere ai domini applicazione a livello di codice  e include metodi per creare e scaricare domini, per creare istanze di tipi nei domini e per effettuare la registrazione per varie notifiche, come ad esempio quelle per scaricare i domini applicazione.  Nella tabella riportata di seguito vengono elencati i metodi di [AppDomain](frlrfSystemAppDomainMethodsTopic) comunemente usati.  
  
|Metodo AppDomain|Descrizione|  
|----------------------|-----------------|  
|<xref:System.AppDomain.CreateDomain%2A>|Crea un nuovo dominio applicazione.  Si consiglia di usare un overload di questo metodo che specifica un oggetto <xref:System.AppDomainSetup>.  Si tratta del sistema preferito per impostare le proprietà di un nuovo dominio, quali la base o la directory radice dell'applicazione, il percorso del file di configurazione del dominio e il percorso di ricerca usato da Common Language Runtime per caricare gli assembly nel dominio.|  
|<xref:System.AppDomain.ExecuteAssembly%2A> e <xref:System.AppDomain.ExecuteAssemblyByName%2A>|Esegue un assembly nel dominio applicazione.  Si tratta di un metodo di istanza, pertanto è possibile utilizzarlo per eseguire codice in un altro dominio applicazione per il quale si dispone di un riferimento.|  
|<xref:System.AppDomain.CreateInstanceAndUnwrap%2A>|Crea un'istanza del tipo specificato nel dominio applicazione e restituisce un proxy.  Usando questo metodo è possibile evitare di caricare l'assembly che contiene il tipo creato nell'assembly chiamante.|  
|<xref:System.AppDomain.Unload%2A>|Esegue un arresto ponderato del dominio.  Il dominio applicazione non viene scaricato fino a quando tutti i thread del dominio non sono stati interrotti o non sono più presenti nel dominio.|  
  
> [!NOTE]
>  Poiché Common Language Runtime non supporta la serializzazione di metodi globali, non è possibile usare i delegati per eseguire metodi globali in altri domini applicazione.  
  
 Anche le interfacce non gestite descritte nelle specifiche delle interfacce di hosting di Common Language Runtime forniscono l'accesso ai domini applicazione.  Gli host di runtime possono usare tali interfacce dal codice non gestito per creare i domini applicazione e accedervi nell'ambito di un processo.  
  
## Variabile di ambiente COMPLUS\_LoaderOptimization  
 Variabile di ambiente tramite cui vengono impostati i criteri predefiniti di ottimizzazione del caricatore di un'applicazione eseguibile.  
  
### Sintassi  
  
```  
COMPLUS_LoaderOptimization = 1  
```  
  
### Note  
 Tramite un'applicazione tipica vengono caricati diversi assembly in un dominio applicazione prima che il codice in essi contenuto possa essere eseguito.  
  
 Il modo in cui viene caricato l'assembly determina se il codice con compilazione JIT può essere condiviso da più domini applicazione nel processo.  
  
-   Se un assembly viene caricato come indipendente dal dominio, tutti i domini applicazione che condividono lo stesso set di autorizzazioni di sicurezza possono condividere lo stesso codice compilato tramite JIT.  In questo modo, la memoria richiesta dall'applicazione viene ridotta.  
  
-   Se un assembly non viene caricato come indipendente dal dominio, deve essere compilato tramite JIT in ogni dominio applicazione in cui viene caricato e da parte del caricatore non devono essere condivise le risorse interne tra domini applicazione.  
  
 Se impostato su 1, tramite il flag di ambiente COMPLUS\_LoaderOptimization viene forzato il caricamento di tutti gli assembly nella modalità non indipendente dal dominio nota come SingleDomain da parte dell'host di runtime.  Con SingleDomain non viene caricato alcun assembly come indipendente dal dominio, a eccezione di Mscorlib, che viene sempre caricato come indipendente dal dominio.  Questa impostazione viene denominata a dominio singolo perché viene usata in genere quando sull'host è in esecuzione una sola applicazione nel processo.  
  
> [!CAUTION]
>  Il flag di ambiente COMPLUS\_LoaderOptimization è stato progettato per essere usato negli scenari di test e di diagnostica.  L'abilitazione del flag può provocare notevoli rallentamenti e aumentare l'utilizzo della memoria.  
  
### Esempio di codice  
 Per evitare il caricamento di tutti gli assembly come indipendenti dal dominio per il servizio IISADMIN, aggiungere `COMPLUS_LoaderOptimization=1` al valore multistringa dell'ambiente nella chiave HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\IISADMIN.  
  
```  
Key = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN  
Name = Environment  
Type = REG_MULTI_SZ  
Value (to append) = COMPLUS_LoaderOptimization=1  
  
```  
  
<a name="reference"></a>   
## Riferimento  
 <xref:System.MarshalByRefObject?displayProperty=fullName>