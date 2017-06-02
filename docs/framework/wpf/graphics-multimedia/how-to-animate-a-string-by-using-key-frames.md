---
title: "Procedura: animare una stringa utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, stringhe con fotogrammi chiave"
  - "fotogrammi chiave, animazione di stringhe"
  - "stringhe, animazione con fotogrammi chiave"
ms.assetid: c62bc9fd-c09a-4227-bce0-0a1ab82049dd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: animare una stringa utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare una stringa, che in questo caso corrisponde alla proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un controllo <xref:System.Windows.Controls.Button>, utilizzando i fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames> per animare la proprietà <xref:System.Windows.Controls.ContentControl.Content%2A> di un oggetto <xref:System.Windows.Controls.Button>.  
  
 Tutti i fotogrammi chiave di questo esempio utilizzano un'istanza della classe <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame> perché un'animazione di stringa creata con fotogrammi chiave può utilizzare solo fotogrammi chiave discreti.  I fotogrammi chiave discreti come <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame> creano salti improvvisi tra valori, ovvero le modifiche dell'animazione si verificano rapidamente e risultano immediatamente evidenti.  
  
 [!code-xml[keyframes_snip#StringAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/StringAnimationUsingKeyFramesExample.xaml#stringanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>   
 <xref:System.Windows.Controls.ContentControl.Content%2A>   
 <xref:System.Windows.Controls.Button>   
 <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)