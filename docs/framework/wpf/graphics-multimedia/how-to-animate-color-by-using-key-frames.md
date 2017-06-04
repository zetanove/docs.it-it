---
title: "Procedura: animare il colore utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, colori con fotogrammi chiave"
  - "colori, animazione con fotogrammi chiave"
  - "fotogrammi chiave, animazione dei colori"
ms.assetid: ab04ffa6-4de9-4d5b-a3b4-4e35d5b2ef35
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: animare il colore utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzando fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush>.  In questa animazione vengono utilizzati tre fotogrammi chiave nel modo seguente:  
  
1.  Durante i primi due secondi, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearColorKeyFrame> per modificare gradualmente il colore da verde a rosso.  I fotogrammi chiave lineari come <xref:System.Windows.Media.Animation.LinearColorKeyFrame> creano una transizione lineare uniforme tra valori.  
  
2.  Durante la fine del mezzo secondo successivo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> per modificare rapidamente il colore da rosso a giallo.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteColorKeyFrame> creano modifiche improvvise tra valori, ovvero la modifica di colore in questa parte dell'animazione si verifica rapidamente e risulta immediatamente evidente.  
  
3.  Durante i due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplineColorKeyFrame> per cambiare nuovamente il colore, questa volta da giallo in verde.  I fotogrammi chiave [Spline](GTMT) come <xref:System.Windows.Media.Animation.SplineColorKeyFrame> creano una transizione variabile tra i valori a seconda dei valori della proprietà <xref:System.Windows.Media.Animation.SplineColorKeyFrame.KeySpline%2A>.  In questo esempio la modifica di colore inizia lentamente e aumenta di velocità in modo esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-csharp[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/ColorAnimationUsingKeyFramesExample.cs#coloranimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/coloranimationusingkeyframesexample.vb#coloranimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#ColorAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ColorAnimationUsingKeyFramesExample.xaml#coloranimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.SolidColorBrush.Color%2A>   
 <xref:System.Windows.Media.SolidColorBrush>   
 <xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)