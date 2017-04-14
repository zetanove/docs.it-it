---
title: "Procedura: creare e utilizzare un&#39;area di disegno | Microsoft Docs"
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
  - "Canvas (controllo), creazione"
  - "Canvas (controllo), utilizzo"
  - "controlli, Canvas"
ms.assetid: 420b9487-9a15-477c-9489-a22a4dec7779
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: creare e utilizzare un&#39;area di disegno
In questo esempio viene illustrato come creare e utilizzare un'istanza di <xref:System.Windows.Controls.Canvas>.  
  
## Esempio  
 Nell'esempio seguente vengono posizionati in modo esplicito due elementi <xref:System.Windows.Controls.TextBlock> utilizzando i metodi <xref:System.Windows.Controls.Canvas.SetTop%2A> e <xref:System.Windows.Controls.Canvas.SetLeft%2A> di <xref:System.Windows.Controls.Canvas>.  Nell'esempio viene inoltre assegnato il colore `LightSteelBlue` della proprietà <xref:System.Windows.Controls.Control.Background%2A> all'oggetto <xref:System.Windows.Controls.Canvas>.  
  
> [!NOTE]
>  Quando si utilizza [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] per posizionare elementi <xref:System.Windows.Controls.TextBlock>, utilizzare le proprietà <xref:System.Windows.Controls.Canvas.Top%2A> e <xref:System.Windows.Controls.Canvas.Left%2A>.  
  
 [!code-csharp[CanvasCode#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasCode/CSharp/Canvas_Code.cs#1)]
 [!code-vb[CanvasCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasCode/VisualBasic/canvas_vb.vb#1)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.TextBlock>   
 <xref:System.Windows.Controls.Canvas.SetTop%2A>   
 <xref:System.Windows.Controls.Canvas.SetLeft%2A>   
 <xref:System.Windows.Controls.Canvas.Top%2A>   
 <xref:System.Windows.Controls.Canvas.Left%2A>   
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)