---
title: "Task Cancellation | Microsoft Docs"
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
  - "tasks, cancellation"
  - "asynchronous task cancellation"
ms.assetid: 3ecf1ea9-e399-4a6a-a0d6-8475f48dcb28
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Task Cancellation
Le classi <xref:System.Threading.Tasks.Task?displayProperty=fullName> e <xref:System.Threading.Tasks.Task%601?displayProperty=fullName> supportano l'annullamento tramite l'utilizzo dei token di annullamento in .NET Framework. Per altre informazioni, vedere [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md). Nelle classi Task l'annullamento comporta la cooperazione tra il delegato dell'utente, che rappresenta un'operazione annullabile, e il codice che ha richiesto l'annullamento.  Un annullamento riuscito prevede una chiamata al metodo <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName> da parte del codice richiedente nonché l'interruzione tempestiva dell'operazione da parte del delegato dell'utente. L'operazione può essere interrotta tramite una di queste opzioni:  
  
-   Completare l'esecuzione del delegato. In molti scenari questo approccio è sufficiente. Tuttavia, un'istanza di attività "annullata" in questo modo passa allo stato <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>, non allo stato <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>.  
  
-   Generare un oggetto <xref:System.OperationCanceledException> e passare a quest'ultimo il token in cui è stato richiesto l'annullamento. Il modo preferito per eseguire queste operazioni è tramite il metodo <xref:System.Threading.CancellationToken.ThrowIfCancellationRequested%2A>. Un'attività annullata in questo modo passa allo stato Canceled. Il codice chiamante può usare tale stato per verificare che l'attività ha risposto alla richiesta di annullamento.  
  
 Nell'esempio seguente viene mostrato il modello di base relativo all'annullamento di attività che genera l'eccezione. Notare che il token viene passato al delegato dell'utente e all'istanza di attività stessa.  
  
 [!code-csharp[TPL_Cancellation#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/snippet02.cs#02)]
 [!code-vb[TPL_Cancellation#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/module1.vb#02)]  
  
 Per un esempio più esaustivo, vedere [How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md).  
  
 Quando un'istanza dell'attività rileva un oggetto <xref:System.OperationCanceledException> generato dal codice utente, confronta il token dell'eccezione con il token associato, ovvero il token passato all'API che ha creato l'attività. Se i due token sono uguali e la proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> del token restituisce true, ciò viene interpretato dall'attività come una conferma di annullamento e passa allo stato Canceled. Se non si usa un metodo <xref:System.Threading.Tasks.Task.Wait%2A> o <xref:System.Threading.Tasks.Task.WaitAll%2A> per attendere l'attività, quest'ultima si limita a impostare il proprio stato su <xref:System.Threading.Tasks.TaskStatus>.  
  
 Se si resta in attesa di un'attività che effettua la transizione allo stato Canceled, viene generata un'eccezione <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=fullName> \(di cui viene eseguito il wrapping in un'eccezione <xref:System.AggregateException>\). Notare che questa eccezione non indica una situazione di errore, bensì l'esito positivo di un annullamento. Di conseguenza la proprietà <xref:System.Threading.Tasks.Task.Exception%2A> dell'attività restituisce `null`.  
  
 Se la proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> del token restituisce false o se il token dell'eccezione non corrisponde a quello dell'attività, l'oggetto <xref:System.OperationCanceledException> viene trattato come un'eccezione normale, il che comporta la transizione dell'attività allo stato Faulted. Notare inoltre che anche la presenza di altre eccezioni comporterà il passaggio dell'attività allo stato Faulted. È possibile ottenere lo stato dell'attività completata nella proprietà <xref:System.Threading.Tasks.Task.Status%2A>.  
  
 È possibile che un'attività continui a elaborare alcuni elementi dopo la richiesta di annullamento.  
  
## Vedere anche  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)   
 [How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)