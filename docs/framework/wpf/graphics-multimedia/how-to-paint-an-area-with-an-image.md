---
title: "Procedura: disegnare un&#39;area con un&#39;immagine | Microsoft Docs"
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
  - "pennelli, disegno con oggetti Image"
  - "immagini, disegno"
  - "disegno, con oggetti Image"
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedura: disegnare un&#39;area con un&#39;immagine
In questo esempio viene illustrato come utilizzare la classe <xref:System.Windows.Media.ImageBrush> per disegnare un'area con un'immagine.  In un oggetto <xref:System.Windows.Media.ImageBrush> viene visualizzata una sola immagine, specificata dalla relativa proprietà <xref:System.Windows.Media.ImageBrush.ImageSource%2A>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene disegnata la proprietà <xref:System.Windows.Controls.Control.Background%2A> di un pulsante utilizzando un oggetto <xref:System.Windows.Media.ImageBrush>.  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 Per impostazione predefinita, un oggetto <xref:System.Windows.Media.ImageBrush> estende la propria immagine in modo da riempire completamente l'area che si sta disegnando.  Nell'esempio precedente, l'immagine viene estesa per riempire il pulsante, con il rischio che l'immagine venga distorta.  È possibile controllare questo comportamento impostando la proprietà <xref:System.Windows.Media.TileBrush.Stretch%2A> di <xref:System.Windows.Media.TileBrush> su <xref:System.Windows.Media.Stretch> o <xref:System.Windows.Media.Stretch> in modo che il pennello mantenga le[proporzioni](GTMT) dell'immagine.  
  
 Se si impostano le proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.TileMode%2A> di un oggetto <xref:System.Windows.Media.ImageBrush>, è possibile creare un pattern ripetuto.  Nell'esempio riportato di seguito viene disegnato un pulsante utilizzando un pattern creato da un'immagine.  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.ImageBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
 Questo esempio di codice fa parte di un esempio più esteso fornito per la classe <xref:System.Windows.Media.ImageBrush>.  Per l'esempio completo, vedere [Esempio ImageBrush](http://go.microsoft.com/fwlink/?LinkID=160005) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)