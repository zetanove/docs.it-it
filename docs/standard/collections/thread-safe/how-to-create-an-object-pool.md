---
title: 'Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag | Microsoft Docs'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- object pool, in .NET Framework
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
caps.latest.revision: 5
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: bfe61501586deed112d6a94bf90fd83e84f2639f
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-create-an-object-pool-by-using-a-concurrentbag"></a>Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag
Questo esempio illustra come usare un contenitore simultaneo per implementare un pool di oggetti. I pool di oggetti possono migliorare le prestazioni dell'applicazione in situazioni in cui vengono richieste più istanze di una classe e la classe è costosa da creare o eliminare. Quando un programma client richiede un nuovo oggetto, il pool di oggetti prima tenta di specificarne uno che è già stato creato e restituito al pool. Se non è disponibile nessun oggetto, solo in questo caso viene creato.  
  
 <xref:System.Collections.Concurrent.ConcurrentBag%601> viene usato per archiviare gli oggetti poiché supporta inserimento e rimozione veloci, specialmente quando lo stesso thread aggiunge e rimuove elementi. È possibile ampliare ancora questo esempio per incentrarlo su <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>, implementato dalla struttura dei dati del contenitore come fanno <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
## <a name="example"></a>Esempio  
 [!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
 [!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
