---
title: "Cenni preliminari sugli oggetti Drawing | Microsoft Docs"
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
  - "Disegnare oggetti"
  - "DrawingGroup (oggetti)"
  - "disegni, informazioni sui disegni"
  - "GeometryDrawing (oggetti)"
  - "GlyphRunDrawing (oggetti)"
  - "ImageDrawing (oggetti)"
ms.assetid: 9b5ce5c0-e204-4320-a7a8-0b2210d62f88
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Cenni preliminari sugli oggetti Drawing
In questo argomento viene fornita un'introduzione agli oggetti <xref:System.Windows.Media.Drawing> e ne viene descritto l'utilizzo per creare forme, bitmap, testo e contenuti multimediali in modo efficace.  Utilizzare gli oggetti <xref:System.Windows.Media.Drawing> quando si creano ClipArt, si disegna con <xref:System.Windows.Media.DrawingBrush> o si utilizzano oggetti <xref:System.Windows.Media.Visual>.  
  
   
  
<a name="whatisadrawingsection"></a>   
## Definizione di oggetto Drawing  
 Un oggetto <xref:System.Windows.Media.Drawing> descrive il contenuto visibile, ad esempio una forma, una bitmap, un video o una riga di testo.  Tipi diversi di disegni descrivono tipi diversi di contenuto.  Di seguito viene fornito un elenco dei diversi tipi di oggetti Drawing.  
  
-   <xref:System.Windows.Media.GeometryDrawing> \- Consente di disegnare una forma.  
  
-   <xref:System.Windows.Media.ImageDrawing> \- Consente di disegnare un'immagine.  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> \- Consente di creare del testo.  
  
-   <xref:System.Windows.Media.VideoDrawing> \- Consente di riprodurre un file audio o video.  
  
-   <xref:System.Windows.Media.DrawingGroup> \- Consente di eseguire altri disegni.  Utilizzare un gruppo di disegni per combinare altri disegni in un unico disegno composto.  
  
 Gli oggetti <xref:System.Windows.Media.Drawing> sono versatili. Sono molti i modi in cui è possibile utilizzare un oggetto <xref:System.Windows.Media.Drawing>.  
  
-   Può essere visualizzato come immagine utilizzando un oggetto <xref:System.Windows.Media.DrawingImage> e un controllo <xref:System.Windows.Controls.Image>.  
  
-   Può essere utilizzato con un oggetto <xref:System.Windows.Media.DrawingBrush> per disegnare un oggetto come l'oggetto <xref:System.Windows.Controls.Page.Background%2A> di <xref:System.Windows.Controls.Page>.  
  
-   Può essere utilizzato per descrivere l'aspetto di un oggetto <xref:System.Windows.Media.DrawingVisual>.  
  
-   Può essere utilizzato per enumerare il contenuto di un oggetto <xref:System.Windows.Media.Visual>.  
  
 WPF fornisce altri tipi di oggetti che consentono di disegnare forme, bitmap, testo e contenuti multimediali.  Ad esempio, è anche possibile utilizzare gli oggetti <xref:System.Windows.Shapes.Shape> per disegnare forme e il controllo <xref:System.Windows.Controls.MediaElement> fornisce un altro modo di aggiungere video all'applicazione.  Pertanto, quando è necessario utilizzare gli oggetti <xref:System.Windows.Media.Drawing>?  Quando è possibile sacrificare le funzionalità a livello framework per ottenere vantaggi in termini di prestazioni o quando sono necessarie funzionalità <xref:System.Windows.Freezable>.  Poiché gli oggetti <xref:System.Windows.Media.Drawing> mancano del supporto per [Layout](../../../../docs/framework/wpf/advanced/layout.md), l'input e lo stato attivo, forniscono vantaggi in termini di prestazioni che li rendono ideali per descrivere sfondi, ClipArt e il disegno di basso livello con gli oggetti <xref:System.Windows.Media.Visual>.  
  
 Poiché si tratta di un tipo di oggetto <xref:System.Windows.Freezable>, gli oggetti <xref:System.Windows.Media.Drawing> acquisiscono molte funzionalità speciali, ad esempio possono essere dichiarati come [risorse](../../../../docs/framework/wpf/advanced/xaml-resources.md), condivisi tra più oggetti, resi disponibili in sola lettura per migliorare le prestazioni, duplicati, nonché resi thread\-safe.  Per ulteriori informazioni sulle diverse funzionalità disponibili per gli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
