---
title: "Garbage Collection and Performance | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "garbage collection, troubleshooting"
  - "garbage collection, performance"
ms.assetid: c203467b-e95c-4ccf-b30b-953eb3463134
caps.latest.revision: 35
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 33
---
# Garbage Collection and Performance
Questo argomento descrive i problemi relativi a Garbage Collection e all'utilizzo della memoria.  Sono incluse informazioni per risolvere i problemi che riguardano l'heap gestito e che descrivono come ridurre al minimo l'effetto di Garbage Collection sulle applicazioni.  Per ogni problema sono disponibili collegamenti alle procedure che è possibile usare per approfondimenti aggiuntivi.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Strumenti di analisi delle prestazioni](#performance_analysis_tools)  
  
-   [Risoluzione dei problemi relativi alle prestazioni](#troubleshooting_performance_issues)  
  
-   [Linee guida per la risoluzione dei problemi](#troubleshooting_guidelines)  
  
-   [Procedure di controllo delle prestazioni](#performance_check_procedures)  
  
<a name="performance_analysis_tools"></a>   
## Strumenti di analisi delle prestazioni  
 Le sezioni seguenti descrivono gli strumenti disponibili per esaminare i problemi relativi a utilizzo della memoria e Garbage Collection.  Le [procedure](#performance_check_procedures) disponibili più avanti in questo argomento fanno riferimento a questi strumenti.  
  
<a name="perf_counters"></a>   
### Contatori delle prestazioni di memoria  
 È possibile usare i contatori delle prestazioni per raccogliere dati sulle prestazioni.  Per istruzioni, vedere [Profilatura runtime](../../../docs/framework/debug-trace-profile/runtime-profiling.md).  La categoria Memoria CLR .NET dei contatori delle prestazioni, descritta in [Contatori delle prestazioni in .NET Framework](../../../docs/framework/debug-trace-profile/performance-counters.md), fornisce informazioni su Garbage Collector.  
  
<a name="sos"></a>   
### Debug con SOS  
 È possibile usare il [debugger di Windows \(WinDbg\)](http://go.microsoft.com/fwlink/?LinkId=186482) per controllare gli oggetti nell'heap gestito.  
  
 Per installare WinDbg, installare gli strumenti di debug per Windows dal [sito Download di WDK e WinDbg](http://go.microsoft.com/fwlink/?LinkID=103787).  
  
<a name="etw"></a>   
### Eventi ETW di Garbage Collection  
 Event Tracing for Windows \(ETW\) è un sistema di traccia che integra il supporto per profilatura e debug offerto da .NET Framework.  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], gli [eventi ETW di Garbage Collection](../../../docs/framework/performance/garbage-collection-etw-events.md) acquisiscono informazioni utili per l'analisi dell'heap gestito da un punto di vista statistico.  Ad esempio, l'evento `GCStart_V1`, generato quando sta per verificarsi un'operazione di Garbage Collection, fornisce le informazioni seguenti:  
  
-   Generazione di oggetti raccolta.  
  
-   Che cosa ha attivato l'operazione di Garbage Collection.  
  
-   Tipo di Garbage Collection \(simultanea o non simultanea\).  
  
 La registrazione degli eventi ETW è efficiente e non maschera alcun problema di prestazioni associato a Garbage Collection.  Un processo può fornire i propri eventi insieme agli eventi ETW.  Una volta registrati, sia gli eventi dell'applicazione sia quelli di Garbage Collection possono essere correlati per determinare come e quando si verificano problemi relativi all'heap.  Ad esempio, un'applicazione server può fornire eventi all'inizio e alla fine di una richiesta client.  
  
<a name="profiling_api"></a>   
### API di profilatura  
 Le interfacce di profilatura Common Language Runtime \(CLR\) forniscono informazioni dettagliate sugli oggetti interessati durante l'operazione di Garbage Collection.  Un profiler può ricevere una notifica all'inizio o alla fine di un'operazione di Garbage Collection  e può fornire report sugli oggetti nell'heap gestito, inclusa un'identificazione degli oggetti in ogni generazione.  Per altre informazioni, vedere [Panoramica della profilatura](../../../ocs/framework/unmanaged-api/profiling/profiling-overview.md).  
  
 I profiler possono fornire informazioni complete.  Tuttavia, i profiler complessi possono potenzialmente modificare il comportamento di un'applicazione.  
  
### Monitoraggio delle risorse del dominio applicazione  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], il monitoraggio delle risorse del dominio applicazione permette agli host di monitorare l'utilizzo di CPU e memoria da parte del dominio applicazione.  Per altre informazioni, vedere [Application Domain Resource Monitoring](../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md).  
  
 [Torna all'inizio](#top)  
  
<a name="troubleshooting_performance_issues"></a>   
## Risoluzione dei problemi relativi alle prestazioni  
 Il primo passaggio consiste nel [determinare se il problema è in realtà causato dall'operazione di Garbage Collection](#IsGC).  In questo caso, selezionare una delle voci nell'elenco seguente per risolvere il problema.  
  
-   [Viene generata un'eccezione di memoria esaurita](#Issue_OOM)  
  
-   [Il processo usa una quantità eccessiva di memoria](#Issue_TooMuchMemory)  
  
-   [Garbage Collector non recupera gli oggetti in modo abbastanza veloce](#Issue_NotFastEnough)  
  
-   [L'heap gestito è troppo frammentato](#Issue_Fragmentation)  
  
-   [Le pause di Garbage Collection sono troppo prolungate](#Issue_LongPauses)  
  
-   [La generazione 0 ha dimensioni eccessive](#Issue_Gen0)  
  
-   [L'utilizzo della CPU durante un'operazione di Garbage Collection è eccessivo](#Issue_HighCPU)  
  
<a name="Issue_OOM"></a>   
### Problema: viene generata un'eccezione di memoria esaurita  
 Esistono due casi legittimi per la generazione di un'eccezione <xref:System.OutOfMemoryException> gestita:  
  
-   Esaurimento della memoria virtuale.  
  
     Garbage Collector alloca memoria dal sistema in segmenti di dimensioni predeterminate.  Se un'allocazione richiede un segmento aggiuntivo, ma non è più disponibile un blocco contiguo libero nello spazio di memoria virtuale del processo, l'allocazione per l'heap gestito non riesce.  
  
-   Mancanza di memoria fisica sufficiente da allocare.  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Determinare se l'eccezione di memoria esaurita è gestita.](#OOMIsManaged)<br /><br /> [Determinare la quantità di memoria virtuale che è possibile riservare.](#GetVM)<br /><br /> [Determinare se è disponibile memoria fisica sufficiente.](#Physical)|  
  
 Se si determina che l'eccezione non è legittima, contattare il Supporto tecnico Microsoft avendo a portata di mano le informazioni seguenti:  
  
-   Stack con l'eccezione di memoria esaurita gestita.  
  
-   Dump di memoria completo.  
  
-   Dati che dimostrano che non si tratta di un'eccezione di memoria esaurita legittima, inclusi quelli che indicano che la memoria fisica o virtuale non è la causa del problema.  
  
<a name="Issue_TooMuchMemory"></a>   
### Problema: il processo usa una quantità eccessiva di memoria  
 Un presupposto comune è che l'utilizzo della memoria visualizzato nella scheda **Prestazioni** di Gestione attività di Windows può indicare quando viene usata una quantità eccessiva di memoria.  Tuttavia, queste informazioni visualizzate riguardano il set di lavoro e non l'utilizzo della memoria virtuale.  
  
 Se si determina che il problema è causato dall'heap gestito, è necessario misurare l'heap gestito nel tempo per stabilire gli eventuali modelli.  
  
 Se si determina che il problema non è causato dall'heap gestito, è necessario usare il debug nativo.  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Determinare la quantità di memoria virtuale che è possibile riservare.](#GetVM)<br /><br /> [Determinare la quantità di memoria di cui l'heap gestito esegue il commit.](#ManagedHeapCommit)<br /><br /> [Determinare la quantità di memoria riservata dall'heap gestito.](#ManagedHeapReserve)<br /><br /> [Determinare gli oggetti di grandi dimensioni nella generazione 2.](#ExamineGen2)<br /><br /> [Determinare i riferimenti agli oggetti.](#ObjRef)|  
  
<a name="Issue_NotFastEnough"></a>   
### Problema: Garbage Collector non recupera gli oggetti in modo abbastanza veloce  
 Quando sembra che gli oggetti non vengano recuperati nel modo previsto per l'operazione di Garbage Collection, è necessario determinare se vi siano riferimenti sicuri a tali oggetti.  
  
 È possibile riscontrare questo problema anche se non è stata eseguita alcuna operazione di Garbage Collection per la generazione che contiene un oggetto inutilizzato, a indicare che il finalizzatore per tale oggetto inutilizzato non è stato eseguito.  Ad esempio, ciò è possibile quando si esegue un'applicazione apartment a thread singolo \(STA, Single\-Threaded Apartment\) e il thread che gestisce la coda del finalizzatore non può eseguire chiamate al suo interno.  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Controllare i riferimenti agli oggetti.](#ObjRef)<br /><br /> [Determinare se è stato eseguito un finalizzatore.](#Induce)<br /><br /> [Determinare se sono presenti oggetti in attesa di essere finalizzati.](#Finalize)|  
  
<a name="Issue_Fragmentation"></a>   
### Problema: l'heap gestito è troppo frammentato  
 Il livello di frammentazione viene calcolato come percentuale di spazio libero rispetto alla memoria totale allocata per la generazione.  Per la generazione 2, un livello accettabile di frammentazione non è maggiore del 20%.  Poiché la generazione 2 può assumere dimensioni molto grandi, il rapporto di frammentazione è più importante del valore assoluto.  
  
 La disponibilità di una quantità elevata di spazio libero nella generazione 0 non costituisce un problema, perché si tratta della generazione in cui vengono allocati nuovi oggetti.  
  
 La frammentazione si verifica sempre nell'heap oggetti grandi in quanto non viene compattato.  Gli oggetti liberi adiacenti vengono naturalmente compressi in un unico spazio per soddisfare le richieste di allocazione di oggetti grandi.  
  
 La frammentazione può diventare un problema nella generazione 1 e nella generazione 2.  Se in queste generazioni è disponibile una quantità elevata di spazio libero dopo un'operazione di Garbage Collection, potrebbe essere necessario modificare l'utilizzo degli oggetti di un'applicazione e provare a eseguire una nuova valutazione della durata degli oggetti a lungo termine.  
  
 Il blocco eccessivo di oggetti può aumentare la frammentazione.  Se la frammentazione è elevata, potrebbe essere bloccato un numero eccessivo di oggetti.  
  
 Se la frammentazione della memoria virtuale impedisce a Garbage Collector di aggiungere segmenti, la causa può essere una delle seguenti:  
  
-   Caricamento e scaricamento frequenti di molti assembly di piccole dimensioni.  
  
-   Presenza di troppi riferimenti a oggetti COM durante l'interoperabilità con codice non gestito.  
  
-   Creazione di oggetti temporanei di grandi dimensioni, che fa sì che l'heap grandi oggetti allochi e liberi frequentemente segmenti di heap.  
  
     Quando si ospita CLR, un'applicazione può richiedere che Garbage Collector ne mantenga i segmenti.  In questo modo, viene ridotta la frequenza delle allocazioni di segmenti.  A questo scopo, viene usato il flag STARTUP\_HOARD\_GC\_VM nell'[Enumerazione STARTUP\_FLAGS](../../../ocs/framework/unmanaged-api/hosting/startup-flags-enumeration.md).  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Determinare la quantità di spazio libero nell'heap gestito.](#Fragmented)<br /><br /> [Determinare il numero di oggetti bloccati.](#Pinned)|  
  
 Se si ritiene che non sussista una causa legittima per la frammentazione, contattare il Supporto tecnico Microsoft.  
  
<a name="Issue_LongPauses"></a>   
### Problema: le pause di Garbage Collection sono troppo prolungate  
 Poiché le operazioni di Garbage Collection avvengono in tempo reale "soft", un'applicazione deve essere in grado di tollerare alcune pause.  Un criterio che determina l'esecuzione in tempo reale "soft" è che il 95% delle operazioni deve terminare in tempo.  
  
 Nelle operazioni di Garbage Collection simultanee, i thread gestiti possono essere eseguiti durante una raccolta, che significa che le pause sono minime.  
  
 Poiché le operazioni di Garbage Collection effimere \(generazioni 0 e 1\) durano solo pochi millisecondi, la riduzione delle pause non è in genere possibile.  Tuttavia, è possibile ridurre le pause nelle raccolte di generazione 2 modificando il modello delle richieste di allocazione da parte di un'applicazione.  
  
 Un altro metodo, più accurato, consiste nell'usare [eventi ETW di Garbage Collection](../../../docs/framework/performance/garbage-collection-etw-events.md).  È possibile individuare gli intervalli di tempo per le raccolte aggiungendo le differenze dei timestamp per una sequenza di eventi.  L'intera sequenza di raccolta include la sospensione del motore di esecuzione, l'operazione di Garbage Collection stessa e la ripresa del motore di esecuzione.  
  
 È possibile usare [Garbage Collection Notifications](../../../docs/standard/garbage-collection/notifications.md) per determinare se in un server sta per essere eseguita una raccolta di generazione 2 e se le richieste di reindirizzamento a un altro server potrebbero risolvere eventuali problemi relativi alle pause.  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Determinare il periodo di tempo in un'operazione di Garbage Collection.](#TimeInGC)<br /><br /> [Determinare la causa di un'operazione di Garbage Collection.](#Triggered)|  
  
<a name="Issue_Gen0"></a>   
### Problema: la generazione 0 ha dimensioni eccessive  
 È probabile che la generazione 0 abbia un numero maggiore di oggetti in un sistema a 64 bit, in particolare se si usa un'operazione di Garbage Collection per server invece che per workstation.  Ciò è dovuto al fatto che la soglia per attivare un'operazione di Garbage Collection di generazione 0 è maggiore in questi ambienti e le raccolte di generazione 0 possono essere molto più grandi.  Le prestazioni sono migliori quando un'applicazione alloca molta memoria prima dell'attivazione di un'operazione di Garbage Collection.  
  
<a name="Issue_HighCPU"></a>   
### Problema: l'utilizzo della CPU durante un'operazione di Garbage Collection è eccessivo  
 L'utilizzo della CPU durante un'operazione di Garbage Collection è elevato.  Se il periodo di tempo del processo è significativo in un'operazione di Garbage Collection, il numero di raccolte è troppo frequente oppure la raccolta dura troppo a lungo.  Una frequenza di allocazione di oggetti maggiore nell'heap gestito fa sì che le operazioni di Garbage Collection avvengano più spesso.  La riduzione della frequenza di allocazione riduce anche la frequenza delle operazioni di Garbage Collection.  
  
 È possibile monitorare le frequenze di allocazione usando il contatore delle prestazioni `Allocated Bytes/second`.  Per altre informazioni, vedere [Contatori delle prestazioni in .NET Framework](../../../docs/framework/debug-trace-profile/performance-counters.md).  
  
 La durata di una raccolta è principalmente un fattore del numero di oggetti rimanenti in seguito all'allocazione.  Garbage Collector deve usare una quantità elevata di memoria se restano molti oggetti da raccogliere.  L'attività di compattazione degli oggetti rimanenti richiede molto tempo.  Per determinare quanti oggetti sono stati gestiti durante una raccolta, impostare un punto di interruzione nel debugger alla fine di un'operazione di Garbage Collection per una generazione specificata.  
  
|Controlli delle prestazioni|  
|---------------------------------|  
|[Determinare se l'utilizzo elevato della CPU è causato dall'operazione di Garbage Collection.](#HighCPU)<br /><br /> [Impostare un punto di interruzione alla fine dell'operazione di Garbage Collection.](#GenBreak)|  
  
 [Torna all'inizio](#top)  
  
<a name="troubleshooting_guidelines"></a>   
## Linee guida per la risoluzione dei problemi  
 Questa sezione contiene linee guida da tenere presenti quando si inizia a esaminare i problemi.  
  
### Garbage Collection per workstation o per server  
 Determinare se il tipo di Garbage Collection usato è quello corretto.  Se l'applicazione usa più thread e istanze di oggetto, usare Garbage Collection per server anziché per workstation.  Un'operazione di Garbage Collection per server viene eseguita su più thread, mentre una per workstation richiede l'esecuzione di più istanze di un'applicazione nei rispettivi thread di Garbage Collection e che queste competano per il tempo di CPU.  
  
 Un'applicazione associata a un carico ridotto e che esegue raramente attività in background, ad esempio un servizio, può usare un'operazione di Garbage Collection per workstation con le operazioni di Garbage Collection simultanee disattivate.  
  
### Quando misurare le dimensioni dell'heap gestito  
 Se non si usa un profiler, è necessario definire un modello di misurazione coerente per diagnosticare con efficacia i problemi di prestazioni.  Per definire una pianificazione, considerare i punti seguenti:  
  
-   Se si esegue una misurazione dopo un'operazione di Garbage Collection di generazione 2, l'intero heap gestito sarò libero da oggetti inutilizzati.  
  
-   Se si esegue una misurazione immediatamente dopo un'operazione di Garbage Collection di generazione 0, gli oggetti nelle generazioni 1 e 2 non verranno ancora raccolti.  
  
-   Se si esegue una misurazione immediatamente prima di un'operazione di Garbage Collection, è necessario misurare tutta l'allocazione possibile prima dell'avvio dell'operazione di Garbage Collection.  
  
-   La misurazione durante un'operazione di Garbage Collection è problematica, perché le strutture di dati di Garbage Collector non sono in uno stato valido per l'attraversamento e potrebbero non essere in grado di fornire i risultati completi.  Si tratta di un comportamento correlato alla progettazione.  
  
-   Quando si usa un'operazione di Garbage Collection per workstation con un'operazione di Garbage Collection simultanea, gli oggetti recuperati non vengono compattati e di conseguenza le dimensioni dell'heap possono essere uguali o maggiori \(la frammentazione può farle apparire maggiori\).  
  
-   Un'operazione di Garbage Collection simultanea nella generazione 2 viene ritardata quando il carico di memoria fisica è troppo elevato.  
  
 La procedura seguente descrive come impostare un punto di interruzione per misurare l'heap gestito.  
  
<a name="GenBreak"></a>   
##### Per impostare un punto di interruzione alla fine dell'operazione di Garbage Collection  
  
-   In WinDbg con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **bp mscorwks\!WKS::GCHeap::RestartEE "j \(dwo\(mscorwks\!WKS::GCHeap::GcCondemnedGeneration\)\=\=2\) 'kb';'g'"**  
  
     dove **GcCondemnedGeneration** è impostato sulla generazione desiderata.  Questo comando richiede simboli privati.  
  
     Il comando forza un'interruzione se **RestartEE** viene eseguito dopo il recupero di oggetti di generazione 2 per l'operazione di Garbage Collection.  
  
     In un'operazione di Garbage Collection per server, solo un thread chiama **RestartEE**, in modo che il punto di interruzione si verifica solo una volta durante un'operazione di Garbage Collection di generazione 2.  
  
 [Torna all'inizio](#top)  
  
<a name="performance_check_procedures"></a>   
## Procedure di controllo delle prestazioni  
 Questa sezione descrive le procedure per isolare la causa del problema di prestazioni:  
  
-   [Determinare se il problema è causato da Garbage Collection.](#IsGC)  
  
-   [Determinare se l'eccezione di memoria esaurita è gestita.](#OOMIsManaged)  
  
-   [Determinare la quantità di memoria virtuale che è possibile riservare.](#GetVM)  
  
-   [Determinare se è disponibile memoria fisica sufficiente.](#Physical)  
  
-   [Determinare la quantità di memoria di cui l'heap gestito esegue il commit.](#ManagedHeapCommit)  
  
-   [Determinare la quantità di memoria riservata dall'heap gestito.](#ManagedHeapReserve)  
  
-   [Determinare gli oggetti di grandi dimensioni nella generazione 2.](#ExamineGen2)  
  
-   [Determinare i riferimenti agli oggetti.](#ObjRef)  
  
-   [Determinare se è stato eseguito un finalizzatore.](#Induce)  
  
-   [Determinare se sono presenti oggetti in attesa di essere finalizzati.](#Finalize)  
  
-   [Determinare la quantità di spazio libero nell'heap gestito.](#Fragmented)  
  
-   [Determinare il numero di oggetti bloccati.](#Pinned)  
  
-   [Determinare il periodo di tempo in un'operazione di Garbage Collection.](#TimeInGC)  
  
-   [Determinare che cosa ha attivato un'operazione di Garbage Collection.](#Triggered)  
  
-   [Determinare se l'utilizzo elevato della CPU è causato da Garbage Collection.](#HighCPU)  
  
<a name="IsGC"></a>   
##### Per determinare se il problema è causato da Garbage Collection  
  
-   Esaminare i due contatori delle prestazioni della memoria seguenti:  
  
    -   **Percentuale tempo in GC**.  Visualizza la percentuale di tempo trascorso, impiegato per l'esecuzione di un'operazione di Garbage Collection dopo l'ultimo ciclo di Garbage Collection.  Usare questo contatore per determinare se Garbage Collector sta impiegando troppo tempo per rendere disponibile lo spazio dell'heap gestito.  Se il tempo impiegato nell'operazione di Garbage Collection è relativamente ridotto, ciò può indicare un problema di risorse all'esterno dell'heap gestito.  Questo contatore potrebbe non essere accurato se sono interessate operazioni di Garbage Collection simultanee o in background.  
  
    -   **Totale byte di cui è stato eseguito il commit**.  Visualizza la quantità di memoria virtuale di cui Garbage Collector ha attualmente eseguito il commit.  Usare questo contatore per determinare se la memoria usata da Garbage Collector è una parte eccessiva della memoria usata dall'applicazione.  
  
     La maggior parte dei contatori delle prestazioni della memoria viene aggiornata alla fine di ogni operazione di Garbage Collection.  Di conseguenza, i contatori potrebbero non riflettere le attuali condizioni su cui si vuole ottenere informazioni.  
  
<a name="OOMIsManaged"></a>   
##### Per determinare se l'eccezione di memoria esaurita è gestita  
  
1.  Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando di stampa dell'eccezione \(**pe**\):  
  
     **\!pe**  
  
     Se l'eccezione è gestita, <xref:System.OutOfMemoryException> viene visualizzato come tipo di eccezione, come mostrato nell'esempio seguente.  
  
    ```  
    Exception object: 39594518  
    Exception type: System.OutOfMemoryException  
    Message: <none>  
    InnerException: <none>  
    StackTrace (generated):  
    ```  
  
2.  Se l'output non specifica un'eccezione, è necessario determinare il thread da cui proviene l'eccezione di memoria esaurita.  Digitare il comando seguente nel debugger per mostrare tutti i thread con i rispettivi stack di chiamate:  
  
     **~\*kb**  
  
     Il thread con lo stack che include le chiamate dell'eccezione è indicato dall'argomento `RaiseTheException`.  Si tratta dell'oggetto eccezione gestita.  
  
    ```  
    28adfb44 7923918f 5b61f2b4 00000000 5b61f2b4 mscorwks!RaiseTheException+0xa0   
    ```  
  
3.  È possibile usare il comando seguente per eseguire il dump delle eccezioni annidate:  
  
     **\!pe \-nested**  
  
     Se non si trova alcuna eccezione, l'eccezione di memoria esaurita proviene da codice non gestito.  
  
<a name="GetVM"></a>   
##### Per determinare la quantità di memoria virtuale che è possibile riservare  
  
-   In WinDbg con l'estensione del debugger SOS caricata, digitare il comando seguente per ottenere l'area libera più grande:  
  
     **\!address \-summary**  
  
     L'area libera più grande viene visualizzata come indicato nell'output seguente.  
  
    ```  
    Largest free region: Base 54000000 - Size 0003A980  
    ```  
  
     In questo esempio la dimensione dell'area libera più grande è circa 24000 KB \(3A980 in formato esadecimale\).  Questa area è molto minore rispetto alle dimensioni richieste da Garbage Collector per un segmento.  
  
     \-oppure\-  
  
-   Usare il comando **vmstat**:  
  
     **\!vmstat**  
  
     L'area libera più grande corrisponde al valore maggiore nella colonna MAXIMUM, come indicato nell'output seguente.  
  
    ```  
    TYPE        MINIMUM   MAXIMUM     AVERAGE   BLK COUNT   TOTAL  
    ~~~~        ~~~~~~~   ~~~~~~~     ~~~~~~~   ~~~~~~~~~~  ~~~~  
    Free:  
    Small       8K        64K         46K       36          1,671K  
    Medium      80K       864K        349K      3           1,047K  
    Large       1,384K    1,278,848K  151,834K  12          1,822,015K  
    Summary     8K        1,278,848K  35,779K   51          1,824,735K  
    ```  
  
<a name="Physical"></a>   
##### Per determinare se è disponibile memoria fisica sufficiente  
  
1.  Avviare Gestione risorse di Windows.  
  
2.  Nella scheda **Prestazioni** osservare il valore di cui è stato eseguito il commit.  In Windows 7 osservare il valore di **Commit \(KB\)** nel **gruppo di sistema**.  
  
     Se il valore specificato in **Totale** si avvicina al valore di **Limite**, la memoria fisica è insufficiente.  
  
<a name="ManagedHeapCommit"></a>   
##### Per determinare la quantità di memoria di cui l'heap gestito esegue il commit  
  
-   Usare il contatore delle prestazioni della memoria `# Total committed bytes` per ottenere il numero di byte di cui l'heap gestito sta eseguendo il commit.  Garbage Collector esegue il commit dei blocchi in un segmento nel modo necessario e non di tutti allo stesso tempo.  
  
    > [!NOTE]
    >  Non usare il contatore delle prestazioni `# Bytes in all Heaps`, perché non rappresenta l'effettivo utilizzo della memoria da parte dell'heap gestito.  La dimensione di una generazione è inclusa in questo valore e corrisponde i n realtà alla dimensione della soglia, ovvero la dimensione che provoca un'operazione di Garbage Collection se la generazione include molti oggetti.  Di conseguenza, questo valore è in genere uguale a zero.  
  
<a name="ManagedHeapReserve"></a>   
##### Per determinare la quantità di memoria riservata dall'heap gestito  
  
-   Usare il contatore delle prestazioni della memoria `# Total reserved bytes`.  
  
     Garbage Collector riserva memoria in segmenti ed è possibile determinare il punto di inizio di un segmento usando il comando **eeheap**.  
  
    > [!IMPORTANT]
    >  Benché sia possibile determinare la quantità di memoria allocata da Garbage Collector per ogni segmento, le dimensioni dei segmenti sono specifiche dell'implementazione e soggette a modifiche, tra cui aggiornamenti periodici, in qualsiasi momento.  L'applicazione non deve dare per scontata o dipendere da una particolare dimensione del segmento, né provare a configurare la quantità di memoria disponibile per le allocazioni di segmenti.  
  
-   Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **\!eeheap \-gc**  
  
     Il risultato è il seguente.  
  
    ```  
    Number of GC Heaps: 2  
    ------------------------------  
    Heap 0 (002db550)  
    generation 0 starts at 0x02abe29c  
    generation 1 starts at 0x02abdd08  
    generation 2 starts at 0x02ab0038  
    ephemeral segment allocation context: none  
     segment    begin allocated     size  
    02ab0000 02ab0038  02aceff4 0x0001efbc(126908)  
    Large object heap starts at 0x0aab0038  
     segment    begin allocated     size  
    0aab0000 0aab0038  0aab2278 0x00002240(8768)  
    Heap Size   0x211fc(135676)  
    ------------------------------  
    Heap 1 (002dc958)  
    generation 0 starts at 0x06ab1bd8  
    generation 1 starts at 0x06ab1bcc  
    generation 2 starts at 0x06ab0038  
    ephemeral segment allocation context: none  
     segment    begin allocated     size  
    06ab0000 06ab0038  06ab3be4 0x00003bac(15276)  
    Large object heap starts at 0x0cab0038  
     segment    begin allocated     size  
    0cab0000 0cab0038  0cab0048 0x00000010(16)  
    Heap Size    0x3bbc(15292)  
    ------------------------------  
    GC Heap Size   0x24db8(150968)  
    ```  
  
     Gli indirizzi indicati da "segment" sono gli indirizzi iniziali dei segmenti.  
  
<a name="ExamineGen2"></a>   
##### Per determinare gli oggetti di grandi dimensioni nella generazione 2  
  
-   Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **\!dumpheap –stat**  
  
     Se l'heap gestito è di grandi dimensioni, il completamento di **dumpheap** può richiedere alcuni minuti.  
  
     È possibile iniziare l'analisi dalle ultime righe dell'output, perché elencano gli oggetti che usano la maggior parte dello spazio.  Ad esempio:  
  
    ```  
    2c6108d4   173712     14591808 DevExpress.XtraGrid.Views.Grid.ViewInfo.GridCellInfo  
    00155f80      533     15216804      Free  
    7a747c78   791070     15821400 System.Collections.Specialized.ListDictionary+DictionaryNode  
    7a747bac   700930     19626040 System.Collections.Specialized.ListDictionary  
    2c64e36c    78644     20762016 DevExpress.XtraEditors.ViewInfo.TextEditViewInfo  
    79124228   121143     29064120 System.Object[]  
    035f0ee4    81626     35588936 Toolkit.TlkOrder  
    00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]  
    791242ec    40182     90664128 System.Collections.Hashtable+bucket[]  
    790fa3e0  3154024    137881448 System.String  
    Total 8454945 objects  
    ```  
  
     L'ultimo oggetto elencato è una stringa e occupa la maggior parte dello spazio.  È possibile esaminare l'applicazione per determinare come ottimizzare gli oggetti stringa.  Per visualizzare le stringhe comprese tra 150 e 200 byte, digitare:  
  
     **\!dumpheap \-type System.String \-min 150 \-max 200**  
  
     Di seguito viene riportato un esempio dei risultati.  
  
    ```  
    Address  MT           Size  Gen  
    1875d2c0 790fa3e0      152    2 System.String HighlightNullStyle_Blotter_PendingOrder-11_Blotter_PendingOrder-11  
    …  
    ```  
  
     L'uso di un numero intero invece di una stringa per un ID può rivelarsi più efficiente.  Se la stessa stringa è ripetuta migliaia di volte, provare ad applicare l'inserimento di stringhe.  Per altre informazioni sull'inserimento di stringhe, vedere l'argomento di riferimento per il metodo <xref:System.String.Intern%2A?displayProperty=fullName>.  
  
<a name="ObjRef"></a>   
##### Per determinare i riferimenti agli oggetti  
  
-   In WinDbg con l'estensione del debugger SOS caricata, digitare il comando seguente per elencare i riferimenti agli oggetti:  
  
     **\!gcroot**  
  
     `-or-`  
  
-   Per determinare i riferimenti per un oggetto specifico, includere l'indirizzo:  
  
     **\!gcroot 1c37b2ac**  
  
     Le radici trovate negli stack possono essere falsi positivi.  Per altre informazioni, usare il comando `!help gcroot`.  
  
    ```  
    ebx:Root:19011c5c(System.Windows.Forms.Application+ThreadContext)->  
    19010b78(DemoApp.FormDemoApp)->  
    19011158(System.Windows.Forms.PropertyStore)->  
    … [omitted]  
    1c3745ec(System.Data.DataTable)->  
    1c3747a8(System.Data.DataColumnCollection)->  
    1c3747f8(System.Collections.Hashtable)->  
    1c376590(System.Collections.Hashtable+bucket[])->  
    1c376c98(System.Data.DataColumn)->  
    1c37b270(System.Data.Common.DoubleStorage)->  
    1c37b2ac(System.Double[])  
    Scan Thread 0 OSTHread 99c  
    Scan Thread 6 OSTHread 484  
    ```  
  
     Il completamento del comando **gcroot** può richiedere molto tempo.  Qualsiasi oggetto non recuperato dall'operazione di Garbage Collection è un oggetto attivo.  Questo significa che una radice mantiene direttamente o indirettamente l'oggetto, motivo per cui **gcroot** deve restituire le informazioni sul percorso dell'oggetto.  È consigliabile esaminare i grafici restituiti e determinare perché viene ancora fatto riferimento a questi oggetti.  
  
<a name="Induce"></a>   
##### Per determinare se è stato eseguito un finalizzatore  
  
-   Eseguire un programma di test contenente il codice seguente:  
  
    ```  
    GC.Collect();  
    GC.WaitForPendingFinalizers();  
    GC.Collect();  
    ```  
  
     Se il test risolve il problema, significa che Garbage Collector non ha recuperato gli oggetti perché il finalizzatore per tali oggetti è stato sospeso.  Il metodo <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=fullName> permette ai finalizzatori di completare le rispettive attività e corregge il problema.  
  
<a name="Finalize"></a>   
##### Per determinare se sono presenti oggetti in attesa di essere finalizzati  
  
1.  Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **\!finalizequeue**  
  
     Osservare il numero di oggetti pronti per la finalizzazione.  Se il numero è elevato, è necessario esaminare il motivo per cui i finalizzatori non possono continuare del tutto o in modo abbastanza veloce.  
  
2.  Per ottenere un output dei thread, digitare il comando seguente:  
  
     **threads \-special**  
  
     Questo comando genera un output simile al seguente.  
  
    ```  
       OSID     Special thread type  
    2    cd0    DbgHelper   
    3    c18    Finalizer   
    4    df0    GC SuspendEE   
    ```  
  
     Il thread del finalizzatore indica quale finalizzatore, se presente, è attualmente in esecuzione.  Quando un thread del finalizzatore non esegue alcun finalizzatore, è in attesa di un evento che indichi di eseguire il lavoro.  Nella maggior parte dei casi il thread del finalizzatore verrà visualizzato in questo stato, perché viene eseguito in THREAD\_HIGHEST\_PRIORITY e si suppone che completi l'esecuzione dei finalizzatori, se presenti, molto rapidamente.  
  
<a name="Fragmented"></a>   
##### Per determinare la quantità di spazio libero nell'heap gestito  
  
-   Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **\!dumpheap \-type Free \-stat**  
  
     Questo comando visualizza le dimensioni totali di tutti gli oggetti liberi nell'heap gestito, come mostrato nell'esempio seguente.  
  
    ```  
    total 230 objects  
    Statistics:  
          MT    Count    TotalSize Class Name  
    00152b18      230     40958584      Free  
    Total 230 objects  
    ```  
  
-   Per determinare lo spazio libero nella generazione 0, digitare il comando seguente per informazioni sull'utilizzo della memoria da parte della generazione:  
  
     **\!eeheap \-gc**  
  
     Questo comando genera un output simile al seguente.  L'ultima riga mostra il segmento effimero.  
  
    ```  
    Heap 0 (0015ad08)  
    generation 0 starts at 0x49521f8c  
    generation 1 starts at 0x494d7f64  
    generation 2 starts at 0x007f0038  
    ephemeral segment allocation context: none  
    segment  begin     allocated  size  
    00178250 7a80d84c  7a82f1cc   0x00021980(137600)  
    00161918 78c50e40  78c7056c   0x0001f72c(128812)  
    007f0000 007f0038  047eed28   0x03ffecf0(67103984)  
    3a120000 3a120038  3a3e84f8   0x002c84c0(2917568)  
    46120000 46120038  49e05d04   0x03ce5ccc(63855820)  
    ```  
  
-   Calcolare lo spazio usato dalla generazione 0:  
  
     **?  49e05d04\-0x49521f8c**  
  
     Il risultato è il seguente.  La generazione 0 è di circa 9 MB.  
  
    ```  
    Evaluate expression: 9321848 = 008e3d78  
    ```  
  
-   Il comando seguente esegue il dump dello spazio libero all'interno dell'intervallo della generazione 0:  
  
     **\!dumpheap \-type Free \-stat 0x49521f8c 49e05d04**  
  
     Il risultato è il seguente.  
  
    ```  
    ------------------------------  
    Heap 0  
    total 409 objects  
    ------------------------------  
    Heap 1  
    total 0 objects  
    ------------------------------  
    Heap 2  
    total 0 objects  
    ------------------------------  
    Heap 3  
    total 0 objects  
    ------------------------------  
    total 409 objects  
    Statistics:  
          MT    Count TotalSize Class Name  
    0015a498      409   7296540      Free  
    Total 409 objects  
    ```  
  
     Questo output mostra che la parte di generazione 0 dell'heap usa 9 MB di spazio per gli oggetti e ha 7 MB di spazio libero.  Questa analisi mostra in quale misura la generazione 0 contribuisce alla frammentazione.  Questa quantità di utilizzo dell'heap deve essere sottratta dalla quantità locale come causa di frammentazione da parte di oggetti a lungo termine.  
  
<a name="Pinned"></a>   
##### Per determinare il numero di oggetti bloccati  
  
-   Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente:  
  
     **\!gchandles**  
  
     Le statistiche visualizzate includono il numero di handle bloccati, come indicato nell'esempio seguente.  
  
    ```  
    GC Handle Statistics:  
    Strong Handles:      29  
    Pinned Handles:      10  
    ```  
  
<a name="TimeInGC"></a>   
##### Per determinare il periodo di tempo in un'operazione di Garbage Collection  
  
-   Esaminare il contatore delle prestazioni della memoria `% Time in GC`.  
  
     Il valore viene calcolato usando un intervallo di tempo di esempio.  Poiché i contatori vengono aggiornati alla fine di ogni operazione di Garbage Collection, l'esempio corrente avrà lo stesso valore di quello precedente se durante l'intervallo non è stata eseguita alcuna raccolta.  
  
     La durata della raccolta viene ottenuta moltiplicando l'intervallo di esempio per il valore percentuale.  
  
     I dati seguenti mostrano quattro intervalli di campionamento di due secondi, per uno studio di otto secondi.  Le colonne `Gen0`, `Gen1` e `Gen2` mostrano il numero di operazioni di Garbage Collection eseguite durante l'intervallo per la generazione.  
  
    ```  
    Interval    Gen0    Gen1    Gen2    % Time in GC  
           1       9       3       1              10  
           2      10       3       1               1  
           3      11       3       1               3  
           4      11       3       1               3  
    ```  
  
     Queste informazioni non indicano quando è avvenuta l'operazione di Garbage Collection, ma è possibile determinare il numero di operazioni di Garbage Collection eseguite in un intervallo di tempo specifico.  Presupponendo il caso peggiore, la decima operazione di Garbage Collection di generazione 0 è terminata all'inizio del secondo intervallo, mentre l'undicesima è terminata alla fine del quinto intervallo.  Poiché l'intervallo di tempo tra la fine della decima e la fine dell'undicesima operazione di Garbage Collection è circa 2 secondi e il contatore delle prestazioni indica 3%, la durata dell'undicesima operazione di Garbage Collection di generazione 0 è pari a \(2 secondi \* 3% \= 60 ms\).  
  
     Questo esempio include cinque periodi.  
  
    ```  
    Interval    Gen0    Gen1    Gen2     % Time in GC  
           1       9       3       1                3  
           2      10       3       1                1  
           3      11       4       2                1  
           4      11       4       2                1  
           5      11       4       2               20  
    ```  
  
     La seconda operazione di Garbage Collection di generazione 2 è iniziata durante il terzo intervallo ed è terminata durante il quinto intervallo.  Presupponendo il caso peggiore, l'ultima operazione di Garbage Collection è avvenuta per una raccolta di generazione 0 terminata all'inizio del secondo intervallo, mentre l'operazione di Garbage Collection di generazione 2 è terminata alla fine del quinto intervallo.  Di conseguenza, l'intervallo di tempo tra la fine dell'operazione di Garbage Collection di generazione 0 e la fine dell'operazione di Garbage Collection di generazione 2 è 4 secondi.  Poiché il contatore `% Time in GC` indica 20%, la quantità massima di tempo che l'operazione di Garbage Collection di generazione 2 avrebbe potuto impiegare è \(4 secondi \* 20% \= 800 ms\).  
  
-   In alternativa, è possibile determinare la lunghezza di un'operazione di Garbage Collection usando [eventi ETW di Garbage Collection](../../../docs/framework/performance/garbage-collection-etw-events.md) e analizzare le informazioni per stabilire la durata dell'operazione di Garbage Collection.  
  
     Ad esempio, i dati seguenti mostrano una sequenza di eventi verificatasi durante un'operazione di Garbage Collection non simultanea.  
  
    ```  
    Timestamp    Event name  
    513052        GCSuspendEEBegin_V1  
    513078        GCSuspendEEEnd  
    513090        GCStart_V1  
    517890        GCEnd_V1  
    517894        GCHeapStats  
    517897        GCRestartEEBegin  
    517918        GCRestartEEEnd  
    ```  
  
     La sospensione del thread gestito ha richiesto 26 us \(`GCSuspendEEEnd` \- `GCSuspendEEBegin_V1`\).  
  
     L'effettiva operazione di Garbage Collection ha richiesto 4,8 ms \(`GCEnd_V1` \- `GCStart_V1`\).  
  
     La ripresa dei thread gestiti ha richiesto 21 us \(`GCRestartEEEnd` \- `GCRestartEEBegin`\).  
  
     L'output seguente offre un esempio di un'operazione di Garbage Collection in background e include il processo, il thread e i campi evento.  Non tutti i dati vengono visualizzati.  
  
    ```  
    timestamp(us)    event name            process    thread    event field  
    42504385        GCSuspendEEBegin_V1    Test.exe    4372             1  
    42504648        GCSuspendEEEnd         Test.exe    4372          
    42504816        GCStart_V1             Test.exe    4372        102019  
    42504907        GCStart_V1             Test.exe    4372        102020  
    42514170        GCEnd_V1               Test.exe    4372          
    42514204        GCHeapStats            Test.exe    4372        102020  
    42832052        GCRestartEEBegin       Test.exe    4372          
    42832136        GCRestartEEEnd         Test.exe    4372          
    63685394        GCSuspendEEBegin_V1    Test.exe    4744             6  
    63686347        GCSuspendEEEnd         Test.exe    4744          
    63784294        GCRestartEEBegin       Test.exe    4744          
    63784407        GCRestartEEEnd         Test.exe    4744          
    89931423        GCEnd_V1               Test.exe    4372        102019  
    89931464        GCHeapStats            Test.exe    4372          
    ```  
  
     L'evento `GCStart_V1` in corrispondenza di 42504816 indica che si tratta di un'operazione di Garbage Collection in background, perché l'ultimo campo è `1`.  Questa diventa l'operazione di Garbage Collection n.  102019.  
  
     L'evento `GCStart` si verifica perché è necessaria un'operazione di Garbage Collection effimera prima di avviare un'operazione di Garbage Collection in background.  Questa diventa l'operazione di Garbage Collection n.  102020.  
  
     In corrispondenza di 42514170, l'operazione di Garbage Collection n.  102020 viene completata.  I thread gestiti vengono riavviati a questo punto.  Questa operazione viene completata nel thread 4372, che ha attivato l'operazione di Garbage Collection in background.  
  
     Nel thread 4744 si verifica una sospensione.  Si tratta dell'unica volta in cui l'operazione di Garbage Collection in background deve sospendere i thread gestiti.  Questa durata è di circa 99 ms \(\(63784407\-63685394\)\/1000\).  
  
     L'evento `GCEnd` per l'attività di Garbage Collection in background si trova in corrispondenza di 89931423.  Di conseguenza, l'operazione di Garbage Collection è durata circa 47 secondi \(\(89931423\-42504816\)\/1000\).  
  
     Durante l'esecuzione dei thread gestiti, è possibile visualizzare un numero qualsiasi di operazioni di Garbage Collection effimere in esecuzione.  
  
<a name="Triggered"></a>   
##### Per determinare che cosa ha attivato un'operazione di Garbage Collection  
  
-   Nel debugger WinDbg o di Visual Studio con l'estensione del debugger SOS caricata, digitare il comando seguente per mostrare tutti i thread con i rispettivi stack di chiamate:  
  
     **~\*kb**  
  
     Questo comando genera un output simile al seguente.  
  
    ```  
    0012f3b0 79ff0bf8 mscorwks!WKS::GCHeap::GarbageCollect   
    0012f454 30002894 mscorwks!GCInterface::CollectGeneration+0xa4  
    0012f490 79fa22bd fragment_ni!request.Main(System.String[])+0x48  
    ```  
  
     Se l'operazione di Garbage Collection è stata provocata da una notifica di memoria insufficiente dal sistema operativo, lo stack di chiamate è simile, ad eccezione del fatto che il thread è il thread del finalizzatore.  Il thread del finalizzatore ottiene una notifica di memoria insufficiente asincrona e provoca l'operazione di Garbage Collection.  
  
     Se l'operazione di Garbage Collection è stata causata dall'allocazione di memoria, lo stack viene visualizzato in questo modo:  
  
    ```  
    0012f230 7a07c551 mscorwks!WKS::GCHeap::GarbageCollectGeneration  
    0012f2b8 7a07cba8 mscorwks!WKS::gc_heap::try_allocate_more_space+0x1a1  
    0012f2d4 7a07cefb mscorwks!WKS::gc_heap::allocate_more_space+0x18  
    0012f2f4 7a02a51b mscorwks!WKS::GCHeap::Alloc+0x4b  
    0012f310 7a02ae4c mscorwks!Alloc+0x60  
    0012f364 7a030e46 mscorwks!FastAllocatePrimitiveArray+0xbd  
    0012f424 300027f4 mscorwks!JIT_NewArr1+0x148  
    000af70f 3000299f fragment_ni!request..ctor(Int32, Single)+0x20c  
    0000002a 79fa22bd fragment_ni!request.Main(System.String[])+0x153  
    ```  
  
     Un helper JIT \(`JIT_New*`\) chiama infine `GCHeap::GarbageCollectGeneration`.  Se si determina che le operazioni di Garbage Collection di generazione 2 sono causate da allocazioni, è necessario definire gli oggetti raccolti da tali operazioni e come evitarli.  Ovvero, si vuole determinare la differenza tra l'inizio e la fine di un'operazione di Garbage Collection di generazione 2, nonché gli oggetti che hanno provocato la raccolta di generazione 2.  
  
     Ad esempio, digitare il comando seguente nel debugger per mostrare l'inizio di una raccolta di generazione 2:  
  
     **\!dumpheap –stat**  
  
     Output di esempio \(abbreviato per mostrare gli oggetti che usano la maggior parte dello spazio\):  
  
    ```  
    79124228    31857      9862328 System.Object[]  
    035f0384    25668     11601936 Toolkit.TlkPosition  
    00155f80    21248     12256296      Free  
    79103b6c   297003     13068132 System.Threading.ReaderWriterLock  
    7a747ad4   708732     14174640 System.Collections.Specialized.HybridDictionary  
    7a747c78   786498     15729960 System.Collections.Specialized.ListDictionary+DictionaryNode  
    7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary  
    035f0ee4    89192     38887712 Toolkit.TlkOrder  
    00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]  
    7912c444    91616     71887080 System.Double[]  
    791242ec    32451     82462728 System.Collections.Hashtable+bucket[]  
    790fa3e0  2459154    112128436 System.String  
    Total 6471774 objects  
    ```  
  
     Ripetere il comando alla fine della generazione 2:  
  
     **\!dumpheap –stat**  
  
     Output di esempio \(abbreviato per mostrare gli oggetti che usano la maggior parte dello spazio\):  
  
    ```  
    79124228    26648      9314256 System.Object[]  
    035f0384    25668     11601936 Toolkit.TlkPosition  
    79103b6c   296770     13057880 System.Threading.ReaderWriterLock  
    7a747ad4   708730     14174600 System.Collections.Specialized.HybridDictionary  
    7a747c78   786497     15729940 System.Collections.Specialized.ListDictionary+DictionaryNode  
    7a747bac   700298     19608344 System.Collections.Specialized.ListDictionary  
    00155f80    13806     34007212      Free  
    035f0ee4    89187     38885532 Toolkit.TlkOrder  
    00fcae40     6193     44911636 WaveBasedStrategy.Tick_Snap[]  
    791242ec    32370     82359768 System.Collections.Hashtable+bucket[]  
    790fa3e0  2440020    111341808 System.String  
    Total 6417525 objects  
    ```  
  
     Gli oggetti `double[]` sono scomparsi dalla fine dell'output, a indicare che sono stati raccolti.  Questi oggetti corrispondono a circa 70 MB.  Gli oggetti rimanenti non sono cambiati molto.  Di conseguenza, questi oggetti `double[]` sono il motivo per cui si è verificata un'operazione di Garbage Collection di generazione 2 .  Il passaggio successivo consiste nel determinare il motivo per cui gli oggetti `double[]` sono ancora presenti e perché sono diventati inutilizzati.  È possibile chiedere allo sviluppatore del codice da dove provengono questi oggetti oppure è possibile usare il comando **gcroot**.  
  
<a name="HighCPU"></a>   
##### Per determinare se l'utilizzo elevato della CPU è causato da Garbage Collection  
  
-   Correlare il valore del contatore delle prestazioni della memoria `% Time in GC` alla durata del processo.  
  
     Se il valore `% Time in GC` mostra la presenza di picchi contemporaneamente alla durata del processo, l'operazione di Garbage Collection è la causa dell'elevato utilizzo della CPU.  In caso contrario, profilare l'applicazione per individuare il punto in cui si verifica un utilizzo elevato.  
  
## Vedere anche  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)