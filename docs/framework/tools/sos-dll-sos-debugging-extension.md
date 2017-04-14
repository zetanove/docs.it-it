---
title: "SOS.dll (estensione del debugger SOS) | Microsoft Docs"
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
  - "estensioni di debug"
  - "SOS (estensioni di debug)"
  - "SOS.dll"
ms.assetid: 9ac1b522-77ab-4cdc-852a-20fcdc9ae498
caps.latest.revision: 55
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 55
---
# SOS.dll (estensione del debugger SOS)
L'estensione del debugger SOS (SOS.dll) facilita l'esecuzione del debug di programmi gestiti in Visual Studio e nel debugger Windows (WinDbg.exe) fornendo informazioni sull'ambiente Common Language Runtime (CLR) interno. L'uso di questo strumento richiede l'abilitazione del debug non gestito nel progetto. SOS.dll viene installato automaticamente con .NET Framework. Per utilizzare SOS. dll in Visual Studio, installare il [Windows Driver Kit (WDK)](http://msdn.microsoft.com/windows/hardware/hh852362).  
  
> [!NOTE]
>  Se si utilizza [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], SOS.dll è supportato nel debugger Windows all'interno di Visual Studio, ma non nella finestra di controllo immediato del debugger di Visual Studio.  
  
## <a name="syntax"></a>Sintassi  
  
```  
![command] [options]   
```  
  
## <a name="commands"></a>Comandi:  
  
