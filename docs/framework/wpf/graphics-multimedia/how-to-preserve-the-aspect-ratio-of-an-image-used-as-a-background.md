---
title: "Procedura: conservare le proporzioni di un&#39;immagine utilizzata come sfondo | Microsoft Docs"
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
  - "proporzioni di immagini di sfondo, mantenimento"
  - "immagini di sfondo, mantenimento di proporzioni"
  - "pennelli, mantenimento di proporzioni di immagini di sfondo"
ms.assetid: 28c39478-13d7-4011-80a3-8b9cc3e54478
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: conservare le proporzioni di un&#39;immagine utilizzata come sfondo
In questo esempio viene illustrato come utilizzare la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> di un oggetto <xref:System.Windows.Media.ImageBrush> per mantenere le [proporzioni](GTMT) dell'immagine.  
  
 Per impostazione predefinita, quando si utilizza un oggetto <xref:System.Windows.Media.ImageBrush> per disegnare un'area, il contenuto si estende per riempire completamente l'area di output.  Quando l'area di output e l'immagine hanno[proporzioni](GTMT)differenti, tale espansione distorce l'immagine.  
  
 Per fare in modo che un oggetto <xref:System.Windows.Media.ImageBrush> mantenga le proporzioni della relativa immagine, impostare la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> su <xref:System.Windows.Media.Stretch> o su <xref:System.Windows.Media.Stretch>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono utilizzati due oggetti <xref:System.Windows.Media.ImageBrush> per disegnare due rettangoli.  Ogni rettangolo è di 300 x 150 [pixel](GTMT) e contiene un immagine da 300 x 300 pixel.  La proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> del primo pennello è impostata su <xref:System.Windows.Media.Stretch> e la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> del secondo controllo è impostata su <xref:System.Windows.Media.Stretch>.  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushStretchModesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/StretchModes.cs#imagebrushstretchmodesexamplewholepage)]  
  
 Nell'illustrazione seguente viene illustrato l'output del primo pennello, la cui proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> è impostata su <xref:System.Windows.Media.Stretch>.  
  
 ![ImageBrush con allungamento Uniform](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagebrushuniformstretch.png "graphicsmm\_ImageBrushUniformStretch")  
  
 Nell'illustrazione successiva viene illustrato l'output del secondo pennello, la cui proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> è impostata su <xref:System.Windows.Media.Stretch>.  
  
 ![ImageBrush con allungamento UniformToFill](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-imagebrushuniformtofillstretch.png "graphicsmm\_ImageBrushUniformToFillStretch")  
  
 Si noti che la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> ha lo stesso comportamento per gli altri oggetti <xref:System.Windows.Media.TileBrush>, ovvero per <xref:System.Windows.Media.DrawingBrush> e <xref:System.Windows.Media.VisualBrush>.  Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.ImageBrush> e gli altri oggetti  <xref:System.Windows.Media.TileBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
 Si noti inoltre che, sebbene sembri che la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> specifichi in che modo il contenuto dell'oggetto <xref:System.Windows.Media.TileBrush> venga adattato all'area di output, in realtà specifica in che modo il contenuto dell'oggetto <xref:System.Windows.Media.TileBrush> venga adattato alla tessera di base.  Per ulteriori informazioni, vedere <xref:System.Windows.Media.TileBrush>.  
  
 Questo esempio di codice fa parte di un esempio più esteso fornito per la classe <xref:System.Windows.Media.ImageBrush>.  Per l'esempio completo, vedere [Esempio ImageBrush](http://go.microsoft.com/fwlink/?LinkID=160005) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Media.TileBrush>   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)