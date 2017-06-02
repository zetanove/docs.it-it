---
title: "Procedura: controllare un oggetto MediaElement (Play, Pause, Stop, Volume e Speed) | Microsoft Docs"
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
  - "controllo della riproduzione di contenuti multimediali"
  - "supporto, controllo della riproduzione"
  - "elementi multimediali, controllo della riproduzione di contenuti multimediali"
  - "riproduzione di contenuti multimediali, controllo"
ms.assetid: 6885a730-e054-4c16-8c1e-ffe17b1f7c32
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: controllare un oggetto MediaElement (Play, Pause, Stop, Volume e Speed)
Nell'esempio riportato di seguito viene illustrato come controllare la riproduzione dei supporti multimediali tramite <xref:System.Windows.Controls.MediaElement>.  In questo esempio viene creato un semplice lettore multimediale che consente di riprodurre, mettere in pausa, interrompere e andare avanti e indietro all'interno del contenuto del supporto multimediale, oltre a regolare volume e velocità.  
  
## Esempio  
 Nel codice riportato di seguito viene creata l'interfaccia utente.  
  
> [!NOTE]
>  La proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> di <xref:System.Windows.Controls.MediaElement> deve essere impostata su `Manual` per essere in grado di interrompere, mettere in pausa e riprodurre in modo interattivo il supporto multimediale.  
  
 [!code-xml[MediaGallery_snip#MediaElementExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml#mediaelementexamplewholepage)]  
  
## Esempio  
 Nel codice riportato di seguito viene implementata la funzionalità dei controlli interfaccia utente.  I metodi <xref:System.Windows.Controls.MediaElement.Play%2A>, <xref:System.Windows.Controls.MediaElement.Pause%2A> e <xref:System.Windows.Controls.MediaElement.Stop%2A> vengono utilizzati, rispettivamente, per riprodurre, mettere in pausa e interrompere il supporto multimediale.  La modifica della proprietà <xref:System.Windows.Controls.MediaElement.Position%2A> di <xref:System.Windows.Controls.MediaElement> consente di spostarsi nel contenuto del supporto multimediale.  Infine, le proprietà <xref:System.Windows.Controls.MediaElement.Volume%2A> e <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> vengono utilizzate per regolare il volume e la velocità di riproduzione del supporto multimediale.  
  
 [!code-csharp[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaGallery_snip/CSharp/MediaElementExample.xaml.cs#codebehindmediaelementexamplewholepage)]
 [!code-vb[MediaGallery_snip#CodeBehindMediaElementExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MediaGallery_snip/VB/MediaElementExample.xaml.vb#codebehindmediaelementexamplewholepage)]  
  
## Vedere anche  
 [Controllare un MediaElement utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-by-using-a-storyboard.md)