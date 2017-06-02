---
title: "How to: Wrap EAP Patterns in a Task | Microsoft Docs"
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
  - "tasks, how to wrap EAP patterns"
ms.assetid: f11ed467-af2f-4504-8a2e-299a6c36d44e
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Wrap EAP Patterns in a Task
Nell'esempio seguente viene illustrato come esporre una sequenza arbitraria di operazioni asincrone del modello asincrono basato su eventi \(EAP\) come un'unica attività tramite un oggetto <xref:System.Threading.Tasks.TaskCompletionSource%601>.  Nell'esempio viene inoltre mostrato come utilizzare un oggetto <xref:System.Threading.CancellationToken> per richiamare sugli oggetti <xref:System.Net.WebClient> i metodi di annullamento incorporati.  
  
## Esempio  
 [!code-csharp[FromAsync#08](../../../samples/snippets/csharp/VS_Snippets_Misc/fromasync/cs/fromasync.cs#08)]
 [!code-vb[FromAsync#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/fromasync/vb/module1.vb#08)]  
  
## Vedere anche  
 [TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md)