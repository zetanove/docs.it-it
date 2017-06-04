---
title: "Understanding Speedup in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, performance tuning"
ms.assetid: 53706c7e-397d-467a-98cd-c0d1fd63ba5e
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Understanding Speedup in PLINQ
Lo scopo principale di PLINQ è incrementare la velocità con cui vengono eseguite le query LINQ to Objects mediante l'esecuzione parallela di delegati di query in computer con processori multicore.  Le prestazioni di PLINQ migliorano quando ogni elemento di una raccolta di origine viene eseguito indipendentemente e quando i singoli delegati non condividono alcuno stato.  Tali operazioni sono comuni in LINQ to Objects e PLINQ e spesso sono chiamate "*deliziosamente parallele*" perché si prestano facilmente alla pianificazione su più thread.  Non tutte le query tuttavia sono interamente costituite da operazioni deliziosamente parallele. Nella maggior parte dei casi una query comporta l'uso di alcuni operatori che non possono essere eseguiti in parallelo o che rallentano l'esecuzione parallela.  Anche quando le query sono interamente deliziosamente parallele, PLINQ deve comunque suddividere l'origine dati e pianificare il lavoro sui thread e generalmente unisce i risultati quando la query viene completata.  Tutte queste operazioni si aggiungono al costo computazionale della parallelizzazione. I costi derivanti dall'aggiunta di parallelizzazione vengono chiamati *sovraccarico*.  Per ottenere prestazioni ottimali in una query PLINQ, è necessario aumentare al massimo le parti deliziosamente parallele e ridurre al minimo le parti che richiedono sovraccarico.  In questo articolo vengono fornite informazioni che consentiranno di scrivere query PLINQ più efficaci possibile che producano comunque risultati corretti.  
  
## Fattori che hanno un impatto sulle prestazioni delle query PLINQ  
 Nelle sezioni seguenti sono elencati alcuni dei più importanti fattori che hanno un impatto sulle prestazioni delle query parallele.  Si tratta di istruzioni generali che da sole non sono sufficienti per prevedere le prestazioni delle query in tutti i casi.  Come sempre, è importante misurare le prestazioni effettive di query specifiche sui computer con un intervallo di configurazioni e carichi rappresentativi.  
  
1.  Costo computazionale del lavoro complessivo.  
  
     Per realizzare un aumento di velocità, è necessario che in una query PLINQ venga eseguito lavoro deliziosamente parallelo sufficiente a compensare il sovraccarico.  Il lavoro può essere espresso come costo computazionale di ogni delegato moltiplicato per il numero di elementi della raccolta di origine.  Presupponendo che un'operazione può essere parallelizzata, a un costo computazionale maggiore corrispondono maggiori probabilità di aumento della velocità.  Se ad esempio per l'esecuzione di una funzione è necessario un millisecondo, per l'esecuzione di una query sequenziale su più di 1000 elementi sarà necessario un secondo, mentre per una query parallela su un computer con processori a quattro core potrebbero essere necessari solo 250 millisecondi.  Ciò produce un aumento di velocità di 750 millisecondi.  Se per l'esecuzione di ogni elemento della funzione fosse necessario un secondo, l'aumento di velocità sarebbe 750 secondi.  Se il delegato è molto costoso, PLINQ potrebbe garantire un aumento di velocità significativo con solo alcuni elementi nella raccolta di origine.  Viceversa, raccolte di origine di dimensioni ridotte con semplici delegati non sono generalmente candidati validi per PLINQ.  
  
     Nell'esempio seguente, queryA è probabilmente un candidato valido per PLINQ, presupponendo che questa funzione select comporti molto lavoro. queryB probabilmente non è un candidato valido in quanto non c'è abbastanza lavoro nell'istruzione SELECT e il sovraccarico della parallelizzazione inciderà nella maggior parte o in tutto l'aumento di velocità.  
  
    ```vb  
    Dim queryA = From num In numberList.AsParallel()  
                 Select ExpensiveFunction(num); 'good for PLINQ  
  
    Dim queryB = From num In numberList.AsParallel()  
                 Where num Mod 2 > 0  
                 Select num; 'not as good for PLINQ  
    ```  
  
    ```csharp  
    var queryA = from num in numberList.AsParallel()  
                 select ExpensiveFunction(num); //good for PLINQ  
  
    var queryB = from num in numberList.AsParallel()  
                 where num % 2 > 0  
                 select num; //not as good for PLINQ  
  
    ```  
  
