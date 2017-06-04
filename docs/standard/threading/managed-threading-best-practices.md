---
title: "Managed Threading Best Practices | Microsoft Docs"
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
  - "threading [.NET Framework], design guidelines"
  - "threading [.NET Framework], best practices"
  - "managed threading"
ms.assetid: e51988e7-7f4b-4646-a06d-1416cee8d557
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Managed Threading Best Practices
Il multithreading richiede un'attenta programmazione.  È possibile ridurre la complessità della maggior parte delle attività accodando le richieste di esecuzione tramite thread di pool di thread.  In questo argomento vengono analizzate situazioni più complesse, quali la coordinazione del lavoro di più thread o la gestione di thread che effettuano un blocco.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] la libreria TPL \(Task Parallel Library\) e PLINQ forniscono API che riducono, in parte, la complessità e i rischi associati alla programmazione a thread multipli.  Per ulteriori informazioni, vedere [Parallel Programming](../../../docs/standard/parallel-programming/index.md).  
  
## Deadlock e race condition  
 Il multithreading consente di risolvere problemi di trasmissione dei dati e di velocità di risposta, ma è anche causa di nuovi problemi: i deadlock e le race condition.  
  
### Deadlock  
 Un deadlock si verifica quando uno di due thread tenta di bloccare una risorsa già bloccata dall'altro.  Nessuno dei due è in grado di fare ulteriori progressi.  
  
 È possibile rilevare i deadlock tramite i timeout disponibili in molti metodi delle classi di threading gestito.  Il codice riportato di seguito, ad esempio, tenta di acquisire un blocco sull'istanza corrente.  Se non si ottiene il blocco entro 300 millisecondi, <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=fullName> restituisce **false**.  
  
```vb  
If Monitor.TryEnter(lockObject, 300) Then  
    Try  
        ' Place code protected by the Monitor here.  
    Finally  
        Monitor.Exit(Me)  
    End Try  
Else  
    ' Code to execute if the attempt times out.  
End If  
```  
  
```csharp  
if (Monitor.TryEnter(lockObject, 300)) {  
    try {  
        // Place code protected by the Monitor here.  
    }  
    finally {  
        Monitor.Exit(this);  
    }  
}  
else {  
    // Code to execute if the attempt times out.  
}  
```  
  
