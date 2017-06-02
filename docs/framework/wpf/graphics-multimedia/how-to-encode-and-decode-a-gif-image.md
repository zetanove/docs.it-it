---
title: "Procedura: codificare e decodificare un&#39;immagine GIF | Microsoft Docs"
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
  - "decodifica di immagini GIF"
  - "decodifica di formati di immagine"
  - "codifica di immagini GIF"
  - "codifica di formati di immagine"
  - "GIF (decodifica)"
  - "GIF (codifica)"
ms.assetid: 9cdd9ec7-71eb-444b-b9e3-991958461163
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: codificare e decodificare un&#39;immagine GIF
Negli esempi seguenti viene illustrato come decodificare e codificare un'immagine [!INCLUDE[TLA#tla_gif](../../../../includes/tlasharptla-gif-md.md)] utilizzando gli oggetti <xref:System.Windows.Media.Imaging.GifBitmapDecoder> e <xref:System.Windows.Media.Imaging.GifBitmapEncoder> specifici.  
  
## Esempio  
 In questo esempio viene illustrato come decodificare un'immagine [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] utilizzando un oggetto <xref:System.Windows.Media.Imaging.GifBitmapDecoder> da un oggetto <xref:System.IO.FileStream>.  
  
 [!code-cpp[GifBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#1)]
 [!code-csharp[GifBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#1)]
 [!code-vb[GifBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#1)]  
  
## Esempio  
 In questo esempio viene mostrato come codificare un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> in un'immagine [!INCLUDE[TLA2#tla_gif](../../../../includes/tla2sharptla-gif-md.md)] tramite un oggetto <xref:System.Windows.Media.Imaging.GifBitmapEncoder>.  
  
 [!code-cpp[GifBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CPP/GifEncoderDecoder.cpp#4)]
 [!code-csharp[GifBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GifBitmapDecoderEncoder/CSharp/GifEncoderDecoder.cs#4)]
 [!code-vb[GifBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GifBitmapDecoderEncoder/VB/GifEncoderDecoder.vb#4)]  
  
## Vedere anche  
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)