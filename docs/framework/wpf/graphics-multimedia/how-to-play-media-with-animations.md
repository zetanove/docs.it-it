---
title: "Procedura: riprodurre contenuto multimediale con animazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "riproduzione di contenuti multimediale, con animazioni"
  - "riproduzione di contenuti multimediali, con animazioni"
  - "animazione, la riproduzione multimediale con"
  - "Media, la riproduzione con animazioni"
ms.assetid: 8982b7b7-1c6c-4b24-8801-b328862975f5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: riprodurre contenuto multimediale con animazioni
In questo esempio viene illustrato come riprodurre contenuto multimediale e animazioni contemporaneamente utilizzando il <xref:System.Windows.Media.MediaTimeline> e <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames> classi nello stesso <xref:System.Windows.Media.Animation.Storyboard>.  
  
## <a name="example"></a>Esempio  
 È possibile utilizzare uno o più <xref:System.Windows.Media.MediaTimeline> gli oggetti in un <xref:System.Windows.Media.Animation.Storyboard> con altri <xref:System.Windows.Media.Animation.Timeline> oggetti, ad esempio animazioni.  
  
 Nell'esempio seguente il <xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A> proprietà del <xref:System.Windows.Media.Animation.Storyboard> su un valore di `Slip`, che specifica che l'animazione solo quando avanza il contenuto multimediale (un video in questo esempio). Questa funzionalità potrebbe essere necessaria se la riproduzione multimediale viene ritardata a causa del tempo di caricamento.  
  
 [!code-xml[MediaGallery_snippet#MediaTimelinePlusAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snippet/CSharp/MediaTimelinePlusAnimationExample.xaml#mediatimelineplusanimationexamplewholepage)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Media.MediaTimeline>   
 <xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 <xref:System.Windows.Media.Animation.ParallelTimeline.SlipBehavior%2A>   
 [Procedure](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Grafica e Multimedia](../../../../docs/framework/wpf/graphics-multimedia/index.md)