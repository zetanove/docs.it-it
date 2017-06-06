---
title: Ngen.exe (generatore di immagini native) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Native Image Generator
- images [.NET Framework], native
- side-by-side execution, native images
- assemblies [.NET Framework], native image
- Ngen.exe
- native image generation
- native image cache
- publisher policy applied for native images
- invalid images
- BypassNGenAttribute
- System.Runtime.BypassNGenAttribute
ms.assetid: 44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66
caps.latest.revision: 57
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6f3dc4235c75d7438f019838cb22192f4dc7c41a
ms.openlocfilehash: 65ecfdf69d739e76e386ed334c95f31ad266b904
ms.contentlocale: it-it
ms.lasthandoff: 06/02/2017

---
# <a name="ngenexe-native-image-generator"></a>Ngen.exe (generatore di immagini native)
Il generatore di immagini native (Ngen.exe) consente di migliorare le prestazioni delle applicazioni gestite. Questo strumento crea immagini native, ovvero file contenenti codice macchina compilato specifico del processore, e le installa nella cache delle immagini native del computer locale. Il runtime può usare le immagini native della cache anziché il compilatore Just-In-Time (JIT) per compilare l'assembly originale.  
  
 Modifiche apportate a Ngen.exe in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]:  
  
-   Ngen.exe ora compila assembly con attendibilità totale e i criteri di sicurezza dall'accesso di codice non vengono più valutati.  
  
-   Le immagini native generate con Ngen.exe non possono più essere caricate in applicazioni in modalità di esecuzione parzialmente attendibile.  
  
 Modifiche apportate a Ngen.exe in .NET Framework versione 2.0:  
  
-   Insieme a un assembly vengono installate anche le relative dipendenze. In questo modo la sintassi di Ngen.exe risulta semplificata.  
  
-   È ora possibile condividere le immagini native in più domini applicazione.  
  
-   È ora disponibile una nuova azione, `update`, che consente di ricreare le immagini invalidate.  
  
-   È possibile rinviare l'esecuzione delle azioni affidandola a un servizio che usa il tempo di inattività sul computer per generare e installare le immagini.  
  
