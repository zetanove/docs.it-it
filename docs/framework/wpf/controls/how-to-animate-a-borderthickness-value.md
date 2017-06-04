---
title: "Procedura: animare un valore BorderThickness | Microsoft Docs"
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
  - "animazione, modifiche dello spessore del bordo"
  - "spessore del bordo, animazione delle modifiche"
ms.assetid: fd021978-f74b-4e7b-a7f7-3987dcad9e0f
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: animare un valore BorderThickness
In questo esempio viene illustrato come animare le modifiche apportate allo spessore di un bordo utilizzando la classe <xref:System.Windows.Media.Animation.ThicknessAnimation>.  
  
## Esempio  
 Nell'esempio seguente viene animato lo spessore di un bordo utilizzando <xref:System.Windows.Media.Animation.ThicknessAnimation>.  Viene utilizzata la proprietà <xref:System.Windows.Controls.Border.BorderThickness%2A> di <xref:System.Windows.Controls.Border>.  
  
 [!code-csharp[BasicAnimations_snip#ThicknessAnimationWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/ThicknessAnimationExample.cs#thicknessanimationwholepage)]
 [!code-vb[BasicAnimations_snip#ThicknessAnimationWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/ThicknessAnimationExample.vb#thicknessanimationwholepage)]  
  
 Per l'esempio completo, vedere [Raccolta di esempi di animazioni](http://go.microsoft.com/fwlink/?LinkID=159969) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.ThicknessAnimation>   
 <xref:System.Windows.Controls.Border.BorderThickness%2A>   
 <xref:System.Windows.Controls.Border>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [Animare lo spessore di un bordo utilizzando i fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-the-thickness-of-a-border-by-using-key-frames.md)