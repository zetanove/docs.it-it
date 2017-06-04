---
title: "Come il runtime individua gli assembly | Microsoft Docs"
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
  - "distribuzione di applicazioni .NET Framework, individuazione di assembly"
  - "app.config (file), posizioni degli assembly"
  - "file di configurazione dell'applicazione, individuazione di assembly"
  - "assembly [.NET Framework], posizione"
  - "distribuzione di applicazioni [.NET Framework], posizioni degli assembly"
  - "individuazione di assembly"
ms.assetid: 772ac6f4-64d2-4cfb-92fd-58096dcd6c34
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# Come il runtime individua gli assembly
Per distribuire correttamente l'applicazione .NET Framework, è necessario comprendere in che modo Common Language Runtime individua e associa gli assembly che costituiscono l'applicazione. Per impostazione predefinita, il runtime tenta di eseguire l'associazione con la versione esatta di un assembly con cui è stata compilata l'applicazione. Questo comportamento predefinito può essere sottoposto a override dalle impostazioni del file di configurazione.  
  
 Quando si tenta di individuare un assembly e risolvere un riferimento ad assembly, Common Language Runtime esegue una serie di passaggi. Ogni passaggio è descritto nelle sezioni seguenti. Il termine "individuazione tramite probe" viene usato quando si descrive la modalità di individuazione degli assembly mediante runtime e fa riferimento al set di euristiche usato per individuare l'assembly in base al nome e alle impostazioni cultura.  
  
