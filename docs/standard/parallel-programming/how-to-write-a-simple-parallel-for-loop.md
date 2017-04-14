---
title: "How to: Write a Simple Parallel.For Loop | Microsoft Docs"
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
  - "Parallel.For, How to Write"
  - "for loop, parallel construction in .NET"
  - "parallel for loops, how to use"
ms.assetid: 9029ba7f-a9d1-4526-8c84-c88716dba5d4
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# How to: Write a Simple Parallel.For Loop
Questo argomento contiene due esempi che mostrano il metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>.  Il primo usa l'overload del metodo <xref:System.Threading.Tasks.Parallel.For%28System.Int64%2CSystem.Int64%2CSystem.Action%7BSystem.Int64%7D%29?displayProperty=fullName>, mentre il secondo usa l'overload <xref:System.Threading.Tasks.Parallel.For%28System.Int32%2CSystem.Int32%2CSystem.Action%7BSystem.Int32%7D%29?displayProperty=fullName>, ovvero i due overload più semplici del metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>.  È possibile usare questi due overload del metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> quando non è necessario annullare il ciclo, interrompere le iterazioni del ciclo o mantenere qualsiasi stato locale dei thread.  
  
> [!NOTE]
>  Questa documentazione usa espressioni lambda per definire delegati in TPL.  Se non si ha familiarità con le espressioni lambda in C\# o Visual Basic, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
 Il primo esempio calcola le dimensioni dei file in una singola directory.  Il secondo calcola il prodotto di due matrici.  
  
## Esempio  
 Questo esempio è una semplice utilità da riga di comando che calcola le dimensioni totali dei file in una directory.  È previsto un singolo percorso di directory come argomento e l'esempio indica il numero e le dimensioni totali dei file presenti nella directory.  Dopo aver verificato l'esistenza della directory, l'esempio usa il metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> per enumerare i file nella directory e determinarne le dimensioni.  Le dimensioni di ogni file vengono quindi aggiunte alla variabile `totalSize`.  Tenere presente che l'aggiunta viene eseguita chiamando il metodo <xref:System.Threading.Interlocked.Add%2A?displayProperty=fullName>, in modo che sia un'operazione atomica.  In caso contrario, più attività potrebbero tentare di aggiornare la variabile `totalSize` contemporaneamente.  
  
 [!code-csharp[Conceptual.Parallel.For#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.parallel.for/cs/for1.cs#1)]
 [!code-vb[Conceptual.Parallel.For#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.parallel.for/vb/for1.vb#1)]  
  
## Esempio  
 Questo esempio usa il metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> per calcolare il prodotto di due matrici.  L'esempio mostra anche come usare la classe <xref:System.Diagnostics.Stopwatch?displayProperty=fullName> per confrontare le prestazioni di un ciclo parallelo con uno non parallelo.  Poiché può generare un volume elevato di output, l'esempio permette il reindirizzamento dell'output a un file.  
  
 [!code-csharp[TPL_Parallel#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleparallelfor.cs#01)]
 [!code-vb[TPL_Parallel#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleparallelfor.vb#01)]  
  
 Quando si parallelizza qualsiasi codice, inclusi i cicli, un obiettivo importante consiste nell'utilizzare i processori quanto più possibile senza eseguire una parallelizzazione eccessiva che faccia sì che l'overhead per l'elaborazione parallela vanifichi qualsiasi vantaggio in termini di prestazioni.  In questo esempio specifico viene parallelizzato solo il ciclo esterno, perché nel ciclo interno non vengono eseguite molte attività.  La combinazione di una quantità ridotta di attività e di effetti della cache indesiderati può provocare un peggioramento delle prestazioni nei cicli paralleli annidati.  Di conseguenza, la parallelizzazione del solo ciclo esterno è il modo migliore per ottimizzare i vantaggi della concorrenza sulla maggior parte dei sistemi.  
  
## Delegato  
 Il terzo parametro di questo overload di <xref:System.Threading.Tasks.Parallel.For%2A> è un delegato di tipo `Action<int>` in C\# o `Action(Of Integer)` in Visual Basic.  Un delegato `Action`, che abbia nessuno, uno o sedici parametri di tipo, restituisce sempre void.  In Visual Basic il comportamento di un delegato `Action` viene definito con un oggetto `Sub`.  L'esempio usa un'espressione lambda per creare il delegato, ma è possibile creare il delegato anche in altri modi.  Per altre informazioni, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## Valore di iterazione  
 Il delegato accetta un singolo parametro di input il cui valore è l'iterazione corrente.  Questo valore di iterazione viene fornito dal runtime e il suo valore iniziale è l'indice del primo elemento nel segmento \(partizione\) dell'origine elaborata nel thread corrente.  
  
 Se si vuole esercitare maggiore controllo sul livello di concorrenza, usare uno degli overload che accetta un parametro di input <xref:System.Threading.Tasks.ParallelOptions?displayProperty=fullName>, come <xref:System.Threading.Tasks.Parallel.For%28System.Int32%2CSystem.Int32%2CSystem.Threading.Tasks.ParallelOptions%2CSystem.Action%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%7D%29?displayProperty=fullName>.  
  
## Valore restituito e gestione delle eccezioni  
 <xref:System.Threading.Tasks.Parallel.For%2A> restituisce un oggetto <xref:System.Threading.Tasks.ParallelLoopResult?displayProperty=fullName> al completamento di tutti i thread.  Questo valore restituito è utile quando si arresta o si interrompe l'iterazione del ciclo manualmente, perché l'oggetto <xref:System.Threading.Tasks.ParallelLoopResult> archivia informazioni come l'ultima iterazione eseguita fino al completamento.  Se si verificano una o più eccezioni in uno dei thread, verrà generato un oggetto <xref:System.AggregateException?displayProperty=fullName>.  
  
 Nel codice di questo esempio il valore restituito di <xref:System.Threading.Tasks.Parallel.For%2A> non viene usato.  
  
## Analisi e prestazioni  
 È possibile usare la Creazione guidata sessione di prestazioni per visualizzare l'utilizzo CPU nel computer.  Come esperimento, aumentare il numero di colonne e righe nelle matrici.  Più grandi sono le matrici, maggiore sarà la differenza in termini di prestazioni tra le versioni parallela e sequenziale del calcolo.  Quando la matrice è di dimensioni ridotte, la versione sequenziale verrà eseguita più rapidamente a causa dell'overhead durante la configurazione del ciclo parallelo.  
  
 Le chiamate sincrone a risorse condivise, come la console o il file system, riducono significativamente le prestazioni di un ciclo parallelo.  Per la misurazione delle prestazioni, provare a evitare chiamate come <xref:System.Console.WriteLine%2A?displayProperty=fullName> all'interno del ciclo.  
  
## Compilazione del codice  
  
-   Copiare e incollare questo codice in un progetto di Visual Studio 2010.  
  
## Vedere anche  
 <xref:System.Threading.Tasks.Parallel.For%2A>   
 <xref:System.Threading.Tasks.Parallel.ForEach%2A>   
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)