-   Alcune cause di invalidamento delle immagini sono state eliminate.  
  
 In Windows 8 vedere [Attività di immagini native](http://msdn.microsoft.com/en-us/9b1f7590-4e0d-4737-90ef-eaf696932afb).  
  
 Per altre informazioni sull'uso di Ngen.exe e del servizio immagini native, vedere [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
> [!NOTE]
>  Per la sintassi di Ngen.exe per le versioni 1.0 e 1.1 di .NET Framework, vedere [Sintassi legacy del generatore di immagini native (Ngen.exe)](http://msdn.microsoft.com/en-us/5a69fc7a-103f-4afc-8ab4-606adcb46324).  
  
 Viene installato automaticamente con Visual Studio. Per eseguire lo strumento, usare il prompt dei comandi per sviluppatori o il prompt dei comandi di Visual Studio in Windows 7. Per altre informazioni, vedere [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 Al prompt dei comandi digitare quanto segue:  
  
## <a name="syntax"></a>Sintassi  
  
```  
ngen action [options]  
```  
  
```  
ngen /? | /help  
```  
  
## <a name="actions"></a>Azioni  
 Nella tabella riportata di seguito viene illustrata la sintassi di ciascuna `action`. Per le descrizioni delle singole parti di `action`, vedere le tabelle [Argomenti](#ArgumentTable), [Livelli di priorità](#PriorityTable), [Scenari](#ScenarioTable) e [Configurazione](#ConfigTable). Nella tabella [Opzioni](#OptionTable) vengono descritte le `options` e le opzioni della Guida.  
  
|Azione|Descrizione|  
|------------|-----------------|  
|`install` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`] [`/queue`[`:`{`1`&#124;`2`&#124;`3`}]]|Genera le immagini native per un assembly e le relative dipendenze e installa le immagini nella cache delle immagini native.<br /><br /> Se si specifica l'opzione `/queue`, l'azione viene accodata per il servizio immagini native. La priorità predefinita è 3. Vedere la tabella [Livelli di priorità](#PriorityTable).|  
|`uninstall` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`]|Elimina le immagini native di un assembly e le relative dipendenze dalla cache delle immagini native.<br /><br /> Per disinstallare una singola immagine e le relative dipendenze, ricorrere agli stessi argomenti della riga di comando usati per l'installazione dell'immagine. **Nota:** a partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] l'azione `uninstall`* non è più supportata.|  
|`update` [`/queue`]|Aggiorna le immagini native diventate non valide.<br /><br /> Se si specifica l'opzione `/queue`, gli aggiornamenti vengono accodati per il servizio immagini native. Gli aggiornamenti vengono sempre pianificati con priorità 3, in modo da essere eseguiti durante i periodi di inattività del computer.|  
|`display` [`assemblyName` &#124; `assemblyPath`]|Visualizza lo stato delle immagini native di un assembly e le relative dipendenze.<br /><br /> Se non viene fornito alcun argomento, verrà visualizzato l'intero contenuto della cache delle immagini native.|  
|`executeQueuedItems` [`1``&#124;``2``&#124;``3`]<br /><br /> -oppure-<br /><br /> `eqi` [1&#124;2&#124;3]|Esegue i processi di compilazione accodati.<br /><br /> Se è specificata una priorità, verranno eseguiti i processi di compilazione che hanno un livello di priorità maggiore o uguale a quello specificato. Se non è specificata alcuna priorità, verranno eseguiti tutti i processi di compilazione accodati.|  
|`queue` {`pause` &#124; `continue` &#124; `status`}|Sospende il servizio immagini native, riprende il servizio sospeso o esegue una query sullo stato del servizio.|  
  
<a name="ArgumentTable"></a>   
## <a name="arguments"></a>Argomenti  
  
|Argomento|Descrizione|  
|--------------|-----------------|  
|`assemblyName`|Nome visualizzato completo dell'assembly. Ad esempio `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`. **Nota:** è possibile fornire un nome parziale di assembly, ad esempio `myAssembly`, per le azioni `display` e `uninstall`. <br /><br /> È possibile specificare un solo assembly per ogni riga di comando di Ngen.exe.|  
|`assemblyPath`|Percorso esplicito dell'assembly. È possibile specificare un percorso completo o relativo.<br /><br /> Se si specifica un nome di file senza percorso, l'assembly deve trovarsi nella directory corrente.<br /><br /> È possibile specificare un solo assembly per ogni riga di comando di Ngen.exe.|  
  
<a name="PriorityTable"></a>   
## <a name="priority-levels"></a>Livelli di priorità  
  
|Priorità|Descrizione|  
|--------------|-----------------|  
|`1`|Le immagini native vengono generate e installate immediatamente, senza attendere il tempo di inattività.|  
|`2`|Le immagini native vengono generate e installate senza attendere il tempo di inattività, ma dopo il completamento di tutte le azioni con priorità 1 (e delle relative dipendenze).|  
|`3`|Le immagini native vengono installate quando il relativo servizio rileva lo stato di inattività del computer. Vedere [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).|  
  
<a name="ScenarioTable"></a>   
## <a name="scenarios"></a>Scenari  
  
|Scenario|Descrizione|  
|--------------|-----------------|  
|`/Debug`|Genera immagini native utilizzabili con un debugger.|  
|`/Profile`|Genera immagini native utilizzabili con un profiler.|  
|`/NoDependencies`|Genera il numero minimo di immagini native richiesto dalle opzioni dello scenario specificato.|  
  
<a name="ConfigTable"></a>   
## <a name="config"></a>Config  
  
|Configurazione|Descrizione|  
|-------------------|-----------------|  
|`/ExeConfig:` `exePath`|Usa la configurazione dell'assembly eseguibile specificato.<br /><br /> Al momento dell'associazione alle dipendenze, le decisioni di Ngen.exe devono coincidere con quelle del caricatore. Quando un componente condiviso viene caricato in fase di esecuzione, mediante il metodo <xref:System.Reflection.Assembly.Load%2A>, il file di configurazione dell'applicazione determina le dipendenze che devono essere caricate per il componente condiviso, ad esempio la versione di una dipendenza caricata. L'opzione `/ExeConfig` indica a Ngen.exe le dipendenze che verranno caricate in fase di esecuzione.|  
|`/AppBase:` `directoryPath`|Al momento dell'individuazione delle dipendenze, la directory specificata viene usata come base dell'applicazione.|  
  
<a name="OptionTable"></a>   
## <a name="options"></a>Opzioni  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|`/nologo`|Evita la visualizzazione del messaggio di avvio Microsoft.|  
|`/silent`|Evita la visualizzazione dei messaggi di operazione riuscita.|  
|`/verbose`|Visualizza informazioni dettagliate per il debug. **Nota:** a causa di limitazioni del sistema operativo, in Windows 98 e Windows Millennium Edition viene visualizzata una quantità ridotta di informazioni aggiuntive.|  
|`/help`, `/?`|Visualizza la sintassi e le opzioni di comando della versione corrente.|  
  
## <a name="remarks"></a>Note  
 Per eseguire Ngen.exe, è necessario disporre di privilegi amministrativi.  
  
> [!CAUTION]
>  Non eseguire Ngen.exe su assembly che non sono completamente attendibili. A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Ngen.exe compila assembly con attendibilità totale e i criteri di sicurezza dall'accesso di codice non vengono più valutati.  
  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], le immagini native generate con Ngen.exe non possono più essere caricate in applicazioni in modalità di esecuzione parzialmente attendibile. Viene invece richiamato il compilatore JIT.  
  
 Ngen.exe genera immagini native per l'assembly specificato dall'argomento `assemblyname` di `install` e tutte le relative dipendenze. Le dipendenze vengono determinate in base ai riferimenti presenti nel manifesto dell'assembly. L'unico scenario in cui è necessario installare separatamente una dipendenza si verifica quando l'applicazione ne esegue il caricamento tramite reflection, ad esempio chiamando il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>.  
  
> [!IMPORTANT]
>  Non usare il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> con le immagini native. Un'immagine caricata con questo metodo non può essere usata da altri assembly nel contesto di esecuzione.  
  
 Lo strumento Ngen.exe gestisce un conteggio delle dipendenze. Si supponga, ad esempio, che `MyAssembly.exe` e `YourAssembly.exe` siano installati nella cache delle immagini native e che entrambi contengano riferimenti a `OurDependency.dll`. Se `MyAssembly.exe` viene disinstallato, `OurDependency.dll` non verrà disinstallato. Quest'ultimo verrà rimosso soltanto dopo la disinstallazione di `YourAssembly.exe`.  
  
 Se si sta generando un'immagine nativa per un assembly nella Global Assembly Cache, è necessario specificare il relativo nome visualizzato. Vedere <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName>.  
  
 Le immagini native generate da Ngen.exe possono essere condivise tra più domini applicazione. È pertanto possibile usare Ngen.exe in scenari di applicazioni che richiedono la condivisione di assembly tra più domini applicazione. Per specificare l'indipendenza dal dominio, effettuare le seguenti operazioni:  
  
-   Applicare l'attributo <xref:System.LoaderOptimizationAttribute> all'applicazione.  
  
-   Impostare la proprietà <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=fullName> quando si creano le informazioni di impostazione di un nuovo dominio applicazione.  
  
 Per il caricamento dello stesso assembly in più domini applicazione si consiglia di usare sempre codice indipendente dal dominio. Un'immagine nativa caricata in un dominio applicazione non condiviso dopo essere stata caricata in un dominio condiviso non può essere usata.  
  
> [!NOTE]
>  Il codice indipendente dal dominio non può essere scaricato e le prestazioni potranno risultare leggermente inferiori, in particolare durante l'accesso ai membri statici.  
  
 Nella sezione Osservazioni:  
  
-   [Generazione delle immagini per scenari diversi](#Scenarios)  
  
-   [Uso delle immagini native](#WhenToUse)  
  
    -   [Uso più efficiente della memoria](#Memory)  
  
    -   [Avvio più rapido delle applicazioni](#Startup)  
  
    -   [Riepilogo delle considerazioni sull'utilizzo](#UsageSummary)  
  
-   [Importanza degli indirizzi di base degli assembly](#BaseAddresses)  
  
-   [Hard binding](#HardBinding)  
  
    -   [Specifica di un suggerimento di binding per una dipendenza](#DependencyHint)  
  
    -   [Specifica di un suggerimento di binding predefinito per un assembly](#AssemblyHint)  
  
-   [Rinvio dell'elaborazione](#Deferred)  
  
-   [Immagini native e compilazione JIT](#JITCompilation)  
  
    -   [Immagini non valide](#InvalidImages)  
  
-   [Risoluzione dei problemi](#Troubleshooting)  
  
    -   [Visualizzatore log binding assembly](#Fusion)  
  
    -   [Assistente al debug gestito JITCompilationStart](#MDA)  
  
    -   [Rifiuto esplicito della generazione di immagini native](#OptOut)  
  
<a name="Scenarios"></a>   
## <a name="generating-images-for-----different-scenarios"></a>Generazione delle immagini per scenari diversi  
 Una volta generata l'immagine nativa di un assembly, il runtime tenta automaticamente di individuarla e usarla ogni volta che viene eseguito l'assembly. Possono essere generate più immagini, a seconda degli scenari di utilizzo.  
  
 Se ad esempio si esegue un assembly in uno scenario di debug o di profilatura, il runtime cercherà un'immagine nativa generata con le opzioni `/Debug` o `/Profile`. Se non è possibile individuare un'immagine nativa corrispondente, verrà ripristinata la compilazione JIT standard. L'unico modo per eseguire il debug delle immagini native consiste nel creare un'immagine nativa con l'opzione `/Debug`.  
  
 Poiché anche l'azione `uninstall` supporta gli scenari, è possibile disinstallare tutti gli scenari o solo quelli selezionati.  
  
<a name="WhenToUse"></a>   
## <a name="determining-when-to-use-native-images"></a>Uso delle immagini native  
 Le immagini native offrono i seguenti vantaggi prestazionali: utilizzo migliore della memoria e riduzione del tempo di avvio.  
  
> [!NOTE]
>  Le prestazioni delle immagini native dipendono da diversi fattori che possono risultare difficili da analizzare, ad esempio i modelli di accesso a dati e codice, il numero delle chiamate effettuate tra i vari moduli e il numero delle dipendenze già caricate da altre applicazioni. L'unico modo per determinare se l'applicazione può trarre benefici dall'utilizzo delle immagini native consiste nell'eseguire un'attenta valutazione delle prestazioni negli scenari di distribuzione chiave.  
  
<a name="Memory"></a>   
### <a name="improved-memory-use"></a>Uso più efficiente della memoria  
 Le immagini native possono migliorare in modo significativo l'utilizzo della memoria quando il codice è condiviso tra più processi. Poiché le immagini native sono file Windows di tipo PE, una singola copia di un file DLL può essere condivisa tra più processi. Il codice nativo prodotto dal compilatore JIT, invece, viene archiviato nella memoria privata e non può essere condiviso.  
  
 Anche le applicazioni che vengono eseguite in Servizi terminal possono ottenere vantaggi dall'utilizzo di tabelle codici condivise.  
  
 Inoltre, il mancato caricamento del compilatore JIT consente di risparmiare una quantità fissa di memoria per ciascuna istanza dell'applicazione.  
  
<a name="Startup"></a>   
### <a name="faster-application-startup"></a>Avvio più rapido delle applicazioni  
 La precompilazione degli assembly con Ngen.exe consente di ridurre il tempo di avvio di alcune applicazioni. In generale, i maggiori vantaggi si ottengono con le applicazioni che condividono assembly di componenti. In questo caso, infatti, una volta avviata la prima applicazione, i componenti condivisi risulteranno già caricati per le applicazioni successive. In caso di avvio a freddo, in cui tutti gli assembly di un'applicazione devono essere caricati dal disco rigido, le immagini native non offrono molti vantaggi poiché il tempo di accesso al disco rigido svolge un ruolo predominante.  
  
 L'associazione forte può influire negativamente sul tempo di avvio, poiché tutte le immagini associate in maniera forte all'assembly principale dell'applicazione devono essere caricate simultaneamente.  
  
> [!NOTE]
>  Per le versioni precedenti a [!INCLUDE[net_v35SP1_long](../../../includes/net-v35sp1-long-md.md)] è opportuno inserire i componenti condivisi con nome sicuro nella Global Assembly Cache, perché il caricatore esegue un ulteriore controllo di convalida sugli assembly con nome sicuro che non si trovano nella Global Assembly Cache, annullando quindi qualsiasi miglioramento a livello di tempo di avvio ottenuto grazie alle immagini native. Con le ottimizzazioni introdotte in [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] è stata rimossa la convalida aggiuntiva.  
  
<a name="UsageSummary"></a>   
### <a name="summary-of-usage-considerations"></a>Riepilogo delle considerazioni sull'utilizzo  
 Di seguito sono riportate alcune considerazioni di carattere generale e specifiche per le applicazioni che possono aiutare a decidere se l'utilizzo delle immagini native può essere una soluzione vantaggiosa per la propria applicazione.  
  
-   Le immagini native vengono caricate più rapidamente rispetto al codice MSIL, poiché eliminano la necessità di eseguire molte attività di avvio, ad esempio la compilazione JIT e la verifica dell'indipendenza dai tipi.  
  
-   Le immagini native richiedono un working set iniziale più piccolo, poiché il compilatore JIT non è necessario.  
  
-   Le immagini native consentono di condividere il codice tra più processi.  
  
-   Le immagini native occupano una quantità di spazio su disco maggiore rispetto agli assembly MSIL e possono richiedere molto tempo per la generazione.  
  
-   Per le immagini native sono necessarie alcune attività di gestione.  
  
    -   Le immagini devono essere rigenerate quando vengono apportate delle modifiche all'assembly originale o a una delle relative dipendenze.  
  
    -   È possibile che uno stesso assembly richieda più immagini native da usare in applicazioni o scenari differenti. Ad esempio, le informazioni di configurazione in due applicazioni potrebbero comportare decisioni di associazione diverse per lo stesso assembly dipendente.  
  
    -   Le immagini native devono essere generate da un amministratore, ovvero da un account Windows del gruppo Administrators.  
  
 Oltre a queste considerazioni generali, per determinare se le immagini native possono offrire vantaggi in termini di prestazioni occorre valutare anche la natura dell'applicazione:  
  
-   Se l'applicazione viene eseguita in un ambiente che usa molti componenti condivisi, le immagini native consentiranno di condividere tali componenti tra più processi.  
  
-   Se l'applicazione usa più domini applicazione, le immagini native consentiranno di condividere le tabelle codici tra più domini.  
  
    > [!NOTE]
    >  In .NET Framework versioni 1.0 e 1.1, le immagini native non possono essere condivise tra più domini applicazione. Questa limitazione è stata rimossa nella versione 2.0 o successiva.  
  
-   Se l'applicazione verrà eseguita in Terminal Server, le immagini native consentiranno di condividere le tabelle codici.  
  
-   La compilazione in immagini native in genere comporta un miglioramento delle prestazioni per le applicazioni di grandi dimensioni, ma non per quelle di piccole dimensioni.  
  
-   Per le applicazioni a esecuzione prolungata, la compilazione JIT in fase di esecuzione offre prestazioni leggermente migliori rispetto alle immagini native, anche se tale differenza può comunque essere ridotta mediante l'utilizzo dell'associazione forte.  
  
<a name="BaseAddresses"></a>   
## <a name="importance-of-assembly-base-addresses"></a>Importanza degli indirizzi di base degli assembly  
 Poiché sono file Windows di tipo PE, le immagini native sono soggette agli stessi problemi di rilocazione degli altri file eseguibili. L'impatto della rilocazione sulle prestazioni risulta ancora più accentuato in caso di utilizzo dell'associazione forte.  
  
 Per impostare l'indirizzo di base di un'immagine nativa, usare l'opzione appropriata del compilatore per impostare l'indirizzo di base dell'assembly, che verrà quindi usato da Ngen.exe come indirizzo di base dell'immagine nativa.  
  
> [!NOTE]
>  Le immagini native sono più grandi rispetto agli assembly gestiti da cui sono state create. Gli indirizzi di base devono quindi essere calcolati tenendo conto di queste dimensioni maggiori.  
  
 Per visualizzare l'indirizzo di base preferenziale di un'immagine nativa è possibile usare uno strumento quale dumpbin.exe.  
  
<a name="HardBinding"></a>   
## <a name="hard-binding"></a>Hard binding  
 L'associazione forte consente di aumentare la velocità effettiva e ridurre la dimensione del working set per le immagini native. Lo svantaggio consiste nel fatto che tutte le immagini associate in maniera forte a un assembly devono essere caricate al momento del caricamento dell'assembly, cosa che può provocare un aumento significativo del tempo di avvio per un'applicazione di grandi dimensioni.  
  
 L'associazione forte è appropriata per le dipendenze che vengono caricate in tutti gli scenari dell'applicazione in cui è fondamentale che le prestazioni siano elevate. Come accade con qualsiasi altro aspetto relativo all'utilizzo delle immagini native, l'unico modo per determinare se l'associazione forte è in grado di migliorare le prestazioni dell'applicazione consiste in un'attenta valutazione delle prestazioni.  
  
 Gli attributi <xref:System.Runtime.CompilerServices.DependencyAttribute> e <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> consentono di fornire a Ngen.exe alcuni suggerimenti per l'utilizzo dell'associazione forte.  
  
> [!NOTE]
>  Questi attributi non sono comandi ma semplici suggerimenti e il loro utilizzo non garantisce l'associazione forte. Il significato di questi attributi potrebbe cambiare nelle versioni future.  
  
<a name="DependencyHint"></a>   
### <a name="specifying-a-binding-hint-for-a-dependency"></a>Specifica di un suggerimento di binding per una dipendenza  
 Applicare <xref:System.Runtime.CompilerServices.DependencyAttribute> a un assembly per indicare la probabilità che una dipendenza specificata venga caricata. <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=fullName> indica che l'associazione forte è appropriata, <xref:System.Runtime.CompilerServices.LoadHint.Default> indica che deve essere usato il valore predefinito per la dipendenza e <xref:System.Runtime.CompilerServices.LoadHint.Sometimes> indica che l'associazione forte non è appropriata.  
  
 Nell'esempio di codice riportato di seguito vengono illustrati gli attributi per un assembly con due dipendenze. La prima dipendenza (Assembly1) è un candidato appropriato per l'associazione forte, al contrario della seconda (Assembly2).  
  
```vb  
Imports System.Runtime.CompilerServices  
<Assembly:DependencyAttribute("Assembly1", LoadHint.Always)>  
<Assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)>  
```  
  
```csharp  
using System.Runtime.CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)]  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)]  
```  
  
```cpp#  
using namespace System::Runtime::CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)];  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)];  
```  
  
 Il nome dell'assembly non include l'estensione ed è possibile usare i nomi visualizzati.  
  
<a name="AssemblyHint"></a>   
### <a name="specifying-a-default-binding-hint-for-an-assembly"></a>Specifica di un suggerimento di binding predefinito per un assembly  
 I suggerimenti di associazione predefinita sono necessari solo per gli assembly che verranno usati immediatamente e di frequente da una qualsiasi applicazione che prevede una dipendenza da tali assembly. Applicare <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> con <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=fullName> a tali assembly per specificare che deve essere usata l'associazione forte.  
  
> [!NOTE]
>  Non esiste alcun motivo per applicare <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> agli assembly DLL che non rientrano in questa categoria, poiché l'applicazione dell'attributo con un qualsiasi valore diverso da <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=fullName> equivale a non applicare l'attributo.  
  
 Microsoft usa <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> per specificare che l'associazione forte è l'impostazione predefinita per un numero molto piccolo di assembly in .NET Framework, ad esempio mscorlib.dll.  
  
<a name="Deferred"></a>   
## <a name="deferred-processing"></a>Rinvio dell'elaborazione  
 La generazione delle immagini native per un'applicazione di grandi dimensioni può richiedere molto tempo. In modo analogo, le modifiche a un componente condiviso o alle impostazioni del computer potrebbero richiedere l'aggiornamento di numerose immagini native. Per le azioni `install` e `update` è disponibile un'opzione `/queue` che accoda l'operazione per rinviare l'esecuzione tramite il servizio immagini native. Inoltre, Ngen.exe include le azioni `queue` e `executeQueuedItems` che forniscono un certo grado di controllo sul servizio. Per altre informazioni, vedere [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
<a name="JITCompilation"></a>   
## <a name="native-images-and-jit-compilation"></a>Immagini native e compilazione JIT  
 Se Ngen.exe individua in un assembly metodi che non possono essere generati, li esclude dall'immagine nativa. Quando il runtime eseguirà questo assembly, utilizzerà la compilazione JIT per i metodi che non sono stati inclusi nell'immagine nativa.  
  
 Inoltre, le immagini native non vengono usate se l'assembly è stato aggiornato o se l'immagine è stata invalidata per qualche motivo.  
  
<a name="InvalidImages"></a>   
### <a name="invalid-images"></a>Immagini non valide  
 Quando si usa Ngen.exe per creare un'immagine nativa di un assembly, l'output dipenderà dalle opzioni della riga di comando specificate e da alcune impostazioni del computer, incluse le seguenti:  
  
-   Versione di .NET Framework.  
  
-   Versione del sistema operativo, se si è passati dalla famiglia Windows 9x alla famiglia Windows NT.  
  
-   Identità esatta dell'assembly (l'identità cambia ad ogni ricompilazione).  
  
-   Identità esatta di tutti gli assembly a cui l'assembly fa riferimento (l'identità cambia ad ogni ricompilazione).  
  
-   Fattori di sicurezza.  
  
 Quando genera un'immagine nativa, Ngen.exe registra queste informazioni. Quando si esegue un assembly, il runtime cerca l'immagine nativa generata con le opzioni e le impostazioni che corrispondono all'ambiente corrente del computer. Se non viene individuata un'immagine nativa corrispondente, viene ripristinata la compilazione JIT di un assembly. Le modifiche alle impostazioni e all'ambiente di un computer che rendono non valide le immagini native sono le seguenti:  
  
-   Versione di .NET Framework.  
  
     Se viene eseguito un aggiornamento di .NET Framework, tutte le immagini native create usando Ngen.exe non saranno più valide. Per questo motivo, tutti gli aggiornamenti di .NET Framework eseguono il comando `Ngen Update` per assicurare che tutte le immagini native vengano rigenerate. .NET Framework crea automaticamente nuove immagini native per le librerie di .NET Framework installate.  
  
-   Versione del sistema operativo, se si è passati dalla famiglia Windows 9x alla famiglia Windows NT.  
  
     Se ad esempio la versione del sistema operativo in esecuzione su un computer passa da Windows 98 a Windows XP, tutte le immagini native archiviate nella cache delle immagini native non sono più valide. Tuttavia, se si passa da Windows 2000 a Windows XP, le immagini continuano a essere valide.  
  
-   Identità esatta dell'assembly.  
  
     Se si ricompila un assembly, l'immagine nativa corrispondente diventerà non valida.  
  
-   Identità esatta di tutti gli assembly a cui fa riferimento l'assembly.  
  
     Se si aggiorna un assembly gestito, tutte le immagini native che dipendono direttamente o indirettamente dall'assembly in questione diventano non valide e devono essere rigenerate. Sono inclusi in tal senso i riferimenti ordinari e le dipendenze con associazione forte. Ogni volta che viene applicato un aggiornamento software, il programma di installazione dovrebbe eseguire un comando `Ngen Update` per assicurare le rigenerazione di tutte le immagini native dipendenti.  
  
-   Fattori di sicurezza.  
  
     La modifica dei criteri di sicurezza del computer per limitare le autorizzazioni concesse in precedenza a un assembly può rendere non valida un'immagine nativa compilata in precedenza per l'assembly in questione.  
  
     Per informazioni dettagliate sulla gestione della sicurezza dall'accesso di codice in Common Language Runtime e sull'uso delle autorizzazioni, vedere [Sicurezza dall'accesso di codice](../../../docs/framework/misc/code-access-security.md).  
  
<a name="Troubleshooting"></a>   
## <a name="troubleshooting"></a>Risoluzione dei problemi  
 Gli argomenti seguenti per la risoluzione dei problemi consentono di vedere quali immagini native vengono usate dall'applicazione e quali non possono essere usate da questa per determinare quando il compilatore JIT inizia a compilare un metodo. Illustrano anche come rifiutare esplicitamente la compilazione di immagini native di metodi specificati.  
  
<a name="Fusion"></a>   
### <a name="assembly-binding-log-viewer"></a>Visualizzatore registro associazione assembly  
 Per assicurarsi che le immagini native vengano usate dall'applicazione, è possibile usare lo strumento [Fuslogvw.exe (Visualizzatore log binding assembly)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md). Selezionare **Immagini native** nella casella **Categorie log** della finestra del visualizzatore dei log di binding. Questo strumento fornisce informazioni sul motivo del rifiuto di un'immagine nativa.  
  
<a name="MDA"></a>   
### <a name="the-jitcompilationstart-managed-debugging-assistant"></a>Assistente al debug gestito JITCompilationStart  
 È possibile usare l'assistente al debug gestito [jitCompilationStart](../../../docs/framework/debug-trace-profile/jitcompilationstart-mda.md) per determinare quando il compilatore JIT inizia a compilare una funzione.  
  
<a name="OptOut"></a>   
### <a name="opting-out-of-native-image-generation"></a>Rifiuto esplicito della generazione di immagini native  
 In alcuni casi, NGen.exe può incontrare difficoltà nella generazione di un'immagine nativa per un metodo specifico oppure può essere preferibile compilare il metodo tramite JIT anziché compilarlo in un'immagine nativa. In questo caso, è possibile usare l'attributo `System.Runtime.BypassNGenAttribute` per evitare che NGen.exe generi un'immagine nativa per un metodo specifico. L'attributo deve essere applicato singolarmente a ogni metodo di cui non si vuole includere il codice nell'immagine nativa. NGen.exe riconosce l'attributo e per il metodo corrispondente non genera codice nell'immagine nativa.  
  
 Si noti tuttavia che `BypassNGenAttribute` non è definito come tipo nella libreria di classi di .NET Framework. Per utilizzare l'attributo nel codice, è prima necessario definirlo come indicato di seguito:  
  
 [!code-csharp[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#1)] [!code-vb[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#1)]  
  
 È quindi possibile applicare l'attributo sulla base di ciascun metodo. L'esempio seguente indica al generatore di immagini native di non generare un'immagine nativa per il metodo `ExampleClass.ToJITCompile`.  
  
 [!code-csharp[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#2)] [!code-vb[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#2)]  
  
## <a name="examples"></a>Esempi  
 Il comando che segue genera un'immagine nativa per `ClientApp.exe`, situato nella directory corrente, e la installa nella cache delle immagini native. Se esiste un file di configurazione per l'assembly, tale file verrà usato da Ngen.exe. Vengono inoltre generate immagini native per gli eventuali file DLL a cui fa riferimento `ClientApp.exe`.  
  
```  
ngen install ClientApp.exe  
```  
  
 Un'immagine installata con Ngen.exe viene anche detta radice. Una radice può essere un'applicazione o un componente condiviso.  
  
 Il comando che segue genera un'immagine nativa per `MyAssembly.exe` con il percorso specificato.  
  
```  
ngen install c:\myfiles\MyAssembly.exe  
```  
  
 Per l'individuazione degli assembly e delle relative dipendenze, Ngen.exe usa la stessa logica di sondaggio usata da Common Language Runtime. Per impostazione predefinita, la directory contenente `ClientApp.exe` viene usata come directory di base dell'applicazione e il sondaggio alla ricerca degli assembly inizia in questa directory. È possibile sostituire questo comportamento usando l'opzione `/AppBase`.  
  
> [!NOTE]
>  Si tratta di una variazione rispetto al comportamento di Ngen.exe in .NET Framework versioni 1.0 e 1.1, in cui la base dell'applicazione viene impostata sulla directory corrente.  
  
 Un assembly può avere una dipendenza senza un riferimento, ad esempio se carica un file DLL usando il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>. È possibile creare un'immagine nativa per tale file usando le informazioni di configurazione dell'assembly dell'applicazione, con l'opzione `/ExeConfig`. Il comando che segue genera un'immagine nativa per `MyLib.dll,` usando le informazioni di configurazione di `MyApp.exe`.  
  
```  
ngen install c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Gli assembly installati con questa modalità non vengono rimossi se l'applicazione viene rimossa.  
  
 Per disinstallare una dipendenza, è necessario usare le stesse opzioni della riga di comando usate per l'installazione. Il comando che segue disinstalla il file `MyLib.dll` dell'esempio precedente.  
  
```  
ngen uninstall c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Per creare un'immagine nativa per un assembly nella Global Assembly Cache, usare il nome visualizzato dell'assembly, Ad esempio:  
  
```  
ngen install "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
```  
  
 Ngen.exe genera un set di immagini separato per ciascuno scenario installato. I comandi che seguono, ad esempio, installano un set completo di immagini native per le normali operazioni, un altro set completo per il debug e un terzo per la profilatura:  
  
```  
ngen install MyApp.exe  
ngen install MyApp.exe /debug  
ngen install MyApp.exe /profile  
```  
  
### <a name="displaying-the-native-image-cache"></a>Visualizzazione della cache delle immagini native  
 Una volta installate immagini native nella cache, è possibile visualizzarle usando Ngen.exe. Il comando che segue visualizza tutte le immagini native presenti nella cache delle immagini native.  
  
```  
ngen display  
```  
  
 L'azione `display` elenca tutti gli assembly radice seguiti da un elenco di tutte le immagini native presenti sul computer.  
  
 Usare il nome semplice di un assembly per visualizzare soltanto le informazioni relative a tale assembly. Il comando che segue visualizza tutte le immagini native contenute nella cache delle immagini native corrispondenti al nome parziale `MyAssembly`, tutte le relative dipendenze e tutte le radici che dipendono da `MyAssembly`:  
  
```  
ngen display MyAssembly  
```  
  
 La possibilità di sapere quali radici dipendono da un assembly di un componente condiviso risulta utile per la valutazione dell'impatto di un'azione `update` dopo l'aggiornamento del componente condiviso.  
  
 Se si specifica l'estensione di file di un assembly, è necessario specificare il percorso o eseguire Ngen.exe dalla directory contenente l'assembly:  
  
```  
ngen display c:\myApps\MyAssembly.exe  
```  
  
 Il comando che segue visualizza tutte le immagini native contenute nella cache delle immagini native con nome `MyAssembly` e versione 1.0.0.0.  
  
```  
ngen display "myAssembly, version=1.0.0.0"  
```  
  
### <a name="updating-images"></a>Aggiornamento delle immagini  
 Le immagini in genere vengono aggiornate dopo l'aggiornamento di un componente condiviso. Per aggiornare tutte le immagini native modificate, o le cui dipendenze sono state modificate, usare l'azione `update` senza alcun argomento.  
  
```  
ngen update  
```  
  
 L'aggiornamento di tutte le immagini può richiedere molto tempo. Per questo motivo, è possibile usare l'opzione `/queue` per accodare gli aggiornamenti in modo che vengano eseguiti dal servizio immagini native. Per altre informazioni sull'opzione `/queue` e sulle priorità di installazione, vedere [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
```  
ngen update /queue  
```  
  
### <a name="uninstalling-images"></a>Disinstallazione delle immagini  
 Poiché Ngen.exe mantiene un elenco di dipendenze, i componenti condivisi verranno rimossi solo quando saranno stati rimossi tutti gli assembly che dipendono da tali componenti. Inoltre, un componente condiviso installato come radice non verrà mai rimosso.  
  
 Il comando che segue disinstalla tutti gli scenari per la radice `ClientApp.exe`:  
  
```  
ngen uninstall ClientApp  
```  
  
 L'azione `uninstall` può essere usata per rimuovere scenari specifici. Il comando che segue disinstalla tutti gli scenari di debug per `ClientApp.exe`:  
  
```  
ngen uninstall ClientApp /debug  
```  
  
> [!NOTE]
>  La disinstallazione degli scenari `/debug` non comporta la disinstallazione di uno scenario che include sia `/profile` che `/debug.`  
  
 Il comando che segue disinstalla tutti gli scenari per una versione specifica di `ClientApp.exe`:  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0"  
```  
  
 I comandi che seguono disinstallano tutti gli scenari per `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",` o semplicemente lo scenario di debug per tale assembly:  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL" /debug  
```  
  
 Come con l'azione `install`, l'eventuale presenza dell'estensione richiede l'esecuzione di Ngen.exe dalla directory contenente l'assembly o la specifica di un percorso completo.  
  
 Per esempi relativi al servizio immagini native, vedere [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
## <a name="native-image-task"></a>Attività di immagini native  
 L'attività di immagini native è un'attività di Windows che esegue automaticamente la generazione e la gestione delle immagini native. L'attività di immagini native genera e recupera le immagini native automaticamente per gli scenari supportati Vedere [Creazione di immagini native](http://msdn.microsoft.com/en-us/2bc8b678-dd8d-4742-ad82-319e9bf52418). Consente poi ai programmi di installazione di usare [Ngen.exe (generatore di immagini native)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) per creare e aggiornare le immagini native a un'ora posticipata.  
  
 L'attività di immagini native viene registrata una volta per ogni architettura della CPU supportata in un computer, per consentire la compilazione di applicazioni destinate a ogni architettura:  
  
|Nome attività|Computer a 32 bit|Computer a 64 bit|  
|---------------|----------------------|----------------------|  
|NET Framework NGEN v4.0.30319|Sì|Sì|  
|NET Framework NGEN v4.0.30319 64|No|Sì|  
  
 L'attività di immagine nativa è disponibile in .NET Framework 4.5 e versioni successive quando eseguita in Windows 8 o versioni successive. Nelle versioni precedenti di Windows, .NET Framework usa il [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309).  
  
### <a name="task-lifetime"></a>Durata delle attività  
 L'utilità di pianificazione di Windows avvia, in genere, l'attività delle immagini native ogni notte quando il computer è inattivo. L'attività controlla ogni lavoro posticipato che viene accodato dai programmi di installazione, eventuali richieste di aggiornamento di immagine nativa posticipate ed eventuali creazioni automatiche di immagini. L'attività completa gli elementi di lavoro in sospeso e quindi viene chiusa. Se il computer diviene attivo mentre l'attività è in esecuzione, l'attività viene interrotta.  
  
 È anche possibile avviare l'attività dell'immagine nativa manualmente tramite l'interfaccia utente dell'utilità di pianificazione o con chiamate manuali a NGen.exe. Se l'attività viene avviata con uno di questi metodi, essa continuerà l'esecuzione quando il computer non è più inattivo. Le immagini create manualmente usando NGen.exe hanno priorità maggiore per abilitare il comportamento prevedibile dei programmi di installazione delle applicazioni.  
  
## <a name="native-image-service"></a>Servizio immagini native  
 Il servizio immagini native è un servizio Windows che esegue automaticamente la generazione e la gestione delle immagini native. Questo servizio consente allo sviluppatore di differire le azioni di installazione e aggiornamento delle immagini native in modo che vengano eseguite nei periodi di inattività del computer.  
  
 Il servizio immagini native viene in genere avviato dal programma di installazione di un'applicazione o di un aggiornamento. Per le azioni con priorità 3, il servizio viene eseguito durante il periodo di inattività del computer. Lo stato del servizio viene salvato automaticamente e, se necessario, l'esecuzione può riprendere anche dopo il riavvio del computer. È supportato l'accodamento di più compilazioni di immagini.  
  
 Il servizio interagisce anche con il comando Ngen.exe manuale. I comandi manuali hanno priorità sull'attività in background.  
  
> [!NOTE]
>  In Windows Vista il nome visualizzato per il servizio immagini native è "Microsoft.NET Framework NGEN v2.0.50727_X86" o "Microsoft.NET Framework NGEN v2.0.50727_X64". In tutte le versioni precedenti di Microsoft Windows il nome è ".NET Runtime Optimization Service v2.0.50727_X86" o ".NET Runtime Optimization Service v2.0.50727_X64".  
  
### <a name="launching-deferred-operations"></a>Avvio delle azioni differite  
 Prima di iniziare un'azione di installazione o aggiornamento, è opportuno sospendere il servizio. In questo modo si ha la garanzia che il servizio non venga eseguito durante la copia dei file o l'inserimento degli assembly nella Global Assembly Cache. Per sospendere l'esecuzione, usare il seguente comando di Ngen.exe:  
  
```  
ngen queue pause  
```  
  
 Quando tutte le azioni differite sono state accodate, il seguente comando consente di riprendere l'esecuzione del servizio:  
  
```  
ngen queue continue  
```  
  
 Per differire la generazione delle immagini native durante l'installazione di una nuova applicazione o l'aggiornamento di un componente condiviso, usare l'opzione `/queue` con le azioni `install` o `update`. Le seguenti stringhe di comando Ngen.exe determinano l'installazione di un'immagine nativa per un componente condiviso e l'esecuzione di un aggiornamento di tutte le radici che possono essere state modificate:  
  
```  
ngen install MyComponent /queue  
ngen update /queue  
```  
  
 L'azione `update` rigenera tutte le immagini native che sono state invalidate, non solo quelle che usano `MyComponent`.  
  
 Se l'applicazione è costituita da più radici, è possibile controllare la priorità delle azioni differite. I comandi riportati di seguito consentono di accodare l'installazione di tre radici. `Assembly1` viene installata per prima, senza attendere l'inattività del computer. Anche `Assembly2` viene installata senza attendere l'inattività, ma dopo il completamento delle azioni con priorità 1. `Assembly3` viene invece installata quando il servizio rileva lo stato di inattività del computer.  
  
```  
ngen install Assembly1 /queue:1  
ngen install Assembly2 /queue:2  
ngen install Assembly3 /queue:3  
```  
  
 È possibile imporre l'esecuzione simultanea delle azioni accodate usando `executeQueuedItems`. Se si specifica la priorità facoltativa, l'esecuzione simultanea ha effetto sulle azioni accodate con priorità uguale o inferiore. La priorità predefinita è 3. Di conseguenza, il comando Ngen.exe riportato di seguito elabora immediatamente tutte le azioni accodate e non restituisce il controllo finché non sono completate:  
  
```  
ngen executeQueuedItems  
```  
  
 I comandi sincroni vengono eseguiti da Ngen.exe e non usano il servizio immagini native. È possibile eseguire azioni mediante Ngen.exe mentre il servizio immagini native è in esecuzione.  
  
### <a name="service-shutdown"></a>Chiusura del servizio  
 Dopo l'avvio mediante l'esecuzione di un comando Ngen.exe con l'opzione `/queue`, il servizio viene eseguito in background finché tutte le azioni non sono state completate. Lo stato del servizio viene salvato, in modo che l'esecuzione possa riprendere anche dopo vari riavvii del computer, se necessario. Quando viene rilevato che non sono più presenti azioni accodate, lo stato del servizio viene ripristinato per evitare che venga riavviato al successivo avvio del computer, quindi il servizio viene chiuso.  
  
### <a name="service-interaction-with-clients"></a>Interazione del servizio con i client  
 In .NET Framework versione 2.0 l'interazione con il servizio immagini native avviene solo tramite lo strumento da riga di comando Ngen.exe. Usare questo strumento negli script di installazione per accodare le azioni per il servizio immagini native e interagire con il servizio.  
  
## <a name="see-also"></a>Vedere anche  
 [Servizio immagini native](http://msdn.microsoft.com/en-us/b15e0e32-59cb-4ae4-967c-6c9527781309)   
 [Attività di immagini native](http://msdn.microsoft.com/en-us/9b1f7590-4e0d-4737-90ef-eaf696932afb)   
 [Strumenti](../../../docs/framework/tools/index.md)   
 [Processo di esecuzione gestita](../../../docs/standard/managed-execution-process.md)   
 [Come il runtime individua gli assembly](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)

