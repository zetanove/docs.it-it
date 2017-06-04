---
title: "Procedura: codificare un oggetto Visual in un file di immagine | Microsoft Docs"
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
  - "codifica di formati di immagine"
  - "file di immagine, codifica da elementi visivi"
  - "elementi visivi, codifica in un file di immagine"
ms.assetid: 2036385b-ea47-4d54-8027-5797f52c8149
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: codificare un oggetto Visual in un file di immagine
In questo esempio viene illustrato come codificare un oggetto <xref:System.Windows.Media.Visual> in un file di immagine utilizzando <xref:System.Windows.Media.Imaging.RenderTargetBitmap> e <xref:System.Windows.Media.Imaging.PngBitmapEncoder>.  
  
## Esempio  
 <xref:System.Windows.Media.DrawingVisual> viene creato utilizzando <xref:System.Windows.Media.Imaging.BitmapImage> e <xref:System.Windows.Media.FormattedText> di cui viene eseguito il rendering in un oggetto <xref:System.Windows.Media.Imaging.RenderTargetBitmap>.  La bitmap di cui viene eseguito il rendering viene quindi utilizzata per creare <xref:System.Windows.Media.Imaging.BitmapFrame> aggiunto a <xref:System.Windows.Media.Imaging.PngBitmapEncoder> per creare un nuovo file [!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)].  
  
 [!code-csharp[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/CSharp/RenderTargetBitmapExample_Encode.cs#rtbencodeinline1)]
 [!code-vb[ImagingSnippetGallery_procedural_snip#RTBEncodeInline1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ImagingSnippetGallery_procedural_snip/VB/RenderTargetBitmapExample_Encode.vb#rtbencodeinline1)]  
  
 In questo esempio viene utilizzato <xref:System.Windows.Media.Imaging.PngBitmapEncoder>, ma è possibile utilizzare qualsiasi oggetto <xref:System.Windows.Media.Imaging.BitmapEncoder> derivato per creare il file di immagine.  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingContext>   
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Utilizzo degli oggetti DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)