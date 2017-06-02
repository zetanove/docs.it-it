---
title: "Procedura: utilizzare un disegno come origine di immagini | Microsoft Docs"
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
  - "disegni, come origini di immagini"
  - "grafica, disegni, come origini di immagini"
  - "origini di immagini, disegni"
ms.assetid: dcf71c7b-9e86-4b8e-8e39-0d0ce0389ef4
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: utilizzare un disegno come origine di immagini
In questo esempio viene mostrato come utilizzare un oggetto <xref:System.Windows.Media.Drawing> come oggetto <xref:System.Windows.Controls.Image.Source%2A> per un controllo <xref:System.Windows.Controls.Image>.  Per visualizzare un oggetto <xref:System.Windows.Media.Drawing> con un controllo <xref:System.Windows.Controls.Image>, utilizzare un oggetto <xref:System.Windows.Media.DrawingImage> come <xref:System.Windows.Controls.Image.Source%2A> del controllo <xref:System.Windows.Controls.Image> e impostare la proprietà <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=fullName> dell'oggetto <xref:System.Windows.Media.DrawingImage> sul disegno che si desidera visualizzare.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.DrawingImage> e un controllo <xref:System.Windows.Controls.Image> per visualizzare un oggetto <xref:System.Windows.Media.GeometryDrawing>.  Questo esempio produce il seguente output:  
  
 ![GeometryDrawing di due ellissi](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
Un oggetto DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
## Vedere anche  
 <xref:System.Windows.Freezable.Freeze%2A>   
 [Disegnare un'immagine con ImageDrawing](../../../../docs/framework/wpf/graphics-multimedia/how-to-draw-an-image-using-imagedrawing.md)   
 [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Attributo PresentationOptions:Freeze](../../../../docs/framework/wpf/advanced/presentationoptions-freeze-attribute.md)