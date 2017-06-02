---
title: "Procedura: animare un punto utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, punti con fotogrammi chiave"
  - "fotogrammi chiave, animazione di punti"
  - "punti, animazione con fotogrammi chiave"
ms.assetid: d2e2ef10-0773-4133-856e-d41c09f60ded
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: animare un punto utilizzando fotogrammi chiave
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> per animare un oggetto <xref:System.Windows.Point>.  
  
## Esempio  
 Nell'esempio seguente viene spostata un'ellisse lungo un percorso triangolare.  Viene utilizzata la classe <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.EllipseGeometry.Center%2A> di un oggetto <xref:System.Windows.Media.EllipseGeometry>.  In questa animazione vengono utilizzati tre fotogrammi chiave nel modo seguente:  
  
1.  Durante il primo mezzo secondo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearPointKeyFrame> per spostare l'ellisse lungo un percorso a una velocità costante dalla posizione iniziale.  I fotogrammi chiave lineari come <xref:System.Windows.Media.Animation.LinearPointKeyFrame> creano un'interpolazione lineare uniforme tra valori.  
  
2.  Durante la fine del mezzo secondo successivo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> per spostare rapidamente l'ellisse lungo il percorso alla posizione successiva.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscretePointKeyFrame> creano salti improvvisi tra valori.  
  
3.  Durante i due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplinePointKeyFrame> per riportare l'ellisse nella posizione iniziale.  I fotogrammi chiave [Spline](GTMT) come <xref:System.Windows.Media.Animation.SplinePointKeyFrame> creano una transizione variabile tra i valori a seconda dei valori della proprietà <xref:System.Windows.Media.Animation.SplinePointKeyFrame.KeySpline%2A>.  In questo esempio l'animazione inizia lentamente e aumenta di velocità in modo esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-csharp[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/PointAnimationUsingKeyFramesExample.cs#pointanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/pointanimationusingkeyframesexample.vb#pointanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#PointAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/PointAnimationUsingKeyFramesExample.xaml#pointanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
 Per coerenza con altri esempi di animazione, nelle versioni del codice di questo esempio viene utilizzato un oggetto <xref:System.Windows.Media.Animation.Storyboard> per applicare <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>.  Tuttavia, quando si applica una sola animazione nel codice, è più conveniente utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> anziché un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  Per un esempio, vedere [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.EllipseGeometry.Center%2A?displayProperty=fullName>   
 <xref:System.Windows.Media.EllipseGeometry>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)