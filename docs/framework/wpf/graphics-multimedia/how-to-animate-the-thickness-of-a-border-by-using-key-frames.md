---
title: "Procedura: animare lo spessore di un bordo utilizzando frame chiave | Microsoft Docs"
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
  - "animazione, spessore del bordo con fotogrammi chiave"
  - "spessore del bordo, animazione con fotogrammi chiave"
  - "fotogrammi chiave, animazione dello spesso del bordo"
ms.assetid: 3a9cb463-0a63-407d-aae7-3fbb1a559947
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: animare lo spessore di un bordo utilizzando frame chiave
In questo esempio viene illustrato come animare la proprietà <xref:System.Windows.Controls.Control.BorderThickness%2A> di un oggetto <xref:System.Windows.Controls.Border>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzata la classe <xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Controls.Control.BorderThickness%2A> di un oggetto <xref:System.Windows.Controls.Border>.  In questa animazione vengono utilizzati tre fotogrammi chiave nel modo seguente:  
  
1.  Durante il primo mezzo secondo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> per aumentare gradualmente lo spessore del bordo.  Nell'esempio viene utilizzato l'oggetto <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame> per creare un aumento lineare uniforme tra valori.  
  
2.  Alla fine del mezzo secondo successivo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> per aumentare improvvisamente lo spessore del bordo.  Fotogrammi chiave discreti come quello derivato dall'oggetto <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame> creano salti improvvisi tra valori, con il risultato di un movimento dell'animazione a scatti.  
  
3.  Durante i due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> per ridurre lo spessore del bordo.  I fotogrammi chiave [Spline](GTMT) come quelli derivati da <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame> creano una transizione variabile tra i valori a seconda dei valori della proprietà <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame.KeySpline%2A>.  In questo frame chiave, l'animazione si avvia lentamente e accelera esponenzialmente verso la fine dell'intervallo di tempo.  
  
 [!code-xml[keyframes_snip#ThicknessAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ThicknessAnimationUsingKeyFramesExample.xaml#thicknessanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.LinearThicknessKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteThicknessKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineThicknessKeyFrame>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)   
 [Animare un valore BorderThickness](../../../../docs/framework/wpf/controls/how-to-animate-a-borderthickness-value.md)