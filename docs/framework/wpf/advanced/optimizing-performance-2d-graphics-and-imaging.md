---
title: "Ottimizzazione delle prestazioni: grafica bidimensionale e creazione di immagini | Microsoft Docs"
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
  - "2D (grafica)"
  - "disegno, ottimizzazione delle prestazioni"
  - "grafica, prestazioni"
  - "immagini, ottimizzazione delle prestazioni"
  - "creazione di immagini, ottimizzazione delle prestazioni"
  - "forme, ottimizzazione delle prestazioni"
ms.assetid: e335601e-28c8-4d64-ba27-778fffd55f72
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# Ottimizzazione delle prestazioni: grafica bidimensionale e creazione di immagini
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un'ampia gamma di funzionalità di grafica bidimensionale e di creazione dell'immagine che possono essere ottimizzate in base ai requisiti dell'applicazione.  In questo argomento sono fornite informazioni sull'ottimizzazione delle prestazioni in tali aree.  
  
   
  
<a name="Drawing_and_Shapes"></a>   
## Disegno e forme  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce gli oggetti <xref:System.Windows.Media.Drawing> e <xref:System.Windows.Shapes.Shape> al fine di rappresentare il contenuto del disegno grafico.  Tuttavia, gli oggetti <xref:System.Windows.Media.Drawing> sono costrutti più semplici rispetto agli oggetti <xref:System.Windows.Shapes.Shape> e forniscono caratteristiche di prestazioni migliori.  
  
 Un oggetto <xref:System.Windows.Shapes.Shape> consente di disegnare una forma grafica sullo schermo.  Dal momento che sono derivati dalla classe <xref:System.Windows.FrameworkElement>, gli oggetti <xref:System.Windows.Shapes.Shape> possono essere utilizzati nei pannelli e nella maggior parte dei controlli.  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono offerti molti livelli di accesso alla grafica e ai servizi di rendering.  Al livello superiore, gli oggetti <xref:System.Windows.Shapes.Shape> sono facili da utilizzare e forniscono varie funzionalità utili, ad esempio il layout e la gestione degli eventi.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre vari oggetti forma pronti all'uso.  Tutti gli oggetti Shape ereditano dalla classe <xref:System.Windows.Shapes.Shape>.  Gli oggetti Shape disponibili includono <xref:System.Windows.Shapes.Ellipse>, <xref:System.Windows.Shapes.Line>, <xref:System.Windows.Shapes.Path>, <xref:System.Windows.Shapes.Polygon>, <xref:System.Windows.Shapes.Polyline>e <xref:System.Windows.Shapes.Rectangle>.  
  
 D'altra parte, gli oggetti <xref:System.Windows.Media.Drawing> non derivano dalla classe <xref:System.Windows.FrameworkElement> e forniscono un'implementazione più semplice per eseguire il rendering di forme, immagini e testo.  
  
 Esistono quattro tipi di oggetti <xref:System.Windows.Media.Drawing>:  
  
-   <xref:System.Windows.Media.GeometryDrawing> Consente di disegnare una forma.  
  
-   <xref:System.Windows.Media.ImageDrawing> Consente di disegnare un'immagine.  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> Consente di disegnare un testo.  
  
