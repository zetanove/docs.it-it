---
title: "Thread Pool ETW Events | Microsoft Docs"
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
  - "thread pool events [.NET Framework]"
  - "ETW, thread pool events (CLR)"
ms.assetid: f2a21e3a-3b6c-4433-97f3-47ff16855ecc
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Thread Pool ETW Events
<a name="top"></a> Questi eventi raccolgono informazioni sui thread di lavoro e di I\/O.  
  
 Esistono due gruppi di eventi del pool di thread:  
  
-   [Eventi del pool di thread di lavoro](#worker), che forniscono informazioni su come un'applicazione usa il pool di thread e l'effetto dei carichi di lavoro sul controllo della concorrenza.  
  
-   [Eventi del pool di thread di I\/O](#io), che forniscono informazioni sui thread di I\/O che vengono creati, ritirati, non ritirati o terminati nel pool di thread.  
  
<a name="worker"></a>   
## Eventi del pool di thread di lavoro  
 Questi eventi sono correlati al pool di thread di lavoro del runtime e forniscono notifiche per gli eventi thread \(ad esempio, quando un thread viene creato o arrestato\). Il pool di thread di lavoro usa un algoritmo adattivo per il controllo della concorrenza, dove il numero di thread viene calcolato in base alla velocità effettiva misurata. Gli eventi di pool del thread di lavoro possono essere usati per comprendere come un'applicazione usa il pool di thread e l'effetto che alcuni carichi di lavoro possono avere sul controllo della concorrenza.  
  
### ThreadPoolWorkerThreadStart e ThreadPoolWorkerThreadStop  
 La tabella seguente illustra la parola chiave e il livello per questi eventi Per altre informazioni, vedere [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
||||  
|-|-|-|  
|Evento|ID evento|Generato quando|  
|`ThreadPoolWorkerThreadStart`|50|Viene creato un thread di lavoro.|  
|`ThreadPoolWorkerThreadStop`|51|Viene arrestato un thread di lavoro.|  
|`ThreadPoolWorkerThreadRetirementStart`|52|Viene ritirato un thread di lavoro.|  
|`ThreadPoolWorkerThreadRetirementStop`|53|Un thread di lavoro ritirato diventa nuovamente attivo.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|ActiveWorkerThreadCount|win:UInt32|Numero di thread di lavoro disponibili per l'elaborazione di lavoro, inclusi quelli che già elaborano il lavoro.|  
|RetiredWorkerThreadCount|win:UInt32|Il numero di thread di lavoro che non sono disponibili per l'elaborazione di lavoro, ma che vengono mantenuti in riserva nel caso in cui più thread sono necessari in un secondo momento.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### ThreadPoolWorkerThreadAdjustment  
 Questi eventi del pool di thread forniscono informazioni per la comprensione e il debug del comportamento dell'algoritmo di inserimento thread \(controllo della concorrenza\). Le informazioni vengono usate internamente dal pool del thread di lavoro.  
  
#### ThreadPoolWorkerThreadAdjustmentSample  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Descrizione|  
|------------|---------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentSample`|54|Fa riferimento alla raccolta di informazioni per un esempio, ovvero una misurazione della velocità effettiva con un livello determinato di concorrenza in un istante di tempo.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Velocità effettiva|win:Double|Numero di completamenti per unità di tempo.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
#### ThreadPoolWorkerThreadAdjustmentAdjustment  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Descrizione|  
|------------|---------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentAdjustment`|55|Registra una modifica nel controllo, quando l'algoritmo di inserimento thread \(spostamento verso l’alto\) determina che una modifica nel livello di concorrenza è attiva.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|AverageThroughput|win:Double|Velocità effettiva Media di un campione di misurazioni.|  
|NewWorkerThreadCount|win:UInt32|Nuovo numero di thread di lavoro attivi.|  
|Motivo|win:UInt32|Motivo della modifica.<br /><br /> 0x00 \- Riscaldamento.<br /><br /> 0x01 \- Inizializzazione test in corso.<br /><br /> 0x02 \- Spostamento casuale.<br /><br /> 0x03 \- Spostamento verso l’alto.<br /><br /> 0x04 \- Modificare il punto.<br /><br /> 0x05 \- Stabilizzazione.<br /><br /> 0x06 \- Esaurimento delle risorse.<br /><br /> 0x07 \- Timeout del thread.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
#### ThreadPoolWorkerThreadAdjustmentStats  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Descrizione|  
|------------|---------------|-----------------|  
|`ThreadPoolWorkerThreadAdjustmentStats`|56|Raccoglie i dati nel pool di thread.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Durata|win:Double|Quantità di tempo, espresso in secondi, durante il quale sono state raccolte queste statistiche.|  
|Velocità effettiva|win:Double|Numero medio di completamenti al secondo durante questo intervallo.|  
|ThreadWave|win:Double|Riservato per uso interno.|  
|ThroughputWave|win:Double|Riservato per uso interno.|  
|ThroughputErrorEstimate|win:Double|Riservato per uso interno.|  
|AverageThroughputErrorEstimate|win:Double|Riservato per uso interno.|  
|ThroughputRatio|win:Double|L'aumento relativo di velocità effettiva causata dalle variazioni nel numero di thread di lavoro attivi durante questo intervallo.|  
|Probabilità|win:Double|Una misura della validità del campo ThroughputRatio.|  
|NewcontrolSetting|win:Double|Il numero di thread di lavoro attivi che verrà utilizzato come base per le variazioni future nel conteggio dei thread attivi.|  
|NewThreadWaveMagnitude|win:UInt16|La grandezza delle variazioni future nel conteggio dei thread attivi.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
 [Torna all'inizio](#top)  
  
<a name="io"></a>   
## Eventi dei Thread di I\/O  
 Questi eventi si verificano per i thread nel pool di thread di I\/O \(porte di completamento\), che è asincrono.  
  
### IOThreadCreate\_V1  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
||||  
|-|-|-|  
|Evento|ID evento|Generato quando|  
|`IOThreadCreate_V1`|44|Viene creato un thread di I\/O nel pool di thread.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt64|Numero di thread di I\/O, tra cui il thread appena creato.|  
|NumRetired|win:UInt64|Numero di thread di lavoro ritirato.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### IOThreadRetire\_V1  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`IOThreadRetire_V1`|46|Un thread di I\/O diventa un candidato al ritiro.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt64|Numero di thread di I\/O rimanenti nel pool di thread.|  
|NumRetired|win:UInt64|Numero di thread di I\/O ritirato.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### IOThreadUnretire\_V1  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`IOThreadUnretire_V1`|47|Un thread di I\/O viene ritirato a causa dell’I\/O pervenuto entro un periodo di attesa dopo che il thread diventa un candidato al ritiro.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt64|Numero di thread di I\/O nel pool di thread, incluso il presente.|  
|NumRetired|win:UInt64|Numero di thread di I\/O ritirato.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
### IOThreadTerminate  
 La tabella seguente illustra la parola chiave e il livello  
  
|Parola chiave per la generazione dell'evento|Livello|  
|--------------------------------------------------|-------------|  
|`ThreadingKeyword` \(0x10000\)|Informativo \(4\)|  
  
 La tabella seguente mostra le informazioni sull'evento.  
  
|Evento|ID evento|Generato quando|  
|------------|---------------|---------------------|  
|`IOThreadTerminate`|45|Viene creato un thread di I\/O nel pool di thread.|  
  
 La tabella seguente mostra i dati dell'evento.  
  
|Nome campo|Tipo di dati|Descrizione|  
|----------------|------------------|-----------------|  
|Conteggio|win:UInt64|Numero di thread di I\/O rimanenti nel pool di thread.|  
|NumRetired|win:UInt64|Numero di thread di I\/O ritirato.|  
|ClrInstanceID|win:UInt16|ID univoco per l'istanza di CLR o CoreCLR.|  
  
## Vedere anche  
 [CLR ETW Events](../../../docs/framework/performance/clr-etw-events.md)