> [!NOTE]
>  Per visualizzare le informazioni di associazione nel file di log, usare il [Visualizzatore log associazioni assembly \(Fuslogvw.exe\)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md), incluso in [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
## Avvio dell'associazione  
 Il processo di individuazione e associazione di un assembly inizia quando il runtime tenta di risolvere un riferimento a un altro assembly. Questo riferimento può essere statico o dinamico. I compilatore registra i riferimenti statici nei metadati del manifesto dell'assembly in fase di compilazione. I riferimenti dinamici vengono costruiti al momento, in base ai risultati delle chiamate a diversi metodi, ad esempio <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>.  
  
 Il modo migliore per fare riferimento a un assembly consiste nell'usare un riferimento completo che includa il nome dell'assembly, la versione, le impostazioni cultura il e token di chiave pubblica \(se presente\). Il runtime usa queste informazioni per individuare l'assembly, seguendo i passaggi descritti più avanti in questa sezione. Il runtime usa lo stesso processo di risoluzione a prescindere che il riferimento riguardi un assembly statico o dinamico.  
  
 Un riferimento dinamico a un assembly può essere eseguito anche fornendo il metodo di chiamata solo con informazioni parziali sull'assembly, ad esempio specificando solo il nome dell'assembly. In questo caso, l'assembly viene cercato solo nella directory dell'applicazione e non vengono eseguiti altri controlli. È possibile creare un riferimento parziale usando uno dei diversi metodi per il caricamento degli assembly, ad esempio <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> o <xref:System.AppDomain.Load%2A?displayProperty=fullName>.  
  
 È infine possibile creare un riferimento dinamico usando un metodo come [System.Reflection.Assembly.Load](https://msdn.microsoft.com/en-us/library/system.reflection.assembly.load.aspx) e fornire solo informazioni parziali, specificando però successivamente le informazioni complete sul riferimento tramite l'elemento [\<qualifyAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md) nel file di configurazione dell'applicazione. Questo elemento consente di specificare le informazioni di riferimento complete \(nome, versione, impostazioni cultura e, se applicabile, il token di chiave pubblica\) nel file di configurazione dell'applicazione anziché nel codice. Questa tecnica si usa quando si vuole completare un riferimento a un assembly di fuori della directory dell'applicazione oppure se si vuole fare riferimento a un assembly nella Global Assembly Cache, ma si preferisce definirlo in modo completo nel file di configurazione anziché nel codice.  
  
> [!NOTE]
>  Questo tipo di riferimento parziale non deve essere usato con gli assembly condivisi tra diverse applicazioni. Poiché le impostazioni di configurazione vengono applicate per applicazione e non per assembly, per usare questo tipo di riferimento parziale in un assembly condiviso ogni applicazione che usa l'assembly condiviso dovrebbe disporre delle informazioni complete nel file di configurazione.  
  
 Il runtime usa la procedura seguente per risolvere un riferimento ad assembly:  
  
1.  [Determina la versione corretta dell'assembly](#step1) esaminando i file di configurazione applicabili, tra cui il file di configurazione dell'applicazione, il file dei criteri editore e il file di configurazione del computer. Se il file di configurazione si trova in un computer remoto, il runtime deve prima individuare e scaricare il file di configurazione dell'applicazione.  
  
2.  [Controlla se il nome dell'assembly è stato associato in precedenza](#step2) e, in questo caso, usa l'assembly caricato in precedenza. Se una richiesta precedente di caricamento dell'assembly non è riuscita, la richiesta viene interrotta immediatamente senza effettuare alcun tentativo di caricamento dell'assembly.  
  
    > [!NOTE]
    >  La memorizzazione nella cache di errori relativi all'associazione di assembly è stata introdotta in .NET Framework versione 2.0.  
  
3.  [Controlla la Global Assembly Cache](#step3). Se viene trovato nella Global Assembly Cache, il runtime usa questo assembly.  
  
4.  [Individua tramite probe l'assembly](#step4) usando la procedura seguente:  
  
    1.  Se i criteri dell'editore e della configurazione non hanno effetto sul riferimento originale e se la richiesta di associazione è stata creata usando il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>, il runtime cerca suggerimenti per la posizione.  
  
    2.  Se viene trovata una codebase nei file di configurazione, il runtime controlla solo questo percorso. Se la probe non riesce, il runtime determina che la richiesta di associazione non è riuscita e non vengono eseguite altre individuazioni tramite probe.  
  
    3.  Le probe per l'assembly che usa le euristiche descritte nella [sezione relativa all'individuazione tramite probe](#step4). Se l'assembly non è stato trovato dopo l'individuazione tramite probe, il runtime lo richiede a Windows Installer. Questa operazione opera come una funzionalità di installazione su richiesta.  
  
        > [!NOTE]
        >  Per gli assembly senza nomi sicuri non vengono eseguiti controlli della versione né controlli nella Global Assembly Cache con il runtime.  
  
<a name="step1"></a>   
## Passaggio 1: Esame dei file di configurazione  
 Il comportamento dell'associazione di assembly può essere configurato a livelli diversi in base a tre file XML:  
  
-   File di configurazione dell'applicazione.  
  
-   File dei criteri editore.  
  
-   File di configurazione del computer.  
  
 Questi file seguono la stessa sintassi e forniscono informazioni quali i reindirizzamenti delle associazioni, la posizione del codice e le modalità di associazione per determinati assembly. In ogni file di configurazione può essere contenuto un elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) tramite cui viene reindirizzato il processo di associazione. Negli elementi figlio dell'elemento [\<assemblyBinding\>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) è incluso l'elemento [\<dependentAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md). Negli elementi figlio dell'elemento [\<dependentAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md) sono inclusi gli elementi [\<assemblyIdentity\>](../Topic/%3CassemblyIdentity%3E%20Element%20\(ClickOnce%20Deployment\).md), [\<bindingRedirect\>](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md) e [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md).  
  
> [!NOTE]
>  Le informazioni di configurazione sono disponibili nei tre file di configurazione; non tutti gli elementi sono validi in tutti i file di configurazione. Ad esempio, le informazioni sulla modalità di associazione e sul percorso privato possono trovarsi solo nel file di configurazione dell'applicazione. Per un elenco completo delle informazioni contenute in ciascun file, vedere [Configurazione delle app con file di configurazione](../../../docs/framework/configure-apps/index.md).  
  
### File di configurazione dell'applicazione  
 Common Language Runtime controlla innanzitutto il file di configurazione dell'applicazione per le informazioni che eseguono l'override delle informazioni sulla versione memorizzate nel manifesto dell'assembly chiamante. Il file di configurazione dell'applicazione può essere distribuito con un'applicazione, ma non è necessario per la sua esecuzione. In genere il recupero di questo file è quasi istantaneo, ma in situazioni in cui la base dell'applicazione si trova in un computer remoto, ad esempio in uno scenario basato su Web di Internet Explorer, il file di configurazione deve essere scaricato.  
  
 Per gli eseguibili del client, il file di configurazione dell'applicazione si trova nella stessa directory del file eseguibile dell'applicazione e ha lo stesso nome di base dell'eseguibile con estensione config. Ad esempio, il file di configurazione per C:\\Programmi\\Myapp\\Myapp.exe è C:\\Programmi\\Myapp\\Myapp.exe.config. In un scenario basato sul browser, nel file HTML deve essere usato l'elemento **\<link\>** per puntare in modo esplicito al file di configurazione.  
  
 Il codice seguente fornisce un esempio semplice di un file di configurazione dell'applicazione. Questo esempio aggiunge <xref:System.Diagnostics.TextWriterTraceListener> a una raccolta <xref:System.Diagnostics.Debug.Listeners%2A> per consentire la registrazione di informazioni di debug in un file.  
  
```  
<configuration> <system.diagnostics> <trace useGlobalLock="false" autoflush="true" indentsize="0"> <listeners> <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" /> </listeners> </trace> </system.diagnostics> </configuration>  
```  
  
### File dei criteri editore  
 In secondo luogo, il runtime esamina il file dei criteri editore, se presente. I file dei criteri editore vengono distribuiti da un editore del componente, ad esempio una correzione o un aggiornamento, a un componente condiviso. Questi file contengono le informazioni sulla compatibilità dell'editore del componente condiviso che indirizzano un riferimento ad assembly a una nuova versione. A differenza dei file di configurazione del computer e dell'applicazione, i file dei criteri editore sono contenuti nei propri assembly che devono essere installati nella Global Assembly Cache.  
  
 Di seguito è riportato un esempio di un file di configurazione dei criteri editore:  
  
```  
<configuration> <runtime> <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"> <dependentAssembly> <assemblyIdentity name="asm6" publicKeyToken="c0305c36380ba429" /> <bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0"/> </dependentAssembly> </assemblyBinding> </runtime> </configuration>  
```  
  
 Per creare un assembly, è possibile usare lo strumento [Al.exe \(Assembly Linker\)](../../../docs/framework/tools/al-exe-assembly-linker.md) con un comando analogo al seguente:  
  
```  
Al.exe /link:asm6.exe.config /out:policy.3.0.asm6.dll /keyfile: compatkey.dat /v:3.0.0.0  
```  
  
 `compatkey.dat` è un file di chiave con nome sicuro. Questo comando crea un assembly con nome sicuro che è possibile inserire nella Global Assembly Cache.  
  
> [!NOTE]
>  I criteri dell'editore hanno effetto su tutte le applicazioni che usano un componente condiviso.  
  
 Il file di configurazione dei criteri editore esegue l'override delle informazioni sulla versione provenienti dall'applicazione \(ovvero, dal manifesto dell'assembly o dal file di configurazione dell'applicazione\). Se non è presente alcuna istruzione nel file di configurazione dell'applicazione per reindirizzare la versione specificata nel manifesto dell'assembly, il file dei criteri editore esegue l'override della versione specificata nel manifesto dell'assembly. Tuttavia, se esiste un'istruzione di reindirizzamento nel file di configurazione dell'applicazione, i criteri editore eseguono l'override di questa versione e non di quella specificata nel manifesto.  
  
 Un file dei criteri editore viene usato quando un componente condiviso viene aggiornato e la nuova versione del componente condiviso deve essere selezionata da tutte le applicazioni che usano il componente. Le impostazioni nel file dei criteri editore eseguono l'override delle impostazioni nel file di configurazione dell'applicazione, a meno che quest'ultimo non attivi la modalità sicura.  
  
#### Modalità sicura  
 I file dei criteri editore vengono generalmente installati in maniera esplicita insieme a un Service Pack o a un aggiornamento di un programma. Se si verifica un problema con il componente condiviso aggiornato, è possibile ignorare gli override nel file dei criteri editore usando la modalità sicura. La modalità provvisoria è determinata dall'elemento **\<publisherPolicy apply\="yes**&#124;**no"\/\>**, disponibile solo nel file di configurazione dell'applicazione. Specifica se le informazioni di configurazione dei criteri editore devono essere rimosse dal processo di associazione.  
  
 La modalità sicura può essere impostata per l'intera applicazione o per gli assembly selezionati. In altre parole è possibile disattivare i criteri per tutti gli assembly che costituiscono l'applicazione o attivarlo solo in alcuni assembly. Per applicare i criteri dell'editore solo agli assembly che costituiscono un'applicazione, impostare **\<publisherPolicy apply\=no\/\>** e specificare gli assembly da includere usando l'elemento \<**dependentAssembly**\>. Per applicare i criteri dell'editore a tutti gli assembly che costituiscono un'applicazione, impostare **\<publisherPolicy apply\=no\/\>** senza usare gli elementi relativi agli assembly dipendenti. Per altre informazioni sulla configurazione, vedere [Configurazione delle app con file di configurazione](../../../docs/framework/configure-apps/index.md).  
  
### File di configurazione del computer  
 In terzo luogo, il runtime esamina il file di configurazione del computer. Questo file, denominato Machine.config, si trova nel computer locale nella sottodirectory Config della directory radice in cui è installato il runtime. Questo file può essere usato dagli amministratori per specificare le restrizioni relative all'associazione di assembly locali nel computer. Le impostazioni nel file di configurazione del computer hanno la precedenza su tutte le altre impostazioni di configurazione. Tuttavia, ciò non implica che tutte le impostazioni di configurazione debbano essere inserite in questo file. La versione determinata dal file dei criteri amministratore è finale e non può essere sottoposta a override. Gli override specificati nel file Machine.config file hanno effetto su tutte le applicazioni. Per altre informazioni sui file di configurazione, vedere [Configurazione delle app con file di configurazione](../../../docs/framework/configure-apps/index.md).  
  
<a name="step2"></a>   
## Passaggio 2: Controllo di assembly a cui è stato fatto riferimento in precedenza  
 Se l'assembly è stato richiesto anche nelle chiamate precedenti, Common Language Runtime usa l'assembly è già caricato. Ciò può avere implicazioni per la denominazione di assembly che costituiscono un'applicazione. Per altre informazioni sulla denominazione degli assembly, vedere [Nomi degli assembly](../../../docs/framework/app-domains/assembly-names.md).  
  
 Se una richiesta precedente per l'assembly non è riuscita, le richieste successive verranno interrotte immediatamente senza effettuare alcun tentativo di caricamento dell'assembly. A partire da .NET Framework versione 2.0, gli errori relativi all'associazione di assembly vengono memorizzati nella cache e le informazioni memorizzate nella cache vengono usate per determinare se tentare di caricare l'assembly.  
  
> [!NOTE]
>  Per ripristinare il comportamento di .NET Framework versioni 1.0 e 1.1, che non memorizza nella cache gli errori di associazione, includere l'[Elemento \<disableCachingBindingFailures\>](../../../docs/framework/configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md) nel file di configurazione.  
  
<a name="step3"></a>   
## Passaggio 3: Controllo della Global Assembly Cache  
 Per gli assembly con nome sicuro, il processo di associazione prosegue con la ricerca nella Global Assembly Cache. Gli assembly che possono essere usati da più applicazioni in un computer vengono archiviati nella Global Assembly Cache. Tutti gli assembly nella Global Assembly Cache devono avere nomi sicuri.  
  
<a name="step4"></a>   
## Passaggio 4: Individuazione dell'assembly mediante codebase o probe  
 Dopo aver determinato la versione corretta dell'assembly usando le informazioni nel riferimento dell'assembly chiamante e nei file di configurazione e dopo aver archiviato tale versione nella Global Assembly Cache \(solo per assembly con nome sicuro\), Common Language Runtime tenta di trovare l'assembly. Il processo di individuazione di un assembly prevede i seguenti passaggi:  
  
1.  Se nel file di configurazione dell'applicazione viene rilevato un elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md), il percorso specificato viene verificato dal runtime. Se viene rilevata una corrispondenza, viene usato l'assembly trovato e non vengono eseguite individuazioni tramite probe. Se l'assembly non viene trovato, la richiesta di associazione non riesce.  
  
2.  Il runtime esegue quindi l'individuazione tramite probe per l'assembly di riferimento usando le regole specificate più avanti in questa sezione.  
  
> [!NOTE]
>  Se sono presenti più versioni di un assembly in una directory e si desidera fare riferimento a una versione specifica, è necessario usare l'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) invece dell'attributo `privatePath` dell'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md). Se si usa l'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md), tramite il runtime viene arrestata l'individuazione tramite probe non appena viene trovato un assembly che corrisponde al nome semplice dell'assembly a cui viene fatto riferimento, indipendentemente dalla correttezza della corrispondenza. Se la corrispondenza è corretta, viene usato questo assembly. Se la corrispondenza non è corretta, l'individuazione tramite probe si arresta e l'associazione non riesce.  
  
### Individuazione dell'assembly mediante codebase  
 È possibile fornire le informazioni relative alla codebase usando un elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) in un file di configurazione. Questa codebase viene sempre controllata prima che il runtime tenti l'individuazione tramite probe per l'assembly di riferimento. Se in un file dei criteri dell'editore contenente le informazioni per il reindirizzamento a una versione finale è incluso anche un elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md), verrà usato tale elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md). Se, ad esempio, nel file di configurazione dell'applicazione è specificato un elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) e anche in un file dei criteri dell'editore tramite cui viene eseguito l'override delle informazioni dell'applicazione è specificato un elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md), verrà usato l'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) presente nel file dei criteri dell'editore.  
  
 Se nel percorso specificato dall'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) non viene individuato alcun assembly, la richiesta di associazione non viene completata e non vengono eseguite ulteriori operazioni. Se il runtime determina che un assembly soddisfa i criteri dell'assembly chiamante, viene usato questo assembly. Quando viene caricato il file indicato dall'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) specificato, tramite il runtime viene controllato che il nome, la versione, le impostazioni cultura e la chiave pubblica corrispondano al riferimento dell'assembly chiamante.  
  
> [!NOTE]
>  Gli assembly a cui viene fatto riferimento che sono esterni alla directory radice dell'applicazione devono avere nomi sicuri e devono essere installati nella Global Assembly Cache o specificati mediante l'elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md).  
  
