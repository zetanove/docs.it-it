---
title: "Procedura: disegnare un’immagine con ImageDrawing | Microsoft Docs"
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
  - "classi, ImageDrawing"
  - "disegno, immagini"
  - "grafica, disegno di immagini"
  - "ImageDrawing (classe)"
  - "immagini, disegno"
ms.assetid: df28ab41-25fb-4ab3-b51d-7f695b24f55e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: disegnare un’immagine con ImageDrawing
In questo esempio viene illustrato come utilizzare un oggetto <xref:System.Windows.Media.ImageDrawing> per disegnare un'immagine.  Un oggetto <xref:System.Windows.Media.ImageDrawing> consente di visualizzare un oggetto <xref:System.Windows.Media.ImageSource> con gli oggetti <xref:System.Windows.Media.DrawingBrush>, <xref:System.Windows.Media.DrawingImage> o <xref:System.Windows.Media.Visual>.  Per disegnare un'immagine, creare un oggetto <xref:System.Windows.Media.ImageDrawing> e impostarne le proprietà <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=fullName> e <xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=fullName>.  La proprietà <xref:System.Windows.Media.ImageDrawing.ImageSource%2A?displayProperty=fullName> specifica l'immagine da disegnare e la proprietà <xref:System.Windows.Media.ImageDrawing.Rect%2A?displayProperty=fullName> specifica la posizione e la dimensione di ciascuna immagine.  
  
## Esempio  
 Nell'esempio seguente viene creato un disegno composto utilizzando quattro oggetti <xref:System.Windows.Media.ImageDrawing>.  Questo esempio produce l'immagine che segue:  
  
 ![Alcuni oggetti DrawingImage](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagedrawingexample.png "graphicsmm\_ImageDrawingExample")  
Quattro oggetti ImageDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawingExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawingexample)]
 [!code-xml[DrawingMiscSnippets_snip#ImageDrawingExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawingexample)]  
  
 Per un esempio in cui viene mostrato un modo semplice per visualizzare un'immagine senza utilizzare <xref:System.Windows.Media.ImageDrawing>, vedere [Utilizzare l'elemento di immagine](../../../../docs/framework/wpf/controls/how-to-use-the-image-element.md).  
  
## Vedere anche  
 <xref:System.Windows.Freezable.Freeze%2A>   
 <xref:System.Windows.Controls.Image>   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Attributo PresentationOptions:Freeze](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)