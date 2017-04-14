---
title: "Canceling Threads Cooperatively | Microsoft Docs"
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
  - "threads, cancellation"
ms.assetid: d2d6d5fd-e263-4fa0-847b-2fc3e0d82337
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Canceling Threads Cooperatively
Nelle versioni precedenti a [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], .NET Framework non forniva alcun metodo incorporato per annullare un thread in modo cooperativo dopo l'avvio dello stesso. Tuttavia, in [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] è possibile usare i token di annullamento per annullare i thread, nello stesso modo in cui è possibile usarli per annullare oggetti <xref:System.Threading.Tasks.Task?displayProperty=fullName> o query PLINQ. Anche se la classe <xref:System.Threading.Thread?displayProperty=fullName> non offre supporto incorporato per i token di annullamento, è possibile passare un token a una routine del thread usando il costruttore <xref:System.Threading.Thread> che accetta un delegato <xref:System.Threading.ParameterizedThreadStart>. Nell'esempio riportato di seguito viene illustrato come procedere.  
  
 [!code-csharp[Cancellation#14](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/CooperativeThreads.cs#14)]
 [!code-vb[Cancellation#14](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/CooperativeThreads.vb#14)]  
  
## Vedere anche  
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)