### Individuazione dell'assembly mediante l'individuazione tramite probe  
 Se nel file di configurazione dell'applicazione non è stato specificato alcun elemento [\<codeBase\>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md), tramite il runtime viene eseguita la ricerca dell'assembly usando quattro criteri:  
  
-   La base dell'applicazione, ovvero il percorso radice in cui viene eseguita l'applicazione.  
  
-   Le impostazioni cultura, ovvero l'attributo delle impostazioni cultura dell'assembly di riferimento.  
  
-   Il nome, ovvero il nome dell'assembly di riferimento.  
  
-   L'attributo `privatePath` dell'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md), cioè l'elenco definito dall'utente delle sottodirectory del percorso radice. Questo percorso può essere specificato nel file di configurazione dell'applicazione e nel codice gestito mediante la proprietà <xref:System.AppDomain.AppendPrivatePath%2A> di un dominio applicazione. Quando è specificato nel codice gestito, viene eseguita prima l'individuazione tramite probe del codice gestito `privatePath`, seguita dal percorso specificato nel file di configurazione dell'applicazione.  
  
#### Individuazione tramite probe delle directory Application Base e Culture  
 Il runtime avvia sempre l'individuazione tramite probe nella base dell'applicazione, che può essere un URL o la directory radice dell'applicazione in un computer. Se l'assembly di riferimento non viene trovato nella base dell'applicazione e non viene fornita alcuna informazione sulle impostazioni cultura, il runtime cerca il nome dell'assembly in tutte le sottodirectory. Le directory di cui viene eseguita l'individuazione tramite probe includono:  
  
 \[application base\]\/\[assembly name\].dll  
  
 \[application base\]\/\[assembly name\]\/\[assembly name\].dll  
  
 Se si specificano le informazioni sulle impostazioni cultura per l'assembly di riferimento, l'individuazione tramite probe viene eseguita solo sulle seguenti directory:  
  
 \[application base\]\/\[culture\]\/\[assembly name\].dll  
  
 \[application base\]\/\[culture\]\/\[assembly name\]\/\[assembly name\].dll  
  
