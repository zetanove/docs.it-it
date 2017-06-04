---
title: "Procedura: animare un rettangolo utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, RectangleGeometry (oggetti con fotogrammi chiave)"
  - "fotogrammi chiave, animazione di oggetti RectangleGeometry"
  - "RectangleGeometry (oggetti), animazione con fotogrammi chiave"
ms.assetid: a8b45ceb-0e32-4ba1-928f-df6d30db17c6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: animare un rettangolo utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare la proprietà <xref:System.Windows.Media.RectangleGeometry.Rect%2A> di un oggetto <xref:System.Windows.Media.RectangleGeometry> utilizzando fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.RectangleGeometry.Rect%2A> di un oggetto <xref:System.Windows.Media.RectangleGeometry>.  In questa animazione vengono utilizzati tre fotogrammi chiave nel modo seguente:  
  
1.  Durante i primi due secondi, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearRectKeyFrame> per animare una modifica graduale nella posizione, nella larghezza e nell'altezza di un rettangolo.  I fotogrammi chiave lineari come <xref:System.Windows.Media.Animation.LinearRectKeyFrame> creano una transizione lineare uniforme tra valori.  
  
2.  Durante la fine del mezzo secondo successivo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> per ridurre rapidamente l'altezza del rettangolo.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteRectKeyFrame> creano modifiche improvvise tra valori, ovvero la riduzione dell'altezza si verifica rapidamente e risulta immediatamente evidente.  
  
3.  Durante i due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplineRectKeyFrame> per ripristinare le dimensioni e la posizione di origine del rettangolo.  I fotogrammi chiave [Spline](GTMT) come <xref:System.Windows.Media.Animation.SplineRectKeyFrame> creano una transizione variabile tra i valori a seconda dei valori della proprietà <xref:System.Windows.Media.Animation.SplineRectKeyFrame.KeySpline%2A>.  In questo esempio la modifica inizia lentamente e aumenta di velocità in modo esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-csharp[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/RectAnimationUsingKeyFramesExample.cs#rectanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/rectanimationusingkeyframesexample.vb#rectanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#RectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/RectAnimationUsingKeyFramesExample.xaml#rectanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.RectangleGeometry>   
 <xref:System.Windows.Media.RectangleGeometry.Rect%2A>   
 <xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)