---
title: "How to: Implement Dynamic Partitions | Microsoft Docs"
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
  - "tasks, how to create a dynamic partitioner"
ms.assetid: c875ad12-a161-43e6-ad1c-3d6927c536a7
caps.latest.revision: 5
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 5
---
# How to: Implement Dynamic Partitions
Nell'esempio seguente viene mostrato come implementare un oggetto <xref:System.Collections.Concurrent.OrderablePartitioner%601?displayProperty=fullName> personalizzato che implementa il partizionamento dinamico e può essere utilizzato da determinati overload <xref:System.Threading.Tasks.Parallel.ForEach%2A> e da PLINQ.  
  
## Esempio  
 Ogni volta che una partizione chiama <xref:System.Collections.IEnumerator.MoveNext%2A> sull'enumeratore, l'enumeratore fornisce la partizione un elemento dell'elenco.  Nel caso di PLINQ e <xref:System.Threading.Tasks.Parallel.ForEach%2A>, la partizione è un'istanza di <xref:System.Threading.Tasks.Task>.  Poiché le richieste si verificano contemporaneamente su più thread, l'accesso all'indice corrente è sincronizzato.  
  
 [!code-csharp[TPL_Partitioners#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#04)]
 [!code-vb[TPL_Partitioners#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/dynamicpartitioner.vb#04)]  
  
 Di seguito viene riportato un esempio di partizionamento a blocchi, con ogni blocco costituito da un elemento.  Fornendo più elementi per volta, sarebbe possibile ridurre il conflitto sul blocco e realizzare teoricamente prestazioni più veloci.  Può tuttavia accadere che blocchi di dimensioni maggiori richiedano logica di bilanciamento del carico aggiuntiva per poter tenere occupati tutti i thread fino a quando non è stato eseguito tutto il lavoro.  
  
## Vedere anche  
 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)   
 [How to: Implement a Partitioner for Static Partitioning](../../../docs/standard/parallel-programming/how-to-implement-a-partitioner-for-static-partitioning.md)