|Comando|Descrizione|  
|-------------|-----------------|  
|**AnalyzeOOM** (**ao**)|Visualizza le informazioni sull'ultimo evento di memoria insufficiente verificatosi in una richiesta di allocazione all'heap di Garbage Collection (in Garbage Collection per il server, visualizza le informazioni sulla memoria insufficiente, se disponibili, per ogni heap di Garbage Collection).|  
|**BPMD** [**-nofuturemodule**] [*module name*> *method name*>] [**-md** <`MethodDesc`>] **-list** **-clear** \<*pending breakpoint number*> **-clearall**|Crea un punto di interruzione in corrispondenza del metodo specificato nel modulo specificato.<br /><br /> Se il modulo e il metodo specificati non sono stati caricati, questo comando attende una notifica del caricamento e della compilazione JIT (just-in-time) del modulo prima di creare un punto di interruzione.<br /><br /> È possibile gestire l'elenco di in sospeso i punti di interruzione utilizzando il **-elenco**, **-deselezionare**, e **- clearall** opzioni:<br /><br /> Il **-elenco** opzione genera un elenco di tutti i punti di interruzione in sospeso. Se un punto di interruzione in sospeso dispone di un ID modulo diverso da zero, il punto di interruzione è specifico di una funzione in quel particolare modulo caricato. Se il punto di interruzione in sospeso dispone di un ID modulo pari a zero, il punto di interruzione si applica a moduli che non sono stati ancora caricati.<br /><br /> Utilizzare il **-deselezionare** o **- clearall** opzione per rimuovere in sospeso dall'elenco dei punti di interruzione.|  
|**CLRStack** [**-a**] [**-l**] [**-p**] [**-n**]|Fornisce l'analisi dello stack del solo codice gestito.<br /><br /> Il **-p** opzione Mostra gli argomenti della funzione gestita.<br /><br /> Il **-l** opzione Mostra le informazioni sulle variabili locali in un frame. L'estensione del debugger SOS non possono essere recuperati i nomi locali, l'output dei nomi locali è nel formato *indirizzo locale*> **=** \<*valore*>.<br /><br /> Il **-**opzione (all) sono un collegamento per **-l** e **-p**combinati.<br /><br /> Il **- n** opzione Disabilita la visualizzazione di nomi di file di origine e i numeri di riga. Se nel debugger è specificata l'opzione SYMOPT_LOAD_LINES, verranno ricercati i simboli di ogni frame gestito e, in caso di esito positivo, verranno visualizzati il nome del file di origine e il numero di riga corrispondenti. Il **- n** (Nessun numero di riga) parametro può essere specificato per disabilitare questo comportamento.<br /><br /> L'estensione del debugger SOS non supporta la visualizzazione di frame di transizione su piattaforme basate su x64 e IA-64.|  
|**COMState**|Elenca il modello di apartment COM per ogni thread e un puntatore `Context`, se disponibile.|  
|**DumpArray** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-details**] [**-nofields**] *array object address*><br /><br /> -oppure-<br /><br /> **DA** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-detail**] [**-nofields**] *array object address*>|Esamina gli elementi di un oggetto matrice.<br /><br /> Il **-start** opzione specifica l'indice iniziale in cui visualizzare gli elementi.<br /><br /> Il **-lunghezza** opzione specifica il numero di elementi da visualizzare.<br /><br /> Il **-dettagli** opzione consente di visualizzare i dettagli dell'elemento utilizzando il **DumpObj** e **DumpVC** formati.<br /><br /> Il **- nofields** opzione impedisce la visualizzazione di matrici. Questa opzione è disponibile solo quando il **-dettagli** opzione specificata.|  
|**DumpAssembly** \<*indirizzo di assembly*>|Visualizza informazioni su un assembly.<br /><br /> Il **DumpAssembly** comando elenca più moduli, se presenti.<br /><br /> È possibile ottenere l'indirizzo di un assembly utilizzando il **DumpDomain** comando.|  
|**DumpClass** \<*indirizzo EEClass*>|Visualizza informazioni sulla struttura `EEClass` associata a un tipo.<br /><br /> Il **DumpClass** comando Visualizza i valori dei campi statici e non visualizza valori di campi non statici.<br /><br /> Utilizzare il **comando DumpMT**, **DumpObj**, **Name2EE**, o **Token2EE** comando per ottenere un `EEClass` indirizzo della struttura.|  
|**DumpDomain** [*indirizzo del dominio*>]|Enumera tutti <xref:System.Reflection.Assembly> oggetto caricata all'interno di specificato <xref:System.AppDomain> indirizzo dell'oggetto.  Quando viene chiamato senza parametri, il **DumpDomain** comando Elenca tutti <xref:System.AppDomain> oggetti in un processo.|  
|**DumpHeap** [**-stat**] [**-strings**] [**-short**] [**-min** \<*size*>] [**-max** \<*size*>] [**-thinlock**] [**-startAtLowerBound**] [**-mt** \<*MethodTable address*>] [**-type** \<*partial type name*>][*start* [*end*]]|Visualizza le informazioni sull'heap sottoposto a procedura di Garbage Collection e le statistiche di raccolta relative agli oggetti.<br /><br /> Il **DumpHeap** comando Visualizza un avviso se rileva una frammentazione eccessiva nell'heap del garbage collector.<br /><br /> Il **-stat** opzione limita l'output al riepilogo di tipo statistico.<br /><br /> Il **-stringhe** opzione limita l'output a un riepilogo di valori di stringa statistici.<br /><br /> Il **-breve** opzione limita l'output a un solo indirizzo di ogni oggetto. In tal modo, è possibile inviare facilmente l'output dal comando a un altro comando del debugger per l'automazione.<br /><br /> Il **-min** opzione Ignora gli oggetti minori del `size` parametro, specificato in byte.<br /><br /> Il **-max** opzione Ignora gli oggetti che superano il `size` parametro, specificato in byte.<br /><br /> Il **- thinlock** opzione segnala presenza di thinlock.  Per ulteriori informazioni, vedere il **SyncBlk** comando.<br /><br /> L'opzione `-startAtLowerBound` forza l'inizio del percorso nell'heap al limite inferiore di un intervallo di indirizzi specificato. Durante la fase della pianificazione, l'heap spesso non è percorribile perché gli oggetti vengono spostati. Questa opzione forza **DumpHeap** per iniziare il percorso al limite inferiore specificato. È necessario fornire l'indirizzo di un oggetto valido come limite inferiore affinché questa opzione funzioni. È possibile visualizzare la memoria in corrispondenza dell'indirizzo di un oggetto non valido per trovare manualmente la tabella dei metodi successiva. Se il processo di Garbage Collection è attualmente impegnato in una chiamata a `memcopy`, è possibile riuscire a trovare l'indirizzo dell'oggetto successivo anche aggiungendo la dimensione all'indirizzo iniziale, fornito come parametro.<br /><br /> Il **- mt** opzione Elenca solo gli oggetti che corrispondono all'oggetto `MethodTable` struttura.<br /><br /> Il **-tipo** opzione Elenca solo gli oggetti il cui nome del tipo è una corrispondenza di sottostringa della stringa specificata.<br /><br /> Il parametro `start` inizia l'elenco a partire dall'indirizzo specificato.<br /><br /> Il parametro `end` arresta l'elenco in corrispondenza dell'indirizzo specificato.|  
|**DumpIL** \<*oggetto gestito DynamicMethod*> |       *DynamicMethodDesc puntatore*> |        *MethodDesc puntatore*>|Visualizza il linguaggio MSIL (Microsoft Intermediate Language) associato a un metodo gestito.<br /><br /> Il codice MSIL dinamico è generato in modo diverso rispetto al codice MSIL caricato da un assembly. Il codice MSIL dinamico fa riferimento agli oggetti in una matrice di oggetti gestiti anziché ai token di metadati.|  
|**DumpLog** [**-addr** \<*addressOfStressLog*>] [*Filenam*`e`>]|Scrive nel file specificato il contenuto di un log di stress in memoria. Se non si specifica un nome, questo comando crea un file denominato StressLog.txt nella directory corrente.<br /><br /> Il log di stress in memoria facilita la diagnosi degli errori da stress senza utilizzare blocchi o I/O. Per abilitare il log di stress, impostare le seguenti chiavi del Registro di sistema sotto HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\. NETFramework:<br /><br /> (DWORD) StressLog = 1<br /><br /> (DWORD) LogFacility = 0xffffffff<br /><br /> (DWORD) StressLogSize = 65536<br /><br /> L'opzione `-addr` facoltativa consente di specificare un log di stress diverso dal log predefinito.|  
|**DumpMD** \<*indirizzo MethodDesc*>|Visualizza informazioni su una struttura `MethodDesc` in corrispondenza dell'indirizzo specificato.<br /><br /> È possibile utilizzare il **IP2MD** comando per ottenere il `MethodDesc` indirizzo da una funzione gestita della struttura.|  
|**Comando DumpMT** [**-MD**] *indirizzo di MethodTable*>|Visualizza informazioni su una tabella dei metodi in corrispondenza dell'indirizzo specificato. Specifica il **-MD** opzione consente di visualizzare un elenco di tutti i metodi definiti con l'oggetto.<br /><br /> Ogni oggetto gestito contiene un puntatore alla tabella dei metodi.|  
|**DumpMethodSig** \<*sigaddr*> *moduleadd*`r`>|Visualizza informazioni su una struttura `MethodSig` in corrispondenza dell'indirizzo specificato.|  
|**DumpModule** [**- mt**] *indirizzo modulo*>|Visualizza informazioni su un modulo in corrispondenza dell'indirizzo specificato. Il **- mt** opzione consente di visualizzare i tipi definiti in un modulo e i tipi a cui fa riferimento il modulo<br /><br /> È possibile utilizzare il **DumpDomain** o **DumpAssembly** comando per recuperare l'indirizzo di un modulo.|  
|**DumpObj** [**- nofields**] *indirizzo dell'oggetto*><br /><br /> -oppure-<br /><br /> **ESEGUIRE** \<*indirizzo dell'oggetto*>|Visualizza informazioni su un oggetto in corrispondenza dell'indirizzo specificato. Il **DumpObj** comando Visualizza i campi di `EEClass` struttura informazioni, la tabella dei metodi e le dimensioni dell'oggetto.<br /><br /> È possibile utilizzare il **DumpStackObjects** comando per recuperare l'indirizzo di un oggetto.<br /><br /> Si noti che è possibile eseguire il **DumpObj** comando sui campi di tipo `CLASS` perché sono anche gli oggetti.<br /><br /> Il `-` **nofields** opzione impedisce campi dell'oggetto visualizzato, è utile per gli oggetti come stringa.|  
|**DumpRuntimeTypes**|Visualizza gli oggetti di tipo runtime nell'heap del Garbage Collector ed elenca i nomi dei tipi e le tabelle dei metodi associati.|  
|**DumpStack** [**-EE**] [**-n**] [`top` *stack* [`bottom` *stac*`k`]]|Visualizza l'analisi di uno stack.<br /><br /> Il **- EE** opzione il **DumpStack** comando visualizzi solo funzioni gestite. Utilizzare i parametri `top` e `bottom` per limitare gli stack frame visualizzati sulle piattaforme x86.<br /><br /> Il **- n** opzione Disabilita la visualizzazione di nomi di file di origine e i numeri di riga. Se nel debugger è specificata l'opzione SYMOPT_LOAD_LINES, verranno ricercati i simboli di ogni frame gestito e, in caso di esito positivo, verranno visualizzati il nome del file di origine e il numero di riga corrispondenti. Il **- n** (Nessun numero di riga) parametro può essere specificato per disabilitare questo comportamento.<br /><br /> Sulle piattaforme x86 e x64 il **DumpStack** comando crea una traccia dello stack dettagliata.<br /><br /> Sulle piattaforme basate su IA-64 il **DumpStack** comando simula il debugger **K** comando. I parametri `top` e `bottom` vengono ignorati sulle piattaforme basate su IA-64.|  
|**DumpSig** \<*sigaddr*> *moduleaddr*>|Visualizza informazioni su una struttura `Sig` in corrispondenza dell'indirizzo specificato.|  
|**DumpSigElem** \<*sigaddr*> *moduleaddr*>|Visualizza un singolo elemento di un oggetto firma. Nella maggior parte dei casi, è necessario utilizzare **DumpSig** esaminare singoli oggetti firma. Tuttavia, se una firma è stata danneggiata in qualche modo, è possibile utilizzare **DumpSigElem** per leggere le parti valide.|  
|**DumpStackObjects** [**-verify**] [`top` *stack* [`bottom` *stack*]]<br /><br /> -oppure-<br /><br /> **DSO** [**-verify**] [`top` *stack* [`bottom` *stack*]]|Visualizza tutti gli oggetti gestiti trovati nell'ambito dei limiti dello stack corrente.<br /><br /> Il **-verificare** opzione convalida ogni statiche `CLASS` campo di un campo dell'oggetto.<br /><br /> Utilizzare il **DumpStackObject** comando con i comandi di traccia dello stack, ad esempio il **K** comando e **CLRStack** comando per determinare i valori di parametri e variabili locali.|  
|**DumpVC** \<*indirizzo di MethodTable*> *indirizzo*>|Visualizza informazioni sui campi di una classe di valori in corrispondenza dell'indirizzo specificato.<br /><br /> Il **MethodTable** parametro consente di **DumpVC** comando per interpretare correttamente i campi. Le classi di valori non dispongono di una tabella dei metodi come primo campo.|  
|**EEHeap** [**-gc**] [**-loader**]|Visualizza informazioni sulla memoria di processo utilizzata dalle strutture dati Common Language Runtime interne.<br /><br /> Il **-gc** e **-caricatore** opzioni limitano l'output di questo comando alle strutture di dati del garbage collector o del caricatore.<br /><br /> Le informazioni relative al Garbage Collector elencano gli intervalli di ogni segmento nell'heap gestito.  Se il puntatore è compreso nell'intervallo di segmenti specificato da **-gc**, il puntatore è un puntatore all'oggetto.|  
|**EEStack** [**-short**] [**-EE**]|Viene eseguito il **DumpStack** comando su tutti i thread nel processo.<br /><br /> Il **- EE** viene passato direttamente all'opzione di **DumpStack** comando. Il **-breve** parametro limita l'output ai seguenti tipi di thread:<br /><br /> Thread che sono stati sottoposti a un blocco.<br /><br /> Thread bloccati per consentire un processo di Garbage Collection.<br /><br /> Thread che sono attualmente nel codice gestito.|  
|**EEVersion**|Visualizza la versione di Common Language Runtime.|  
|**EHInfo** [*indirizzo MethodDesc*>] [*codice indirizzo*>]|Visualizza i blocchi di gestione delle eccezioni in un metodo specificato.  Questo comando visualizza gli indirizzi e gli offset del codice per il blocco della clausola (il blocco `try`) e il blocco del gestore (il blocco `catch`).|  
|**DOMANDE FREQUENTI**|Visualizza le domande frequenti.|  
|**FinalizeQueue** [**-dettagli**] | [**-allReady**] [**-short**]|Visualizza tutti gli oggetti registrati per la finalizzazione.<br /><br /> Il **-dettagli** opzione consente di visualizzare informazioni aggiuntive su eventuali `SyncBlocks` che devono essere puliti e qualsiasi `RuntimeCallableWrappers` (RCW) in attesa di pulizia. Entrambe le strutture dati vengono memorizzate nella cache e pulite dal thread del finalizzatore in esecuzione.<br /><br /> L'opzione `-allReady` visualizza tutti gli oggetti pronti per la finalizzazione, indipendentemente dal fatto che siano già contrassegnati dall'operazione di Garbage Collection o se saranno contrassegnati dalla prossima operazione di Garbage Collection. Gli oggetti che sono nell'elenco "pronti per la finalizzazione" sono oggetti finalizzabili senza più radice. Questa opzione può essere molto costosa, perché verifica se tutti gli oggetti nelle code finalizzabili contengono ancora una radice.<br /><br /> L'opzione `-short` limita l'output all'indirizzo di ogni oggetto. Se viene utilizzato in combinazione con **- già**, enumera tutti gli oggetti che dispongono di un finalizzatore senza più radice. Se utilizzata in modo indipendente, elenca tutti gli oggetti nelle code di oggetti finalizzabili e "pronti per la finalizzazione".|  
|**FindAppDomain** \<*indirizzo dell'oggetto*>|Determina il dominio applicazione di un oggetto in corrispondenza dell'indirizzo specificato.|  
|**FindRoots** **-gen** \<*N*> | **-gen any** |* indirizzo dell'oggetto*>|Determina l'interruzione dell'oggetto del debug da parte del debugger alla raccolta successiva della generazione specificata. L'effetto viene reimpostato appena si verifica l'interruzione. Per impostare l'interruzione alla raccolta successiva, è necessario emettere nuovamente il comando. Il * <object></object> \> * formato di questo comando viene utilizzato dopo l'interruzione causata dal **-gen** o **-gen qualsiasi** si è verificato. In quel momento, l'oggetto del debug è nello stato giusto per **FindRoots** identifichi le radici degli oggetti dall'oggetto generazioni condannate.|  
|**GCHandles** [**- perdomain**]|Visualizza le statistiche relative agli handle del Garbage Collector nel processo.<br /><br /> Il **- perdomain** opzione Organizza le statistiche per dominio applicazione.<br /><br /> Utilizzare il **GCHandles** comando per individuare perdite di memoria causate da perdite degli handle di garbage collection. Una perdita di memoria si verifica ad esempio se nel codice viene mantenuta una matrice di grandi dimensioni perché un handle sicuro del Garbage Collector che punta ancora a essa viene eliminato senza liberarla.|  
|**GCHandleLeaks**|Ricerca nella memoria i riferimenti a handle sicuri e bloccati del Garbage Collector nel processo e visualizza i risultati. Se viene trovato un handle, il **GCHandleLeaks** comando Visualizza l'indirizzo del riferimento. Se invece in memoria non viene trovato alcun handle, il comando visualizza una notifica.|  
|**GCInfo** \<*indirizzo MethodDesc*>\<*indirizzo di codice*>|Visualizza i dati che indicano quando nei registri o nei percorsi dello stack sono contenuti oggetti gestiti. Se si verifica un'operazione di Garbage Collection, il Garbage Collector deve conoscere le posizioni dei riferimenti agli oggetti in modo da poterli aggiornare con i nuovi valori dei puntatori agli oggetti.|  
|**GCRoot** [**- nostacks**] *indirizzo dell'oggetto*>|Visualizza informazioni sui riferimenti (o radici) a un oggetto in corrispondenza dell'indirizzo specificato.<br /><br /> Il **GCRoot** comando esamina l'intero heap gestito e la tabella degli handle per gli handle all'interno di altri oggetti e handle nello stack. In ogni stack viene quindi eseguita la ricerca dei puntatori agli oggetti. Viene eseguita la ricerca anche nella coda del finalizzatore.<br /><br /> Questo comando non determina se la radice di uno stack è valida o viene ignorata. Utilizzare il **CLRStack** e **U** comandi per disassemblare il frame a cui appartiene il valore dell'argomento o locale in modo da determinare se la radice dello stack è ancora in uso.<br /><br /> Il **- nostacks** opzione restringe la ricerca agli handle del garbage collector e agli oggetti.|  
|**GCWhere**  *<object></object>\>*|Visualizza il percorso e le dimensioni dell'argomento passato nell'heap di Garbage Collection. Quando l'argomento rientra nell'heap gestito ma non è un indirizzo di oggetto valido, la dimensione viene visualizzata come 0 (zero).|  
|**help** [*command*>] [`faq`]|Visualizza tutti i comandi disponibili se non è specificato alcun parametro oppure visualizza informazioni di Guida dettagliate sul comando specificato.<br /><br /> Il parametro `faq` visualizza le risposte alle domande frequenti.|  
|**HeapStat** [**- inclUnrooted** | **-iu**]|Visualizza le dimensioni della generazione per ogni heap e lo spazio disponibile totale in ogni generazione su ogni heap. Se-**inclUnrooted** è specificata l'opzione, il report include informazioni sugli oggetti gestiti dall'heap di garbage collection che non è possibile eseguire.|  
|**HistClear**|Rilascia tutte le risorse utilizzate dalla famiglia di comandi `Hist`.<br /><br /> In genere non è necessario chiamare in modo esplicito `HistClear`, perché ogni `HistInit` pulisce le risorse precedenti.|  
|**HistInit**|Inizializza le strutture SOS dal log di stress salvato nell'oggetto del debug.|  
|**HistObj***<obj_address>*</obj_address>|Esamina tutti i record delle rilocazioni del log di stress e visualizza la catena di rilocazioni di Garbage Collection che hanno potuto condurre all'indirizzo passato come argomento.|  
|**HistObjFind**  *<obj_address>*</obj_address>|Visualizza tutte le voci del log che fanno riferimento a un oggetto in corrispondenza dell'indirizzo specificato.|  
|**HistRoot***<>\>*|Visualizza informazioni correlate sia alle promozioni sia alle rilocazioni della radice specificata.<br /><br /> Il valore radice può essere utilizzato per tenere traccia del movimento di un oggetto attraverso le operazioni di Garbage Collection.|  
|**IP2MD** \<*indirizzo di codice*>|Visualizza la struttura `MethodDesc` in corrispondenza dell'indirizzo specificato nel codice con compilazione JIT.|  
|`ListNearObj`(`lno`)*<obj_address>*</obj_address>|Visualizza gli oggetti che precedono e seguono l'indirizzo specificato. Il comando cerca l'indirizzo nell'heap di Garbage Collection che sembra un inizio valido di un oggetto gestito (in base a una tabella dei metodi valida) e l'oggetto che segue l'indirizzo dell'argomento.|  
|**MinidumpMode** [**0**] [**1**]|Impedisce l'esecuzione di comandi non sicuri quando si utilizza un minidump.<br /><br /> Passare **0** di disabilitare questa funzionalità o **1** per abilitare questa funzionalità. Per impostazione predefinita, il **MinidumpMode** è impostato su **0**.<br /><br /> I minidump creati con il **dump /m** comando o **dump** comando dati specifici di CLR sono limitati e consentono di eseguire correttamente solo un sottoinsieme di comandi SOS. È possibile che alcuni comandi abbiano esito negativo con errori imprevisti perché aree richieste di memoria non sono mappate o sono mappate solo parzialmente. Questa opzione impedisce l'esecuzione di comandi non sicuri sui minidump.|  
|**Name2ee** \<*nome modulo*> *nome del tipo o metodo*><br /><br /> -oppure-<br /><br /> **Name2EE** \<*module name*>**!** \< *nome del tipo o metodo*>|Visualizza le strutture `MethodTable` e `EEClass` per il tipo o il metodo specificato nel modulo specificato.<br /><br /> Il modulo specificato deve essere caricato nel processo.<br /><br /> Per ottenere il nome del tipo corretto, sfogliare il modulo utilizzando il [Ildasm.exe (Disassembler IL)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md). È inoltre possibile passare `*` come parametro del nome del modulo per eseguire la ricerca in tutti i moduli gestiti caricati. Il *nome modulo* parametro può essere anche il nome del debugger di un modulo, ad esempio `mscorlib` o `image00400000`.<br /><br /> Il comando supporta la sintassi del debugger Windows di `module` > `!` < `type`>. Il tipo deve essere completo.|  
|**ObjSize** [*indirizzo dell'oggetto*>] | [**-aggregate**] [**-stat**]|Visualizza la dimensione dell'oggetto specificato. Se non si specifica alcun parametro, il **ObjSize** comando Visualizza le dimensioni di tutti gli oggetti trovati nei thread gestiti, Visualizza tutti gli handle di garbage collector nel processo e somma la dimensione degli oggetti a cui puntata tali handle. Il **ObjSize** comando include la dimensione di tutti gli oggetti figlio oltre al padre.<br /><br /> Il **-aggregazione** opzione può essere utilizzata in combinazione con il **-stat** argomento per ottenere una visualizzazione dettagliata dei tipi che sono ancora una radice. Utilizzando **! dumpheap-stat** e **! objsize-aggregate - stat**, è possibile determinare quali oggetti senza più radice e diagnosticare vari problemi di memoria.|  
|**PrintException** [**-nidificata**] [**-righe**] [*indirizzo dell'oggetto eccezione*>]<br /><br /> -oppure-<br /><br /> **PE** [**-nidificata**] [*indirizzo dell'oggetto eccezione*>]|Visualizza e formatta i campi di qualsiasi oggetto derivato dal <xref:System.Exception> (classe) all'indirizzo specificato. Se non si specifica un indirizzo, il **PrintException** comando Visualizza l'ultima eccezione generata sul thread corrente.<br /><br /> Il **-nidificata** opzione Visualizza dettagli sugli oggetti eccezione annidati.<br /><br /> Il **-righe** opzione Visualizza le informazioni di origine, se disponibile.<br /><br /> È possibile utilizzare questo comando per formattare e visualizzare il campo `_stackTrace`, che è una matrice binaria.|  
|**ProcInfo** [**-env**] [**-time**] [**-mem**]|Visualizza le variabili di ambiente del processo, il tempo CPU del kernel e le statistiche di utilizzo della memoria.|  
|**RCWCleanupList** \<*RCWCleanupList indirizzo*>|Visualizza l'elenco di Runtime Callable Wrapper in corrispondenza dell'indirizzo specificato che sono in attesa di pulizia.|  
|**SaveModule** \<*indirizzo di Base*> *nome file*>|Scrive nel file specificato un'immagine caricata in memoria in corrispondenza dell'indirizzo specificato.|  
|**SOSFlush**|Scarica la cache SOS interna.|  
|**StopOnException** [**-derivato**] [**-creare** | **-rapida2**] *eccezione*> *numero pseudo-registrazione*>|Determina l'arresto del debugger solo quando viene generata l'eccezione specificata, consentendo la continuazione dell'esecuzione quando vengono generate altre eccezioni.<br /><br /> Il **-derivato** opzione intercetta l'eccezione specificata e tutte le eccezioni che deriva dall'eccezione specificata.|  
|**SyncBlk** [**-all** | *numero syncblk*>]|Visualizza la struttura `SyncBlock` specificata o tutte le strutture `SyncBlock`.  Se non si passano argomenti, il **SyncBlk** comando Visualizza il `SyncBlock` struttura corrisponde agli oggetti che appartengono a un thread.<br /><br /> Una struttura `SyncBlock` è un contenitore per informazioni aggiuntive che non deve essere creato per ogni oggetto. Può contenere dati di interoperabilità COM, codici hash e informazioni di blocco per operazioni thread-safe.|  
|**Pool di thread**|Visualizza informazioni sul pool di thread gestiti, tra cui il numero di richieste di lavoro nella coda, il numero di thread della porta di completamento e il numero di timer.|  
|**Token2EE** \<*nome modulo*> *token*>|Trasforma il token di metadati specificato del modulo specificato in una struttura `MethodTable` o `MethodDesc`.<br /><br /> È possibile passare `*` come parametro del nome del modulo per trovare il mapping del token in ogni modulo gestito caricato. È anche possibile passare il nome del debugger di un modulo, ad esempio `mscorlib` o `image00400000`.|  
|**Threads** [**-live**] [**-special**]|Visualizza tutti i thread gestiti del processo.<br /><br /> Il **thread** comando Visualizza il debugger ID abbreviato, l'ID di thread di common language runtime e l'ID del thread del sistema operativo.  Inoltre, il **thread** comando Visualizza una colonna Domain che indica il dominio applicazione in cui è in esecuzione un thread, una colonna APT che visualizza la modalità apartment COM e una colonna Exception che visualizza l'ultima eccezione generata nel thread.<br /><br /> Il **-live** opzione Visualizza thread associati a un thread attivo.<br /><br /> Il **-speciali** opzione consente di visualizzare tutti i thread speciali creati da CLR. I thread speciali sono inclusi thread di garbage collection (nell'operazione di garbage collection simultanee e server), thread di supporto del debugger, thread del finalizzatore <xref:System.AppDomain> unload e thread di timer del pool.|  
|**ThreadState ** *campo valore di stato***>**|Visualizza lo stato del thread. Il `value` parametro è il valore di `State` campo di **thread** output dei report.<br /><br /> Esempio:<br /><br /> `0:003> !Threads     ThreadCount:      2     UnstartedThread:  0     BackgroundThread: 1     PendingThread:    0     DeadThread:       0     Hosted Runtime:   no                                           PreEmptive   GC Alloc           Lock            ID OSID ThreadOBJ    State     GC       Context       Domain   Count APT Exception        0    1  250 0019b068      a020 Disabled 02349668:02349fe8 0015def0     0 MTA        2    2  944 001a6020      b220 Enabled  00000000:00000000 0015def0     0 MTA (Finalizer)     0:003> !ThreadState b220         Legal to Join         Background         CLR Owns         CoInitialized         In Multi Threaded Apartment`|  
|**TraverseHeap** [**- xml**] *filename*>|Scrive informazioni sull'heap nel file specificato, in un formato leggibile dal profiler CLR. Il **- xml** opzione il **TraverseHeap** per formattare il file come XML.<br /><br /> È possibile scaricare il Profiler CLR tramite il [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=67325).|  
|**U** [**-gcinfo**] [**-ehinfo**] [**-n**] *MethodDesc address*> | *Indirizzo di codice*>|Visualizza un disassembly annotato di un metodo gestito specificato da un puntatore alla struttura `MethodDesc` del metodo o da un indirizzo di codice all'interno del corpo del metodo. Il **U** comando Visualizza l'intero metodo dall'inizio alla fine, con annotazioni che convertono i token di metadati in nomi.<br /><br /> Il **- gcinfo** opzione il **U** comando per visualizzare il `GCInfo` struttura per il metodo.<br /><br /> Il **- ehinfo** opzione consente di visualizzare informazioni sull'eccezione per il metodo. È inoltre possibile ottenere queste informazioni con il **EHInfo** comando.<br /><br /> Il **- n** opzione Disabilita la visualizzazione di nomi di file di origine e i numeri di riga. Se nel debugger è specificata l'opzione SYMOPT_LOAD_LINES, vengono ricercati i simboli di ogni frame gestito e, in caso di esito positivo, vengono visualizzati il nome del file di origine e il numero di riga corrispondenti. È possibile specificare il **- n** possibile disabilitare questo comportamento.|  
|**VerifyHeap**|Cerca segni di danneggiamento nell'heap del Garbage Collector e visualizza gli eventuali errori trovati.<br /><br /> L'heap può danneggiarsi a causa di chiamate di pInvoke costruite in modo non corretto.|  
|**VerifyObj** \<*indirizzo dell'oggetto*>|Cerca segni di danneggiamento nell'oggetto passato come argomento.|  
|**VMMap**|Attraversa lo spazio degli indirizzi virtuali e visualizza il tipo di protezione applicato a ogni regione.|  
|**VMStat**|Fornisce una visualizzazione di riepilogo dello spazio degli indirizzi virtuali, ordinata in base a ogni tipo di protezione applicato alla memoria (free, reserved, committed, private, mapped, image). La colonna TOTAL visualizza il risultato della colonna AVERAGE moltiplicato per la colonna BLK COUNT.|  
  
