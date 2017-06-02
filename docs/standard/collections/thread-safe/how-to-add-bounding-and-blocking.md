---
title: "Procedura: Aggiungere funzionalità di delimitazione e blocco a una raccolta | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, custom blocking collections
ms.assetid: 4c2492de-3876-4873-b5a1-000bb404d770
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: df159b1ab3f7c16564ce493a585246c4c461a8f9
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-add-bounding-and-blocking-functionality-to-a-collection"></a>Procedura: Aggiungere funzionalità di delimitazione e blocco a una raccolta
In questo esempio viene illustrato come aggiungere la funzionalità di delimitazione e blocco a una classe di raccolta personalizzata tramite l'implementazione dell'interfaccia <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=fullName> nella classe e come usare un'istanza della classe come meccanismo di archiviazione interno per <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName>. Per altre informazioni su delimitazione e blocco, vedere [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).  
  
## <a name="example"></a>Esempio  
 La classe di raccolta personalizzata è una coda di priorità di base in cui i livelli di priorità sono rappresentati come matrice di oggetti <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>. Nessun ordinamento aggiuntivo viene eseguito all'interno di ogni coda.  
  
 Nel codice client vengono avviate tre attività. La prima attività esegue il polling per le sequenze di tasti che abilitano l'annullamento in qualsiasi momento durante l'esecuzione. La seconda attività è il thread producer. Aggiunge nuovi elementi alla raccolta di blocco e assegna a ogni elemento una priorità basata su un valore casuale. La terza attività rimuove gli elementi dalla raccolta appena diventano disponibili.  
  
 È possibile modificare il comportamento dell'applicazione rendendo uno dei thread più veloce rispetto all'altro. Se il producer viene eseguito più velocemente, si noterà la funzionalità di delimitazione perché la raccolta di blocco impedisce l'aggiunta di elementi se contiene già il numero di elementi specificato nel costruttore. Se il consumer viene eseguito più velocemente, si noterà la funzionalità di blocco perché il consumer aspetta che un nuovo elemento venga aggiunto.  
  
 [!code-csharp[CDS_BlockingCollection#06](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/prodcon.cs#06)]  
  
 Per impostazione predefinita, l'archiviazione di <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> è <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolte thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
