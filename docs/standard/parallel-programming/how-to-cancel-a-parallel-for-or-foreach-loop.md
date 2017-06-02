---
title: "How to: Cancel a Parallel.For or ForEach Loop | Microsoft Docs"
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
  - "parallel foreach loop, how to cancel"
  - "parallel for loops, how to cancel"
ms.assetid: 9d19b591-ea95-4418-8ea7-b6266af9905b
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# How to: Cancel a Parallel.For or ForEach Loop
I metodi <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> supportano l'annullamento tramite l'utilizzo di token di annullamento.  Per ulteriori informazioni sull'annullamento in generale, vedere [Annullamento](../../../docs/standard/threading/cancellation-in-managed-threads.md).  In un ciclo parallelo si fornisce l'oggetto <xref:System.Threading.CancellationToken> al metodo nel parametro <xref:System.Threading.Tasks.ParallelOptions> e quindi si include la chiamata parallela in un blocco try\-catch.  
  
## Esempio  
 Nell'esempio seguente viene illustrato come annullare una chiamata a <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName>.  È possibile applicare lo stesso approccio a una chiamata a <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName>.  
  
 [!code-csharp[TPL_Parallel#29](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_cancel.cs#29)]
 [!code-vb[TPL_Parallel#29](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/cancelloop.vb#29)]  
  
 Se il token che segnala l'annullamento è lo stesso token specificato nell'istanza di <xref:System.Threading.Tasks.ParallelOptions>, il ciclo parallelo genererà un solo oggetto <xref:System.OperationCanceledException> al momento dell'annullamento.  Se altri token provocano l'annullamento, il ciclo genererà un oggetto <xref:System.AggregateException> con un oggetto <xref:System.OperationCanceledException> come InnerException.  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md)