---
title: "How to: Unwrap a Nested Task | Microsoft Docs"
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
  - "tasks, how to unwrap nested tasks"
ms.assetid: a0769dd2-0f6d-48ca-8418-a9d39de7f450
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Unwrap a Nested Task
È possibile restituire un'attività da un metodo, quindi restare in attesa o ripartire dall'attività, come mostrato nell'esempio seguente:  
  
 [!code-csharp[TPL_Unwrap#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#01)]
 [!code-vb[TPL_Unwrap#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#01)]  
  
 Nell'esempio precedente la proprietà <xref:System.Threading.Tasks.Task%601.Result%2A> è di tipo `string` \(`String` in Visual Basic\).  
  
 In alcuni scenari, tuttavia, è necessario creare un'attività all'interno di un'altra attività, quindi restituire l'attività annidata.  In questo caso l'oggetto `TResult` dell'attività contenitore è un'attività.  Nell'esempio seguente la proprietà Result è un oggetto `Task<Task<string>>` in C\# o `Task(Of Task(Of String))` in Visual Basic.  
  
 [!code-csharp[TPL_Unwrap#02](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#02)]
 [!code-vb[TPL_Unwrap#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#02)]  
  
 Anche se è possibile scrivere codice per annullare il wrapping dell'attività esterna e recuperare l'attività originale e la relativa proprietà <xref:System.Threading.Tasks.Task%601.Result%2A>, tale codice non è facile da scrivere in quanto è necessario gestire le eccezioni, oltre alle richieste di annullamento.  In questa situazione si consiglia di utilizzare uno dei metodi di estensione <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A>, come mostrato nell'esempio seguente.  
  
 [!code-csharp[TPL_UnWrap#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#03)]
 [!code-vb[TPL_UnWrap#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippets1-3.vb#03)]  
  
 È possibile utilizzare i metodi <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A> per trasformare qualsiasi oggetto `Task<Task>` oppure `Task<Task<TResult>>` \(`Task(Of Task)` oppure `Task(Of Task(Of TResult))` in Visual Basic\) in un oggetto `Task` oppure `Task<TResult>` \(`Task(Of TResult)` in Visual Basic\).  La nuova attività rappresenta pienamente l'attività annidata interna e include lo stato di annullamento e tutte le eccezioni.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come utilizzare i metodi di estensione <xref:System.Threading.Tasks.TaskExtensions.Unwrap%2A>.  
  
 [!code-csharp[TPL_UnWrap#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_unwrap/cs/unwrapprogram.cs#04)]
 [!code-vb[TPL_UnWrap#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_unwrap/vb/snippet04.vb#04)]  
  
## Vedere anche  
 <xref:System.Threading.Tasks.TaskExtensions?displayProperty=fullName>   
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)