#### Individuazione tramite probe con l'attributo privatePath  
 Oltre alle sottodirectory relative alle impostazioni cultura e a quelle specificate per l'assembly a cui viene fatto riferimento, tramite il runtime la ricerca viene anche eseguita nelle directory specificate dall'attributo `privatePath` dell'elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md). Le directory specificate usando l'attributo `privatePath` devono essere sottodirectory della directory radice dell'applicazione. Le directory con individuazione tramite probe variano a seconda che le informazioni sulle impostazioni cultura siano incluse o meno nella richiesta dell'assembly di riferimento.  
  
 Il runtime arresta l'individuazione tramite probe appena trova un assembly che corrisponde al nome semplice dell'assembly indicato, senza tenere conto della correttezza della corrispondenza. Se la corrispondenza è corretta, viene usato questo assembly. Se la corrispondenza non è corretta, l'individuazione tramite probe si arresta e l'associazione non riesce.  
  
 Se le impostazioni cultura sono incluse, l'individuazione tramite probe viene eseguita sulle seguenti directory:  
  
 \[application base\]\/\[binpath\]\/\[culture\]\/\[assembly name\].dll  
  
 \[application base\]\/\[binpath\]\/\[culture\]\/\[assembly name\]\/\[assembly name\].dll  
  
 Se le informazioni sulle impostazioni cultura non sono incluse, l'individuazione tramite probe viene eseguita sulle seguenti directory:  
  
 \[application base\]\/\[binpath\]\/\[assembly name\].dll  
  
 \[application base\]\/\[binpath\]\/\[assembly name\]\/\[assembly name\].dll  
  
