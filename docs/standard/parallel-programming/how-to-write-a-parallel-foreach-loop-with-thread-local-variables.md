---
title: "How to: Write a Parallel.ForEach Loop with Thread-Local Variables | Microsoft Docs"
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
  - "parallel foreach loop, how to use local state"
ms.assetid: 24b10041-b30b-45cb-aa65-66cf568ca76d
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# How to: Write a Parallel.ForEach Loop with Thread-Local Variables
Nell'esempio seguente viene illustrato come scrivere un metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A> che usa variabili locale di thread.  Quando viene eseguito un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A>, la relativa raccolta di origine viene divisa in più partizioni.  Ogni partizione otterrà la propria copia della variabile di "locale di thread".  Il termine "locale di thread" è leggermente impreciso, in quanto in alcuni casi è possibile che due partizioni vengano eseguite sullo stesso thread.  
  
 Il codice e i parametri riportati in questo esempio, somigliano molto al metodo <xref:System.Threading.Tasks.Parallel.For%2A> corrispondente.  Per altre informazioni, vedere [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md).  
  
 Per usare una variabile locale di thread in un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A>, è necessario chiamare uno degli overload del metodo che accetta due parametri di tipo.  Il primo parametro di tipo, `TSource`, specifica il tipo di elemento di origine e il secondo parametro di tipo, `TLocal`, specifica il tipo di variabile locale di thread.  
  
## Esempio  
 Nell'esempio seguente viene chiamato l'overload <xref:System.Threading.Tasks.Parallel.ForEach%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%601%7D%2CSystem.Func%7B%60%600%2CSystem.Threading.Tasks.ParallelLoopState%2C%60%601%2C%60%601%7D%2CSystem.Action%7B%60%601%7D%29?displayProperty=fullName> per calcolare la somma di una matrice di un milione di elementi.  L'overload ha quattro parametri:  
  
-   `source`, ovvero l'origine dati.  Deve implementare <xref:System.Collections.Generic.IEnumerable%601>.  L'origine dati nell'esempio è l'oggetto `IEnumerable<Int32>` da un milione di membri restituito dal metodo <xref:System.Linq.Enumerable.Range%2A?displayProperty=fullName>.  
  
-   `localInit`, ovvero la funzione che inizializza la variabile di thread locale.  Questa funzione viene chiamata una volta per ogni partizione in cui viene eseguita l'operazione <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName>.  Nell'esempio, la variabile locale di thread viene inizializzata su zero.  
  
-   `body`, un delegato <xref:System.Func%604> che viene richiamato dal ciclo parallelo per ogni iterazione del ciclo.  La firma è `Func\<TSource, ParallelLoopState, TLocal, TLocal>`.  Si fornisce il codice per il delegato e il ciclo passa i parametri di input, che sono:  
  
    -   L'elemento corrente dell'oggetto <xref:System.Collections.Generic.IEnumerable%601>.  
  
    -   Una variabile <xref:System.Threading.Tasks.ParallelLoopState> che si può usare nel codice del delegato per esaminare lo stato del ciclo.  
  
    -   La variabile locale di thread.  
  
     Il delegato restituisce la variabile locale di thread, che viene quindi passata all'iterazione successiva del ciclo che viene eseguito in quella partizione specifica.  Ogni partizione del ciclo mantiene un'istanza separata di questa variabile.  
  
     Nell'esempio il delegato aggiunge il valore di ogni valore integer alla variabile locale di thread, che mantiene un totale corrente dei valori degli elementi integer in quella partizione.  
  
-   `localFinally`, un delegato `Action<TLocal>` che viene richiamato da <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> al termine delle operazioni di riproduzione del ciclo in ogni partizione.  Il metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> passa al delegato `Action<TLocal>` il valore finale della variabile locale di thread per il thread corrente \(o partizione del ciclo\) e l'utente fornisce il codice che esegue l'azione necessaria per la combinazione del risultato di questa partizione con i risultati delle altre partizioni.  Questo delegato può essere chiamato simultaneamente da più attività.  Per questo motivo, nell'esempio viene usato il metodo <xref:System.Threading.Interlocked.Add%28System.Int32%40%2CSystem.Int32%29?displayProperty=fullName> per sincronizzare l'accesso alla variabile `total`.  Poiché il tipo del delegato è <xref:System.Action%601>, non viene restituito alcun valore.  
  
 [!code-csharp[TPL_Parallel#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/foreachthreadlocal.cs#04)]
 [!code-vb[TPL_Parallel#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/foreachthreadlocal.vb#04)]  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)