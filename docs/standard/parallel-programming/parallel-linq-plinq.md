---
title: "Parallel LINQ (PLINQ) | Microsoft Docs"
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
  - "PLINQ, overview"
ms.assetid: 3d4d0cd3-bde4-490b-99e7-f4e41be96455
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Parallel LINQ (PLINQ)
Parallel LINQ \(PLINQ\) è un'implementazione in parallelo di LINQ to Objects.  PLINQ implementa il set completo di operatori di query standard LINQ come metodi di estensione per lo spazio dei nomi T:System.Linq e dispone di operatori aggiuntivi per le operazioni in parallelo.  PLINQ combina la semplicità e la leggibilità della sintassi di LINQ con la potenza della programmazione in parallelo.  Analogamente al codice destinato a Task Parallel Library, le query PLINQ adattano il livello di concorrenza in base alla capacità del computer host.  
  
 In molti scenari, PLINQ può aumentare in modo significativo la velocità delle query LINQ to Objects utilizzando in modo più efficiente tutti i core disponibili nel computer host.  Questo aumento di prestazioni comporta una potenza di calcolo a elevate prestazioni nel desktop.  
  
## Argomenti della sezione  
 [Introduction to PLINQ](../../../docs/standard/parallel-programming/introduction-to-plinq.md)  
  
 [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md)  
  
 [Order Preservation in PLINQ](../../../docs/standard/parallel-programming/order-preservation-in-plinq.md)  
  
 [Merge Options in PLINQ](../../../docs/standard/parallel-programming/merge-options-in-plinq.md)  
  
 [How to: Create and Execute a Simple PLINQ Query](../../../docs/standard/parallel-programming/how-to-create-and-execute-a-simple-plinq-query.md)  
  
 [How to: Control Ordering in a PLINQ Query](../../../docs/standard/parallel-programming/how-to-control-ordering-in-a-plinq-query.md)  
  
 [How to: Combine Parallel and Sequential LINQ Queries](../../../docs/standard/parallel-programming/how-to-combine-parallel-and-sequential-linq-queries.md)  
  
 [How to: Handle Exceptions in a PLINQ Query](../../../docs/standard/parallel-programming/how-to-handle-exceptions-in-a-plinq-query.md)  
  
 [How to: Cancel a PLINQ Query](../../../docs/standard/parallel-programming/how-to-cancel-a-plinq-query.md)  
  
 [How to: Write a Custom PLINQ Aggregate Function](../../../docs/standard/parallel-programming/how-to-write-a-custom-plinq-aggregate-function.md)  
  
 [How to: Specify the Execution Mode in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-the-execution-mode-in-plinq.md)  
  
 [How to: Specify Merge Options in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)  
  
 [How to: Iterate File Directories with PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md)  
  
 [How to: Measure PLINQ Query Performance](../../../docs/standard/parallel-programming/how-to-measure-plinq-query-performance.md)  
  
 [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md)  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)