---
title: "Procedura: Aggiungere funzionalit&#224; di delimitazione e blocco a una raccolta | Microsoft Docs"
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
  - "raccolte thread-safe, raccolte di blocco personalizzate"
ms.assetid: 4c2492de-3876-4873-b5a1-000bb404d770
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: Aggiungere funzionalit&#224; di delimitazione e blocco a una raccolta
In questo esempio viene illustrato come aggiungere funzionalità di delimitazione e blocco a una classe di raccolte personalizzata implementando l'interfaccia <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=fullName> nella classe e utilizzando quindi un'istanza della classe come meccanismo di archiviazione interno per un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName>.  Per ulteriori informazioni sulla delimitazione e il blocco, vedere [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).  
  
## Esempio  
 La classe di raccolte personalizzata è una coda prioritaria di base in cui i livelli di priorità sono rappresentati sotto forma di matrice di oggetti <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>.  All'interno di ogni coda non vengono eseguiti altri ordinamenti.  
  
 Nel codice client vengono avviate tre attività.  La prima attività esegue semplicemente il polling delle sequenze di tasti per abilitare l'annullamento in qualsiasi momento durante l'esecuzione.  La seconda attività è il thread producer; aggiunge nuovi elementi alla raccolta di blocco e assegna a ogni elemento una priorità in base a un valore casuale.  La terza attività rimuove gli elementi dalla raccolta non appena diventano disponibili.  
  
 È possibile modificare il comportamento dell'applicazione facendo in modo che uno dei thread venga eseguito più velocemente degli altri.  Se il producer viene eseguito più velocemente, si noterà la funzionalità di delimitazione in quanto la raccolta di blocco impedisce l'aggiunta di elementi se già contiene il numero di elementi specificato nel costruttore.  Se il consumer viene eseguito più velocemente, si noterà la funzionalità di blocco in quanto il consumer attende l'aggiunta di un nuovo elemento.  
  
 [!code-csharp[CDS_BlockingCollection#06](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/prodcon.cs#06)]  
  
 Per impostazione predefinita, lo spazio di memorizzazione di un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> è <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName>.  
  
## Vedere anche  
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)