---
title: "How to: Specify the Execution Mode in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, how to use execution mode"
ms.assetid: e52ff26c-c5d3-4fab-9fec-c937fb387963
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Specify the Execution Mode in PLINQ
In questo esempio viene mostrato come forzare PLINQ a ignorare le proprie regole euristiche predefinite e parallelizzare una query indipendentemente dalla forma della query.  
  
> [!WARNING]
>  Lo scopo di questo esempio è dimostrare l'utilizzo e potrebbe non essere eseguito più velocemente dell'equivalente query LINQ to Objects sequenziale.  Per ulteriori informazioni sull'aumento di velocità, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
## Esempio  
 [!code-csharp[PLINQ#22](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#22)]
 [!code-vb[PLINQ#22](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#22)]  
  
 PLINQ è progettato per sfruttare le opportunità di parallelizzazione.  L'esecuzione parallela, tuttavia, non è vantaggiosa per tutte le query.  Quando ad esempio una query contiene un solo delegato dell'utente che svolge una quantità minima di lavoro, in genere la query risulterà più veloce se eseguita in modo sequenziale.  Ciò è dovuto al fatto che l'overhead necessario per consentire l'esecuzione parallela rappresenta uno svantaggio maggiore dei vantaggi ottenuti in termini di aumento di velocità.  Pertanto, PLINQ non parallelizza automaticamente tutte le query.  Invece, esamina prima la forma della query e i vari operatori che la costituiscono.  In base a questa analisi, nella modalità di esecuzione predefinita PLINQ può decidere di eseguire in modo sequenziale l'intera query o parte di essa.  Tuttavia, in alcuni casi è possibile avere una conoscenza più approfondita della query rispetto a quanto PLINQ sia in grado di determinare dalle proprie analisi.  Ad esempio, è possibile sapere che un delegato è molto dispendioso e che la query certamente trarrà profitto dalla parallelizzazione.  In tali casi è possibile utilizzare il metodo <xref:System.Linq.ParallelEnumerable.WithExecutionMode%2A> e specificare il valore di <xref:System.Linq.ParallelExecutionMode> per indicare a PLINQ di eseguire sempre la query come parallela.  
  
## Compilazione del codice  
 Tagliare e copiare questo codice in [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md) e chiamare il metodo da `Main`.  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable.AsSequential%2A>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)