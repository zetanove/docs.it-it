---
title: "Cenni preliminari sui pennelli di WPF | Microsoft Docs"
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
  - "pennelli, informazioni sui pennelli"
ms.assetid: ecea1955-420b-45c6-bf43-c1404c072c41
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Cenni preliminari sui pennelli di WPF
Tutti gli elementi visibili sullo schermo possono essere visualizzati poiché sono stati disegnati con un pennello.  Ad esempio, un pennello viene utilizzato per descrivere lo sfondo di un pulsante, il primo piano di un testo e il riempimento di una forma.  In questo argomento vengono presentati i concetti di disegno con i pennelli di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e illustrati alcuni esempi.  I pennelli consentono di disegnare oggetti dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] utilizzando colori semplici e a tinta unita, ma anche set complessi di modelli e immagini.  
  
<a name="paintingwithbrush"></a>   
## Disegno con un pennello  
 <xref:System.Windows.Media.Brush> "disegna" un'area con un output specifico.  Tipi differenti di pennelli generano tipi di output diversi.  Alcuni pennelli disegnano un'area con un colore a tinta unita, altri con una sfumatura, un modello, un'immagine o un disegno.  Nell'immagine riportata di seguito vengono illustrati esempi di tutti i diversi tipi di <xref:System.Windows.Media.Brush>.  
  
 ![Tipi di pennello](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brushtypes.png "graphicsmm\_brushtypes")  
Esempi di pennello  
  
 La maggior parte degli oggetti visivi consente di specificare il modo in cui vengono disegnati.  Nella tabella riportata di seguito vengono elencati alcuni oggetti e proprietà comuni con cui è possibile utilizzare un oggetto <xref:System.Windows.Media.Brush>.  
  
|Classe|Proprietà del pennello|  
|------------|----------------------------|  
|<xref:System.Windows.Controls.Border>|<xref:System.Windows.Controls.Border.BorderBrush%2A>, <xref:System.Windows.Controls.Border.Background%2A>|  
|<xref:System.Windows.Controls.Control>|<xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A>|  
|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Panel.Background%2A>|  
|<xref:System.Windows.Media.Pen>|<xref:System.Windows.Media.Pen.Brush%2A>|  
|<xref:System.Windows.Shapes.Shape>|<xref:System.Windows.Shapes.Shape.Fill%2A>, <xref:System.Windows.Shapes.Shape.Stroke%2A>|  
|<xref:System.Windows.Controls.TextBlock>|<xref:System.Windows.Controls.TextBlock.Background%2A>|  
  
 Nella sezione riportata di seguito vengono descritti i vari tipi di <xref:System.Windows.Media.Brush> e viene fornito un esempio per ciascuno di essi.  
  
<a name="paintwithsolidcolorbrush"></a>   
## Disegnare con un oggetto Color a tinta unita  
 <xref:System.Windows.Media.SolidColorBrush> disegna un'area con un oggetto <xref:System.Windows.Media.Color> a tinta unita.  Sono disponibili molti modi per specificare l'oggetto <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush>: ad esempio, è possibile specificare i canali alfa, rosso, blu e verde oppure utilizzare uno dei colori predefiniti forniti dalla classe <xref:System.Windows.Media.Colors>.  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.SolidColorBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando SolidColorBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-solidcolorbrush.png "graphicsmm\_brush\_ovw\_solidcolorbrush")  
Rettangolo disegnato con un oggetto SolidColorBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmsolidcolorbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmsolidcolorbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMSolidColorBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmsolidcolorbrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.SolidColorBrush>, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithlineargradientbrush"></a>   
## Disegnare con una sfumatura lineare  
 <xref:System.Windows.Media.LinearGradientBrush> disegna un'area con una sfumatura lineare.  Una sfumatura lineare consente di fondere due o più colori lungo una linea definita asse di sfumatura.  Per specificare i colori della sfumatura e le relative posizioni, utilizzare gli oggetti <xref:System.Windows.Media.GradientStop>.  
  
 Nell'esempio seguente viene utilizzato <xref:System.Windows.Media.LinearGradientBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando LinearGradientBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-lineargradientbrush.png "graphicsmm\_brush\_ovw\_lineargradientbrush")  
