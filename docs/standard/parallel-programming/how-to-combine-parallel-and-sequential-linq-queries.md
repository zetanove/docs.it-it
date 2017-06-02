---
title: "How to: Combine Parallel and Sequential LINQ Queries | Microsoft Docs"
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
  - "parallel queries, combine parallel and sequential"
ms.assetid: 1167cfe6-c8aa-4096-94ba-c66c3a4edf4c
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Combine Parallel and Sequential LINQ Queries
In questo esempio viene illustrato come utilizzare il metodo <xref:System.Linq.ParallelEnumerable.AsSequential%2A> per indicare a PLINQ di elaborare in modo sequenziale tutti gli operatori successivi nella query.  Benché in genere l'elaborazione sequenziale sia più lenta rispetto a quella in parallelo, in alcuni casi è necessario produrre risultati corretti.  
  
> [!WARNING]
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato uno scenario in cui si richiede l'utilizzo di <xref:System.Linq.ParallelEnumerable.AsSequential%2A>, in particolare per conservare l'ordine stabilito in una clausola precedente della query.  
  
 [!code-csharp[PLINQ#24](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#24)]
 [!code-vb[PLINQ#24](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#24)]  
  
## Compilazione del codice  
 Per compilare ed eseguire questo codice, incollarlo nel progetto [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md), aggiungere una riga per chiamare il metodo da `Main` e premere F5.  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)