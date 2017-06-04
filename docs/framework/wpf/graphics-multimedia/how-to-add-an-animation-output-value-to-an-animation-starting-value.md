---
title: "Procedura: aggiungere un valore di output dell&#39;animazione a un valore iniziale dell&#39;animazione | Microsoft Docs"
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
  - "animazione"
  - "IsAdditive (proprietà)"
ms.assetid: b89a82be-b03d-481e-a8d3-cc513d09ca00
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Procedura: aggiungere un valore di output dell&#39;animazione a un valore iniziale dell&#39;animazione
In questo esempio viene illustrato come aggiungere un valore di output dell'animazione a un valore iniziale dell'animazione.  
  
## Esempio  
 La proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> specifica se si desidera che il valore di output di un'animazione venga aggiunto al valore iniziale \(valore di base\) di una proprietà animata.  È possibile utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A> con la maggior parte delle animazioni di base e con la maggior parte delle animazioni con fotogrammi chiave.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) e [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
 Nell'esempio seguente è illustrato l'effetto dell'utilizzo della proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsAdditive%2A?displayProperty=fullName> con <xref:System.Windows.Media.Animation.DoubleAnimation> e dell'utilizzo della proprietà <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsAdditive%2A?displayProperty=fullName> con <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>.  
  
 [!code-xml[timingbehaviors_snip#IsAdditiveWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsAdditiveExample.xaml#isadditivewholepage)]  
  
## Vedere anche  
 [Accumulare valori di animazione durante i cicli ripetuti](../../../../docs/framework/wpf/graphics-multimedia/how-to-accumulate-animation-values-during-repeat-cycles.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Animation and Timing](http://msdn.microsoft.com/it-it/7d83765b-d5ae-41b1-b423-80206e1124aa)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)