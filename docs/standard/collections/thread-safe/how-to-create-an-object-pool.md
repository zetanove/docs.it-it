---
title: "Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag | Microsoft Docs"
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
  - "pool di oggetti, in .NET Framework"
ms.assetid: 0480e7ff-b6f9-480e-a889-2ed4264d8372
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag
In questo esempio viene illustrato come utilizzare un contenitore simultaneo per implementare un pool di oggetti.  I pool di oggetti possono migliorare le prestazioni dell'applicazione nelle situazioni in cui vengono richieste più istanze di una classe e la classe è dispendiosa da creare o eliminare.  Quando un programma client richiede un nuovo oggetto, il pool di oggetti tenta innanzitutto di fornirne uno che è già stato creato e restituito al pool.  Se non ne è disponibile alcuno, solo a quel punto viene creato un nuovo oggetto.  
  
 <xref:System.Collections.Concurrent.ConcurrentBag%601> viene utilizzato per archiviare gli oggetti poiché supporta l'inserimento e la rimozione veloci, soprattutto quando lo stesso thread aggiunge e rimuove elementi.  Questo esempio potrebbe essere ulteriormente ampliato sviluppando un oggetto <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>, che la struttura dei dati del contenitore implementa, come nel caso di <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
## Esempio  
 [!code-csharp[CDS#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds/cs/objectpool.cs#04)]
 [!code-vb[CDS#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds/vb/objectpool04.vb#04)]  
  
## Vedere anche  
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)