---
title: "Procedura: accumulare valori di animazione durante i cicli ripetuti | Microsoft Docs"
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
  - "accumulazione di valori di animazione durante i cicli ripetuti"
  - "animazione, accumulazione di valori durante i cicli ripetuti"
ms.assetid: 548df369-c7cc-4dab-b569-08b95ced2e7e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Procedura: accumulare valori di animazione durante i cicli ripetuti
In questo esempio viene illustrato come utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> per accumulare valori di animazione nei cicli ripetuti.  
  
## Esempio  
 Utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> per accumulare valori di base di un'animazione nei cicli ripetuti.  Ad esempio, se si imposta la ripetizione di un'animazione per 9 volte \(<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> \= "9x"\) e si imposta la proprietà da animare tra 10 e 15 \(Da \= 10 A \= 15\), la proprietà viene animata da 10 a 15 durante il primo ciclo, da 15 a 20 durante il secondo ciclo, da 20 a 25 durante il terzo ciclo e così via.  Di conseguenza, ogni ciclo di animazione utilizza il valore dell'animazione finale del ciclo di animazione precedente come valore di base.  
  
 È possibile utilizzare la proprietà `IsCumulative` con la maggior parte delle animazioni di base e delle animazioni con fotogrammi chiave.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md) e [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
 Nell'esempio riportato di seguito viene illustrato questo comportamento tramite l'animazione della larghezza di quattro rettangoli.  Esempio:  
  
-   Viene animato il primo rettangolo con <xref:System.Windows.Media.Animation.DoubleAnimation> e viene impostata la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> su `true`.  
  
-   Viene animato il secondo rettangolo con <xref:System.Windows.Media.Animation.DoubleAnimation> e viene impostata la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A> sul valore predefinito di `false`.  
  
-   Viene animato il terzo rettangolo con <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> e viene impostata la proprietà <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> su `true`.  
  
-   Viene animato l'ultimo rettangolo con <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> e viene impostata la proprietà <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A> su `false`.  
  
 [!code-xml[timingbehaviors_snip#IsCumulativeWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsCumulativeExample.xaml#iscumulativewholepage)]  
  
## Vedere anche  
 [Aggiungere un valore di output dell'animazione a un valore iniziale dell'animazione](../../../../docs/framework/wpf/graphics-multimedia/how-to-add-an-animation-output-value-to-an-animation-starting-value.md)   
 [Ripetere un'animazione](../../../../docs/framework/wpf/graphics-multimedia/how-to-repeat-an-animation.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)