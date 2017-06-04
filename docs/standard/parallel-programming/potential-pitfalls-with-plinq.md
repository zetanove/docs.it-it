---
title: "Potential Pitfalls with PLINQ | Microsoft Docs"
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
  - "PLINQ queries, pitfalls"
ms.assetid: 75a38b55-4bc4-488a-87d5-89dbdbdc76a2
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Potential Pitfalls with PLINQ
In molti casi, PLINQ può fornire miglioramenti significativi delle prestazioni per le query LINQ to Objects sequenziali.  Tuttavia, le operazioni necessarie per parallelizzare l'esecuzione della query introducono complessità in grado di comportare problemi che in un codice sequenziale sono meno frequenti o persino assenti.  In questo argomento sono elencati alcuni suggerimenti da tenere presente quando si scrivono query PLINQ.  
  
## Non presupporre che l'approccio in parallelo sia sempre più veloce  
 Talvolta la parallelizzazione fa in modo che una query PLINQ presenti un'esecuzione più lenta rispetto alla query LINQ to Objects equivalente.  La regola generale di base è che per le query con pochi elementi di origine e con delegati dell'utente veloci raramente si verifica un aumento significativo della velocità di esecuzione.  Tuttavia, poiché molti fattori influiscono sulle prestazioni, è consigliabile misurare i risultati effettivi prima di decidere se utilizzare PLINQ.  Per ulteriori informazioni, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Evitare di scrivere in percorsi di memoria condivisi  
 Nel codice sequenziale spesso si eseguono operazioni di lettura e scrittura su variabili o campi di classe statici.  Tuttavia, ogni volta che più thread eseguono un accesso simultaneo a queste variabili, è molto probabile che si verifichino race condition.  Anche se è possibile sincronizzare l'accesso alla variabile mediante l'utilizzo di blocchi, il costo di questa sincronizzazione può influire negativamente sulle prestazioni.  È pertanto consigliabile evitare \(o almeno limitare\) il più possibile l'accesso allo stato condiviso in una query PLINQ.  
  
