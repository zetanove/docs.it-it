---
title: "Procedura: creare un oggetto Bitmap da un oggetto Visual | Microsoft Docs"
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
  - "bitmap, rendering da elementi visivi"
  - "elementi visivi, rendering in bitmap"
ms.assetid: 103fc7f5-7306-4026-9d61-2005e79959f3
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: creare un oggetto Bitmap da un oggetto Visual
In questo esempio viene illustrato come creare una bitmap da un oggetto <xref:System.Windows.Media.Visual>.  Viene eseguito il rendering di <xref:System.Windows.Media.DrawingVisual> con <xref:System.Windows.Media.FormattedText>.  Viene quindi eseguito il rendering di <xref:System.Windows.Media.Visual> su <xref:System.Windows.Media.Imaging.RenderTargetBitmap> per creare una bitmap del testo specificato.  
  
## Esempio  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#CreateRTBImage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample.cs#creatertbimage)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#CreateRTBImage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample.vb#creatertbimage)]  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingContext>   
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Utilizzo degli oggetti DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)