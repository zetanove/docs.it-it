---
title: "Procedura: animare la posizione di un oggetto utilizzando PointAnimation | Microsoft Docs"
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
  - "animazione, PointAnimation"
  - "classi, PointAnimation"
  - "grafica [WPF], animazione"
  - "PointAnimation (classe)"
ms.assetid: 42310977-cc90-438a-8a47-0345898e01be
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: animare la posizione di un oggetto utilizzando PointAnimation
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.Animation.PointAnimation> per animare un oggetto lungo un oggetto <xref:System.Windows.Shapes.Path>.  
  
## Esempio  
 Nell'esempio riportato di seguito un'ellisse viene spostata lungo un oggetto <xref:System.Windows.Shapes.Path> da un punto dello schermo a un altro.  Nell'esempio la posizione di un oggetto <xref:System.Windows.Media.EllipseGeometry> viene animata utilizzando <xref:System.Windows.Media.Animation.PointAnimation> per animare la proprietà <xref:System.Windows.Media.EllipseGeometry.Center%2A>.  
  
 [!code-csharp[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/PointAnimationExample.cs#pointanimationwholepage)]
 [!code-vb[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/PointAnimationExample.vb#pointanimationwholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.PointAnimation>   
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.EllipseGeometry>   
 <xref:System.Windows.Media.EllipseGeometry.Center%2A>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Grafica e funzionalità multimediali](../../../../docs/framework/wpf/graphics-multimedia/index.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/graphics-how-to-topics.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)