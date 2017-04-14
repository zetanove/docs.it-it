---
title: "How to: Synchronize Concurrent Operations with a Barrier | Microsoft Docs"
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
  - "Barrier, how to use"
ms.assetid: e1a253ff-e0fb-4df8-95ff-d01a90d4cb19
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# How to: Synchronize Concurrent Operations with a Barrier
Nell'esempio seguente viene mostrato come sincronizzare attività simultanee con un oggetto <xref:System.Threading.Barrier>.  
  
## Esempio  
 Lo scopo del programma seguente è contare le iterazioni \(o fasi\) necessarie per due thread affinché per ciascuno di essi venga trovata la relativa metà della soluzione nella stessa fase utilizzando un algoritmo di casualità per riprodurre con sequenza casuale le parole.  Una volta che ciascun thread ha riprodotto con sequenza casuale le proprie parole, l'operazione post\-fase della barriera confronta i due risultati per verificare se è stato eseguito il rendering della frase completa nell'ordine delle parole corretto.  
  
 [!code-csharp[CDS_Barrier#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_barrier/cs/barrier.cs#01)]
 [!code-vb[CDS_Barrier#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_barrier/vb/barrier_vb.vb#01)]  
  
 Gli oggetti <xref:System.Threading.Barrier> impediscono l'esecuzione di singole attività in un'operazione in parallelo finché tutte le attività non raggiungono la barriera.  Questo approccio risulta utile quando un'operazione in parallelo prevede più fasi e per ogni fase occorre garantire la sincronizzazione tra le attività.  In questo esempio l'operazione prevede due fasi.  Nella prima fase, ogni attività riempie la propria sezione del buffer con dati.  Quando un'attività completa il riempimento della propria sezione, indica alla barriera che è pronta a continuare e quindi resta in attesa.  Quando tutte le attività hanno eseguito questa operazione, vengono sbloccate e inizia la seconda fase.  La barriera è necessaria poiché nella seconda fase ogni attività deve essere in grado di accedere a tutti i dati generati fino alla fine della prima fase.  Senza la barriera, le prime attività che completano la prima fase potrebbero tentare di leggere dati da buffer che ancora non sono stati riempiti dalle altre attività.  In questo modo è possibile sincronizzare il numero desiderato di fasi.  
  
## Vedere anche  
 [Data Structures for Parallel Programming](../../../docs/standard/parallel-programming/data-structures-for-parallel-programming.md)