## <a name="remarks"></a>Note  
 L'estensione del debugger SOS consente di visualizzare informazioni sul codice in esecuzione nell'ambiente Common Language Runtime. È ad esempio possibile utilizzarla per visualizzare informazioni sull'heap gestito, cercare eventuali danneggiamenti dell'heap, visualizzare i tipi di dati interni utilizzati dal runtime e visualizzare informazioni su tutto il codice gestito in esecuzione nel runtime.  
  
 Per utilizzare l'estensione del debugger SOS in Visual Studio, installare il [Windows Driver Kit (WDK)](http://msdn.microsoft.com/windows/hardware/hh852362). Per informazioni sull'ambiente di debug integrata in Visual Studio, vedere [debug ambienti](http://msdn.microsoft.com/library/windows/hardware/hh406268.aspx) nel Centro sviluppatori Windows.  
  
 È possibile utilizzare anche l'estensione del debugger SOS caricandola nel debugger WinDbg.exe, disponibile tramite il [sito Web WDK and Developer Tools](http://go.microsoft.com/fwlink/?LinkId=103787)e l'esecuzione di comandi all'interno di WinDbg.exe.  
  
 Per caricare l'estensione del debugger SOS nel debugger WinDbg.exe, eseguire il comando riportato sotto nello strumento:  
  
```  
.loadby sos clr  
```  
  
 In WinDbg.exe e Visual Studio viene utilizzata una versione di SOS.dll che corrisponde alla versione di Mscorwks.dll attualmente in uso. Nelle versioni 1.1 e 2.0 di .NET Framework SOS.dll è installato nella stessa directory di Mscorwks.dll. Per impostazione predefinita, è necessario utilizzare la versione di SOS.dll che corrisponde alla versione corrente di Mscorwks.dll.  
  
 Per utilizzare un file dump creato in un altro computer, assicurarsi che il file Mscorwks.dll fornito con l'installazione sia contenuto nel percorso dei simboli e caricare la versione corrispondente di SOS.dll.  
  
 Per caricare una versione specifica di SOS.dll, digitare il comando seguente nel debugger Windows:  
  
```  
.load <full path to sos.dll>  
```  
  
## <a name="examples"></a>Esempi  
 Il comando riportato di seguito visualizza il contenuto di una matrice in corrispondenza dell'indirizzo `00ad28d0`.  La visualizzazione parte dal secondo elemento e continua per cinque elementi.  
  
```  
!dumparray -start 2 -length 5 -detail 00ad28d0   
```  
  
 Il comando riportato di seguito visualizza il contenuto di un assembly in corrispondenza dell'indirizzo `1ca248`.  
  
```  
!dumpassembly 1ca248  
```  
  
 Il comando riportato di seguito visualizza informazioni sull'heap del Garbage Collector.  
  
```  
!dumpheap  
```  
  
 Il comando riportato di seguito scrive il contenuto del log di stress in memoria in un file (predefinito) denominato StressLog.tx nella directory corrente.  
  
```  
!DumpLog  
```  
  
 Il comando riportato di seguito visualizza la struttura `MethodDesc` in corrispondenza dell'indirizzo `902f40`.  
  
```  
!dumpmd 902f40  
```  
  
 Il comando riportato di seguito visualizza informazioni su un modulo in corrispondenza dell'indirizzo `1caa50`.  
  
```  
!dumpmodule 1caa50  
```  
  
 Il comando riportato di seguito visualizza informazioni su un oggetto in corrispondenza dell'indirizzo `a79d40`.  
  
```  
!DumpObj a79d40  
```  
  
 Il comando riportato di seguito visualizza i campi di una classe di valori in corrispondenza dell'indirizzo `00a79d9c` utilizzando la tabella dei metodi in corrispondenza dell'indirizzo `0090320c`.  
  
```  
!DumpVC 0090320c 00a79d9c  
```  
  
 Il comando riportato di seguito visualizza la memoria di processo utilizzata dal Garbage Collector.  
  
```  
!eeheap -gc  
```  
  
 Il comando riportato di seguito visualizza tutti gli oggetti per i quali è pianificata la finalizzazione.  
  
```  
!finalizequeue  
```  
  
 Il comando riportato di seguito determina il dominio applicazione di un oggetto in corrispondenza dell'indirizzo `00a79d98`.  
  
```  
!findappdomain 00a79d98  
```  
  
 Il comando riportato di seguito visualizza tutti gli handle del Garbage Collector nel processo corrente.  
  
```  
!gcinfo 5b68dbb8   
```  
  
 Il comando riportato di seguito visualizza le strutture `MethodTable` e `EEClass` per il metodo `Main` nella classe `MainClass` nel modulo `unittest.exe`.  
  
```  
!name2ee unittest.exe MainClass.Main  
```  
  
 Il comando riportato di seguito visualizza informazioni sul token di metadati in corrispondenza dell'indirizzo `02000003` nel modulo `unittest.exe`.  
  
```  
!token2ee unittest.exe 02000003  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti](../../../docs/framework/tools/index.md)   
 [Prompt dei comandi](../../../docs/framework/tools/developer-command-prompt-for-vs.md)