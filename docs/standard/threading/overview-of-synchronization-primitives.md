---
title: "Overview of Synchronization Primitives | Microsoft Docs"
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
  - "synchronization, threads"
  - "threading [.NET Framework],synchronizing threads"
  - "managed threading"
ms.assetid: b782bcb8-da6a-4c6a-805f-2eb46d504309
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Overview of Synchronization Primitives
.NET Framework fornisce diverse primitive di sincronizzazione per controllare le interazioni dei thread ed evitare race condition.  Queste possono essere divise approssimativamente in tre categorie: blocco, segnalazione e operazioni interlocked.  
  
 Le categorie non sono definite in modo chiaro e preciso. Alcuni meccanismi di sincronizzazione possono avere caratteristiche comuni a più categorie: gli eventi che rilasciano un solo thread alla volta sono simili ai blocchi a livello funzionale, il rilascio dei blocchi può essere assimilato a un segnale e le operazioni interlocked possono essere usate per costruire i blocchi.  Questa suddivisione in categorie è comunque utile.  
  
 È importante ricordare che la sincronizzazione dei thread è cooperativa.  Se anche un solo thread ignora un meccanismo di sincronizzazione e accede direttamente alla risorsa protetta, meccanismo di sincronizzazione non può essere efficace.  
  
 In questa panoramica sono incluse le sezioni seguenti:  
  
