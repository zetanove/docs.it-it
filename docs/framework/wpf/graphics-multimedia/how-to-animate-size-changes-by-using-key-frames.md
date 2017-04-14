---
title: "Procedura: animare le modifiche di dimensione utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, modifica delle dimensioni con i fotogrammi chiave"
  - "fotogrammi chiave, animazione della modifica delle dimensioni"
  - "modifiche alle dimensioni, animazione con fotogrammi chiave"
ms.assetid: 86bd2950-d4c9-4ec4-aa8d-7dc3ccadded4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: animare le modifiche di dimensione utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare le modifiche di dimensione utilizzando i fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.ArcSegment.Size%2A> di un oggetto <xref:System.Windows.Media.ArcSegment>.  In questa animazione vengono utilizzati tre fotogrammi chiave nel modo seguente:  
  
1.  Durante il primo mezzo secondo dell'animazione, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> per aumentare gradualmente la dimensione dell'arco.  I fotogrammi chiave lineari come <xref:System.Windows.Media.Animation.LinearSizeKeyFrame> creano una transizione lineare uniforme tra valori.  
  
2.  Alla fine del mezzo secondo successivo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> per aumentare rapidamente la dimensione dell'arco.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame> creano salti improvvisi tra valori, ovvero le modifiche di dimensione si verificano improvvisamente e risultano immediatamente evidenti.  
  
3.  Durante i due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> per aumentare la dimensione dell'arco.  I fotogrammi chiave [Spline](GTMT) come <xref:System.Windows.Media.Animation.SplineSizeKeyFrame> creano una transizione variabile tra i valori a seconda dei valori della proprietà <xref:System.Windows.Media.Animation.SplineSizeKeyFrame.KeySpline%2A>.  In questo esempio la dimensione dell'arco aumenta lentamente all'inizio e quindi in modo esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-xml[keyframes_snip#SizeAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/SizeAnimationUsingKeyFramesExample.xaml#sizeanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.ArcSegment.Size%2A>   
 <xref:System.Windows.Media.ArcSegment>   
 <xref:System.Windows.Media.Animation.LinearSizeKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteSizeKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineSizeKeyFrame>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)