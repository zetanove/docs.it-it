---
title: "How to: Write a Parallel.For Loop with Thread-Local Variables | Microsoft Docs"
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
  - "parallel for loops, how to use local state"
ms.assetid: 68384064-7ee7-41e2-90e3-71f00bde01bb
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# How to: Write a Parallel.For Loop with Thread-Local Variables
Questo esempio illustra come usare le variabili locali di thread per archiviare e recuperare lo stato in ogni attività separata creata da un ciclo <xref:System.Threading.Tasks.Parallel.For%2A>.  L'uso dei dati locali di thread permette di evitare il sovraccarico dovuto alla sincronizzazione di un numero elevato di accessi a uno stato condiviso.  Invece di scrivere in una risorsa condivisa a ogni iterazione, si calcola e si archivia il valore fino al completamento di tutte le iterazioni per l'attività.  È quindi possibile scrivere il risultato finale una volta sola nella risorsa condivisa oppure passarlo a un altro metodo.  
  
## Esempio  
 L'esempio seguente chiama il metodo <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> per calcolare la somma dei valori in una matrice contenente un milione di elementi.  Il valore di ogni elemento è uguale all'indice corrispondente.  
  
 [!code-csharp[TPL_Parallel#05](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/forandforeach_simple.cs#05)]
 [!code-vb[TPL_Parallel#05](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/forwiththreadlocal.vb#05)]  
  
 I primi due parametri di ogni metodo <xref:System.Threading.Tasks.Parallel.For%2A> specificano i valori di iterazione iniziali e finali.  In questo overload del metodo, il terzo parametro corrisponde alla posizione di inizializzazione dello stato locale.  In questo contesto lo stato locale indica una variabile la cui durata si estende da immediatamente prima della prima iterazione del ciclo nel thread corrente a immediatamente dopo l'ultima iterazione.  
  
 Il tipo del terzo parametro è <xref:System.Func%601>, dove `TResult` indica il tipo della variabile in cui sarà archiviato lo stato locale di thread.  Il tipo corrispondente è definito dall'argomento di tipo generico fornito quando si chiama il metodo <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> generico, che in questo caso è <xref:System.Int64>.  Il tipo di argomento indica al compilatore il tipo di variabile temporanea che sarà usata per l'archiviazione dello stato locale di thread.  In questo esempio l'espressione `() => 0` \(o `Function() 0` in Visual Basic\) inizializza la variabile locale di thread su zero.  Se un argomento di tipo generico è un tipo di riferimento o un tipo di valore definito dall'utente, l'espressione avrà un aspetto analogo al seguente:  
  
```csharp  
() => new MyClass()  
```  
  
```vb  
Function() new MyClass()  
```  
  
 Il quarto parametro definisce la logica del ciclo.  Deve essere un delegato o un'espressione lambda con firma `Func<int, ParallelLoopState, long, long>` in C\# o `Func(Of Integer, ParallelLoopState, Long, Long)` in Visual Basic.  Il primo parametro è il valore del contatore di cicli per quell'iterazione del ciclo.  Il secondo è un oggetto <xref:System.Threading.Tasks.ParallelLoopState> che può essere usato per uscire dal ciclo. L'oggetto è fornito dalla classe <xref:System.Threading.Tasks.Parallel> a ogni occorrenza del ciclo.  Il terzo parametro è la variabile locale di thread.  L'ultimo parametro è il tipo restituito.  In questo caso il tipo è <xref:System.Int64>, poiché questo è il tipo specificato nell'argomento di tipo <xref:System.Threading.Tasks.Parallel.For%2A>.  Questa variabile è denominata `subtotal` ed è restituita dall'espressione lambda.  Il valore restituito è usato per inizializzare `subtotal` in ogni iterazione successiva del ciclo.  È anche possibile considerare quest'ultimo parametro come un valore passato a ogni iterazione e quindi passato al delegato `localFinally` al completamento dell'ultima iterazione.  
  
 Il quinto parametro definisce il metodo chiamato una volta, dopo il completamento di tutte le iterazioni in un determinato thread.  Il tipo di argomento di input corrisponde di nuovo all'argomento di tipo del metodo <xref:System.Threading.Tasks.Parallel.For%60%601%28System.Int32%2CSystem.Int32%2CSystem.Func%7B%60%600%7D%2CSystem.Func%7BSystem.Int32%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%600%2C%60%600%7D%2CSystem.Action%7B%60%600%7D%29> e al tipo restituito dall'espressione lambda del corpo.  In questo esempio il valore è aggiunto a una variabile nell'ambito delle classi in un modo thread\-safe chiamando il metodo <xref:System.Threading.Interlocked.Add%2A?displayProperty=fullName>.  L'uso di una variabile locale di thread permette di evitare di scrivere nella variabile della classe a ogni iterazione del ciclo.  
  
 Per altre informazioni su come usare le espressioni lambda, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)