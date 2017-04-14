---
title: "Data Structures for Parallel Programming | Microsoft Docs"
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
  - "data structures, multi-threading"
ms.assetid: bdc82f2f-4754-45a1-a81e-fe2e9c30cef9
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Data Structures for Parallel Programming
La versione 4 di .NET Framework introduce molti nuovi tipi particolarmente utili per la programmazione in parallelo, fra cui un set di classi di raccolte simultanee, primitive di sincronizzazione leggere e tipi per l'inizializzazione differita.  Questi tipi possono essere utilizzati con qualsiasi codice di applicazione multithreading, compresi Task Parallel Library e PLINQ.  
  
## Classi di raccolte simultanee  
 Le classi di raccolte nello spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName> forniscono operazioni di aggiunta e rimozione thread\-safe che, laddove possibile, evitano i blocchi. Quando i blocchi sono necessari, tali classi utilizzano blocchi con granularità fine.  A differenza delle raccolte introdotte nelle versioni 1.0 e 2.0 di .NET Framework, una classe di raccolte simultanee non richiede l'acquisizione di blocchi da parte del codice utente quando quest'ultimo accede agli elementi.  Le classi di raccolte simultanee possono migliorare significativamente le prestazioni dei tipi quali <xref:System.Collections.ArrayList?displayProperty=fullName> e <xref:System.Collections.Generic.List%601?displayProperty=fullName> \(con blocco implementato dall'utente\) negli scenari in cui più thread aggiungono e rimuovono elementi da una raccolta.  
  
 Nella tabella seguente vengono elencate le nuove classi di raccolte simultanee:  
  
|Type|Descrizione|  
|----------|-----------------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName>|Fornisce funzionalità di blocco e limitazione per le raccolte thread\-safe che implementano <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=fullName>.  I thread producer si bloccano in caso di assenza di slot disponibili o se la raccolta è completa.  I thread consumer si bloccano se la raccolta è vuota.  Questo tipo supporta inoltre l'accesso non bloccante da parte di consumer e producer.  L'oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> può essere utilizzato come una classe base o un archivio di backup per fornire funzionalità di blocco e limitazione per qualsiasi classe di raccolte che supporta <xref:System.Collections.Generic.IEnumerable%601>.|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName>|Implementazione di contenitore thread\-safe che fornisce operazioni scalabili di aggiunta e get.|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>|Tipo di dizionario simultaneo e scalabile.|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>|Coda FIFO simultanea e scalabile.|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName>|Stack LIFO simultaneo e scalabile.|  
  
 Per ulteriori informazioni, vedere [Raccolte thread\-safe](../../../docs/standard/collections/thread-safe/index.md).  
  
## Primitive di sincronizzazione  
 Le nuove primitive di sincronizzazione nello spazio dei nomi <xref:System.Threading?displayProperty=fullName> evitano i dispendiosi meccanismi di blocco presenti nel codice multithreading legacy e pertanto sono in grado di offrire una concorrenza con granularità fine e una maggiore velocità di esecuzione.  Per alcuni dei nuovi tipi, ad esempio <xref:System.Threading.Barrier?displayProperty=fullName> e <xref:System.Threading.CountdownEvent?displayProperty=fullName>, non esiste alcuna controparte nelle prime versioni di .NET Framework.  
  
 Nella tabella seguente sono elencati i nuovi tipi di sincronizzazione:  
  
|Type|Descrizione|  
|----------|-----------------|  
|<xref:System.Threading.Barrier?displayProperty=fullName>|Consente a più thread di utilizzare un algoritmo in parallelo fornendo un punto in cui ogni attività può segnalare il proprio arrivo e quindi bloccarsi fino all'arrivo di tutte le attività o di una parte di esse.  Per ulteriori informazioni, vedere [Barrier](../../../docs/standard/threading/barrier.md).|  
|<xref:System.Threading.CountdownEvent?displayProperty=fullName>|Semplifica gli scenari di fork e join fornendo un facile meccanismo di incontro.  Per ulteriori informazioni, vedere [CountdownEvent](../../../docs/standard/threading/countdownevent.md).|  
|<xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>|Primitiva di sincronizzazione simile a <xref:System.Threading.ManualResetEvent?displayProperty=fullName>.  L'oggetto <xref:System.Threading.ManualResetEventSlim> è più leggero ma può essere utilizzato solo per le comunicazioni interne del processo.  Per ulteriori informazioni, vedere [ManualResetEvent and ManualResetEventSlim](../../../docs/standard/threading/manualresetevent-and-manualreseteventslim.md).|  
|<xref:System.Threading.SemaphoreSlim?displayProperty=fullName>|Primitiva di sincronizzazione che limita il numero di thread che possono accedere simultaneamente a una risorsa o a un pool di risorse.  Per ulteriori informazioni, vedere [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md).|  
|<xref:System.Threading.SpinLock?displayProperty=fullName>|Primitiva di blocco di esclusione reciproca che impone a un thread che sta tentando di acquisire il blocco di restare in attesa in un ciclo \(*spin*\) per un periodo di tempo prima di cedere il proprio il quantum.  Negli scenari in cui si prevede che l'attesa del blocco sarà breve, <xref:System.Threading.SpinLock> offre prestazioni migliori rispetto alle altre forme di blocco.  Per ulteriori informazioni, vedere [SpinLock](../../../docs/standard/threading/spinlock.md).|  
|<xref:System.Threading.SpinWait?displayProperty=fullName>|Tipo leggero e di dimensioni ridotte che eseguirà spin per un determinato periodo di tempo e che infine metterà il thread in uno stato di attesa se viene superato il numero di spin.  Per ulteriori informazioni, vedere [SpinWait](../../../docs/standard/threading/spinwait.md).|  
  
 Per ulteriori informazioni, vedere:  
  
-   [How to: Use SpinLock for Low\-Level Synchronization](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md)  
  
-   [How to: Synchronize Concurrent Operations with a Barrier](../../../docs/standard/threading/how-to-synchronize-concurrent-operations-with-a-barrier.md).  
  
## Classi di inizializzazione differita  
 Nell'inizializzazione differita la memoria per un oggetto viene allocata solo quando occorre.  L'inizializzazione differita può migliorare le prestazioni distribuendo uniformemente le allocazioni degli oggetti nel corso della durata di un programma.  È possibile consentire l'inizializzazione differita di qualsiasi tipo personalizzato tramite il wrapping del tipo <xref:System.Lazy%601>.  
  
 Nella tabella seguente sono elencati i tipi di inizializzazione differita:  
  
|Type|Descrizione|  
|----------|-----------------|  
|<xref:System.Lazy%601?displayProperty=fullName>|Fornisce un'inizializzazione differita leggera e thread\-safe.|  
|<xref:System.Threading.ThreadLocal%601?displayProperty=fullName>|Fornisce per ogni singolo thread un valore con inizializzazione differita, in cui ogni thread richiama in modo differito la funzione di inizializzazione.|  
|<xref:System.Threading.LazyInitializer?displayProperty=fullName>|Fornisce metodi statici che evitano la necessità di allocare un'istanza dedicata con inizializzazione differita.  Tali metodi, invece, utilizzano riferimenti per garantire che le destinazioni siano state inizializzate al momento dell'accesso.|  
  
 Per ulteriori informazioni, vedere [Lazy Initialization](../../../docs/framework/performance/lazy-initialization.md).  
  
## Eccezioni di aggregazione  
 È possibile utilizzare il tipo <xref:System.AggregateException?displayProperty=fullName> per acquisire più eccezioni generate contemporaneamente in thread separati e restituirle al thread di unione come singola eccezione.  I tipi <xref:System.Threading.Tasks.Task?displayProperty=fullName> e <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> e PLINQ utilizzano ampiamente <xref:System.AggregateException> a tale scopo.  Per ulteriori informazioni, vedere [NIB: How to: Handle Exceptions Thrown by Tasks](http://msdn.microsoft.com/it-it/d6c47ec8-9de9-4880-beb3-ff19ae51565d) e [How to: Handle Exceptions in a PLINQ Query](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md).  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 <xref:System.Threading?displayProperty=fullName>   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)