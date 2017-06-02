---
title: "Procedura: animare una propriet&#224; utilizzando un oggetto AnimationClock | Microsoft Docs"
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
  - "animazione, proprietà, con AnimationClocks"
  - "AnimationClocks"
ms.assetid: e6542021-714c-4675-9567-04f1c7380834
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: animare una propriet&#224; utilizzando un oggetto AnimationClock
In questo esempio viene mostrato come utilizzare oggetti <xref:System.Windows.Media.Animation.Clock> per aggiungere un'animazione a una proprietà.  
  
 Esistono tre modi per aggiungere un'animazione a una [proprietà di dipendenza](GTMT):  
  
-   Creare un oggetto <xref:System.Windows.Media.Animation.AnimationTimeline> e associarlo a quella proprietà utilizzando un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  
  
-   Utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> dell'oggetto per applicare un singolo oggetto <xref:System.Windows.Media.Animation.AnimationTimeline> a una proprietà di destinazione.  
  
-   Creare un oggetto <xref:System.Windows.Media.Animation.AnimationClock> da un oggetto <xref:System.Windows.Media.Animation.AnimationTimeline> e applicarlo a una proprietà.  
  
 Gli oggetti <xref:System.Windows.Media.Animation.Storyboard> e il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> consentono di animare le proprietà senza creare e distribuire orologi in modo diretto \(ad esempio, vedere [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md) and [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)\); gli orologi vengono creati e distribuiti automaticamente.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto <xref:System.Windows.Media.Animation.AnimationClock> e come applicarlo a due proprietà simili.  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 Per un esempio in cui sia illustrato come controllare un oggetto <xref:System.Windows.Media.Animation.Clock> in modo interattivo una volta avviato, vedere [Controllare in modo interattivo un oggetto Clock](../../../../docs/framework/wpf/graphics-multimedia/how-to-interactively-control-a-clock.md).  
  
## Vedere anche  
 [Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [Animare una proprietà senza utilizzare uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md)   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)