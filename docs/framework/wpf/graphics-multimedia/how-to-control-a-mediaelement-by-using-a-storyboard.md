---
title: "Procedura: controllare un MediaElement utilizzando uno storyboard | Microsoft Docs"
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
  - "controllo della riproduzione di contenuti multimediali, con gli storyboard"
  - "supporto, controllo della riproduzione con gli storyboard"
  - "elementi multimediali, controllo della riproduzione di contenuti multimediali con gli storyboard"
  - "riproduzione di contenuti multimediali, controllo con gli storyboard"
  - "Storyboard, controllo della riproduzione di contenuti multimediali"
ms.assetid: 6128ca77-b826-4e36-b968-6f237157c543
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: controllare un MediaElement utilizzando uno storyboard
In questo esempio viene illustrato come controllare un oggetto <xref:System.Windows.Controls.MediaElement> utilizzando un oggetto <xref:System.Windows.Media.MediaTimeline> in un oggetto <xref:System.Windows.Media.Animation.Storyboard>.  
  
## Esempio  
 Quando si utilizza un oggetto <xref:System.Windows.Media.MediaTimeline> in un oggetto <xref:System.Windows.Media.Animation.Storyboard> per controllare i tempi di un oggetto <xref:System.Windows.Controls.MediaElement>, la funzionalità è identica alla funzionalità di altri oggetti <xref:System.Windows.Media.Animation.Timeline>, ad esempio le animazioni.  Ad esempio, un oggetto <xref:System.Windows.Media.MediaTimeline> utilizza proprietà <xref:System.Windows.Media.Animation.Timeline> come la proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> per specificare quando avviare un oggetto <xref:System.Windows.Controls.MediaElement> \(avvio della riproduzione di contenuti multimediali\).  Viene inoltre utilizzata la proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> per specificare per quanto tempo rimane attivo l'oggetto <xref:System.Windows.Controls.MediaElement> \(durata della riproduzione di contenuti multimediali\).  Per ulteriori informazioni sull'utilizzo degli oggetti <xref:System.Windows.Media.Animation.Timeline> con un oggetto <xref:System.Windows.Media.Animation.Storyboard>, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
 In questo esempio viene illustrato come creare un semplice lettore multimediale che utilizza un oggetto <xref:System.Windows.Media.MediaTimeline> per controllare la riproduzione.  Il lettore multimediale include i pulsanti per riprodurre, mettere in pausa, riprendere e arrestare l'esecuzione.  Il lettore dispone anche di un controllo <xref:System.Windows.Controls.Slider> che può essere utilizzato come indicatore di stato.  
  
 Nell'esempio riportato di seguito viene creata l'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] per il lettore multimediale.  
  
 [!code-xml[MediaGallery_snip#MediaTimelineExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml#mediatimelineexamplewholepage)]  
  
 Nell'esempio riportato di seguito viene creata la funzionalità per l'indicatore di stato.  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaTimelineExample.xaml.cs#codebehindmediatimelineexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaTimelineExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaTimelineExample.xaml.vb#codebehindmediatimelineexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Controls.MediaElement>   
 <xref:System.Windows.Media.MediaTimeline>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [Controllare un oggetto MediaElement \(riproduzione, sospensione, interruzione, volume e velocità\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)   
 [Grafica e funzionalità multimediali](../../../../docs/framework/wpf/graphics-multimedia/index.md)