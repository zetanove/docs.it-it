---
title: "Procedura: riprodurre contenuti multimediali utilizzando un oggetto VideoDrawing | Microsoft Docs"
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
  - "classi, Media Player"
  - "classi, VideoDrawing"
  - "MediaPlayer (classe)"
  - "riproduzione di contenuti multimediali"
  - "VideoDrawing (classe)"
ms.assetid: 165d47ed-22ce-4ded-aa6a-aa9b7467de87
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: riprodurre contenuti multimediali utilizzando un oggetto VideoDrawing
Per riprodurre un file audio o video, si utilizza un oggetto <xref:System.Windows.Media.VideoDrawing> e <xref:System.Windows.Media.MediaPlayer>.  È possibile caricare e riprodurre contenuti multimediali in due modi diversi.  Il primo consiste nell'utilizzo di <xref:System.Windows.Media.MediaPlayer> e di un oggetto <xref:System.Windows.Media.VideoDrawing> da soli e il secondo nella creazione di un oggetto <xref:System.Windows.Media.MediaTimeline> personalizzato da utilizzare con <xref:System.Windows.Media.MediaPlayer> e <xref:System.Windows.Media.VideoDrawing>.  
  
> [!NOTE]
>  Quando si distribuiscono contenuti multimediali con l'applicazione, non è possibile utilizzare un file multimediale come risorsa di progetto, come avviene per un'immagine.  Invece, è necessario impostare il tipo di contenuti multimediali su `Content` nel file del progetto e `CopyToOutputDirectory` su `PreserveNewest` o su `Always`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.VideoDrawing> e un oggetto <xref:System.Windows.Media.MediaPlayer> per riprodurre un file video una volta.  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 Per un ulteriore controllo della durata dei contenuti multimediali, utilizzare un oggetto <xref:System.Windows.Media.MediaTimeline> con gli oggetti <xref:System.Windows.Media.MediaPlayer> e <xref:System.Windows.Media.VideoDrawing>.  L'oggetto <xref:System.Windows.Media.MediaTimeline> consente di specificare se il file video deve essere ripetuto.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.MediaTimeline> con gli oggetti <xref:System.Windows.Media.MediaPlayer> e <xref:System.Windows.Media.VideoDrawing> per riprodurre ripetutamente un video.  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 Quando si utilizza un oggetto <xref:System.Windows.Media.MediaTimeline>, si impiega l'oggetto interattivo <xref:System.Windows.Media.Animation.ClockController> restituito dalla proprietà <xref:System.Windows.Media.Animation.Clock.Controller%2A> dell'oggetto <xref:System.Windows.Media.MediaClock> per controllare la riproduzione di contenuti multimediali invece dei metodi interattivi di <xref:System.Windows.Media.MediaPlayer>.  
  
## Vedere anche  
 <xref:System.Windows.Media.VideoDrawing>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)