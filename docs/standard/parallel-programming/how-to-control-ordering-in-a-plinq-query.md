---
title: "How to: Control Ordering in a PLINQ Query | Microsoft Docs"
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
  - "PLINQ queries, how to control ordering"
ms.assetid: c67eccc7-004d-4b2f-987e-919cbbd62ef7
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Control Ordering in a PLINQ Query
In questi esempi viene illustrato come controllare l'ordine in una query PLINQ tramite il metodo di estensione <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>.  
  
> [!WARNING]
>  Lo scopo di questi esempi è principalmente quello di dimostrare l'utilizzo e potrebbero essere o meno eseguiti più velocemente delle equivalenti query LINQ to Objects sequenziali.  
  
## Esempio  
 Nell'esempio seguente viene conservato l'ordine della sequenza di origine.  In alcuni casi ciò è necessario. Ad esempio, alcuni operatori di query richiedono una sequenza di origine ordinata per produrre risultati corretti.  
  
 [!code-csharp[PLINQ#12](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#12)]
 [!code-vb[PLINQ#12](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#12)]  
  
## Esempio  
 Nell'esempio seguente vengono mostrati alcuni operatori di query la cui sequenza di origine dovrebbe essere ordinata.  Questi operatori agiranno su sequenze non ordinate, ma potrebbero produrre risultati imprevisti.  
  
 [!code-csharp[PLINQ#14](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#14)]
 [!code-vb[PLINQ#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#14)]  
  
 Per eseguire questo metodo, incollarlo nella classe PLINQDataSample nel progetto [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md) e premere F5.  
  
## Esempio  
 Nell'esempio seguente viene mostrato come conservare l'ordine per la prima parte di una query, rimuovere la conservazione dell'ordine per aumentare le prestazioni di una clausola join e quindi riapplicare l'ordine alla sequenza del risultato finale.  
  
 [!code-csharp[PLINQ#15](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#15)]
 [!code-vb[PLINQ#15](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#15)]  
  
 Per eseguire questo metodo, incollarlo nella classe PLINQDataSample nel progetto [PLINQ Data Sample](../../../docs/standard/parallel-programming/plinq-data-sample.md) e premere F5.  
  
## Vedere anche  
 <xref:System.Linq.ParallelEnumerable>   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)