---
title: 'Procedura: utilizzare matrici di raccolte di blocco in una pipeline | Documenti di Microsoft'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, blocking collections in pipeline
ms.assetid: a39c7ec3-3ad7-4f4d-8fe4-b3e9dbabe2ed
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 234dfa6a3a905b9db53ae8699bbe1c62f3411184
ms.lasthandoff: 04/18/2017

---
# <a name="how-to-use-arrays-of-blocking-collections-in-a-pipeline"></a>Procedura: utilizzare matrici di raccolte di blocco in una pipeline
Nell'esempio seguente viene illustrato come usare matrici di oggetti <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> con metodi statici, ad esempio <xref:System.Collections.Concurrent.BlockingCollection%601.TryAddToAny%2A> e <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%2A> per implementare il trasferimento dati rapido e flessibile tra componenti.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente illustra un'implementazione della pipeline di base in cui ogni oggetto preleva simultaneamente dati dalla raccolta di input, li trasforma e li passa alla raccolta di output.  
  
 [!code-csharp[CDS_BlockingCollection#07](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example07.cs#07)]
 [!code-vb[CDS_BlockingCollection#07](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/bcpipeline.vb#07)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
