---
title: Thread di sincronizzazione (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 04f485d1-8333-4510-9e72-c334e7427e7e
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ec8fa89c8921eadee428a90971d9ae4ce305a109
ms.lasthandoff: 03/13/2017

---
# <a name="thread-synchronization-visual-basic"></a>Sincronizzazione dei thread (Visual Basic)
Le sezioni seguenti descrivono le funzionalità e le classi che possono essere utilizzate per sincronizzare l'accesso alle risorse in applicazioni multithreading.  
  
 Uno dei vantaggi dell'utilizzo di più thread in un'applicazione consiste nel fatto che ogni thread esegue in modo asincrono. Per le applicazioni di Windows, in questo modo l'attività richiede molto tempo essere eseguita in background mentre la finestra dell'applicazione e controlli rimangano attiva. Per server applicazioni, multithreading offre la possibilità di gestire ogni richiesta in ingresso con un altro thread. In caso contrario, ogni nuova richiesta verrebbe soddisfatta fino a quando la richiesta precedente fosse stata siano soddisfatta.  
  
 Tuttavia, data la natura asincrona dei thread implica che l'accesso alle risorse, ad esempio memoria, handle di file e le connessioni di rete deve essere coordinata. In caso contrario, due o più thread potrebbero accedere alla stessa risorsa nello stesso momento, ogni riconosce le azioni di altro. Il risultato è il danneggiamento dei dati imprevisti.  
  
 Per operazioni semplici sui tipi di dati numerici integrali, la sincronizzazione dei thread può essere eseguita con i membri di <xref:System.Threading.Interlocked>classe.</xref:System.Threading.Interlocked> Per tutti gli altri dati tipi e le risorse non thread-safe, multithreading possono essere tranquillamente eseguite solo utilizzando i costrutti in questo argomento.  
  
 Per informazioni generali sulla programmazione multithreading, vedere:  
  
-   [Nozioni di base di Threading gestito](http://msdn.microsoft.com/library/b2944911-0e8f-427d-a8bb-077550618935)  
  
-   [Utilizzo di thread e Threading](http://msdn.microsoft.com/library/9b5ec2cd-121b-4d49-b075-222cf26f2344)  
  
-   [Procedure consigliate di Threading gestito](http://msdn.microsoft.com/library/e51988e7-7f4b-4646-a06d-1416cee8d557)  
  
## <a name="the-lock-and-synclock-keywords"></a>Il blocco e parole chiave SyncLock  
 Visual Basic `SyncLock` istruzione può essere utilizzata per garantire che un blocco di codice viene eseguito fino al completamento senza interruzioni da altri thread. Questa operazione viene eseguita ottenendo un blocco a esclusione reciproca per un determinato oggetto per la durata del blocco di codice.  
  
 Oggetto `SyncLock` istruzione viene assegnata un oggetto come argomento, seguita da un blocco di codice che deve essere eseguito da un solo thread alla volta. Ad esempio:  
  
```vb  
Public Class TestThreading  
    Dim lockThis As New Object  
  
    Public Sub Process()  
        SyncLock lockThis  
            ' Access thread-sensitive resources.  
        End SyncLock  
    End Sub  
End Class  
```  
  
 L'argomento fornito per il `SyncLock` (parola chiave) deve essere un oggetto basato su un tipo di riferimento e viene utilizzato per definire l'ambito del blocco. Nell'esempio precedente, l'ambito del blocco è limitato a questa funzione perché nessun riferimento all'oggetto `lockThis` esiste all'esterno della funzione. Se esiste un riferimento, ambito del blocco si estende anche a tale oggetto. In teoria, l'oggetto fornito viene utilizzato esclusivamente per identificare la risorsa condivisa tra più thread, pertanto può essere un'istanza di classe arbitraria. In pratica, tuttavia, questo oggetto rappresenta in genere la risorsa per il thread su cui sia necessaria la sincronizzazione. Ad esempio, se un oggetto contenitore deve essere utilizzato da più thread, quindi il contenitore può essere passato per bloccare e il blocco di codice sincronizzato segue il blocco acceda al contenitore. Come altri thread vengano bloccati sullo stesso contengono prima dell'accesso, in modo sicuro l'accesso all'oggetto è sincronizzato.  
  
 In genere, è consigliabile evitare il blocco di un `public` tipo, o istanze di oggetti sotto il controllo dell'applicazione. Ad esempio, `lockThis` può risultare problematico se l'istanza è possibile accedere pubblicamente, perché il codice fuori controllo potrebbe causare il blocco anche l'oggetto. Questo può creare situazioni di deadlock in cui due o più thread sono in attesa per la versione dello stesso oggetto. Il blocco di un tipo di dati pubblici, anziché su un oggetto, può causare problemi per lo stesso motivo. Il blocco di stringhe letterali è particolarmente rischioso poiché le stringhe letterali sono *inserite* da common language runtime (CLR). Questo significa che è presente un'istanza di una stringa letterale per l'intero programma, lo stesso oggetto rappresenta il valore letterale in tutti domini applicazione, in esecuzione su tutti i thread. Di conseguenza, un blocco collocato su una stringa con lo stesso contenuto in qualsiasi posizione il processo dell'applicazione blocca tutte le istanze di tale stringa nell'applicazione. Di conseguenza, si consiglia di bloccare un membro privato o protetto che non è inserito. Alcune classi sono disponibili membri specifici per il blocco. Il <xref:System.Array>tipo, ad esempio, fornisce <xref:System.Array.SyncRoot%2A>.</xref:System.Array.SyncRoot%2A> </xref:System.Array> Molti tipi di raccolta forniscono un `SyncRoot` nonché membro.  
  
 Per ulteriori informazioni sui `SyncLock` istruzione, vedere gli argomenti seguenti:  
  
-   [Istruzione SyncLock](../../../../visual-basic/language-reference/statements/synclock-statement.md)  
  
-   @System.Threading.Monitor  
  
## <a name="monitors"></a>Monitoraggi  
 Ad esempio il `SyncLock` (parola chiave), monitoraggi evitare blocchi di codice dall'esecuzione simultanea di più thread. Il <xref:System.Threading.Monitor.Enter%2A>metodo consente un solo thread procedere nelle istruzioni seguenti, tutti gli altri thread sono bloccati fino a quando l'esecuzione del thread chiama <xref:System.Threading.Monitor.Exit%2A>.</xref:System.Threading.Monitor.Exit%2A> </xref:System.Threading.Monitor.Enter%2A> Si tratta come quando si utilizza il `SyncLock` (parola chiave). Ad esempio:  
  
```vb  
SyncLock x  
    DoSomething()  
End SyncLock  
```  
  
 Ciò equivale a:  
  
```vb  
Dim obj As Object = CType(x, Object)  
System.Threading.Monitor.Enter(obj)  
Try  
    DoSomething()  
Finally  
    System.Threading.Monitor.Exit(obj)  
End Try  
```  
  
 Utilizzando il `SyncLock` (parola chiave) viene in genere preferibile all'utilizzo di <xref:System.Threading.Monitor>direttamente alla classe, sia perché `SyncLock` è più conciso e poiché `SyncLock` assicura il rilascio del monitor sottostante, anche se il codice protetto genera un'eccezione.</xref:System.Threading.Monitor> Questa operazione viene eseguita con il `Finally` (parola chiave), che esegue il blocco di codice associato indipendentemente dal fatto che viene generata un'eccezione.  
  
## <a name="synchronization-events-and-wait-handles"></a>Eventi di sincronizzazione e gli handle di attesa  
 Utilizzo di un blocco o il monitoraggio è utile per impedire l'esecuzione simultanea di blocchi di codice sensibili thread, ma questi costrutti non consentono un solo thread comunicare un evento a un altro. Questa operazione richiede *gli eventi di sincronizzazione*, che sono oggetti che presentano uno dei due stati, segnalato e non segnalato, che può essere utilizzato per attivare e sospendere i thread. Thread può essere sospesa dal stabilite per attendere un evento di sincronizzazione che viene segnalato e può essere attivato modificando lo stato dell'evento su segnalato. Se si tenta di un thread in attesa di un evento che è già segnalato, il thread continua l'esecuzione senza ritardo.  
  
 Esistono due tipi di eventi di sincronizzazione: <xref:System.Threading.AutoResetEvent>e <xref:System.Threading.ManualResetEvent>.</xref:System.Threading.ManualResetEvent> </xref:System.Threading.AutoResetEvent> L'unica differenza che <xref:System.Threading.AutoResetEvent>le modifiche da segnalato allo stato non segnalato automaticamente ogni volta che si attiva un thread.</xref:System.Threading.AutoResetEvent> Al contrario, un <xref:System.Threading.ManualResetEvent>consente qualsiasi numero di thread da attivare con lo stato segnalato e torna allo stato non segnalato solo stato quando il relativo <xref:System.Threading.EventWaitHandle.Reset%2A>viene chiamato.</xref:System.Threading.EventWaitHandle.Reset%2A> </xref:System.Threading.ManualResetEvent>  
  
 I thread possono essere resi per attendere gli eventi chiamando uno dei metodi di attesa, ad esempio <xref:System.Threading.WaitHandle.WaitOne%2A>, <xref:System.Threading.WaitHandle.WaitAny%2A>, o <xref:System.Threading.WaitHandle.WaitAll%2A>.</xref:System.Threading.WaitHandle.WaitAll%2A> </xref:System.Threading.WaitHandle.WaitAny%2A> </xref:System.Threading.WaitHandle.WaitOne%2A> <xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=fullName>fa sì che il thread in attesa finché non viene segnalato un singolo evento, <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName>Blocca un thread finché non viene segnalati uno o più eventi indicati, e <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName>Blocca il thread finché tutti gli eventi indicati non diventano segnalati.</xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName> </xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName></xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=fullName> L'evento diventa segnalato quando il relativo <xref:System.Threading.EventWaitHandle.Set%2A>viene chiamato.</xref:System.Threading.EventWaitHandle.Set%2A>  
  
 Nell'esempio seguente viene creato e avviato da un thread di `Main` (funzione). Il nuovo thread attende un evento utilizzando il <xref:System.Threading.WaitHandle.WaitOne%2A>(metodo).</xref:System.Threading.WaitHandle.WaitOne%2A> Il thread viene sospesa fino a quando l'evento viene segnalato dal thread principale è in esecuzione il `Main` (funzione). Una volta che viene segnalato l'evento, viene restituito il thread ausiliario. In questo caso, poiché l'evento viene utilizzato solo per l'attivazione di un thread, è il <xref:System.Threading.AutoResetEvent>o <xref:System.Threading.ManualResetEvent>classi potrebbero essere utilizzate.</xref:System.Threading.ManualResetEvent> </xref:System.Threading.AutoResetEvent>  
  
```vb  
Imports System.Threading  
  
Module Module1  
    Dim autoEvent As AutoResetEvent  
  
    Sub DoWork()  
        Console.WriteLine("   worker thread started, now waiting on event...")  
        autoEvent.WaitOne()  
        Console.WriteLine("   worker thread reactivated, now exiting...")  
    End Sub  
  
    Sub Main()  
        autoEvent = New AutoResetEvent(False)  
  
        Console.WriteLine("main thread starting worker thread...")  
        Dim t As New Thread(AddressOf DoWork)  
        t.Start()  
  
        Console.WriteLine("main thread sleeping for 1 second...")  
        Thread.Sleep(1000)  
  
        Console.WriteLine("main thread signaling worker thread...")  
        autoEvent.Set()  
    End Sub  
End Module  
```  
  
## <a name="mutex-object"></a>Oggetto mutex  
 Oggetto *mutex* è simile a un monitoraggio, impedisce l'esecuzione simultanea di un blocco di codice da più thread contemporaneamente. Infatti, il nome "mutex" è una versione abbreviata del termine "si escludono a vicenda." A differenza dei monitoraggi, tuttavia, un mutex consente di sincronizzare i thread tra processi. Un mutex è rappresentato dalla <xref:System.Threading.Mutex>classe.</xref:System.Threading.Mutex>  
  
 Quando utilizzato per la sincronizzazione tra processo, il mutex viene definito un *mutex denominato* perché deve essere utilizzato in un'altra applicazione e pertanto non può essere condiviso mediante una variabile globale o statica. Deve essere provvisto di un nome in modo che entrambe le applicazioni possono accedere lo stesso oggetto mutex.  
  
 Sebbene un mutex può essere utilizzato per la sincronizzazione dei thread all'interno del processo, utilizzando <xref:System.Threading.Monitor>è in genere preferibile, perché i monitoraggi sono stati progettati specificamente per .NET Framework e pertanto un migliore utilizzo delle risorse.</xref:System.Threading.Monitor> Al contrario, la <xref:System.Threading.Mutex>classe è un wrapper per un costrutto Win32.</xref:System.Threading.Mutex> Sebbene sia più potente di un monitor, un mutex richiede transizioni di interoperabilità che sono più dispendiosa rispetto a quelle richieste dalla <xref:System.Threading.Monitor>classe.</xref:System.Threading.Monitor> Per un esempio di utilizzo di un mutex, vedere [mutex](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2).  
  
## <a name="interlocked-class"></a>Interlocked (classe)  
 È possibile utilizzare i metodi della <xref:System.Threading.Interlocked>classe per evitare i problemi che possono verificarsi quando più thread tentano contemporaneamente di aggiornare o confrontare lo stesso valore.</xref:System.Threading.Interlocked> I metodi di questa classe consentono in modo sicuro di incremento, decrementano, scambino e confrontano i valori da qualsiasi thread.  
  
## <a name="readerwriter-locks"></a>Blocchi ReaderWriter  
 In alcuni casi, si desidera bloccare una risorsa solo durante la scrittura di dati e consentire a leggere contemporaneamente i dati quando i dati non vengono aggiornati più client. La <xref:System.Threading.ReaderWriterLock>classe impone l'accesso esclusivo a una risorsa mentre un thread sta modificando la risorsa, ma consente l'accesso non esclusivo durante la lettura della risorsa.</xref:System.Threading.ReaderWriterLock> Blocchi ReaderWriter rappresentano un'alternativa utile per i blocchi esclusivi, che altri thread in attesa, anche quando i thread non è necessitano aggiornare i dati.  
  
## <a name="deadlocks"></a>Deadlock  
 La sincronizzazione dei thread si rivela particolarmente utile nelle applicazioni multithreading, ma è sempre presente il pericolo di creazione di un `deadlock`, in cui più thread in attesa di loro e l'applicazione si blocca. È analogo a una situazione in cui automobili sono stati interrotti in un'interruzione di quattro direzioni e ogni persona è in attesa per l'altra passare un deadlock. Evitare i deadlock è importante. la chiave è un'attenta pianificazione. È spesso possibile prevedere situazioni di deadlock creando diagrammi prima di iniziare la codifica di applicazioni multithread.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Thread></xref:System.Threading.Thread>   
 <xref:System.Threading.WaitHandle.WaitOne%2A></xref:System.Threading.WaitHandle.WaitOne%2A>   
 <xref:System.Threading.WaitHandle.WaitAny%2A></xref:System.Threading.WaitHandle.WaitAny%2A>   
 <xref:System.Threading.WaitHandle.WaitAll%2A></xref:System.Threading.WaitHandle.WaitAll%2A>   
 <xref:System.Threading.Thread.Join%2A></xref:System.Threading.Thread.Join%2A>   
 <xref:System.Threading.Thread.Start%2A></xref:System.Threading.Thread.Start%2A>   
 <xref:System.Threading.Thread.Sleep%2A></xref:System.Threading.Thread.Sleep%2A>   
 <xref:System.Threading.Monitor></xref:System.Threading.Monitor>   
 <xref:System.Threading.Mutex></xref:System.Threading.Mutex>   
 <xref:System.Threading.AutoResetEvent></xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent></xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.Interlocked></xref:System.Threading.Interlocked>   
 <xref:System.Threading.WaitHandle></xref:System.Threading.WaitHandle>   
 <xref:System.Threading.EventWaitHandle></xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading></xref:System.Threading>   
 <xref:System.Threading.EventWaitHandle.Set%2A></xref:System.Threading.EventWaitHandle.Set%2A>   
 [Applicazioni multithreading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [Istruzione SyncLock](../../../../visual-basic/language-reference/statements/synclock-statement.md)   
 [Mutex](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2)   
 @System.Threading.Monitor   
 [Operazioni interlocked](http://msdn.microsoft.com/library/cbda7114-c752-4f3e-ada1-b1e8dd262f2b)   
 [AutoResetEvent](http://msdn.microsoft.com/library/6d39c48d-6b37-4a9b-8631-f2924cfd9c18)   
 [Sincronizzazione dei dati per il Multithreading](http://msdn.microsoft.com/library/b980eb4c-71d5-4860-864a-6dfe3692430a)
