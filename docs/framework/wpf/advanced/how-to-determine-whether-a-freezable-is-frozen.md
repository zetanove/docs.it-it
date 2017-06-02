---
title: "Procedura: determinare se un oggetto Freezable &#232; bloccato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Freezable (oggetti), rilevamento eventuale blocco"
  - "IsFrozen (proprietà)"
ms.assetid: 92e58baa-ee12-4a9e-ac3a-ca458807a8b2
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: determinare se un oggetto Freezable &#232; bloccato
In questo esempio viene illustrato come determinare se un oggetto <xref:System.Windows.Freezable> è bloccato.  Se si tenta di modificare un oggetto <xref:System.Windows.Freezable> bloccato, viene generata un'eccezione <xref:System.InvalidOperationException>.  Per evitare di generare questa eccezione, utilizzare la proprietà <xref:System.Windows.Freezable.IsFrozen%2A> dell'oggetto <xref:System.Windows.Freezable> per determinare se è bloccato.  
  
## Esempio  
 Nell'esempio seguente viene bloccato un oggetto <xref:System.Windows.Media.SolidColorBrush>, che viene quindi testato utilizzando la proprietà <xref:System.Windows.Freezable.IsFrozen%2A> per determinare se è bloccato.  
  
 [!code-csharp[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
 [!code-vb[freezablesample_procedural#CheckIsFrozenExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Freezable>   
 <xref:System.Windows.Freezable.IsFrozen%2A>   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/advanced/base-elements-how-to-topics.md)