---
title: "Procedura: disegnare un&#39;area con un video | Microsoft Docs"
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
  - "pennelli, disegno con un video"
  - "disegno con un video"
  - "video, disegno"
ms.assetid: 04dd6600-4a6e-4b43-a93e-21cce7dfbcb8
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: disegnare un&#39;area con un video
In questo esempio viene illustrato come disegnare un'area con i supporti.  Una modalità per disegnare un'area con i supporti consiste nell'utilizzare <xref:System.Windows.Controls.MediaElement> con <xref:System.Windows.Media.VisualBrush>.  Utilizzare <xref:System.Windows.Controls.MediaElement> per caricare e riprodurre i supporti, quindi per impostare la proprietà <xref:System.Windows.Media.VisualBrush.Visual%2A> di <xref:System.Windows.Media.VisualBrush>.  È quindi possibile utilizzare <xref:System.Windows.Media.VisualBrush> per disegnare un'area con i supporti caricati.  
  
## Esempio  
 Nell'esempio riportato di seguito vengono utilizzati <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Media.VisualBrush> per disegnare la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> di un controllo <xref:System.Windows.Controls.TextBlock> con video.  In questo esempio la proprietà <xref:System.Windows.Controls.MediaElement.IsMuted%2A> di <xref:System.Windows.Controls.MediaElement> viene impostata su `true` in modo da non riprodurre suoni.  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundinline)]
 [!code-xml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundinline)]  
  
## Esempio  
 Poiché <xref:System.Windows.Media.VisualBrush> eredita dalla classe <xref:System.Windows.Media.TileBrush>, offre varie modalità di affiancamento.  Impostando la proprietà <xref:System.Windows.Media.TileBrush.TileMode%2A> di <xref:System.Windows.Media.VisualBrush> su <xref:System.Windows.Media.TileMode> e la proprietà <xref:System.Windows.Media.TileBrush.Viewport%2A> su un valore più piccolo dell'area da disegnare, è possibile creare un modello affiancato.  
  
 Nell'esempio riportato di seguito è identico al precedente, tranne per il fatto che <xref:System.Windows.Media.VisualBrush> genera un modello dal video.  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-xml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundtiledinline)]  
  
 Per informazioni sull'aggiunta di un file di dati, ad esempio un file multimediale, all'applicazione, vedere [File di dati e di risorse dell'applicazione WPF.](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md).  Quando si aggiunge un file multimediale, è necessario aggiungerlo come file di dati, non come file di risorse.  
  
## Vedere anche  
 <xref:System.Windows.Media.VisualBrush>   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Cenni preliminari sugli oggetti TileBrush](../../../../docs/framework/wpf/graphics-multimedia/tilebrush-overview.md)   
 [Panoramica delle funzionalità multimediali](../../../../docs/framework/wpf/graphics-multimedia/multimedia-overview.md)