-   [Blocco](#locking)  
  
-   [Signaling](#signaling)  
  
-   [Tipi di sincronizzazione leggera](#lightweight_synchronization_types)  
  
-   [SpinWait](#spinwait)  
  
-   [Operazioni interlocked](#interlocked_operations)  
  
<a name="locking"></a>   
## Blocco  
 I blocchi consentono il controllo di una risorsa usando un thread alla volta o un numero di thread specificato.  Un thread che richiede un blocco esclusivo quando il blocco è in uso si blocca finché il blocco non diventa disponibile.  
  
### Blocchi esclusivi  
 La forma di blocco più semplice è l'istruzione `lock` di C\# \(`SyncLock` in Visual Basic\) che controlla l'accesso a un blocco di codice.  Questo blocco viene spesso denominato sezione critica.  L'istruzione `lock` viene implementata usando i metodi <xref:System.Threading.Monitor.Enter%2A> e <xref:System.Threading.Monitor.Exit%2A> della classe <xref:System.Threading.Monitor> e usa `try…catch…finally` per verificare il rilascio del blocco.  
  
 In generale l'uso dell'istruzione `lock` per proteggere piccoli blocchi di codice che non comprendono più di un metodo è la soluzione migliore per usare la classe <xref:System.Threading.Monitor>.  Sebbene sia potete, la classe <xref:System.Threading.Monitor> è soggetta a blocchi orfani e deadlock.  
  
#### Classe Monitor  
 La classe <xref:System.Threading.Monitor> fornisce funzionalità aggiuntive che possono essere usate insieme all'istruzione `lock`:  
  
-   Il metodo <xref:System.Threading.Monitor.TryEnter%2A> consente a thread bloccato in attesa della risorsa di annullare l'operazione dopo un intervallo specificato.  Restituisce un valore booleano che indica l'esito dell'operazione, che può essere usato per rilevare ed evitare potenziali deadlock.  
  
-   Il metodo <xref:System.Threading.Monitor.Wait%2A> viene chiamato da un thread in una sezione critica.  Annulla il controllo della risorsa e si blocca finché la risorsa non torna disponibile.  
  
-   I metodi <xref:System.Threading.Monitor.Pulse%2A> e <xref:System.Threading.Monitor.PulseAll%2A> consentono a un thread che sta per rilasciare un blocco o per chiamare <xref:System.Threading.Monitor.Wait%2A> di inserire uno o più thread nella coda degli elementi pronti, in modo che possano acquisire il blocco.  
  
 I timeout negli overload del metodo <xref:System.Threading.Monitor.Wait%2A> consentono ai thread in attesa di eseguire l'escape nella coda degli elementi pronti.  
  
 La classe <xref:System.Threading.Monitor> può fornire il blocco in più domini applicazioni se l'oggetto usato per il blocco deriva da <xref:System.MarshalByRefObject>.  
  
 <xref:System.Threading.Monitor> presenta affinità di thread.  In altre parole, un thread che accede al monitor deve uscire chiamando <xref:System.Threading.Monitor.Exit%2A> o <xref:System.Threading.Monitor.Wait%2A>.  
  
 Non è possibile creare istanze della classe <xref:System.Threading.Monitor>.  I metodi sono statici \(`Shared` in Visual Basic\) e vengono eseguiti in un oggetto di blocco istanziabile.  
  
 Per una panoramica concettuale, vedere [Monitor](../Topic/Monitors.md).  
  
#### Classe Mutex  
 I thread richiedono un <xref:System.Threading.Mutex> chiamando un overload del metodo <xref:System.Threading.WaitHandle.WaitOne%2A>.  Gli overload con timeout vengono forniti per consentire ai thread di annullare l'attesa.  A differenza della classe <xref:System.Threading.Monitor>, un mutex può essere sia locale che globale.  I mutex globali, denominati anche mutex, sono visibili in tutto il sistema operativo e possono essere usati per sincronizzare i thread in più domini applicazioni o processi.  I mutex locali derivano da <xref:System.MarshalByRefObject> e possono essere usati tra i limiti dei domini applicazioni.  
  
 Inoltre <xref:System.Threading.Mutex> deriva da <xref:System.Threading.WaitHandle>, quindi può essere usato con i meccanismi di segnalazione forniti da <xref:System.Threading.WaitHandle>, ad esempio i metodi <xref:System.Threading.WaitHandle.WaitAll%2A>, <xref:System.Threading.WaitHandle.WaitAny%2A> e <xref:System.Threading.WaitHandle.SignalAndWait%2A>.  
  
 Analogamente a <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex> presenta affinità di thread.  A differenza di <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex> è un oggetto istanziabile.  
  
 Per una panoramica concettuale, vedere [Mutexes](../../../docs/standard/threading/mutexes.md).  
  
#### Classe SpinLock  
 A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], è possibile usare la classe <xref:System.Threading.SpinLock> quando il sovraccarico richiesto da <xref:System.Threading.Monitor> riduce le prestazioni.  Quando <xref:System.Threading.SpinLock> rileva una sezione critica bloccata, avvia semplicemente una rotazione ciclica finché il blocco non diventa disponibile.  Se il blocco viene mantenuto per un tempo molto breve, la rotazione può fornire prestazioni migliori rispetto al blocco.  Tuttavia, se il blocco viene mantenuto per diverse decine di cicli, le prestazioni di <xref:System.Threading.SpinLock> sono analoghe a <xref:System.Threading.Monitor>, ma richiedono più cicli CPU, riducendo così le prestazioni degli altri thread o processi.  
  
### Altri blocchi  
 Non è necessario che i blocchi siano esclusivi.  Spesso è utile consentire l'accesso simultaneo a una risorsa a un numero limitato di thread.  I semafori e i blocchi in lettura\/scrittura sono progettati per controllare questo tipo di accesso alle risorse in pool.  
  
#### Classe ReaderWriterLock  
 La classe <xref:System.Threading.ReaderWriterLockSlim> viene usata quando un thread in grado di modificare i dati \(writer\) deve avere un accesso esclusivo a una risorsa.  Quando il writer non è arrivo, l'accesso alla risorsa può essere eseguito da un qualsiasi numero di lettori \(ad esempio, chiamando il metodo <xref:System.Threading.ReaderWriterLockSlim.EnterReadLock%2A>\).  Quando un thread richiede l'accesso esclusivo, ad esempio chiamando il metodo <xref:System.Threading.ReaderWriterLockSlim.EnterWriteLock%2A>, le richieste del lettore successive vengono bloccate finché tutti i lettori esistenti non escono dal blocco e il writer non è entrato e uscito dal blocco.  
  
 <xref:System.Threading.ReaderWriterLockSlim> presenta affinità di thread.  
  
 Per una panoramica concettuale, vedere [Reader\-Writer Locks](../../../docs/standard/threading/reader-writer-locks.md).  
  
#### Classe Semaphore  
 La classe <xref:System.Threading.Semaphore> consente a un numero di thread specificato di accedere a una risorsa.  Eventuali altri thread che richiedono la risorsa vengono bloccati finché un thread rilascia il semaforo.  
  
 Analogamente alla classe <xref:System.Threading.Mutex>, <xref:System.Threading.Semaphore> deriva da <xref:System.Threading.WaitHandle>.  Analogamente a <xref:System.Threading.Mutex>, inoltre, <xref:System.Threading.Semaphore> può essere sia locale che globale.  Può essere usato tra i limiti dei domini applicazioni.  
  
 A differenza di <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex> e <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Semaphore> non presenta affinità di thread.  Ciò significa che può essere usato in scenari in cui un thread acquisisce il semaforo e un altro lo rilascia.  
  
 Per una panoramica concettuale, vedere [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md).  
  
 <xref:System.Threading.SemaphoreSlim?displayProperty=fullName> è un semaforo leggero per la sincronizzazione all'interno di un unico processo.  
  
 [Torna all'inizio](#top)  
  
<a name="signaling"></a>   
## Signaling  
 Il modo più semplice per attendere un segnale da un altro thread consiste nel chiamare il metodo <xref:System.Threading.Thread.Join%2A> che si blocca fino al completamento dell'altro thread.  <xref:System.Threading.Thread.Join%2A> ha due overload che consentono al thread bloccato di interrompere l'attesa dopo che è trascorso un intervallo di tempo specificato.  
  
 Gli handle di attesa forniscono un set di funzionalità di attesa e di segnalazione più completo.  
  
### Handle di attesa  
 Gli handle di attesa derivano dalla classe <xref:System.Threading.WaitHandle>, che a sua volta deriva da <xref:System.MarshalByRefObject>.  Quindi, gli handle di attesa possono essere usati per sincronizzare le attività dei thread tra i limiti dei domini applicazioni.  
  
 I thread si bloccano negli handle di attesa chiamando il metodo di istanza <xref:System.Threading.WaitHandle.WaitOne%2A> o uno dei metodi statici <xref:System.Threading.WaitHandle.WaitAll%2A>, <xref:System.Threading.WaitHandle.WaitAny%2A> o <xref:System.Threading.WaitHandle.SignalAndWait%2A>.  Le modalità di rilascio dipendono dal metodo chiamato e dal tipo di handle di attesa.  
  
 Per una panoramica concettuale, vedere [Wait Handles](../Topic/Wait%20Handles.md).  
  
#### Handle di attesa evento  
 Gli handle di attesa evento includono la classe <xref:System.Threading.EventWaitHandle> e le classi derivate, <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.ManualResetEvent>.  I thread vengono rilasciati da un handle di attesa evento quando questo handle viene segnalato chiamando il metodo <xref:System.Threading.EventWaitHandle.Set%2A> o usando il metodo <xref:System.Threading.WaitHandle.SignalAndWait%2A>.  
  
 L'handle di attesa evento li reimposta automaticamente, come un tornello che consente il passaggio di solo un thread ogni volta che viene segnalato, oppure è necessario reimpostarli manualmente, come un cancello che viene chiuso fino a segnalazione e resta aperto finché qualcuno non lo chiude.  Come indicato dai nomi, <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.ManualResetEvent> rappresentano la prima e la seconda opzione, rispettivamente.  <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> è un evento leggero per la sincronizzazione all'interno di un unico processo.  
  
 <xref:System.Threading.EventWaitHandle> può rappresentare qualsiasi tipo di evento e può essere locale o globale.  Le classi derivate <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.ManualResetEvent> sono sempre locali.  
  
 Gli handle di attesa evento non presentano affinità di thread.  Qualsiasi thread può segnalare un handle di attesa evento.  
  
 Per una panoramica concettuale, vedere [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md).  
  
#### Classi Mutex e Semaphore  
 Poiché le classi <xref:System.Threading.Mutex> e <xref:System.Threading.Semaphore> derivano da <xref:System.Threading.WaitHandle>, possono essere usate con i metodi statici di <xref:System.Threading.WaitHandle>.  Ad esempio, un thread può usare il metodo <xref:System.Threading.WaitHandle.WaitAll%2A> per attendere finché tutte e tre le condizioni seguenti non risultano vere: <xref:System.Threading.EventWaitHandle> viene segnalato e <xref:System.Threading.Mutex> e <xref:System.Threading.Semaphore> vengono rilasciati.  Analogamente, un thread può usare il metodo <xref:System.Threading.WaitHandle.WaitAny%2A> per attendere finché non si verifica una delle condizioni.  
  
 Per <xref:System.Threading.Mutex> o <xref:System.Threading.Semaphore>, la segnalazione equivale al rilascio.  Se uno dei due tipi viene usato come primo argomento del metodo <xref:System.Threading.WaitHandle.SignalAndWait%2A>, viene rilasciato.  Nel caso di <xref:System.Threading.Mutex>, che presenta affinità di thread, viene generata un'eccezione se il thread chiamante non è proprietario del mutex.  Come indicato in precedenza, i semafori non presentano affinità di thread.  
  
#### Barriera  
 La classe <xref:System.Threading.Barrier> fornisce un modo per sincronizzare ciclicamente più thread in modo che tutti si blocchino allo stesso punto e attendano il completamento degli altri thread.  Una barriera è utile quando uno o più thread richiede i risultati di un altro thread prima di continuare con la fase successiva dell'algoritmo.  Per altre informazioni, vedere [Barrier](../../../docs/standard/threading/barrier.md).  
  
 [Torna all'inizio](#top)  
  
<a name="lightweight_synchronization_types"></a>   
## Tipi di sincronizzazione leggera  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], è possibile usare le primitive di sincronizzazione che forniscono prestazioni ottimali perché, quando è possibile, evitano la dipendenza da oggetti kernel Win32, come gli handle di attesa, dispendiosa in termini di tempo.  In generale, è opportuno usare questi tipi quando i tempi di attesa sono brevi e solo quando i tipi di sincronizzazione originali sono stati testati e sono risultati inefficaci.  I tipi leggeri non possono essere usati in scenari che richiedono la comunicazione tra processi.  
  
-   <xref:System.Threading.SemaphoreSlim?displayProperty=fullName> è una versione leggera di <xref:System.Threading.Semaphore?displayProperty=fullName>.  
  
-   <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> è una versione leggera di <xref:System.Threading.ManualResetEvent?displayProperty=fullName>.  
  
-   <xref:System.Threading.CountdownEvent?displayProperty=fullName> rappresenta l'evento che diventa segnalato quando il relativo conteggio è zero.  
  
-   <xref:System.Threading.Barrier?displayProperty=fullName> abilita la sincronizzazione reciproca di più thread senza richiedere il controllo da parte di un thread master.  Una barriera evita che i singoli thread proseguano le operazioni finché tutti i thread non hanno raggiunto un punto specificato.  
  
 [Torna all'inizio](#top)  
  
<a name="spinwait"></a>   
## SpinWait  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], è possibile usare la struttura <xref:System.Threading.SpinWait?displayProperty=fullName> quando un thread deve attendere che un evento venga segnalato o una condizione soddisfatta. Tuttavia, il tempo di attesa previsto deve essere inferiore a quello richiesto da un handle di attesa o da altre operazioni di blocco del thread corrente.  Usando <xref:System.Threading.SpinWait>, è possibile specificare un breve intervallo di tempo di rotazione durante l'attesa e quindi produrre un risultato \(ad esempio, mediante l'attesa o la sospensione\) solo se la condizione non viene soddisfatta nel tempo specificato.  
  
 [Torna all'inizio](#top)  
  
<a name="interlocked_operations"></a>   
## Operazioni interlocked  
 Le operazioni interlocked sono operazioni atomiche semplici eseguite in un percorso di memoria dai metodi statici della classe <xref:System.Threading.Interlocked>.  Queste operazioni atomiche includono operazioni di aggiunta, incremento e decremento, scambio, scambio condizionale in base a un confronto e lettura per i valori a 64 bit in piattaforme a 32 bit.  
  
> [!NOTE]
>  La garanzia di atomicità è limitata alle singole operazioni. Se è necessario eseguire più operazioni unitariamente, è necessario usare un meccanismo di sincronizzazione con granularità più grossolana.  
  
 Sebbene nessuna di queste operazioni corrisponda a blocchi o segnali, è possibile usarle per costruire blocchi e segnali.  Poiché sono native nel sistema operativo Windows, le operazioni interlocked sono estremamente veloci.  
  
 Le operazioni interlocked possono essere usate con le garanzie di memoria volatile per scrivere applicazioni con un'efficace concorrenza senza blocchi.  Tuttavia, richiedono programmazione sofisticata di basso livello, quindi per la maggior parte degli obiettivi la scelta migliore restano i blocchi semplici.  
  
 Per una panoramica concettuale, vedere [Interlocked Operations](../../../docs/standard/threading/interlocked-operations.md).  
  
## Vedere anche  
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)   
 [Monitor](../Topic/Monitors.md)   
 [Mutexes](../../../docs/standard/threading/mutexes.md)   
 [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)   
 [Interlocked Operations](../../../docs/standard/threading/interlocked-operations.md)   
 [Reader\-Writer Locks](../../../docs/standard/threading/reader-writer-locks.md)   
 [Barrier](../../../docs/standard/threading/barrier.md)   
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [SpinLock](../../../docs/standard/threading/spinlock.md)