Rettangolo disegnato con un oggetto LinearGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmlineargradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmlineargradientbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMLinearGradientBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmlineargradientbrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.LinearGradientBrush>, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithradialgradientbrush"></a>   
## Disegnare con una sfumatura radiale  
 <xref:System.Windows.Media.RadialGradientBrush> disegna un'area con una sfumatura radiale.  Una sfumatura radiale consente di fondere due o più colori in un cerchio.  Come per la classe <xref:System.Windows.Media.LinearGradientBrush>, per specificare i colori della sfumatura e le relative posizioni, utilizzare <xref:System.Windows.Media.GradientStop>.  
  
 Nell'esempio seguente viene utilizzato <xref:System.Windows.Media.RadialGradientBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando RadialGradientBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-radialgradientbrush.png "graphicsmm\_brush\_ovw\_radialgradientbrush")  
Rettangolo disegnato con un oggetto RadialGradientBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmradialgradientbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmradialgradientbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMRadialGradientBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmradialgradientbrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.RadialGradientBrush>, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="paintwithimage"></a>   
## Disegnare con un oggetto Image  
 <xref:System.Windows.Media.ImageBrush> disegna un'area con un oggetto <xref:System.Windows.Media.ImageSource>.  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.ImageBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando ImageBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-imagebrush.png "graphicsmm\_brush\_ovw\_imagebrush")  
Rettangolo disegnato con un oggetto Image  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmimagebrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmimagebrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMImageBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmimagebrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.ImageBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithdrawing"></a>   
## Disegnare con un oggetto Drawing  
 <xref:System.Windows.Media.DrawingBrush> disegna un'area con un oggetto <xref:System.Windows.Media.Drawing>.  <xref:System.Windows.Media.Drawing> può contenere forme, immagini, testi e contenuti multimediali.  
  
 Nell'esempio seguente viene utilizzato <xref:System.Windows.Media.DrawingBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando DrawingBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-drawingbrush.png "graphicsmm\_brush\_ovw\_drawingbrush")  
Rettangolo disegnato con un oggetto DrawingBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmdrawingbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmdrawingbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMDrawingBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmdrawingbrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.DrawingBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithvisual"></a>   
## Disegnare con un oggetto Visual  
 <xref:System.Windows.Media.VisualBrush> disegna un'area con <xref:System.Windows.Media.Visual>.  <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Page> e <xref:System.Windows.Controls.MediaElement> rappresentano esempi di oggetti Visual.  <xref:System.Windows.Media.VisualBrush> consente inoltre di proiettare il contenuto da una parte dell'applicazione in un'altra area; questa funzione è molto utile per la creazione di effetti reflection e per l'ingrandimento di parti dello schermo.  
  
 Nell'esempio seguente viene utilizzato <xref:System.Windows.Media.VisualBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle>.  Nell'immagine riportata di seguito viene illustrato il rettangolo disegnato.  
  
 ![Rettangolo disegnato usando VisualBrush](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-brush-ovw-visualbrush.png "graphicsmm\_brush\_ovw\_visualbrush")  
