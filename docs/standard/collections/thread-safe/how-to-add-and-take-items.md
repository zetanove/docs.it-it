---
title: "Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection | Microsoft Docs"
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
  - "raccolte thread-safe, dizionario di blocco"
ms.assetid: 38f2f3d8-15e5-4bf4-9c83-2b5b6f22bad1
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection
Questo esempio mostra come aggiungere e rimuovere elementi da un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> bloccando e non bloccando le operazioni. Per altre informazioni su <xref:System.Collections.Concurrent.BlockingCollection%601>, vedere [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).  
  
 Per un esempio su come enumerare un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> finché non risulta vuoto e non verranno aggiunti altri elementi, vedere [Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md)  
  
## Esempio  
 Il primo esempio mostra come aggiungere e rimuovere elementi in modo che da bloccare le operazioni se la raccolta è temporaneamente vuota \(durante la rimozione\), ha raggiunto la capacità massima \(durante l'aggiunta\) oppure quando è trascorso un periodo di timeout specificato. Si noti che il blocco relativo alla capacità massima è abilitato solo quando l'oggetto BlockingCollection è stato creato specificando una capacità massima nel costruttore.  
  
 [!code-csharp[CDS_BlockingCollection#01](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example01.cs#01)]
 [!code-vb[CDS_BlockingCollection#01](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/simpleblocking.vb#01)]  
  
## Esempio  
 Questo secondo esempio mostra come aggiungere e rimuovere elementi in modo da non bloccare le operazioni. Se non è presente alcun elemento, se è stata raggiunta la capacità massima per una raccolta limitata oppure se è trascorso il periodo di timeout, l'operazione <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> o <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> restituisce false. In questo modo si consente al thread di eseguire per un breve periodo altre operazioni utili e quindi, in un secondo momento, provare a recuperare il nuovo elemento o ad aggiungere lo stesso elemento che non è stato possibile aggiungere in precedenza. Il programma illustra inoltre come implementare l'annullamento quando si accede a un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601>.  
  
 [!code-csharp[CDS_BlockingCollection#02](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example02.cs#02)]
 [!code-vb[CDS_BlockingCollection#02](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/nonblockingbc.vb#02)]  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)