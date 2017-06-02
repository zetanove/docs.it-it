---
title: "Procedura: animare un oggetto utilizzando fotogrammi chiave | Microsoft Docs"
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
  - "animazione, oggetti con fotogrammi chiave"
  - "fotogrammi chiave, animazione di oggetti"
ms.assetid: b1f15ba9-cac7-4cea-8699-5c6b55c05c5e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: animare un oggetto utilizzando fotogrammi chiave
In questo esempio viene illustrato come animare un oggetto, che in questo caso corrisponde alla proprietà <xref:System.Windows.Controls.Page.Background%2A> di un controllo <xref:System.Windows.Controls.Page>, utilizzando i fotogrammi chiave.  
  
## Esempio  
 Nell'esempio seguente viene utilizzata la classe <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> per animare le modifiche di colore per la proprietà <xref:System.Windows.Controls.Page.Background%2A> di un controllo <xref:System.Windows.Controls.Page>.  L'animazione passa a un pennello di sfondo diverso a intervalli regolari.  Viene utilizzata la classe <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> per creare tre fotogrammi chiave diversi.  I fotogrammi chiave vengono utilizzati nel modo seguente:  
  
1.  Alla fine del primo secondo viene animata un'istanza della classe <xref:System.Windows.Media.LinearGradientBrush>.  In questa sezione dell'esempio viene applicata una sfumatura lineare al colore di sfondo in modo che passi dal giallo all'arancione al rosso.  
  
2.  Alla fine del secondo successivo viene animata un'istanza della classe <xref:System.Windows.Media.RadialGradientBrush>.  In questa sezione dell'esempio viene applicata una sfumatura radiale al colore di sfondo in modo che passi dal bianco al blu al nero.  
  
3.  Alla fine del terzo secondo viene animata un'istanza della classe <xref:System.Windows.Media.DrawingBrush>.  In questa sezione dell'esempio viene applicato un motivo a scacchiera allo sfondo.  
  
4.  L'animazione inizia di nuovo e si ripete all'infinito.  
  
> [!NOTE]
>  <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> è l'unico tipo di fotogramma chiave che è possibile utilizzare con la classe <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>.  I fotogrammi chiave come <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> creano modifiche improvvise nei valori, ovvero le modifiche di colore di questo esempio si verificano all'improvviso.  
  
 [!code-xml[keyframes_snip#ObjectAnimationUsingKeyFramesWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ObjectAnimationUsingKeyFramesExample.xaml#objectanimationusingkeyframeswholepage)]  
  
 Per l'esempio completo, vedere [Esempio di animazione con fotogrammi chiave](http://go.microsoft.com/fwlink/?LinkID=160012) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>   
 <xref:System.Windows.Controls.Page.Background%2A>   
 <xref:System.Windows.Controls.Page>   
 <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>   
 <xref:System.Windows.Media.LinearGradientBrush>   
 <xref:System.Windows.Media.RadialGradientBrush>   
 <xref:System.Windows.Media.DrawingBrush>   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)