<a name="drawinggeometriessection"></a>   
## Disegnare una forma  
 Per disegnare una forma si utilizza <xref:System.Windows.Media.GeometryDrawing>.  La proprietà <xref:System.Windows.Media.GeometryDrawing.Geometry%2A> del disegno della geometria descrive la forma da disegnare, la proprietà <xref:System.Windows.Media.GeometryDrawing.Brush%2A> descrive il modo in cui deve essere disegnato l'interno della forma e la proprietà <xref:System.Windows.Media.GeometryDrawing.Pen%2A> descrive il modo in cui tracciarne il contorno.  
  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.Media.GeometryDrawing> per disegnare una forma.  La forma è descritta da un oggetto <xref:System.Windows.Media.GeometryGroup> e due oggetti <xref:System.Windows.Media.EllipseGeometry>.  L'interno della forma viene disegnato con <xref:System.Windows.Media.LinearGradientBrush> e il contorno con <xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen>.  
  
 Nell'esempio riportato di seguito viene creato il seguente oggetto <xref:System.Windows.Media.GeometryDrawing>.  
  
 ![GeometryDrawing di due ellissi](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
Un oggetto GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexampleinline)]
 [!code-xml[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexampleinline)]  
  
 Per l'esempio completo, vedere [Creare un oggetto GeometryDrawing](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-geometrydrawing.md).  
  
 Altre classi <xref:System.Windows.Media.Geometry>, come <xref:System.Windows.Media.PathGeometry>, consentono di creare forme più complesse, quali curve e archi.  Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Geometry>, vedere [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
 Per ulteriori informazioni sugli altri modi di disegnare forme che non utilizzino gli oggetti <xref:System.Windows.Media.Drawing>, vedere [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md).  
  
<a name="drawingimagessection"></a>   
## Disegnare un'immagine  
 Per disegnare un'immagine, si utilizza un oggetto <xref:System.Windows.Media.ImageDrawing>.  La proprietà <xref:System.Windows.Media.ImageDrawing.ImageSource%2A> di un oggetto <xref:System.Windows.Media.ImageDrawing> descrive l'immagine da disegnare, mentre la proprietà <xref:System.Windows.Media.ImageDrawing.Rect%2A> definisce l'area in cui viene tracciata l'immagine.  
  
 Nell'esempio riportato di seguito viene disegnata un'immagine in un rettangolo posizionata nel punto \(75,75\) vale a dire 100 x 100 [pixel](GTMT).  Nella figura riportata di seguito viene illustrato l'oggetto <xref:System.Windows.Media.ImageDrawing> creato dall'esempio.  Un bordo grigio è stato aggiunto per mostrare i limiti dell'oggetto <xref:System.Windows.Media.ImageDrawing>.  
  
 ![ImageDrawing di 100 per 100 disegnata in corrispondenza di &#40;75,75&#41;](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple-imagedrawing-offset.png "graphicsmm\_simple\_imagedrawing\_offset")  
Un oggetto ImageDrawing 100 x 100  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawing100by100inline)]
 [!code-xml[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawing100by100inline)]  
  
 Per ulteriori informazioni sulle immagini, vedere [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md).  
  
<a name="playmedia"></a>   
## Riprodurre contenuti multimediali \(Solo codice\)  
  
