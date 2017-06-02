---
title: "How to: Traverse a Binary Tree with Parallel Tasks | Microsoft Docs"
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
  - "tasks, how to traverse a tree"
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Traverse a Binary Tree with Parallel Tasks
Nell'esempio seguente vengono mostrati due modi in cui è possibile utilizzare attività parallele per attraversare una struttura di dati ad albero.  La creazione della struttura ad albero stessa viene lasciata come esercizio.  
  
## Esempio  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 I due metodi mostrati sono equivalenti dal punto di vista funzionale.  Se si utilizza il metodo <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> per creare ed eseguire le attività, si riceve da queste un handle utilizzabile per restare in attesa delle attività e gestire le eccezioni.  
  
## Vedere anche  
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)