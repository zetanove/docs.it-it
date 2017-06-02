---
title: "Procedura: animare un valore Boolean utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, valori booleani con fotogrammi chiave"
  - "valori booleani, animazione con fotogrammi chiave"
  - "fotogrammi chiave, animazione di valori booleani"
ms.assetid: 4b0fac96-6231-4fcf-9775-4dd673ddc785
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: animare un valore Boolean utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare il valore della proprietà booleana di un controllo <xref:System.Windows.Controls.Button> utilizzando fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.UIElement.IsEnabled%2A> di un controllo <xref:System.Windows.Controls.Button>.  In tutti i fotogrammi chiave di questo esempio viene utilizzata un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame>.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteBooleanKeyFrame> creano salti improvvisi tra valori, con il risultato di un movimento dell'animazione a scatti.  
  
 [!code-csharp[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/BooleanAnimationUsingKeyFramesExample.cs#booleananimationusingkeyframeswholepage)]
 [!code-vb[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/booleananimationusingkeyframesexample.vb#booleananimationusingkeyframeswholepage)]
 [!code-xml[keyframes_snip#BooleanAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/BooleanAnimationUsingKeyFramesExample.xaml#booleananimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>   
 <xref:System.Windows.UIElement.IsEnabled%2A>   
 <xref:System.Windows.Controls.Button>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)