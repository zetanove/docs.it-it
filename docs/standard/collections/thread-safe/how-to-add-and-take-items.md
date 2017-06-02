---
title: 'Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection | Microsoft Docs'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, blocking dictionary
ms.assetid: 38f2f3d8-15e5-4bf4-9c83-2b5b6f22bad1
caps.latest.revision: 7
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 442e2f9a80c4c0624c90e8a7509cd22f6be9a4a0
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-add-and-take-items-individually-from-a-blockingcollection"></a>Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection
In questo esempio viene illustrato come aggiungere e rimuovere elementi da un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> in modo bloccante e non bloccante. Per scoprire di più su <xref:System.Collections.Concurrent.BlockingCollection%601>, vedere [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).  
  
 Per un esempio su come enumerare un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601> finché non sarà vuoto e non verranno aggiunti altri elementi, vedere [Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md).  
  
## <a name="example"></a>Esempio  
 Il primo esempio mostra come aggiungere e rimuovere elementi in modo che da bloccare le operazioni se la raccolta è temporaneamente vuota (durante la rimozione), ha raggiunto la capacità massima (durante l'aggiunta) oppure quando è trascorso un periodo di timeout specificato. Si noti che il blocco relativo alla capacità massima è abilitato solo quando l'oggetto BlockingCollection è stato creato specificando una capacità massima nel costruttore.  
  
 [!code-csharp[CDS_BlockingCollection#01](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example01.cs#01)]
 [!code-vb[CDS_BlockingCollection#01](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/simpleblocking.vb#01)]  
  
## <a name="example"></a>Esempio  
 Questo secondo esempio mostra come aggiungere e rimuovere elementi in modo da non bloccare le operazioni. Se non è presente alcun elemento o è stata raggiunta la capacità massima in un insieme limitato oppure è trascorso il periodo di timeout, l'operazione <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> o <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> restituirà false. In questo modo si consente al thread di eseguire per un breve periodo altre operazioni utili e quindi, in un secondo momento, provare a recuperare il nuovo elemento o ad aggiungere lo stesso elemento che non è stato possibile aggiungere in precedenza. Il programma illustra anche come implementare l'annullamento quando si accede a un oggetto <xref:System.Collections.Concurrent.BlockingCollection%601>.  
  
 [!code-csharp[CDS_BlockingCollection#02](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example02.cs#02)]
 [!code-vb[CDS_BlockingCollection#02](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/nonblockingbc.vb#02)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)