## Evitare parallelizzazioni eccessive  
 L'utilizzo dell'operatore `AsParallel` comporta l'overhead di eseguire il partizionamento della raccolta di origine e di sincronizzare i thread di lavoro.  I vantaggi della parallelizzazione vengono limitati ulteriormente dal numero di processori nel computer.  Non si ottiene alcun aumento di velocità eseguendo più thread con vincoli di calcolo in un unico processore.  Pertanto, è fondamentale evitare la parallelizzazione eccessiva delle query.  
  
 Nella maggior parte dei casi la parallelizzazione eccessiva può verificarsi quando si utilizzano query annidate, come mostrato nel frammento seguente.  
  
 [!code-csharp[PLINQ#20](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#20)]
 [!code-vb[PLINQ#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#20)]  
  
 In questo caso è meglio parallelizzare solo l'origine dati esterna \(customers\) a meno che non sussista almeno una delle condizioni seguenti:  
  
-   È noto che l'origine dati interna \(cust.Orders\) è molto lunga.  
  
-   Si eseguono calcoli dispendiosi in ogni ordine. L'operazione mostrata nell'esempio non è dispendiosa.  
  
-   È noto che il sistema di destinazione presenta un numero di processori sufficiente per gestire il numero di thread che verranno prodotti dalla parallelizzazione della query su `cust.Orders`.  
  
 In ogni caso, il miglior modo per determinare la forma ottimale della query è tramite lo svolgimento di test e misure.  Per ulteriori informazioni, vedere [How to: Measure PLINQ Query Performance](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md).  
  
## Evitare chiamate a metodi non thread\-safe  
 La scrittura in metodi di istanza non thread\-safe da una query PLINQ può comportare un danneggiamento dei dati che può passare inosservato nel programma.  Può inoltre comportare la generazione di eccezioni.  L'esempio seguente mostra uno scenario in cui più thread tentano di chiamare simultaneamente il metodo `Filestream.Write`. Tuttavia, la classe non supporta le chiamate simultanee.  
  
```vb  
Dim fs As FileStream = File.OpenWrite(…)  
a.Where(...).OrderBy(...).Select(...).ForAll(Sub(x) fs.Write(x))  
```  
  
```csharp  
FileStream fs = File.OpenWrite(...);  
a.Where(...).OrderBy(...).Select(...).ForAll(x => fs.Write(x));  
```  
  
## Limitare le chiamate ai metodi thread\-safe  
 La maggior parte dei metodi statici in .NET Framework è thread\-safe e può essere chiamata simultaneamente da più thread.  Tuttavia, anche in questi casi, la sincronizzazione da applicare può comportare un rallentamento significativo della query.  
  
> [!NOTE]
>  Per verificare ciò basta inserire nelle query alcune chiamate a <xref:System.Console.WriteLine%2A>.  Benché questo metodo venga utilizzato a scopo dimostrativo negli esempi della documentazione, evitare di utilizzarlo nelle query PLINQ.  
  
## Evitare operazioni di ordinamento superflue  
 Quando esegue una query in parallelo, PLINQ divide la sequenza di origine in partizioni su cui è possibile intervenire simultaneamente in più thread.  Per impostazione predefinita, l'ordine di elaborazione delle partizioni nonché l'ordine di recapito dei risultati non è prevedibile, tranne nel caso degli operatori come `OrderBy`.  Benché sia possibile indicare a PLINQ di conservare l'ordine di tutte le sequenze di origine, ciò comporta un impatto negativo sulle prestazioni.  La procedura consigliata, laddove possibile, è strutturare le query in modo che non si basino sulla conservazione dell'ordine.  Per ulteriori informazioni, vedere [Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md).  
  
## Preferire ForAll a ForEach quando è possibile  
 Benché PLINQ esegua una query su più thread, se si utilizzano i risultati in un ciclo `foreach` \(`For Each` in Visual Basic\), i risultati della query devono essere uniti in un unico thread. Inoltre, l'enumeratore deve accedere in serie a tali risultati.  In alcuni casi questo è inevitabile. Tuttavia, laddove possibile, utilizzare il metodo `ForAll` per consentire a ogni thread di restituire i propri risultati, ad esempio scrivendo in una raccolta thread\-safe quale <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName>.  
  
 Lo stesso problema si verifica a <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> Ovvero `source.AsParallel().Where().ForAll(...)` deve essere fortemente preferito a  
  
 `Parallel.ForEach(source.AsParallel().Where(), ...)`.  
  
## Tenere presente i problemi di affinità di thread  
 Alcune tecnologie, ad esempio l'interoperabilità COM per i componenti apartment a thread singolo \(STA, Single\-Threaded Apartment\), Windows Form e Windows Presentation Foundation \(WPF\), impongono restrizioni di affinità di thread che richiedono l'esecuzione del codice in un thread specifico.  Ad esempio, sia in Windows Form sia in WPF, l'accesso a un controllo può essere eseguito solo nel thread in cui è stato creato.  Se si tenta di accedere allo stato condiviso di un controllo Windows Form in una query PLINQ, se si è in esecuzione nel debugger viene generata un'eccezione. Questa impostazione può essere disattivata. Tuttavia, se la query viene utilizzata nel thread dell'interfaccia utente, è possibile accedere al controllo dal ciclo `foreach` che enumera i risultati della query, poiché tale codice viene eseguito in un solo thread.  
  
## Non presupporre che le iterazioni di Foreach, For e ForAll vengano eseguite sempre in parallelo  
 È importante ricordare che le iterazioni singole in un ciclo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>, <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> o <xref:System.Linq.ParallelEnumerable.ForAll%2A> possono essere eseguite in parallelo ma non è necessario che lo siano.  È pertanto necessario evitare di scrivere codice la cui correttezza dipenda dall'esecuzione parallela delle iterazioni o dall'esecuzione delle iterazioni in un particolare ordine.  
  
 Il codice seguente, ad esempio, è molto probabile che conduca a un deadlock:  
  
```vb  
Dim mre = New ManualResetEventSlim()  
    Enumerable.Range(0, ProcessorCount * 100).AsParallel().ForAll(Sub(j)   
  
                                                     If j = Environment.ProcessorCount Then  
  
                                                         Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
                                                         mre.Set()  
  
                                                     Else  
  
                                                         Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j)  
                                                         mre.Wait()  
                                                     End If  
    End Sub) ' deadlocks  
```  
  
```csharp  
ManualResetEventSlim mre = new ManualResetEventSlim();  
            Enumerable.Range(0, ProcessorCount * 100).AsParallel().ForAll((j) =>  
            {  
                if (j == Environment.ProcessorCount)  
                {  
                    Console.WriteLine("Set on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
                    mre.Set();  
                }  
                else  
                {  
                    Console.WriteLine("Waiting on {0} with value of {1}", Thread.CurrentThread.ManagedThreadId, j);  
                    mre.Wait();  
                }  
            }); //deadlocks  
```  
  
 In questo esempio, un'unica iterazione imposta un evento e tutte le altre iterazioni attendono l'evento.  Nessuna delle iterazioni in attesa può essere completata fino a quando non viene completata l'iterazione di impostazione dell'evento.  È tuttavia possibile che le iterazioni in attesa blocchino tutti i thread utilizzati per eseguire il ciclo parallelo, prima che l'iterazione di impostazione dell'evento abbia avuto la possibilità di essere eseguita.  Ciò comporta un deadlock. L'iterazione di impostazione dell'evento non verrà mai eseguita e le iterazioni in attesa non verranno mai riattivate.  
  
 In particolare, l'avanzamento di un'iterazione di un ciclo parallelo non deve dipendere da un'altra iterazione del ciclo.  Se il ciclo parallelo decide di pianificare le iterazioni in sequenza ma nell'ordine opposto, si verificherà un deadlock.  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)