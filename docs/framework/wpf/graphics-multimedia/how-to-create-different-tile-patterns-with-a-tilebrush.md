---
title: "Procedura: creare modelli di elementi affiancati differenti con un TileBrush | Microsoft Docs"
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
  - "creazione, elementi affiancati con TileBrush"
  - "elementi affiancati, creazione"
  - "TileBrush, creazione di elementi affiancati"
ms.assetid: 5aa46632-3527-4668-9d8d-0375c8af28aa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: creare modelli di elementi affiancati differenti con un TileBrush
In questo esempio viene illustrato come utilizzare la proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A> di un <xref:System.Windows.Media.TileBrush> per creare un modello.  
  
 La proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A> consente di specificare in che modo viene ripetuto il contenuto di un oggetto <xref:System.Windows.Media.TileBrush>, ovvero in che modo viene affiancato per riempire un'area di output.  Per creare un modello, impostare la proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A> su <xref:System.Windows.Media.TileMode>, <xref:System.Windows.Media.TileMode>, <xref:System.Windows.Media.TileMode> o <xref:System.Windows.Media.TileMode>.  È necessario inoltre impostare la proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> dell'oggetto <xref:System.Windows.Media.TileBrush> in modo che risulti più piccolo dell'area che si sta disegnando. In caso contrario, verrà prodotto un solo elemento affiancato, indipendentemente dall'impostazione utilizzata per la proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono creati cinque oggetti <xref:System.Windows.Media.DrawingBrush>, viene assegnata a ciascuno un'impostazione diversa della proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A>, quindi gli oggetti vengono utilizzati per disegnare cinque rettangoli.  Anche se in questo esempio viene utilizzata la classe <xref:System.Windows.Media.DrawingBrush> per illustrare il comportamento della proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A>, la proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A> ha un funzionamento identico per tutti gli oggetti <xref:System.Windows.Media.TileBrush>, ovvero per <xref:System.Windows.Media.ImageBrush>, <xref:System.Windows.Media.VisualBrush> e <xref:System.Windows.Media.DrawingBrush>.  
  
 Nella figura riportata di seguito viene illustrato l'output che si ottiene dall'esempio.  
  
 ![Output dell'esempio di affiancamento di TileBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrushtilemodeexample.png "graphicsmm\_DrawingBrushTileModeExample")  
Modelli di elementi affiancati creati con la proprietà TileMode  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/TileModeExample.cs#graphicsmmdrawingbrushtilemodeexample)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/tilemodeexample.vb#graphicsmmdrawingbrushtilemodeexample)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/TileModeExample.xaml#graphicsmmdrawingbrushtilemodeexample)]  
  
## Vedere anche  
 [Impostare la dimensione degli elementi affiancati di un TileBrush](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-the-tile-size-for-a-tilebrush.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)