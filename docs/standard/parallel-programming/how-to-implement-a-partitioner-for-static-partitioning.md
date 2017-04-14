---
title: "How to: Implement a Partitioner for Static Partitioning | Microsoft Docs"
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
  - "tasks, how to create a static partitioner"
ms.assetid: f4410508-cac6-4ba7-bef1-c5e68b2794f3
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Implement a Partitioner for Static Partitioning
Nell'esempio seguente viene illustrato come implementare un partitioner personalizzato semplice per PLINQ che esegue il partizionamento statico.  Poiché il partitioner non supporta partizioni dinamiche, non può essere utilizzato da <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName>.  Questo particolare partitioner potrebbe garantire un aumento della velocità sul partitioner dell'intervallo predefinito per le origini dati per cui ogni elemento richiede una quantità sempre maggiore di tempo di elaborazione.  
  
## Esempio  
 [!code-csharp[TPL_Partitioners#05](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#05)]  
  
 Le partizioni in questo esempio sono basate sull'ipotesi di un incremento lineare del tempo di elaborazione per ogni elemento.  Nel mondo reale potrebbe essere difficile stimare i tempi di elaborazione in questo modo.  Se si utilizza un partitioner statico con un'origine dati specifica, è possibile ottimizzare la formula del partizionamento per l'origine, aggiungere logica del bilanciamento del carico oppure utilizzare l'approccio del partizionamento a blocchi come dimostrato in [How to: Implement Dynamic Partitions](../../../docs/standard/parallel-programming/how-to-implement-dynamic-partitions.md).  
  
## Vedere anche  
 [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md)