-   <xref:System.Windows.Media.DrawingGroup> Consente di eseguire altri disegni.  Utilizzare un gruppo di disegni per combinare altri disegni in un unico disegno composto.  
  
 L'oggetto <xref:System.Windows.Media.GeometryDrawing> viene utilizzato per eseguire il rendering del contenuto della geometria.  La classe <xref:System.Windows.Media.Geometry> e le classi concrete che derivano da essa, quali <xref:System.Windows.Media.CombinedGeometry>, <xref:System.Windows.Media.EllipseGeometry> e <xref:System.Windows.Media.PathGeometry>, forniscono un modo per eseguire il rendering di immagini bidimensionali, nonché per offrire il supporto per l'hit\-testing e il ritaglio.  Gli oggetti Geometry possono essere utilizzati per definire, ad esempio, l'area di un controllo o l'area di ritaglio da applicare a un'immagine  e possono essere semplici aree, quali rettangoli o cerchi, oppure aree composite create con due o più oggetti Geometry.  Combinando gli oggetti derivati da <xref:System.Windows.Media.PathSegment>, quali <xref:System.Windows.Media.ArcSegment>, <xref:System.Windows.Media.BezierSegment> e <xref:System.Windows.Media.QuadraticBezierSegment>, è possibile creare aree geometriche più complesse.  
  
 Apparentemente, la classe <xref:System.Windows.Media.Geometry> e la classe  <xref:System.Windows.Shapes.Shape> sono abbastanza simili.  Entrambe sono utilizzate per il rendering di immagini bidimensionali e dispongono di classi concrete derivate simili, ad esempio <xref:System.Windows.Media.EllipseGeometry> e <xref:System.Windows.Shapes.Ellipse>.  Vi sono, tuttavia, alcune differenze rilevanti tra questi due insiemi di classi.  La classe <xref:System.Windows.Media.Geometry> non dispone di alcune funzionalità della classe <xref:System.Windows.Shapes.Shape>, ad esempio la possibilità di disegnarsi.  Per disegnare un oggetto Geometry, è necessario utilizzare un'altra classe, ad esempio DrawingContext, Drawing oppure Path \(notare che Path è un oggetto Shape\), al fine di eseguire l'operazione di disegno.  Le proprietà di rendering, ad esempio il riempimento, il tratto e lo spessore del tratto si trovano nella classe che consente di disegnare l'oggetto Geometry, mentre un oggetto forma contiene queste proprietà.  Questa differenza prevede, ad esempio, che un oggetto Geometry definisca un'area, ad esempio un cerchio, mentre un oggetto Shape definisce un'area, il modo in cui quest'area viene riempita e delineata e partecipa al sistema di layout.  
  
 Dal momento che gli oggetti <xref:System.Windows.Shapes.Shape> derivano dalla classe <xref:System.Windows.FrameworkElement>, il loro utilizzo può aumentare in modo significativo il consumo della memoria dell'applicazione.  Se non si necessita delle funzionalità dell'oggetto <xref:System.Windows.FrameworkElement> per il contenuto grafico, prendere in considerazione l'utilizzo di oggetti <xref:System.Windows.Media.Drawing> più semplici.  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Drawing>, vedere [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md).  
  
<a name="StreamGeometry_Objects"></a>   
## Oggetti StreamGeometry  
 L'oggetto <xref:System.Windows.Media.StreamGeometry> è un'alternativa più semplice all'oggetto <xref:System.Windows.Media.PathGeometry> per la creazione di forme geometriche.  Se è necessario descrivere una geometria complessa, utilizzare <xref:System.Windows.Media.StreamGeometry>.  L'oggetto <xref:System.Windows.Media.StreamGeometry> è ottimizzato per la gestione di molti oggetti <xref:System.Windows.Media.PathGeometry> e offre prestazioni migliori, se confrontato con l'utilizzo di più oggetti <xref:System.Windows.Media.PathGeometry> singoli.  
  
 Nell'esempio riportato di seguito viene utilizzata la sintassi dell'attributo per creare un oggetto <xref:System.Windows.Media.StreamGeometry> triangolare in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[GeometriesMiscSnippets_snip#StreamGeometryTriangleExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/StreamGeometryExample.xaml#streamgeometrytriangleexamplewholepage)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.StreamGeometry>, vedere [Creare una forma utilizzando un oggetto StreamGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-using-a-streamgeometry.md).  
  
<a name="DrawingVisual_Objects"></a>   
## Oggetti DrawingVisual  
 L'oggetto <xref:System.Windows.Media.DrawingVisual> rappresenta una classe di disegno semplificata utilizzata per eseguire il rendering di forme, immagini o testo.  Questa classe è considerata semplice perché non fornisce la gestione del layout o degli eventi, migliorando in tal modo le prestazioni.  Per questo motivo, i disegni sono ideali per gli sfondi e per ClipArt.  Per ulteriori informazioni, vedere [Utilizzo degli oggetti DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md).  
  
<a name="Images"></a>   
## Immagini  
 La creazione dell'immagine tramite [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre un miglioramento significativo rispetto alle funzionalità di creazione dell'immagine delle precedenti versioni di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  Le funzionalità di creazione dell'immagine, ad esempio la visualizzazione di una bitmap o l'utilizzo di un'immagine per un controllo comune, inizialmente erano gestiti dalle interfacce API \(Application Programming Interface\) Graphics Device Interface \(GDI\) o GDI\+ di Microsoft Windows.  Queste API fornivano la funzionalità di creazione dell'immagine di base, ma non erano dotate di funzioni quali il supporto per l'estendibilità dei codec e per immagini di elevata fedeltà.  Le API per la creazione dell'immagine tramite WPF sono state riprogettate per risolvere i difetti delle interfacce GDI e GDI\+ e per fornire un nuovo gruppo di API al fine di visualizzare e utilizzare immagini nelle applicazioni.  
  
 Per ottenere prestazioni migliori, in caso di utilizzo di immagini, attenersi alle indicazioni seguenti:  
  
-   Se l'applicazione richiede la visualizzazione di immagini di anteprima, creare una versione ridotta dell'immagine.  Per impostazione predefinita, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], l'immagine viene caricata e decodificata con le dimensioni originali.  Sebbene si desideri soltanto un'immagine di anteprima, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], l'immagine viene comunque decodificata con le dimensioni originali, e successivamente, ridimensionata in base alle esigenze dell'anteprima.  Per evitare questa operazione inutile, è possibile richiedere a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di decodificare l'immagine con le dimensioni dell'anteprima o di caricare l'immagine di anteprima.  
  
