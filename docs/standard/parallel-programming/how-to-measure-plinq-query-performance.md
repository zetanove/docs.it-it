---
title: "How to: Measure PLINQ Query Performance | Microsoft Docs"
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
  - "PLINQ queries, how to measure performance"
ms.assetid: 491ba43b-2c10-473d-9aab-e2cb96446711
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# How to: Measure PLINQ Query Performance
Questo esempio mostra come utilizzare la classe <xref:System.Diagnostics.Stopwatch> per misurare il tempo di esecuzione di una query PLINQ.  
  
## Esempio  
 Questo esempio utilizza un ciclo vuoto `foreach` \(`For Each` in Visual Basic\) per misurare il tempo di esecuzione di una query.  Nelle applicazioni reali di codice, il ciclo in genere contiene passaggi di elaborazione aggiuntivi il cui tempo di esecuzione viene aggiunto al tempo di esecuzione complessivo della query.  Notare che il cronometro è fermo fino a poco prima del ciclo, poiché questo istante corrisponde al momento in cui inizia l'esecuzione della query.  Se si richiede una misura più precisa è possibile utilizzare la proprietà `ElapsedTicks` anziché `ElapsedMilliseconds`.  
  
 [!code-csharp[PLINQ#19](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/measure2.cs#19)]
 [!code-vb[PLINQ#19](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/measure2.vb#19)]  
  
 Benché il tempo di esecuzione totale sia una metrica utile quando si sperimentano le implementazioni della query, in genere non fornisce informazioni esaustive.  Per ottenere una visualizzazione più approfondita e dettagliata dell'interazione dei thread della query con gli altri thread della query e con gli altri processi in esecuzione, utilizzare il Visualizzatore di concorrenze.  Per ulteriori informazioni, vedere [Visualizzatore di concorrenze](../Topic/Concurrency%20Visualizer.md).  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)