> [!NOTE]
>  Anche se è possibile dichiarare un oggetto <xref:System.Windows.Media.VideoDrawing> in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile caricare e riprodurre i contenuti multimediali relativi solo utilizzando il codice.  Per riprodurre video in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], utilizzare invece <xref:System.Windows.Controls.MediaElement>.  
  
 Per riprodurre un file audio o video, si utilizza un oggetto <xref:System.Windows.Media.VideoDrawing> e <xref:System.Windows.Media.MediaPlayer>.  È possibile caricare e riprodurre contenuti multimediali in due modi diversi.  Il primo consiste nell'utilizzo di <xref:System.Windows.Media.MediaPlayer> e di un oggetto <xref:System.Windows.Media.VideoDrawing> da soli e il secondo nella creazione di un oggetto <xref:System.Windows.Media.MediaTimeline> personalizzato da utilizzare con <xref:System.Windows.Media.MediaPlayer> e <xref:System.Windows.Media.VideoDrawing>.  
  
> [!NOTE]
>  Quando si distribuiscono contenuti multimediali con l'applicazione, non è possibile utilizzare un file multimediale come risorsa di progetto, come avviene per un'immagine.  Invece, è necessario impostare il tipo di contenuti multimediali su `Content` nel file del progetto e `CopyToOutputDirectory` su `PreserveNewest` o su `Always`.  
  
 Per riprodurre contenuti multimediali senza creare un oggetto <xref:System.Windows.Media.MediaTimeline> personalizzato, attenersi alla seguente procedura.  
  
1.  Creare un oggetto <xref:System.Windows.Media.MediaPlayer>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline1)]  
  
2.  Utilizzare il metodo <xref:System.Windows.Media.MediaPlayer.Open%2A> per caricare il file multimediale.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline2)]  
  
3.  Creare un oggetto <xref:System.Windows.Media.VideoDrawing>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline3)]  
  
4.  Specificare dimensioni e posizione per tracciare il contenuto multimediale impostando la proprietà <xref:System.Windows.Media.VideoDrawing.Rect%2A> dell'oggetto <xref:System.Windows.Media.VideoDrawing>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline4)]  
  
5.  Impostare la proprietà <xref:System.Windows.Media.VideoDrawing.Player%2A> dell'oggetto <xref:System.Windows.Media.VideoDrawing> con l'oggetto <xref:System.Windows.Media.MediaPlayer> creato.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline5)]  
  
6.  Utilizzare il metodo <xref:System.Windows.Media.MediaPlayer.Play%2A> dell'oggetto <xref:System.Windows.Media.MediaPlayer> per iniziare la riproduzione del contenuto multimediale.  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline6)]  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.VideoDrawing> e un oggetto <xref:System.Windows.Media.MediaPlayer> per riprodurre un file video una volta.  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 Per un ulteriore controllo della durata dei contenuti multimediali, utilizzare un oggetto <xref:System.Windows.Media.MediaTimeline> con gli oggetti <xref:System.Windows.Media.MediaPlayer> e <xref:System.Windows.Media.VideoDrawing>.  L'oggetto <xref:System.Windows.Media.MediaTimeline> consente di specificare se il file video deve essere ripetuto.  Per utilizzare un oggetto <xref:System.Windows.Media.MediaTimeline> con un oggetto <xref:System.Windows.Media.VideoDrawing>, attenersi alla seguente procedura:  
  
1.  Dichiarare l'oggetto <xref:System.Windows.Media.MediaTimeline> e impostarne i comportamenti temporali.  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline1)]  
  
2.  Creare un oggetto <xref:System.Windows.Media.MediaClock> da <xref:System.Windows.Media.MediaTimeline>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline2)]  
  
3.  Creare un oggetto <xref:System.Windows.Media.MediaPlayer> e utilizzare <xref:System.Windows.Media.MediaClock> per impostarne la proprietà <xref:System.Windows.Media.MediaPlayer.Clock%2A>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline3)]  
  
