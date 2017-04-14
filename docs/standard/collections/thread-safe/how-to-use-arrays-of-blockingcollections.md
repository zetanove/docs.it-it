---
title: "Procedura: utilizzare matrici di raccolte di blocco in una pipeline | Microsoft Docs"
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
  - "raccolte thread-safe, raccolte di blocco nella pipeline"
ms.assetid: a39c7ec3-3ad7-4f4d-8fe4-b3e9dbabe2ed
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: utilizzare matrici di raccolte di blocco in una pipeline
Nell'esempio seguente viene illustrato come utilizzare matrici di oggetti <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> con metodi statici quali <xref:System.Collections.Concurrent.BlockingCollection%601.TryAddToAny%2A> e <xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny%2A> per implementare un trasferimento di dati rapido e flessibile tra componenti.  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione della pipeline di base in cui ogni oggetto preleva simultaneamente dati dalla raccolta di input, li trasforma e li passa alla raccolta di output.  
  
 [!code-csharp[CDS_BlockingCollection#07](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example07.cs#07)]
 [!code-vb[CDS_BlockingCollection#07](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/bcpipeline.vb#07)]  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)