Rettangolo disegnato con un oggetto VisualBrush  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTypesExample.cs#graphicsmmvisualbrushexampleinline)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtypesexample.vb#graphicsmmvisualbrushexampleinline)]
 [!code-xml[BrushesIntroduction_snip#GraphicsMMVisualBrushExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTypesExample.xaml#graphicsmmvisualbrushexampleinline)]  
  
 Per ulteriori informazioni sulla classe <xref:System.Windows.Media.VisualBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
<a name="paintwithpredefinedbrushesandsystemcolors"></a>   
## Disegnare utilizzando pennelli predefiniti e di sistema  
 Per motivi di praticità, in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] viene fornito un set di pennelli predefiniti e di sistema che può essere utilizzato per disegnare oggetti.  
  
-   Per un elenco dei pennelli predefiniti disponibili, vedere la classe <xref:System.Windows.Media.Brushes>.  Per un esempio in cui viene illustrato come utilizzare un pennello predefinito, vedere [Disegnare un'area con un colore a tinta unita](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-solid-color.md).  
  
-   Per un elenco dei pennelli di sistema disponibili, vedere la classe <xref:System.Windows.SystemColors>.  Per un esempio, vedere [Disegnare un'area con un pennello di sistema](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md).  
  
<a name="commonbrushfeatures"></a>   
## Funzionalità comuni dei pennelli  
 Gli oggetti <xref:System.Windows.Media.Brush> forniscono una proprietà <xref:System.Windows.Media.Brush.Opacity%2A> che può essere utilizzata per rendere trasparente un pennello, in modo completo oppure parziale.  Un valore <xref:System.Windows.Media.Brush.Opacity%2A> pari a 0 rende un pennello completamente trasparente, mentre un valore <xref:System.Windows.Media.Brush.Opacity%2A> pari a 1 lo rende completamente opaco.  Nell'esempio seguente viene utilizzata la proprietà <xref:System.Windows.Media.Brush.Opacity%2A> per rendere l'oggetto opaco al 25% <xref:System.Windows.Media.SolidColorBrush>.  
  
 [!code-xml[BrushOverviewExamples_snip#OpacityExample1XAML](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/OpacityExample.xaml#opacityexample1xaml)]  
  
 [!code-csharp[BrushOverviewExamples_snip#OpacityExample1CSharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/OpacityExample.cs#opacityexample1csharp)]  
  
 Se il pennello contiene colori parzialmente trasparenti, il valore di opacità del colore viene combinato, tramite moltiplicazione, al valore di opacità del pennello.  Ad esempio, se un pennello dispone di un valore di opacità pari a 0,5 e anche un colore utilizzato dal pennello dispone dello stesso valore, il colore di output avrà un valore di opacità pari a 0,25.  
  
> [!NOTE]
>  È più efficiente modificare il valore di opacità di un pennello anziché cambiare l'opacità di un elemento intero utilizzando la proprietà <xref:System.Windows.UIElement.Opacity%2A?displayProperty=fullName>.  
  
 È possibile ruotare, ridimensionare, inclinare e traslare il contenuto di un pennello utilizzando la rela tiva proprietà <xref:System.Windows.Media.Brush.Transform%2A> o <xref:System.Windows.Media.Brush.RelativeTransform%2A>.  Per ulteriori informazioni, vedere [Cenni preliminari sulle proprietà di trasformazione Brush](../../../../docs/framework/wpf/graphics-multimedia/brush-transformation-overview.md).  
  
 Poiché si tratta di oggetti <xref:System.Windows.Media.Animation.Animatable>, è possibile aggiungere un'animazione agli oggetti <xref:System.Windows.Media.Brush>.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
<a name="freezable_features"></a>   
### Funzionalità dell'oggetto Freezable  
 Poiché eredita dalla classe <xref:System.Windows.Freezable>, la classe <xref:System.Windows.Media.Brush> fornisce diverse funzionalità speciali: gli oggetti <xref:System.Windows.Media.Brush> possono essere dichiarati come [risorse](../../../../docs/framework/wpf/advanced/xaml-resources.md), condivisi tra più oggetti e clonati.  Inoltre, tutti i tipi di oggetti <xref:System.Windows.Media.Brush>, eccetto <xref:System.Windows.Media.VisualBrush> possono essere resi di sola lettura \(per migliorare le prestazioni\) e thread\-safe.  
  
 Per ulteriori informazioni sulle diverse funzionalità fornite dagli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Per ulteriori informazioni sul motivo per cui gli oggetti <xref:System.Windows.Media.VisualBrush> non possono essere bloccati, vedere la pagina relativa al tipo <xref:System.Windows.Media.VisualBrush>.  
  
## Vedere anche  
 <xref:System.Windows.Media.Brush>   
 <xref:System.Windows.Media.Brushes>   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Esempio di oggetti Brush](http://go.microsoft.com/fwlink/?LinkID=159973)   
 [Esempio di ImageBrush](http://go.microsoft.com/fwlink/?LinkID=160005)   
 [Esempio di VisualBrush](http://go.microsoft.com/fwlink/?LinkID=160049)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/brushes-how-to-topics.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)