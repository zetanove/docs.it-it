---
title: "How to: Cancel a Task and Its Children | Microsoft Docs"
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
  - "tasks, how to cancel"
ms.assetid: 08574301-8331-4719-ad50-9cf7f6ff3048
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# How to: Cancel a Task and Its Children
In questi esempi viene mostrato come eseguire le attività seguenti:  
  
1.  Creazione e avvio di un'attività annullabile.  
  
2.  Passaggio di un token di annullamento al delegato dell'utente e facoltativamente all'istanza dell'attività.  
  
3.  Rilevamento della richiesta di annullamento nel delegato dell'utente e risposta a tale richiesta.  
  
4.  Rilevamento facoltativo dell'annullamento dell'attività nel thread chiamante.  
  
 Il thread chiamante non termina forzatamente l'attività, bensì si limita a segnalare la richiesta di annullamento.  Se l'attività è già in esecuzione, è responsabilità del delegato dell'utente rilevare la richiesta e rispondere in modo appropriato.  Se l'annullamento viene richiesto prima dell'esecuzione dell'attività, il delegato dell'utente non viene eseguito e l'oggetto attività passa allo stato Canceled.  
  
## Esempio  
 In questo esempio viene mostrato come terminare un oggetto <xref:System.Threading.Tasks.Task> e i relativi figli in risposta a una richiesta di annullamento.  Viene inoltre mostrato che quando un delegato dell'utente viene terminato mediante la generazione di un oggetto <xref:System.Threading.Tasks.TaskCanceledException>, il thread chiamante può utilizzare facoltativamente il metodo <xref:System.Threading.Tasks.Task.Wait%2A> o il metodo <xref:System.Threading.Tasks.Task.WaitAll%2A> per attendere il completamento delle attività.  In questo caso, si deve utilizzare un blocco `try/catch` per gestire le eccezioni nel thread chiamante.  
  
 [!code-csharp[TPL_Cancellation#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/cancel1.cs#04)]
 [!code-vb[TPL_Cancellation#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/cancel1.vb#04)]  
  
 La classe <xref:System.Threading.Tasks.Task?displayProperty=fullName> è completamente integrata con il modello di annullamento basato sui tipi <xref:System.Threading.CancellationTokenSource?displayProperty=fullName> e <xref:System.Threading.CancellationToken?displayProperty=fullName>.  Per ulteriori informazioni, vedere [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md) e [Task Cancellation](../../../docs/standard/parallel-programming/task-cancellation.md).  
  
## Vedere anche  
 <xref:System.Threading.CancellationTokenSource?displayProperty=fullName>   
 <xref:System.Threading.CancellationToken?displayProperty=fullName>   
 <xref:System.Threading.Tasks.Task?displayProperty=fullName>   
 <xref:System.Threading.Tasks.Task%601?displayProperty=fullName>   
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)   
 [Attached and Detached Child Tasks](../../../docs/standard/parallel-programming/attached-and-detached-child-tasks.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)