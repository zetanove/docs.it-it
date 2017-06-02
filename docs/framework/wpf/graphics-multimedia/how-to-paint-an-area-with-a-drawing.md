---
title: "Procedura: inserire un disegno in un&#39;area | Microsoft Docs"
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
  - "pennelli, disegno con oggetti Drawing"
  - "disegni, disegno"
  - "disegno, con oggetti Drawing"
ms.assetid: c10dc4b1-09b1-41e8-ad14-456b5fb377df
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Procedura: inserire un disegno in un&#39;area
In questo esempio viene illustrato come inserire un disegno in un'area.  Per inserire un disegno in un'area, si utilizza un oggetto <xref:System.Windows.Media.DrawingBrush> e uno o più oggetti <xref:System.Windows.Media.Drawing>.  Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.DrawingBrush> per inserire il disegno di due ellissi.  
  
## Esempio  
 [!code-xml[drawingbrush_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/DrawingBrushExample.vb#drawingbrushexamplewholepage)]  
  
 Nell'immagine seguente viene illustrato l'output dell'esempio:  
  
 ![Output di DrawingBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrush-simple.png "graphicsmm\_drawingbrush\_simple")  
  
 Il centro della forma è bianco per le ragioni descritte in [Controllare il riempimento di una forma composta](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-the-fill-of-a-composite-shape.md).  
  
 Se si impostano le proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.TileMode%2A> di un oggetto <xref:System.Windows.Media.DrawingBrush>, è possibile creare un motivo ripetitivo.  Nell'esempio seguente viene disegnato un oggetto con un motivo creato disegnando due ellissi.  
  
 [!code-xml[drawingbrush_snip#TiledDrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_snip/CS/TiledDrawingBrushExample.xaml#tileddrawingbrushexamplewholepage)]  
  
 [!code-csharp[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/drawingbrush_procedural_snip/CSharp/TiledDrawingBrushExample.cs#tileddrawingbrushexamplewholepage)]
 [!code-vb[drawingbrush_procedural_snip#TiledDrawingBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/drawingbrush_procedural_snip/VisualBasic/TiledDrawingBrushExample.vb#tileddrawingbrushexamplewholepage)]  
  
 Nell'immagine seguente viene mostrato l'output dell'oggetto <xref:System.Windows.Media.DrawingBrush> affiancato.  
  
 ![Output affiancato di DrawingBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrush-tiled.png "graphicsmm\_drawingbrush\_tiled")  
  
 Per ulteriori informazioni sui pennelli per il disegno, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Drawing>, vedere [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md).