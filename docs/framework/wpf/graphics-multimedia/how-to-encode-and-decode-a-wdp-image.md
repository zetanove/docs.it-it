---
title: "Procedura: codificare e decodificare un&#39;immagine WDP | Microsoft Docs"
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
  - "decodifica di immagini WDP"
  - "codifica di formati di immagine"
  - "codifica di immagini WDP"
  - "WDP (decodifica)"
  - "WDP (codifica)"
ms.assetid: 911777d1-516b-49db-a87b-b54e31b18532
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: codificare e decodificare un&#39;immagine WDP
Negli esempi seguenti viene illustrato come decodificare e codificare un'immagine [!INCLUDE[TLA#tla_wdp](../../../../includes/tlasharptla-wdp-md.md)] utilizzando gli oggetti <xref:System.Windows.Media.Imaging.WmpBitmapDecoder> e <xref:System.Windows.Media.Imaging.WmpBitmapEncoder> specifici.  
  
## Esempio  
 In questo esempio viene illustrato come decodificare un'immagine [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)] utilizzando un oggetto <xref:System.Windows.Media.Imaging.WmpBitmapDecoder> da un oggetto <xref:System.Uri>.  
  
 [!code-cpp[WdpBitmapDecoderEncoder#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CPP/WDPEncoderDecoder.cpp#1)]
 [!code-csharp[WdpBitmapDecoderEncoder#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CSharp/WDPEncoderDecoder.cs#1)]
 [!code-vb[WdpBitmapDecoderEncoder#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/VB/WDPEncoderDecoder.vb#1)]  
  
## Esempio  
 In questo esempio viene mostrato come codificare un oggetto <xref:System.Windows.Media.Imaging.BitmapSource> in un'immagine [!INCLUDE[TLA2#tla_wdp](../../../../includes/tla2sharptla-wdp-md.md)] tramite un oggetto <xref:System.Windows.Media.Imaging.WmpBitmapEncoder>.  
  
 [!code-cpp[WdpBitmapDecoderEncoder#4](../../../../samples/snippets/cpp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CPP/WDPEncoderDecoder.cpp#4)]
 [!code-csharp[WdpBitmapDecoderEncoder#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/CSharp/WDPEncoderDecoder.cs#4)]
 [!code-vb[WdpBitmapDecoderEncoder#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WdpBitmapDecoderEncoder/VB/WDPEncoderDecoder.vb#4)]  
  
## Vedere anche  
 [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md)