### Race condition  
 Una race condition è un bug che si verifica quando il risultato di un programma dipende dal thread che per primo raggiunge una determinata porzione di codice.  L'esecuzione del programma produce ogni volta risultati diversi che non è possibile prevedere in anticipo.  
  
 Un semplice esempio di race condition è l'incrementazione di un campo.  Si supponga che una classe disponga di un campo **statico** privato \(**Shared** in Visual Basic\) che viene incrementato ogni volta che viene creata un'istanza della classe tramite codice quale `objCt++;` \(C\#\) o `objCt += 1` \(Visual Basic\).  Per eseguire questa operazione, è necessario caricare il valore da `objCt` in un registro, incrementare il valore e archiviarlo in `objCt`.  
  
 In un'applicazione multithread, un thread che abbia caricato e incrementato il valore potrebbe venire interrotto da un altro thread che esegue tutti e tre i passaggi. Quando il primo thread riprende l'esecuzione e archivia il valore, sovrascrive `objCt` anche se nel frattempo il valore è stato modificato.  
  
 È possibile evitare facilmente questa particolare race condition tramite i metodi della classe <xref:System.Threading.Interlocked> come <xref:System.Threading.Interlocked.Increment%2A?displayProperty=fullName>.  Per informazioni sulle altre tecniche di sincronizzazione dei dati tra più thread, vedere [Sincronizzazione dei dati per il multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md).  
  
 Le race condition possono verificarsi anche quando si sincronizzano le attività di più thread.  Quando si scrive una riga di codice, è necessario considerare le possibili conseguenze nel caso in cui un thread venisse interrotto prima dell'esecuzione della riga o di una qualsiasi delle singole istruzioni del computer che costituiscono la riga e un altro thread lo raggiungesse.  
  
## Numero di processori  
 La maggior parte dei computer dispone di più processori \(detti anche core\), anche i piccoli dispositivi come tablet e telefoni.  Se si sta sviluppando un software che funzionerà anche nei computer a singolo processore, è opportuno notare che il multithreading consente di risolvere diversi problemi per i computer a singolo processore e computer a più processori.  
  
### Computer a più processori  
 Il multithreading consente di migliorare la trasmissione dei dati.  Dieci processori possono decuplicare il lavoro di uno, ma solo a condizione che il lavoro sia suddiviso in modo tale che tutti e dieci possano funzionare contemporaneamente. I thread consentono di suddividere facilmente il lavoro e di sfruttare l'ulteriore capacità di elaborazione.  Se si utilizza il multithreading su un computer a più processori:  
  
-   Il numero di thread che è possibile eseguire contemporaneamente dipende dal numero dei processori.  
  
-   Un thread in background viene eseguito solo quando il numero di thread in primo piano in esecuzione è inferiore al numero dei processori.  
  
-   Quando si chiama il metodo <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> su un thread, l'avvio immediato dell'esecuzione dipende dal numero di processori e di thread attualmente in attesa di esecuzione.  
  
-   Le race condition possono verificarsi non solo perché i thread vengono interrotti inaspettatamente, ma anche perché è possibile che due thread in esecuzione su processori diversi competano per raggiungere lo stesso blocco di codice.  
  
### Computer a processore unico  
 Il multithreading consente di rendere più rapida la risposta all'utente del computer e di utilizzare il tempo di inattività per attività in background.  Se si utilizza il multithreading su un computer a processore singolo:  
  
-   Viene sempre eseguito un solo thread per volta.  
  
-   Viene eseguito un thread in background solo quando il thread utente principale è inattivo.  Un thread in primo piano costantemente in esecuzione priva i thread in background del tempo del processore.  
  
-   Quando si chiama il metodo <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> su un thread, quest'ultimo non viene eseguito finché il thread corrente non viene generato o interrotto dal sistema operativo.  
  
-   Le race condition si verificano in genere perché il programmatore non ha previsto che un thread potesse venire interrotto in un momento inopportuno, consentendo talvolta a un altro thread di raggiungere per primo un blocco di codice.  
  
## Membri e costruttori statici  
 Una classe non viene inizializzata finché non termina l'esecuzione del relativo costruttore \(`static` in C\# e `Shared Sub New` in Visual Basic\).  Per impedire l'esecuzione di codice su un tipo non inizializzato, Common Language Runtime blocca tutte le chiamate degli altri thread ai membri `static` della classe \(ai membri `Shared` in Visual Basic\) fino al termine dell'esecuzione del costruttore.  
  
 Ad esempio, se il costruttore di una classe avvia un nuovo thread e la routine del thread chiama un membro `static` della classe, il nuovo thread si bloccherà fino al completamento dell'esecuzione del costruttore.  
  
 Ciò è valido per qualsiasi tipo che può avere un costruttore `static`.  
  
## Suggerimenti generali  
 Quando si utilizzano più thread, attenersi alle seguenti linee guida:  
  
-   Non utilizzare <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> per terminare altri thread.  Chiamare **Abort** su un altro thread equivale a generare un'eccezione su tale thread, senza conoscere il punto raggiunto dal thread nell'elaborazione.  
  
-   Non utilizzare <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> e <xref:System.Threading.Thread.Resume%2A?displayProperty=fullName> per sincronizzare le attività di più thread.  Utilizzare <xref:System.Threading.Mutex>, <xref:System.Threading.ManualResetEvent>, <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.Monitor>.  
  
-   Non controllare l'esecuzione dei thread in funzione dal programma principale, ad esempio tramite gli eventi.  Progettare invece il programma in modo che i thread in funzione siano responsabili dell'attesa finché il lavoro non è disponibile, dell'esecuzione e della notifica, agli altri componenti del programma, del termine dell'esecuzione.  Se i thread di lavoro non consentono il blocco, prendere in considerazione l'utilizzo di thread del pool di thread.  Il metodo <xref:System.Threading.Monitor.PulseAll%2A?displayProperty=fullName> è utile nelle situazioni in cui i thread di lavoro consentono il blocco.  
  
-   Non utilizzare tipi come oggetti di blocco.  In altri termini, evitare codice quale `lock(typeof(X))` in C\# o `SyncLock(GetType(X))` in Visual Basic oppure l'utilizzo di <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> con oggetti <xref:System.Type>.  Per un determinato tipo, esiste solo un'istanza di <xref:System.Type?displayProperty=fullName> per ogni dominio applicazione.  Se il tipo per cui si acquisisce un blocco è pubblico, anche codice diverso dal proprio può acquisire blocchi su di esso, con il conseguente verificarsi di deadlock.  Per informazioni su ulteriori problematiche, vedere [Reliability Best Practices](../../../docs/framework/performance/reliability-best-practices.md).  
  
-   Procedere con cautela in caso di blocco sulle istanze, ad esempio `lock(this)` in C\# o `SyncLock(Me)` in Visual Basic.  Se altro codice dell'applicazione, esterno al tipo, acquisisce un blocco sull'oggetto, potrebbero verificarsi situazioni di deadlock.  
  
-   Assicurarsi che un thread entrato in un monitor lasci sempre il monitor, anche se si verifica un'eccezione mentre il thread si trova nel monitor.  L'istruzione [lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md) di C\# e l'istruzione [SyncLock](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md) di Visual Basic generano automaticamente questo comportamento, impiegando un blocco **finally** per garantire che venga chiamato <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName>.  Se non è possibile garantire che **Exit** verrà chiamato, modificare la progettazione in modo da utilizzare **Mutex**.  Un mutex viene rilasciato automaticamente quando il thread che ne è attualmente proprietario termina.  
  
-   Utilizzare più thread per le attività che richiedono risorse diverse ed evitare di assegnare più thread a una sola risorsa.  Alcune attività, ad esempio, che dispongono di un proprio thread, usufruiscono dei vantaggi di I\/O, poiché il thread si bloccherà durante le operazioni di I\/O consentendo l'esecuzione di altri thread.  Anche l'input utente è una risorsa che trae vantaggio da un thread dedicato.  In un computer a processore unico, un'attività che consiste in un calcolo a elevato utilizzo di risorse coesiste con l'input utente e con attività che coinvolgono I\/O, ma più attività con un elevato utilizzo di risorse competono fra loro.  
  
-   Si prenda in considerazione l'utilizzo dei metodi della classe <xref:System.Threading.Interlocked> per le modifiche semplici allo stato, anziché l'utilizzo dell'istruzione `lock` \(`SyncLock` in Visual Basic\).  L'istruzione `lock` è un valido strumento generico, ma la classe <xref:System.Threading.Interlocked> fornisce prestazioni migliori per gli aggiornamenti che devono essere atomici.  Internamente esegue un unico prefisso lock se non esistono conflitti.  Nelle analisi di codice controllare il codice simile a quello indicato negli esempi riportati di seguito.  Nel primo esempio viene incrementata una variabile di stato:  
  
    ```vb  
    SyncLock lockObject  
        myField += 1  
    End SyncLock  
    ```  
  
    ```csharp  
    lock(lockObject)   
    {  
        myField++;  
    }  
    ```  
  
     Per migliorare le prestazioni, è possibile utilizzare il metodo <xref:System.Threading.Interlocked.Increment%2A>, anziché l'istruzione `lock`, come illustrato di seguito.  
  
    ```vb  
    System.Threading.Interlocked.Increment(myField)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.Increment(myField);  
    ```  
  
    > [!NOTE]
    >  In .NET Framework versione 2.0 il metodo <xref:System.Threading.Interlocked.Add%2A> fornisce aggiornamenti atomici in incrementi maggiori di 1.  
  
     Nel secondo esempio una variabile del tipo di riferimento viene aggiornata solo se corrisponde a un riferimento null \(`Nothing` in Visual Basic\).  
  
    ```vb  
    If x Is Nothing Then  
        SyncLock lockObject  
            If x Is Nothing Then  
                x = y  
            End If  
        End SyncLock  
    End If  
    ```  
  
    ```csharp  
    if (x == null)  
    {  
        lock (lockObject)  
        {  
            if (x == null)  
            {  
                x = y;  
            }  
        }  
    }  
    ```  
  
     Per migliorare le prestazioni, è possibile utilizzare il metodo <xref:System.Threading.Interlocked.CompareExchange%2A>, come illustrato di seguito.  
  
    ```vb  
    System.Threading.Interlocked.CompareExchange(x, y, Nothing)  
    ```  
  
    ```csharp  
    System.Threading.Interlocked.CompareExchange(ref x, y, null);  
    ```  
  
    > [!NOTE]
    >  In .NET Framework versione 2.0 il metodo <xref:System.Threading.Interlocked.CompareExchange%2A> presenta un overload generico che può essere utilizzato per la sostituzione indipendente dai tipi di qualsiasi tipo di riferimento.  
  
## Suggerimenti per librerie di classi  
 Si prendano in considerazione le linee guida riportate di seguito per la progettazione di librerie di classi per il multithreading.  
  
-   Se possibile, evitare che sia necessario eseguire la sincronizzazione,  soprattutto nel caso di codice di uso più frequente.  È ad esempio possibile modificare un algoritmo per tollerare una race condition piuttosto che per eliminarla.  L'esecuzione di operazioni di sincronizzazione non necessarie riduce le prestazioni e crea la possibilità di deadlock e race condition.  
  
-   Rendere i dati statici \(`Shared` in Visual Basic\) thread\-safe per impostazione predefinita.  
  
-   Non rendere i dati di istanza thread\-safe per impostazione predefinita.  Se si aggiungono blocchi per creare codice thread\-safe, le prestazioni vengono ridotte, aumentano i conflitti di blocco ed è possibile che si verifichino deadlock.  Nei modelli applicativi comuni, solo un thread per volta esegue il codice utente riducendo la necessità di indipendenza dai thread.  Per questo motivo, le librerie di classi di .NET Framework non sono thread\-safe per impostazione predefinita.  
  
-   Evitare di fornire metodi static che modificano lo stato static.  Negli scenari server comuni, lo stato static viene condiviso tra le richieste e, pertanto, più thread possono eseguire contemporaneamente tale codice.  In questo modo è possibile che si verifichino bug dei thread.  Provare a utilizzare un modello di progettazione che incapsula i dati nelle istanze che non sono condivise tra le richieste.  Inoltre, se si sincronizzano i dati statici, le chiamate tra i metodi statici che modificano lo stato possono determinare deadlock o sincronizzazione ridondante e influire negativamente sulle prestazioni.  
  
## Vedere anche  
 [Threading](../../../docs/standard/threading/index.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)