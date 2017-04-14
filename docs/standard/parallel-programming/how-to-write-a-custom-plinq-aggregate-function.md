---
title: "How to: Write a Custom PLINQ Aggregate Function | Microsoft Docs"
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
  - "PLINQ queries, how to create aggregate function"
ms.assetid: 5a70dd49-ab2a-4798-b551-196ee7042b1a
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Write a Custom PLINQ Aggregate Function
In questo esempio viene illustrato come utilizzare il metodo <xref:System.Linq.ParallelEnumerable.Aggregate%2A> per applicare una funzione di aggregazione personalizzata a una sequenza di origine.  
  
> [!WARNING]
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 Nell'esempio seguente viene calcolata la deviazione standard di una sequenza di interi.  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 In questo esempio viene utilizzato un overload dell'operatore di query standard Aggregate univoco in PLINQ.  Questo overload accetta un oggetto <xref:System.Func%603?displayProperty=fullName> aggiuntivo come terzo parametro di input.  Questo delegato combina i risultati di tutti i thread prima di eseguire il calcolo finale sui risultati aggregati.  In questo esempio si sommano le somme di tutti i thread.  
  
 Notare che quando un corpo di espressioni lambda è formato da un'unica espressione, il valore restituito del delegato di <xref:System.Func%602?displayProperty=fullName> è il valore dell'espressione.  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)