4.  Creare un oggetto <xref:System.Windows.Media.VideoDrawing> e assegnare l'oggetto <xref:System.Windows.Media.MediaPlayer> alla proprietà <xref:System.Windows.Media.VideoDrawing.Player%2A> dell'oggetto <xref:System.Windows.Media.VideoDrawing>.  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline4)]  
  
 Nell'esempio riportato di seguito viene utilizzato un elemento <xref:System.Windows.Media.MediaTimeline> con un oggetto <xref:System.Windows.Media.MediaPlayer> e un oggetto <xref:System.Windows.Media.VideoDrawing> per riprodurre ripetutamente un video.  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 Quando si utilizza un oggetto <xref:System.Windows.Media.MediaTimeline>, si impiega l'oggetto interattivo <xref:System.Windows.Media.Animation.ClockController> restituito dalla proprietà <xref:System.Windows.Media.Animation.Clock.Controller%2A> dell'oggetto <xref:System.Windows.Media.MediaClock> per controllare la riproduzione di contenuti multimediali invece dei metodi interattivi di <xref:System.Windows.Media.MediaPlayer>.  
  
<a name="drawtext"></a>   
## Creare testo  
 Per creare testo, si utilizza un oggetto <xref:System.Windows.Media.GlyphRunDrawing> e un oggetto <xref:System.Windows.Media.GlyphRun>.  Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.GlyphRunDrawing> per creare il testo "Hello World".  
  
 [!code-csharp[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GlyphRunDrawingExample.cs#glyphrundrawingexampleinline)]
 [!code-xml[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GlyphRunExample.xaml#glyphrundrawingexampleinline)]  
  
 <xref:System.Windows.Media.GlyphRun> è un oggetto di livello basso da utilizzare con scenari di presentazione e di stampa di documenti con formato fisso.  Un modo più semplice di creare testo sullo schermo consiste nell'utilizzo di <xref:System.Windows.Controls.Label> oppure di <xref:System.Windows.Controls.TextBlock>.  Per ulteriori informazioni su <xref:System.Windows.Media.GlyphRun>, vedere [Introduzione all'oggetto GlyphRun e all'elemento Glyphs](../../../../docs/framework/wpf/advanced/introduction-to-the-glyphrun-object-and-glyphs-element.md).  
  
<a name="compositedrawingssection"></a>   
## Disegni composti  
 Un oggetto <xref:System.Windows.Media.DrawingGroup> consente di combinare più disegni in un unico disegno composto.  Utilizzando un oggetto <xref:System.Windows.Media.DrawingGroup>, è possibile combinare forme, immagini e testo in un singolo oggetto <xref:System.Windows.Media.Drawing>.  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.DrawingGroup> per combinare due oggetti <xref:System.Windows.Media.GeometryDrawing> e un oggetto <xref:System.Windows.Media.ImageDrawing>.  Questo esempio produce l'output che segue.  
  
 ![DrawingGroup con più disegni](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-simple.png "graphicsmm\_simple")  
Un disegno composto  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 <xref:System.Windows.Media.DrawingGroup> consente inoltre di applicare maschere di opacità, trasformazioni, effetti bitmap e altre operazioni al contenuto relativo.  Le operazioni <xref:System.Windows.Media.DrawingGroup> vengono applicate nel seguente ordine: <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>, <xref:System.Windows.Media.DrawingGroup.Opacity%2A>, <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>, <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>, <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>, quindi <xref:System.Windows.Media.DrawingGroup.Transform%2A>.  
  
 Nella figura riportata di seguito viene illustrato l’ordine in cui vengono applicate le operazioni dell'oggetto <xref:System.Windows.Media.DrawingGroup>.  
  
 ![Ordine delle operazioni DrawingGroup](../../../../docs/framework/wpf/graphics-multimedia/media/graphcismm-drawinggroup-order.png "graphcismm\_drawinggroup\_order")  
Ordine delle operazioni dell'oggetto DrawingGroup  
  
 Nella tabella riportata di seguito vengono descritte le proprietà che si possono utilizzare per manipolare il contenuto di un oggetto <xref:System.Windows.Media.DrawingGroup>.  
  
|Proprietà|Descrizione|Illustrazione|  
|---------------|-----------------|-------------------|  
|<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>|Consente di modificare l'opacità delle porzioni selezionate del contenuto dell'oggetto <xref:System.Windows.Media.DrawingGroup>.  Per un esempio, vedere [How to: Control the Opacity of a Drawing](http://msdn.microsoft.com/it-it/68580652-7d32-4d27-93cc-a5148cf4d5ee).||  
|<xref:System.Windows.Media.DrawingGroup.Opacity%2A>|Consente di modificare in modo uniforme l'opacità del contenuto dell'oggetto <xref:System.Windows.Media.DrawingGroup>.  Utilizzare questa proprietà per rendere un oggetto <xref:System.Windows.Media.Drawing> trasparente o parzialmente trasparente.  Per un esempio, vedere [How to: Apply an Opacity Mask to a Drawing](http://msdn.microsoft.com/it-it/d77b420b-9be2-479c-a45e-82f4da30eb9f).||  
|<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>|Consente di applicare un elemento <xref:System.Windows.Media.Effects.BitmapEffect> al contenuto dell'oggetto <xref:System.Windows.Media.DrawingGroup>.  Per un esempio, vedere [How to: Apply a BitmapEffect to a Drawing](http://msdn.microsoft.com/it-it/c5b1de83-8d09-47fb-96db-5f174471f4b5).||  
|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|Consente di ritagliare il contenuto dell'oggetto <xref:System.Windows.Media.DrawingGroup> ottenendo un'area descritta mediante un oggetto <xref:System.Windows.Media.Geometry>.  Per un esempio, vedere [How to: Clip a Drawing](http://msdn.microsoft.com/it-it/1f7d8a2c-c3c2-42cb-a542-e6796f9fb058).||  
|<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>|Consente di bloccare [Device Independent Pixel](GTMT) ai pixel del dispositivo lungo le linee guida specificate.  Questa proprietà è utile per garantire che il rendering degli elementi grafici dettagliati venga eseguito con precisione su schermi a DPI basso.  Per un esempio, vedere [Applicare un GuidelineSet a un disegno](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-a-guidelineset-to-a-drawing.md).||  
|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|Consente di trasformare il contenuto dell'oggetto <xref:System.Windows.Media.DrawingGroup>.  Per un esempio, vedere [How to: Apply a Transform to a Drawing](http://msdn.microsoft.com/it-it/0d525f2b-682d-4d67-9660-cf46929fbabd).||  
  
<a name="usingimagedrawing"></a>   
## Visualizzare un disegno come immagine  
 Per visualizzare un oggetto <xref:System.Windows.Media.Drawing> con un controllo <xref:System.Windows.Controls.Image>, utilizzare un oggetto <xref:System.Windows.Media.DrawingImage> come <xref:System.Windows.Controls.Image.Source%2A> del controllo <xref:System.Windows.Controls.Image> e impostare la proprietà <xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=fullName> dell'oggetto <xref:System.Windows.Media.DrawingImage> sul disegno che si desidera visualizzare.  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.DrawingImage> e un controllo <xref:System.Windows.Controls.Image> per visualizzare un oggetto <xref:System.Windows.Media.GeometryDrawing>.  Questo esempio produce l'output che segue.  
  
 ![GeometryDrawing di due ellissi](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-geodraw.png "graphicsmm\_geodraw")  
Un oggetto DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
<a name="renderingwithdrawingbrushsection"></a>   
## Disegnare un oggetto con un oggetto Drawing  
 Un oggetto <xref:System.Windows.Media.DrawingBrush> è un tipo di pennello che traccia un'area con un oggetto Drawing.  Può essere utilizzato per disegnare quasi tutti gli oggetti grafici con un oggetto Drawing.  La proprietà <xref:System.Windows.Media.Drawing> di un oggetto <xref:System.Windows.Media.DrawingBrush> ne descrive l'oggetto <xref:System.Windows.Media.DrawingBrush.Drawing%2A>.  Per eseguire il rendering di un oggetto <xref:System.Windows.Media.Drawing> con un oggetto <xref:System.Windows.Media.DrawingBrush>, aggiungerlo al pennello utilizzando la proprietà <xref:System.Windows.Media.Drawing> del pennello e utilizzare il pennello per disegnare un oggetto grafico, come un controllo o un pannello.  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.DrawingBrush> per disegnare l'oggetto <xref:System.Windows.Shapes.Shape.Fill%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle> con un modello creato da un oggetto <xref:System.Windows.Media.GeometryDrawing>.  Questo esempio produce l'output che segue.  
  
 ![DrawingBrush affiancato](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-drawingbrush-geometrydrawing.png "graphicsmm\_drawingbrush\_geometrydrawing")  
Un oggetto GeometryDrawing utilizzato con un oggetto DrawingBrush  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-xml[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 La classe <xref:System.Windows.Media.DrawingBrush> fornisce una serie di opzioni per l'allungamento e l'affiancamento del contenuto.  Per ulteriori informazioni su <xref:System.Windows.Media.DrawingBrush>, vedere [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).  
  
<a name="renderingwithvisualsection"></a>   
## Rendering di un disegno con un oggetto Visual  
 <xref:System.Windows.Media.DrawingVisual> è un tipo di oggetto Visual progettato per eseguire il rendering di un disegno.  Lavorare direttamente a livello visivo è un'opportunità per gli sviluppatori che desiderano creare un ambiente grafico altamente personalizzato, ma questo argomento non viene descritto in questi cenni preliminari.  Per ulteriori informazioni, vedere [Utilizzo degli oggetti DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md).  
  
<a name="drawingcontextobjects"></a>   
## Oggetti DrawingContext  
 La classe <xref:System.Windows.Media.DrawingContext> consente di popolare un oggetto <xref:System.Windows.Media.Visual> oppure <xref:System.Windows.Media.Drawing> con contenuto visivo.  Molti oggetti grafici di livello inferiore di questo tipo utilizzano un oggetto <xref:System.Windows.Media.DrawingContext> perché descrive il contenuto grafico in modo molto efficace.  
  
 Sebbene i metodi di disegno di <xref:System.Windows.Media.DrawingContext> possano sembrare simili ai metodi di disegno di <xref:System.Drawing.Graphics?displayProperty=fullName>, sono effettivamente molto diversi.  <xref:System.Windows.Media.DrawingContext> viene utilizzato con un sistema grafico in modalità differita, mentre il tipo <xref:System.Drawing.Graphics?displayProperty=fullName> viene utilizzato con un sistema grafico a modalità immediata.  Quando si utilizzano i comandi di disegno di un oggetto <xref:System.Windows.Media.DrawingContext>, si archivia un insieme di istruzioni di redering \(sebbene l'esatto meccanismo di archiviazione dipenda dal tipo di oggetto che fornisce l'oggetto <xref:System.Windows.Media.DrawingContext>\), che verrà utilizzato in un secondo tempo dal sistema grafico. Non si disegna sullo schermo in tempo reale.  Per ulteriori informazioni sul funzionamento del sistema grafico di [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)], vedere [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md).  
  
 Non si crea mai direttamente un'istanza di <xref:System.Windows.Media.DrawingContext>, tuttavia è possibile acquisire un contesto di disegno tramite determinati metodi, ad esempio <xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=fullName> e <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=fullName>.  
  
<a name="enumeratevisualcontents"></a>   
## Enumerare il contenuto di un oggetto Visual  
 Oltre agli altri utilizzi, gli oggetti <xref:System.Windows.Media.Drawing> forniscono anche un modello a oggetti per l'enumerazione del contenuto di un oggetto <xref:System.Windows.Media.Visual>.  
  
 Nell’esempio riportato di seguito viene utilizzato il metodo <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> per recuperare il valore <xref:System.Windows.Media.DrawingGroup> di un oggetto <xref:System.Windows.Media.Visual> e per enumerarlo.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## Vedere anche  
 <xref:System.Windows.Media.Drawing>   
 <xref:System.Windows.Media.DrawingGroup>   
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Disegnare con oggetti Image, Drawing e Visual](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)   
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Cenni preliminari sugli oggetti Shape e sulle funzionalità di disegno di base di WPF](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Cenni preliminari sul rendering della grafica WPF](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/drawings-how-to-topics.md)