2.  Numero di core logici sul sistema \(grado di parallelismo\).  
  
     Questo punto è un ovvio corollario della sezione precedente, ovvero le query deliziosamente parallele vengono eseguite più rapidamente sulle macchine con processori a più core, in quanto il lavoro può essere suddiviso tra più thread simultanei.  La quantità complessiva di aumento di velocità dipende dalla percentuale di lavoro complessivo della query che è possibile parallelizzare.  Non è detto, tuttavia, che utilizzando un computer con processore a otto core anziché un processore a quattro core, venga raddoppiata la velocità di esecuzione di tutte le query.  Quando si impostano le query per ottenere prestazioni ottimali, è importante misurare i risultati effettivi sui computer con processori con i vari numeri di core.  Questo punto è correlato al punto n. 1: per sfruttare al meglio le risorse di elaborazione, è necessario utilizzare dataset di dimensioni maggiori.  
  
3.  Numero e tipo di operazioni.  
  
     In PLINQ è disponibile l'operatore AsOrdered per situazioni in cui è necessario mantenere l'ordine degli elementi nella sequenza di origine.  All'ordinamento è associato un costo, che tuttavia è generalmente modesto.  GroupBy e le operazioni di unione comportano entrambi sovraccarico.  Le prestazioni di PLINQ sono più elevate se è consentito elaborare elementi nella raccolta di origine in qualsiasi ordine e passarli all'operatore successivo appena sono pronti.  Per ulteriori informazioni, vedere [Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md).  
  
4.  Formato dell'esecuzione della query.  
  
     Se si archiviano i risultati di una query mediante la chiamata a ToArray o a ToList, è necessario unire i risultati di tutti i thread paralleli nell'unica struttura di dati.  Ciò comporta un costo computazionale inevitabile.  Analogamente, se si iterano i risultati tramite un ciclo foreach \(For Each in Visual Basic\), i risultati dei thread di lavoro devono essere serializzati sul thread dell'enumeratore.  Se tuttavia si desidera semplicemente eseguire un'azione basata sul risultato di ogni thread, è possibile utilizzare il metodo ForAll per eseguire questo lavoro su più thread.  
  
5.  Tipo di opzioni di unione.  
  
     È possibile configurare PLINQ in modo che l'output venga memorizzato nel buffer prodotto in blocchi o tutto insieme dopo che è stato prodotto l'intero set di risultati. In alternativa, è possibile trasmettere risultati singoli man mano che vengono prodotti.  La prima opzione comporta una riduzione del tempo complessivo di esecuzione, mentre la seconda comporta minore latenza tra gli elementi prodotti.  Anche se non sempre le opzioni di unione hanno un impatto significativo sulle prestazioni generali di esecuzione delle query, possono avere un impatto sulle prestazioni percepite, in quanto controllano il tempo di attesa dei risultati da parte di un utente.  Per ulteriori informazioni, vedere [Merge Options in PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md).  
  
6.  Tipo di partizionamento.  
  
     Una query PLINQ su una raccolta di origine indicizzabile può comportare in alcuni casi un carico di lavoro non equilibrato.  Quando si verifica questa situazione, è possibile aumentare le prestazioni di esecuzione delle query creando un partitioner personalizzato.  Per ulteriori informazioni, vedere [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md).  
  
## Casi in cui PLINQ sceglie la modalità sequenziale  
 PLINQ tenterà sempre di eseguire una query a una velocità almeno pari a quella con cui verrebbe eseguita in sequenza.  Anche se PLINQ non tiene conto del costo computazionale dei delegati dell'utente o del volume dell'origine di input, cerca determinate "forme" di query. Nello specifico, cerca operatori di query o combinazioni di operatori che in genere comportano un'esecuzione più lenta di una query in modalità parallela.  Quando individua tali forme, per impostazione predefinita PLINQ esegue il fallback alla modalità sequenziale.  
  
 Dopo avere misurato le prestazioni di esecuzione di una query specifica, è tuttavia possibile stabilire che effettivamente l'esecuzione è più veloce in modalità parallela.  In questi casi, è possibile utilizzare il flag <xref:System.Linq.ParallelExecutionMode?displayProperty=fullName> mediante il metodo <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> per indicare a PLINQ di eseguire la query in parallelo.  Per ulteriori informazioni, vedere [How to: Specify the Execution Mode in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md).  
  
 Nell'elenco seguente sono illustrate le forme di query eseguite per impostazione predefinita da PLINQ in modalità sequenziale:  
  
-   Query che contengono una clausola Select, Where indicizzata, SelectMany indicizzata o ElementAt dopo un'operazione di ordinamento o filtro che ha rimosso gli indici originali o ne ha modificato la disposizione.  
  
-   Query che contengono un operatore Take, TakeWhile, Skip, SkipWhile e in cui gli indici nella sequenza di origine sono nell'ordine originale.  
  
-   Query che contengono Zip o SequenceEquals, a meno che in una delle origini dati non sia presente un indice originariamente ordinato e l'altra origine dati non sia indicizzabile \(ad esempio un array o IList\(T\)\).  
  
-   Query che contengono Concat, a meno che non sia applicato a origini dati indicizzabili.  
  
-   Query che contengono Reverse, a meno che non sia applicato a un'origine dati indicizzabile.  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)