#### Esempi di individuazione tramite probe  
 Date le seguenti informazioni:  
  
-   Nome dell'assembly di riferimento: myAssembly  
  
-   Directory radice dell'applicazione: http:\/\/www.code.microsoft.com  
  
-   Elemento [\<probing\>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) specificato nel file di configurazione: bin  
  
-   Impostazioni cultura: de  
  
 Il runtime esegue l'individuazione tramite probe dei seguenti URL:  
  
 http:\/\/www.code.microsoft.com\/de\/myAssembly.dll  
  
 http:\/\/www.code.microsoft.com\/de\/myAssembly\/myAssembly.dll  
  
 http:\/\/www.code.microsoft.com\/bin\/de\/myAssembly.dll  
  
 http:\/\/www.code.microsoft.com\/bin\/de\/myAssembly\/myAssembly.dll  
  
##### Più assembly con lo stesso nome  
 L'esempio seguente mostra come configurare più assembly con lo stesso nome.  
  
```  
<dependentAssembly> <assemblyIdentity name="Server" publicKeyToken="c0305c36380ba429" /> <codeBase version="1.0.0.0" href="v1/Server.dll"/> <codeBase version="2.0.0.0" href="v2/Server.dll"/> </dependentAssembly>  
```  
  
#### Altri percorsi con individuazione tramite probe  
 Il percorso dell'assembly può essere determinato anche usando il contesto di associazione corrente. Questa situazione si verifica spesso quando il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> viene usato in scenari di interoperabilità COM. Se un assembly usa il metodo <xref:System.Reflection.Assembly.LoadFrom%2A> per fare riferimento a un altro assembly, il percorso dell'assembly chiamante viene considerato come un suggerimento su dove trovare l'assembly di riferimento. Se viene trovata una corrispondenza, l'assembly viene caricato. Se non viene trovata alcuna corrispondenza, il runtime continua con la semantica di ricerca, quindi esegue una query in Windows Installer per richiedere l'assembly. Se non vengono forniti assembly corrispondenti alla richiesta di associazione, viene generata un'eccezione. Questa eccezione è <xref:System.TypeLoadException> nel codice gestito, se è stato fatto riferimento a un tipo, oppure <xref:System.IO.FileNotFoundException> se l'assembly in fase di caricamento non è stato trovato.  
  
 Ad esempio, se Assembly1 fa riferimento ad Assembly2 e Assembly1 è stato scaricato da http:\/\/www.code.microsoft.com\/utils, il percorso viene considerato come un suggerimento su dove trovare Assembly2.dll. Il runtime quindi esegue l'individuazione tramite probe per l'assembly in http:\/\/www.code.microsoft.com\/utils\/Assembly2.dll e http:\/\/www.code.microsoft.com\/utils\/Assembly2\/Assembly2.dll. Se Assembly2 non viene trovato nei percorsi indicati, il runtime esegue una query in Windows Installer.  
  
## Vedere anche  
 [Procedure consigliate per il caricamento di assembly](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)   
 [Distribuzione](../../../docs/framework/deployment/net-framework-and-applications.md)