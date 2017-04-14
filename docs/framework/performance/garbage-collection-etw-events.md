---
title: "Garbage Collection ETW Events | Microsoft Docs"
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
  - "GC events"
  - "garbage collection events [.NET Framework]"
  - "ETW, garbage collection events (CLR)"
ms.assetid: f14b6fd7-0966-4d87-bc89-54ef3a44a94a
caps.latest.revision: 21
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# Garbage Collection ETW Events
<a name="top"></a> Questi eventi raccolgono informazioni relative alla Garbage Collection ai fini della diagnostica e del debug, tra cui stabilire quante volte è stato eseguito il processo di Garbage Collection, la quantità di memoria liberata durante la procedura di Garbage Collection e così via.  
  
 Questa categoria include i seguenti eventi:  
  
-   [GCStart\_V1 Event](#gcstart_v1_event)  
  
-   [GCEnd\_V1 Event](#gcend_v1_event)  
  
-   [GCHeapStats\_V1 Event](#gcheapstats_v1_event)  
  
-   [GCCreateSegment\_V1 Event](#gccreatesegment_v1_event)  
  
-   [GCFreeSegment\_V1 Event](#gcfreesegment_v1_event)  
  
-   [GCRestartEEBegin\_V1 Event](#gcrestarteebegin_v1_event)  
  
-   [GCRestartEEEnd\_V1 Event](#gcrestarteeend_v1_event)  
  
-   [GCSuspendEE\_V1 Event](#gcsuspendee_v1_event)  
  
-   [GCSuspendEEEnd\_V1 Event](#gcsuspendeeend_v1_event)  
  
-   [GCAllocationTick\_V2 Event](#gcallocationtick_v2_event)  
  
-   [GCFinalizersBegin\_V1 Event](#gcfinalizersbegin_v1_event)  
  
-   [GCFinalizersEnd\_V1 Event](#gcfinalizersend_v1_event)  
  
-   [GCCreateConcurrentThread\_V1 Event](#gccreateconcurrentthread_v1_event)  
  
-   [GCTerminateConcurrentThread\_V1 Event](#gcterminateconcurrentthread_v1_event)  
  
<a name="gcstart_v1_event"></a>   
## GCStart\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello Per altre informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCStart_V1`|1|È stata avviata una procedura di Garbage Collection.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt32|L'*ennesima* Garbage Collection.|  
|Profondità|win:UInt32|La generazione che viene raccolta.|  
|Motivo|win:UInt32|Motivo per cui è stata attivata la Garbage Collection:<br /><br /> 0x0 \- Allocazione heap oggetto piccolo.<br /><br /> 0x1 \- Indotto.<br /><br /> 0x2 \- Memoria insufficiente.<br /><br /> 0x3 \- Vuoto.<br /><br /> 0x4 \- Allocazione heap oggetto grande.<br /><br /> 0x5 \- Spazio esaurito \(per heap oggetto piccolo\).<br /><br /> 0x6 \- Spazio esaurito \(per heap oggetto grande\).<br /><br /> 0x7 \- Indotto ma non forzato come blocco.|  
|Tipo|win:UInt32|0x0 \- Un'operazione di Garbage Collection bloccante è stata eseguita all'esterno della procedura di Garbage Collection in background.<br /><br /> 0x1 \- Garbage Collection in background.<br /><br /> 0x2 \- Un'operazione di Garbage Collection bloccante è stata eseguita durante la procedura di Garbage Collection in background.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gcend_v1_event"></a>   
## GCEnd\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCEnd_V1`|2|È stata terminata una procedura di Garbage Collection.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt32|L'*ennesima* Garbage Collection.|  
|Profondità|win:UInt32|La generazione che è stata raccolta.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gcheapstats_v1_event"></a>   
## GCHeapStats\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Descrizione|  
|------------|---------------|-----------------|  
|`GCHeapStats_V1`|4|Mostra le statistiche heap alla fine di ogni Garbage Collection.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|GenerationSize0|win:UInt64|Dimensione, in byte, della memoria della generazione 0.|  
|TotalPromotedSize0|win:UInt64|Numero di byte promossi dalla generazione 0 alla generazione 1.|  
|GenerationSize1|win:UInt64|Dimensione, in byte, della memoria di generazione 1.|  
|TotalPromotedSize1|win:UInt64|Numero di byte promossi dalla generazione 1 alla generazione 2.|  
|GenerationSize2|win:UInt64|Dimensione, in byte, della memoria della generazione 2.|  
|TotalPromotedSize2|win:UInt64|Numero di byte rimasti nella generazione 2 dopo l'ultima raccolta.|  
|GenerationSize3|win:UInt64|Dimensione, in byte, dell'heap oggetto grande.|  
|TotalPromotedSize3|win:UInt64|Numero di byte rimasti nell'heap oggetto grande dopo l'ultima raccolta.|  
|FinalizationPromotedSize|win:UInt64|Dimensione totale, in byte, degli oggetti pronti per la finalizzazione.|  
|FinalizationPromotedCount|win:UInt64|Numero di oggetti pronti per la finalizzazione.|  
|PinnedObjectCount|win:UInt32|Numero di oggetti bloccati \(fissi\).|  
|SinkBlockCount|win:UInt32|Numero di blocchi di sincronizzazione in uso.|  
|GCHandleCount|win:UInt32|Numero di handle di Garbage Collection in uso.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gccreatesegment_v1_event"></a>   
## GCCreateSegment\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCCreateSegment_V1`|5|È stato creato un nuovo segmento di Garbage Collection. Inoltre, quando la traccia è attivata su un processo già in esecuzione, questo evento viene generato per ogni segmento esistente.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Indirizzo|win:UInt64|Indirizzo del segmento.|  
|Dimensioni|win:UInt64|Dimensione del segmento.|  
|Tipo|win:UInt32|0x0 \- Heap oggetto piccolo.<br /><br /> 0x1 \- Heap oggetto grande.<br /><br /> 0x2 \- Heap di sola lettura.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 Si noti che la dimensione dei segmenti allocati dal Garbage Collector è specifico dell'implementazione ed è soggetta a modifiche in qualsiasi momento, tra cui aggiornamenti periodici. L'applicazione non deve dare per scontata o dipendere da una particolare dimensione del segmento, né provare a configurare la quantità di memoria disponibile per le allocazioni di segmenti.  
  
 [Torna all'inizio](#top)  
  
<a name="gcfreesegment_v1_event"></a>   
## GCFreeSegment\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCFreeSegment_V1`|6|È stato rilasciato un segmento di Garbage Collection.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Indirizzo|win:UInt64|Indirizzo del segmento.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gcrestarteebegin_v1_event"></a>   
## GCRestartEEBegin\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCRestartEEBegin_V1`|7|Il ripristino dalla sospensione di Common Language Runtime è iniziato.|  
  
 Nessun dato dell'evento.  
  
 [Torna all'inizio](#top)  
  
<a name="gcrestarteeend_v1_event"></a>   
## GCRestartEEEnd\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCRestartEEEnd_V1`|3|Il ripristino dalla sospensione di Common Language Runtime è terminato.|  
  
 Nessun dato dell'evento.  
  
 [Torna all'inizio](#top)  
  
<a name="gcsuspendee_v1_event"></a>   
## GCSuspendEE\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCSuspendEE_V1`|9|Inizio della sospensione del motore di esecuzione di operazioni di Garbage Collection.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Motivo|win:UInt16|0x0 \- Altro.<br /><br /> 0x1 \- Garbage Collection.<br /><br /> 0x2 \- Arresto del dominio applicazione.<br /><br /> 0x3. \- Lancio del codice.<br /><br /> 0x4 \- Arresto.<br /><br /> 0x5 \- Debugger.<br /><br /> 0x6 \- Preparazione per l'operazione di Garbage Collection.|  
|Conteggio|win:UInt32|Numero di thread che sono sospesi.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gcsuspendeeend_v1_event"></a>   
## GCSuspendEEEnd\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello:  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento:  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCSuspendEEEnd_V1`|8|Fine della sospensione del motore di esecuzione di operazioni di Garbage Collection.|  
  
 Nessun dato dell'evento.  
  
 [Torna all'inizio](#top)  
  
<a name="gcallocationtick_v2_event"></a>   
## GCAllocationTick\_V2 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCAllocationTick_V2`|10|Ogni volta vengono allocati circa 100 KB.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|AllocationAmount|win:UInt32|Dimensione dell'allocazione, in byte. Questo valore è preciso per le allocazioni minori della lunghezza di un ULONG \(4.294.967.295 byte\). Se l'allocazione è maggiore, questo campo contiene un valore troncato. Usare `AllocationAmount64` per le allocazioni di dimensioni molto grandi.|  
|AllocationKind|win:UInt32|0x0 \- Allocazione di oggetti piccoli \(l'allocazione è nell'heap oggetto piccolo\).<br /><br /> 0x1 \- Allocazione di oggetti grandi \(l'allocazione è nell'heap oggetto grande\).|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
|AllocationAmount64|win:UInt64|Dimensione dell'allocazione, in byte. Questo valore è preciso per le allocazioni di dimensioni molto grandi.|  
|TypeId|win:Pointer|Indirizzo di MethodTable. Quando sono presenti diversi tipi di oggetti allocati durante questo evento, questo è l'indirizzo di MethodTable che corrisponde all'ultimo oggetto allocato \(l'oggetto che ha causato il superamento della soglia di 100 KB\).|  
|TypeName|win:UnicodeString|Nome del tipo che è stato allocato. Quando sono presenti diversi tipi di oggetti allocati durante questo evento, questo è il tipo dell'ultimo oggetto allocato \(l'oggetto che ha causato il superamento della soglia di 100 KB\).|  
|HeapIndex|win:UInt32|Heap in cui l'oggetto è stato allocato. Questo valore è 0 \(zero\) durante l'esecuzione della procedura di Garbage Collection per workstation.|  
  
 [Torna all'inizio](#top)  
  
<a name="gcfinalizersbegin_v1_event"></a>   
## GCFinalizersBegin\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCFinalizersBegin_V1`|14|Inizio dell'esecuzione dei finalizzatori.|  
  
 Nessun dato dell'evento.  
  
 [Torna all'inizio](#top)  
  
<a name="gcfinalizersend_v1_event"></a>   
## GCFinalizersEnd\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCFinalizersEnd_V1`|13|Fine dell'esecuzione dei finalizzatori.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt32|Numero di finalizzatori eseguiti.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="gccreateconcurrentthread_v1_event"></a>   
## GCCreateConcurrentThread\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCCreateConcurrentThread_V1`|11|È stato creato il thread di Garbage Collection in modalità simultanea|  
  
 Nessun dato dell'evento.  
  
 [Torna all'inizio](#top)  
  
<a name="gcterminateconcurrentthread_v1_event"></a>   
## GCTerminateConcurrentThread\_V1 Event  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`GCKeyword` \(0x1\)|Informativo \(4\)|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`GCTerminateConcurrentThread_V1`|12|È stato terminato il thread di Garbage Collection in modalità simultanea.|  
  
 Nessun dato dell'evento.  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)