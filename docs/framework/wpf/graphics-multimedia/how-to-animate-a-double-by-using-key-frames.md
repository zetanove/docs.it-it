---
title: "Procedura: animare un oggetto Double utilizzando i fotogrammi chiave | Microsoft Docs"
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
  - "animazione, valori doppi con fotogrammi chiave"
  - "Doppi, animazione con fotogrammi chiave"
  - "fotogrammi chiave, animazione di valori doppi"
ms.assetid: 3a1a7dba-7694-4907-8a2f-3408baebfa82
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: animare un oggetto Double utilizzando i fotogrammi chiave
In questo esempio viene illustrato come animare il valore di una proprietà che accetta un oggetto <xref:System.Double> utilizzando frame chiave.  
  
## Esempio  
 Nell'esempio riportato di seguito viene spostato un rettangolo attraverso una schermata.  Nell'esempio viene utilizzata la classe <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> di un oggetto <xref:System.Windows.Media.TranslateTransform> applicata a un oggetto <xref:System.Windows.Shapes.Rectangle>.  Questa animazione, che viene ripetuta all'infinito, utilizza tre frame chiave nel modo seguente:  
  
1.  Durante i primi tre secondi, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame> per spostare il rettangolo lungo un percorso a una velocità costante dalla posizione iniziale alla posizione 500.  I frame chiave lineari come <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame> creano una transizione lineare uniforme tra valori.  
  
2.  Alla fine del quarto secondo, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame> per spostare improvvisamente il rettangolo alla posizione successiva.  I frame chiave discreti come <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame> creano salti improvvisi tra valori.  In questo esempio, il rettangolo si trova nella posizione iniziale, quindi viene improvvisamente visualizzato nella posizione 500.  
  
3.  Nei due secondi finali, viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> per riportare il rettangolo nella posizione iniziale.  I fotogrammi chiave [Spline](GTMT) come <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame> creano una transizione variabile tra i valori a seconda del valore della proprietà <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A>.  In questo esempio, il rettangolo inizia a spostarsi lentamente, quindi accelera in modo esponenziale verso la fine dell'intervallo di tempo.  
  
 [!code-csharp[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/AltDoubleAnimationUsingKeyFramesExample.cs#altdoubleanimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/altdoubleanimationusingkeyframesexample.vb#altdoubleanimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#AltDoubleAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/AltDoubleAnimationUsingKeyFramesExample.xaml#altdoubleanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
 Per coerenza con altri esempi di animazione, nelle versioni del codice di questo esempio viene utilizzato un oggetto <xref:System.Windows.Media.Animation.Storyboard> per applicare l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>.  In alternativa, quando si applica una sola animazione al codice, è più semplice utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>, anziché un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  Per un esempio, vedere [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>   
 <xref:System.Windows.Shapes.Rectangle>   
 <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>   
 <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>   
 <xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)