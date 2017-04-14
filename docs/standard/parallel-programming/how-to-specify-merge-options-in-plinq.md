---
title: "How to: Specify Merge Options in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, how to use merge options"
ms.assetid: 0f33b527-e91a-4550-a39a-e63e396fd831
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Specify Merge Options in PLINQ
In questo esempio viene mostrato come specificare le opzioni di unione che verranno applicate a tutti gli operatori successivi in una query PLINQ.  Benché non sia necessario impostare in modo esplicito le opzioni di unione, questa operazione può comportare un miglioramento delle prestazioni.  Per ulteriori informazioni sulle opzioni di unione, vedere [Merge Options in PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md) .  
  
> [!WARNING]
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 Nell'esempio seguente viene mostrato il comportamento delle opzioni di unione in uno scenario di base in cui è presente un'origine non ordinata e si applica una funzione dispendiosa a ogni elemento.  
  
 [!code-csharp[PLINQ#23](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#23)]
 [!code-vb[PLINQ#23](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#23)]  
  
 Nei casi in cui l'opzione <xref:System.Linq.ParallelMergeOptions> comporti una latenza indesiderata prima che venga prodotto il primo elemento, tentare l'opzione <xref:System.Linq.ParallelMergeOptions> per produrre elementi di risultato in modo più veloce ed efficiente.  
  
## Vedere anche  
 <xref:System.Linq.ParallelMergeOptions>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)