-   Decodificare sempre l'immagine con le dimensioni desiderate e non con quelle predefinite.  Pertanto, richiedere a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di effettuare la codifica secondo le dimensioni desiderate e non quelle predefinite.  In tal modo, è possibile ridurre il working set dell'applicazione e la velocità di esecuzione.  
  
-   Se possibile, unire le immagini in una singola immagine, ad esempio una striscia di pellicola composta da più immagini.  
  
-   Per ulteriori informazioni, vedere [Cenni preliminari sulla creazione dell'immagine](../../../../docs/framework/wpf/graphics-multimedia/imaging-overview.md).  
  
### BitmapScalingMode  
 Quando si aggiunge un'animazione alla scala di una bitmap, talvolta è possibile che l'algoritmo di ricampionamento delle immagini di elevata qualità determini il consumo di risorse di sistema fino a rallentare la frequenza dei fotogrammi, causando l'irregolarità delle animazioni.  Impostando la proprietà <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A> dell'oggetto <xref:System.Windows.Media.RenderOptions> su <xref:System.Windows.Media.BitmapScalingMode>, è possibile creare un'animazione più uniforme e fluida quando si ridimensiona una bitmap.  La modalità <xref:System.Windows.Media.BitmapScalingMode> consente al motore di rendering [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di passare da un algoritmo ottimizzato per la qualità a un algoritmo ottimizzato per la velocità durante l'elaborazione delle immagini.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare la proprietà <xref:System.Windows.Media.BitmapScalingMode> per un oggetto Image.  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet2)]
 [!code-vb[RenderOptions#RenderOptionsSnippet2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet2)]  
  
### CachingHint  
 Per impostazione predefinita, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] il contenuto degli oggetti <xref:System.Windows.Media.TileBrush> \(ad esempio <xref:System.Windows.Media.DrawingBrush> e <xref:System.Windows.Media.VisualBrush>\) sottoposto a rendering non viene memorizzato nella cache.  Negli scenari statici in cui il contenuto e l'utilizzo dell'oggetto <xref:System.Windows.Media.TileBrush> rimangono invariati nella scena, tale comportamento è opportuno poiché consente di conservare la memoria video.  Tale comportamento non ha senso se un oggetto <xref:System.Windows.Media.TileBrush> con contenuto statico viene utilizzato in modo non statico, ad esempio nel caso di un oggetto <xref:System.Windows.Media.DrawingBrush> o <xref:System.Windows.Media.VisualBrush> statico che viene mappato alla superficie di un oggetto tridimensionale rotante.  Il comportamento predefinito di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste nell'eseguire nuovamente il rendering dell'intero contenuto dell'oggetto <xref:System.Windows.Media.DrawingBrush> o <xref:System.Windows.Media.VisualBrush> per ogni fotogramma, anche se il contenuto rimane invariato.  
  
 Impostando la proprietà <xref:System.Windows.Media.RenderOptions.CachingHint%2A> dell'oggetto <xref:System.Windows.Media.RenderOptions> su <xref:System.Windows.Media.CachingHint>, è possibile migliorare le prestazioni tramite versioni memorizzate nella cache degli oggetti pennello affiancati.  
  
 I valori delle proprietà <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A> e <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> sono valori di dimensione relativi che determinano il momento in cui è necessario rigenerare l'oggetto <xref:System.Windows.Media.TileBrush> a causa di modifiche in termini di ridimensionamento.  Se, ad esempio, la proprietà <xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A> è impostata su 2,0, è necessario rigenerare la cache per l'oggetto <xref:System.Windows.Media.TileBrush> solo quando la relativa dimensione supera di due volte la dimensione della cache corrente.  
  
 Nell'esempio seguente viene mostrato come utilizzare l'opzione relativa al suggerimento di memorizzazione nella cache per un oggetto <xref:System.Windows.Media.DrawingBrush>.  
  
 [!code-csharp[RenderOptions#RenderOptionsSnippet3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RenderOptions/CSharp/Window1.xaml.cs#renderoptionssnippet3)]
 [!code-vb[RenderOptions#RenderOptionsSnippet3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RenderOptions/visualbasic/window1.xaml.vb#renderoptionssnippet3)]  
  
## Vedere anche  
 [Ottimizzazione delle prestazioni di applicazioni WPF](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [Pianificazione delle prestazioni dell'applicazione](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [Sfruttare appieno l'hardware](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [Comportamento dell'oggetto](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Risorse delle applicazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Altri suggerimenti relativi alle prestazioni](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)   
 [Suggerimenti sulle animazioni](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)