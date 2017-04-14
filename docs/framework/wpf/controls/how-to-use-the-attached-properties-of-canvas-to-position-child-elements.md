---
title: "Procedura: utilizzare le propriet&#224; associate di un&#39;area di disegno per posizionare gli elementi figlio | Microsoft Docs"
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
  - "proprietà associate [Progettazione WPF]"
  - "Canvas (controllo), proprietà associate"
ms.assetid: 48f1d25d-3820-4107-a4cc-d6c1e5664a44
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: utilizzare le propriet&#224; associate di un&#39;area di disegno per posizionare gli elementi figlio
In questo esempio viene illustrato come utilizzare le [proprietà connesse](GTMT) di <xref:System.Windows.Controls.Canvas> per posizionare elementi figlio.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono aggiunti quattro elementi <xref:System.Windows.Controls.Button> come elementi figlio di un oggetto <xref:System.Windows.Controls.Canvas> padre.  Ogni elemento figlio rappresenta una proprietà associata distinta di <xref:System.Windows.Controls.Canvas>: <xref:System.Windows.Controls.Canvas.Bottom%2A>, <xref:System.Windows.Controls.Canvas.Left%2A>, <xref:System.Windows.Controls.Canvas.Right%2A> e <xref:System.Windows.Controls.Canvas.Top%2A>.  Ogni oggetto <xref:System.Windows.Controls.Button> viene posizionato in relazione all'oggetto <xref:System.Windows.Controls.Canvas> padre e in base al valore di proprietà assegnato.  
  
 [!code-cpp[CanvasAttachedProperties#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/CanvasAttachedProperties/CPP/CanvasAttachedProps.cpp#1)]
 [!code-csharp[CanvasAttachedProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasAttachedProperties/CSharp/CanvasAttachedProps.cs#1)]
 [!code-vb[CanvasAttachedProperties#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasAttachedProperties/VisualBasic/CanvasAttachedProps.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.Canvas.Bottom%2A>   
 <xref:System.Windows.Controls.Canvas.Left%2A>   
 <xref:System.Windows.Controls.Canvas.Right%2A>   
 <xref:System.Windows.Controls.Canvas.Top%2A>   
 <xref:System.Windows.Controls.Button>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)   
 [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)