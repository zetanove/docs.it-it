---
title: "Procedura: impostare la dimensione degli elementi affiancati di un TileBrush | Microsoft Docs"
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
  - "TileBrush, dimensione delle tessere"
  - "Viewport (proprietà di TileBrush)"
ms.assetid: 04f41090-1b46-4e36-832f-d27d28708b8c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Procedura: impostare la dimensione degli elementi affiancati di un TileBrush
In questo esempio viene illustrato come impostare la dimensione degli elementi affiancati di un oggetto <xref:System.Windows.Media.TileBrush>.  Per impostazione predefinita, un oggetto <xref:System.Windows.Media.TileBrush> genera un solo elemento affiancato che riempie completamente l'area da disegnare.  È possibile eseguire l'override di questo comportamento impostando le proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.ViewportUnits%2A>.  
  
 La proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> specifica la dimensione della tessera per un oggetto <xref:System.Windows.Media.TileBrush>.  Per impostazione predefinita, il valore della proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> è relativo alla dimensione dell'area disegnata.  Per specificare una dimensione assoluta della tessera tramite la proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A>, impostare la proprietà <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> su <xref:System.Windows.Media.BrushMappingMode>.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.ImageBrush>, un tipo di <xref:System.Windows.Media.TileBrush>, per disegnare un rettangolo con elementi affiancati.  Nell'esempio ogni elemento viene impostato al 50% per 50% dell'area di output \(rettangolo\).  Di conseguenza, il rettangolo viene riempito con quattro proiezioni dell'immagine.  
  
 Nella figura che segue viene illustrato l'output che si ottiene dall'esempio.  
  
 ![Esempio di affiancamento con un tratto con immagine](../../../../docs/framework/wpf/graphics-multimedia/media/0.png "0")  
  
 [!code-csharp[UsingImageBrush_snip#RelativeTileSizeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#relativetilesizeexample)]  
  
 Nell'esempio successivo viene creato un oggetto <xref:System.Windows.Media.ImageBrush>, le cui proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> vengono impostate, rispettivamente, su `0,0,25,25` e <xref:System.Windows.Media.BrushMappingMode>, quindi l'oggetto viene utilizzato per disegnare un altro rettangolo.  Di conseguenza, il pennello genera elementi affiancati con una larghezza di 25 [pixel](GTMT) e un'altezza di 25 [pixel](GTMT).  
  
 Nella figura che segue viene illustrato l'output che si ottiene dall'esempio.  
  
 ![TileBrush affiancato con un viewport di 0,0,0.25,0.25](../../../../docs/framework/wpf/graphics-multimedia/media/25x25viewport.png "25x25viewport")  
  
 [!code-csharp[UsingImageBrush_snip#AbsoluteTileSizeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#absolutetilesizeexample)]  
  
 Gli esempi riportati in precedenza fanno parte di un esempio più esteso.  Per l'esempio completo, vedere [Esempio ImageBrush](http://go.microsoft.com/fwlink/?LinkID=160005) \(la pagina potrebbe essere in inglese\).  
  
 Benché in questo esempio venga utilizzata la classe <xref:System.Windows.Media.ImageBrush>, le proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> si comportano allo stesso modo per gli altri oggetti <xref:System.Windows.Media.TileBrush>, ovvero per <xref:System.Windows.Media.DrawingBrush> e <xref:System.Windows.Media.VisualBrush>.  Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.ImageBrush> e gli altri oggetti  <xref:System.Windows.Media.TileBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.TileBrush>   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Creare modelli di elementi affiancati differenti con un TileBrush](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-different-tile-patterns-with-a-tilebrush.md)