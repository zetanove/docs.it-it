---
title: "Procedura: codificare e decodificare un&#39;immagine PNG | Microsoft Docs"
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
  - "decodifica di formati di immagine"
  - "decodifica di immagini PNG"
  - "codifica di formati di immagine"
  - "codifica di immagini PNG"
  - "PNG (decodifica)"
  - "PNG (codifica)"
ms.assetid: 3d31d186-af73-47f0-b5a7-c26ae46409a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: codificare e decodificare un&#39;immagine PNG
Negli esempi seguenti viene illustrato come decodificare e codificare un'immagine [!INCLUDE[TLA#tla_png](../../../../includes/tlasharptla-png-md.md)] utilizzando gli oggetti <xref:System.Windows.Media.Imaging.PngBitmapDecoder> e <xref:System.Windows.Media.Imaging.PngBitmapEncoder> specifici.  
  
## Esempio  
 In questo esempio viene illustrato come decodificare un'immagine [!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)] utilizzando un oggetto <xref:System.Windows.Media.Imaging.PngBitmapDecoder> da un oggetto <xref:System.IO.FileStream>.  
  
 [!code-cpp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#1)]
 [!code-csharp[PngBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#1)]
 [!code-vb[PngBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#1)]  
  
## Esempio  
 In questo esempio viene illustrato come codificare <xref:System.Windows.Media.Imaging.BitmapSource> in un’immagine [!INCLUDE[TLA2#tla_png](../../../../includes/tla2sharptla-png-md.md)] tramite <xref:System.Windows.Media.Imaging.PngBitmapEncoder>.  
  
 [!code-cpp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CPP/PngEncoderDecoder.cpp#4)]
 [!code-csharp[PngBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PngBitmapDecoderEncoder/CSharp/PngEncoderDecoder.cs#4)]
 [!code-vb[PngBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PngBitmapDecoderEncoder/VB/PngEncoderDecoder.vb#4)]  
  
## Vedere anche  
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)