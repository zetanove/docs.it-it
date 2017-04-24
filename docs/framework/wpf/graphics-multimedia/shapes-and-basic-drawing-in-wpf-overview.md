---
title: "Cenni preliminari sugli oggetti Shape e sulle funzionalit&#224; di disegno di base di WPF | Microsoft Docs"
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
  - "disegno di base"
  - "Shape (oggetti)"
  - "forme, informazioni sulle forme"
  - "disegno vettoriale, panoramica"
  - "vettori, disegno"
ms.assetid: 66d7a6d6-e3b6-47bc-8dfe-8a1b26f7d901
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sugli oggetti Shape e sulle funzionalit&#224; di disegno di base di WPF
In questo argomento vengono forniti cenni preliminari su come disegnare con oggetti <xref:System.Windows.Shapes.Shape>.  <xref:System.Windows.Shapes.Shape> è un tipo di <xref:System.Windows.UIElement> che consente di disegnare una forma sullo schermo.  Poiché si tratta di elementi dell'interfaccia utente, è possibile utilizzare gli oggetti <xref:System.Windows.Shapes.Shape> all'interno degli elementi <xref:System.Windows.Controls.Panel> e della maggior parte dei controlli.  
  
 In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] vengono offerti molti livelli di accesso alla grafica e ai servizi di rendering.  Al livello superiore, gli oggetti <xref:System.Windows.Shapes.Shape> sono facili da utilizzare e forniscono varie funzionalità utili, ad esempio il layout e la partecipazione nel sistema di eventi [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  
  
   
  
<a name="shapes"></a>   
## Oggetti Shape  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre vari oggetti <xref:System.Windows.Shapes.Shape> pronti all'uso.  Tutti gli oggetti Shape ereditano dalla classe <xref:System.Windows.Shapes.Shape>.  Gli oggetti Shape disponibili comprendono <xref:System.Windows.Shapes.Ellipse>, <xref:System.Windows.Shapes.Line>, <xref:System.Windows.Shapes.Path>, <xref:System.Windows.Shapes.Polygon>, <xref:System.Windows.Shapes.Polyline> e <xref:System.Windows.Shapes.Rectangle>. Gli oggetti <xref:System.Windows.Shapes.Shape> condividono le seguenti proprietà comuni.  
  
-   <xref:System.Windows.Shapes.Shape.Stroke%2A>: indica come viene disegnata la struttura della forma.  
  
-   <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>: indica lo spessore della struttura della forma.  
  
-   <xref:System.Windows.Shapes.Shape.Fill%2A>: indica come viene disegnata la parte interna della forma.  
  
-   Proprietà dei dati per specificare coordinate e vertici, misurati in [pixel indipendenti dal dispositivo](GTMT).  
  
 Dal momento che derivano da <xref:System.Windows.UIElement>, gli oggetti Shape possono essere utilizzati nei pannelli e nella maggior parte dei controlli.  Il pannello <xref:System.Windows.Controls.Canvas> è particolarmente indicato per la creazione di disegni complessi, poiché supporta il posizionamento assoluto degli oggetti figlio.  
  
 La classe <xref:System.Windows.Shapes.Line> consente di disegnare una riga tra due punti.  Nell'esempio riportato di seguito vengono illustrate molte modalità per specificare le coordinate della riga e le proprietà del tratto.  
  
 [!code-xml[drawingwithshapeelements#LineExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 [!code-cpp[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/cpp/VS_Snippets_Wpf/ShapesProcedural/CPP/ShapesProcedural.cpp#shapesproceduralline)]
 [!code-csharp[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ShapesProcedural/Csharp/ShapesProcedural.cs#shapesproceduralline)]
 [!code-vb[shapesprocedural#ShapesProceduralLine](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ShapesProcedural/VisualBasic/ShapesProceduralVB.vb#shapesproceduralline)]  
  
 Nell'immagine riportata di seguito viene illustrato <xref:System.Windows.Shapes.Line> sottoposto a rendering.  
  
 ![Illustrazione di Line](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-line2.png "shape\_ovw\_line2")  
  
 Anche se la classe <xref:System.Windows.Shapes.Line> fornisce una proprietà <xref:System.Windows.Shapes.Shape.Fill%2A>, l'impostazione di tale proprietà non ha effetto poiché un oggetto <xref:System.Windows.Shapes.Line> non dispone di area.  
  
 Un'altra forma comune è <xref:System.Windows.Shapes.Ellipse>.  Creare un oggetto <xref:System.Windows.Shapes.Ellipse> definendo le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> della forma.  Per disegnare un cerchio, specificare un oggetto <xref:System.Windows.Shapes.Ellipse> i cui valori <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> siano uguali.  
  
 [!code-xml[ShapeOverviews#ShapesOVW1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ShapeOverviews/CS/Window1.xaml#shapesovw1)]  
  
 [!code-csharp[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/CSharp/SetBackgroundColorOfShapeExample.cs#setbackgroundcolorofshapecodeexamplewholepage)]
 [!code-vb[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/visualbasic/setbackgroundcolorofshapeexample.vb#setbackgroundcolorofshapecodeexamplewholepage)]  
  
 Nell'immagine riportata di seguito viene illustrato un esempio di <xref:System.Windows.Shapes.Ellipse> sottoposto a rendering.  
  
 ![Illustrazione di Ellipse](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-ellipse2.png "shape\_ovw\_ellipse2")  
  
<a name="paths"></a>   
## Utilizzo di percorsi e geometrie  
 La classe <xref:System.Windows.Shapes.Path> consente di disegnare curve e forme complesse.  Queste curve e forme vengono descritte utilizzando oggetti <xref:System.Windows.Media.Geometry>.  Per utilizzare <xref:System.Windows.Shapes.Path>, creare un oggetto <xref:System.Windows.Media.Geometry> e utilizzarlo per impostare la proprietà <xref:System.Windows.Shapes.Path.Data%2A> dell'oggetto <xref:System.Windows.Shapes.Path>.  
  
 Sono disponibili numerosi oggetti <xref:System.Windows.Media.Geometry> tra cui scegliere.  Le classi <xref:System.Windows.Media.LineGeometry>, <xref:System.Windows.Media.RectangleGeometry> e <xref:System.Windows.Media.EllipseGeometry> descrivono forme relativamente semplici.  Per creare forme più complesse o curve, utilizzare un oggetto <xref:System.Windows.Media.PathGeometry>.  
  
<a name="pathgeometry"></a>   
### PathGeometry e PathSegments  
 Gli oggetti <xref:System.Windows.Media.PathGeometry> sono composti da uno o più oggetti <xref:System.Windows.Media.PathFigure>, ciascuno dei quali rappresenta una figura o forma diversa.  Ciascun oggetto <xref:System.Windows.Media.PathFigure> è a sua volta composto da uno o più oggetti <xref:System.Windows.Media.PathSegment>, ognuno dei quali rappresenta una parte collegata della figura o forma.  I tipi di segmento comprendono: <xref:System.Windows.Media.LineSegment>, <xref:System.Windows.Media.BezierSegment> e <xref:System.Windows.Media.ArcSegment>.  
  
 Nell'esempio riportato di seguito, viene utilizzato un oggetto <xref:System.Windows.Shapes.Path> per disegnare una curva di Bézier quadratica.  
  
 [!code-xml[geometrysample#34](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 Nell'immagine riportata di seguito viene illustrata la forma sottoposta a rendering.  
  
 ![Illustrazione di Path](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-path2.png "shape\_ovw\_path2")  
  
 Per ulteriori informazioni su <xref:System.Windows.Media.PathGeometry> e sulle altre classi <xref:System.Windows.Media.Geometry>, vedere [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
<a name="pathdatastring"></a>   
### Sintassi abbreviata XAML  
 In [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], è possibile utilizzare anche una sintassi abbreviata speciale per descrivere un oggetto <xref:System.Windows.Shapes.Path>.  Nell'esempio riportato di seguito, viene utilizzata la sintassi abbreviata per disegnare una forma complessa.  
  
```xaml  
<Path Stroke="DarkGoldenRod" StrokeThickness="3"   
Data="M 100,200 C 100,25 400,350 400,175 H 280" />  
```  
  
 Nell'immagine riportata di seguito viene illustrato <xref:System.Windows.Shapes.Path> sottoposto a rendering.  
  
 ![Illustrazione di Path](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-path.png "shape\_ovw\_path")  
  
 La stringa di attributo <xref:System.Windows.Shapes.Path.Data%2A> inizia con il comando "moveto", indicato da M, mediante il quale viene stabilito un punto di partenza per il percorso nel sistema di coordinate dell'oggetto <xref:System.Windows.Controls.Canvas>.  Nei parametri di dati di <xref:System.Windows.Shapes.Path> viene fatta distinzione tra maiuscole e minuscole.  La lettera M maiuscola indica un percorso assoluto per il nuovo punto corrente.  Una lettera m minuscola indica le coordinate relative.  Il primo segmento è una [curva di Bézier](GTMT) cubica che inizia in corrispondenza del punto \(100,200\) e termina in corrispondenza del punto \(400,175\) e viene disegnata utilizzando i due punti di controllo \(100,25\) e \(400,350\).  Questo segmento è indicato dal comando C nella stringa di attributo <xref:System.Windows.Shapes.Path.Data%2A>.  Anche in questo caso, la lettera C maiuscola indica un percorso assoluto, mentre la lettera c minuscola indica un percorso relativo.  
  
 Il secondo segmento inizia con un comando orizzontale assoluto "lineto" H, che specifica una riga disegnata dal punto finale del sottopercorso precedente \(400,175\) a un nuovo punto finale \(280,175\).  Poiché si tratta di un comando orizzontale "lineto", il valore specificato è una coordinata *x*.  
  
 Per la sintassi completa del percorso, vedere il riferimento <xref:System.Windows.Shapes.Path.Data%2A> e [Creare una forma utilizzando un oggetto PathGeometry](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-shape-by-using-a-pathgeometry.md).  
  
<a name="fillpaint"></a>   
## Disegno di oggetti Shape  
 Gli oggetti <xref:System.Windows.Media.Brush> vengono utilizzati per creare le proprietà <xref:System.Windows.Shapes.Shape.Stroke%2A> e <xref:System.Windows.Shapes.Shape.Fill%2A> di una forma.  Nell'esempio riportato di seguito, vengono specificati il tratto e il riempimento di un oggetto <xref:System.Windows.Shapes.Ellipse>.  Si noti che un input valido per le proprietà del pennello può essere rappresentato da una parola chiave o da un valore di colore esadecimale.  Per ulteriori informazioni sulle parole chiave di colore disponibili, vedere le proprietà della classe <xref:System.Windows.Media.Colors> nello spazio dei nomi <xref:System.Windows.Media>.  
  
```  
  
<Canvas Background="LightGray">   
   <Ellipse  
      Canvas.Top="50"  
      Canvas.Left="50"  
      Fill="#FFFFFF00"  
      Height="75"  
      Width="75"  
      StrokeThickness="5"  
      Stroke="#FF0000FF"/>  
</Canvas>  
  
```  
  
 Nell'immagine riportata di seguito viene illustrato l'oggetto <xref:System.Windows.Shapes.Ellipse> sottoposto a rendering.  
  
 ![Ellisse](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-ellipsefill.png "shape\_ovw\_ellipsefill")  
  
 In alternativa, è possibile utilizzare la sintassi degli elementi delle proprietà per creare in modo esplicito un oggetto <xref:System.Windows.Media.SolidColorBrush> per disegnare la forma con un colore a tinta unita.  
  
```  
  
<!-- This polygon shape uses pre-defined color values for its Stroke and  
     Fill properties.   
     The SolidColorBrush's Opacity property affects the fill color in   
     this case by making it slightly transparent (opacity of 0.4) so   
     that it blends with any underlying color. -->  
  
<Polygon  
    Points="300,200 400,125 400,275 300,200"  
    Stroke="Purple"   
    StrokeThickness="2">  
    <Polygon.Fill>  
       <SolidColorBrush Color="Blue" Opacity="0.4"/>  
    </Polygon.Fill>  
</Polygon>  
```  
  
 Nell'immagine riportata di seguito viene illustrata la forma sottoposta a rendering.  
  
 ![Illustrazione di SolidColorBrush](../../../../docs/framework/wpf/graphics-multimedia/media/shape-ovw-solidcolorbrush.png "shape\_ovw\_solidcolorbrush")  
  
 Inoltre, è possibile disegnare il tratto o il riempimento di una forma con sfumature, immagini, pattern e così via.  Per ulteriori informazioni, vedere [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).  
  
<a name="stretchableshapessection"></a>   
## Oggetti Shape allungabili  
 Le classi <xref:System.Windows.Shapes.Line>, <xref:System.Windows.Shapes.Path>, <xref:System.Windows.Shapes.Polygon>, <xref:System.Windows.Shapes.Polyline> e <xref:System.Windows.Shapes.Rectangle> dispongono tutte di una proprietà <xref:System.Windows.Shapes.Shape.Stretch%2A>.  Questa proprietà determina la modalità in cui il contenuto di un oggetto <xref:System.Windows.Shapes.Shape> \(forma da disegnare\) viene allungato per riempire lo spazio del layout di <xref:System.Windows.Shapes.Shape>.  Lo spazio del layout di un oggetto <xref:System.Windows.Shapes.Shape> è la quantità di spazio allocato a <xref:System.Windows.Shapes.Shape> dal sistema di layout, tramite un'impostazione esplicita di <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> o tramite le impostazioni di <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>.  Per ulteriori informazioni sul layout in Windows Presentation Foundation, vedere i cenni preliminari in [Layout](../../../../docs/framework/wpf/advanced/layout.md).  
  
 La proprietà Stretch accetta uno dei seguenti valori:  
  
-   <xref:System.Windows.Media.Stretch>: il contenuto dell'oggetto <xref:System.Windows.Shapes.Shape> non viene allungato.  
  
-   <xref:System.Windows.Media.Stretch>: il contenuto dell'oggetto <xref:System.Windows.Shapes.Shape> viene allungato per riempire lo spazio del layout.  Le proporzioni non vengono mantenute.  
  
-   <xref:System.Windows.Media.Stretch>: il contenuto dell'oggetto <xref:System.Windows.Shapes.Shape> viene allungato il più possibile per riempire lo spazio del layout mantenendo le proporzioni originali.  
  
-   <xref:System.Windows.Media.Stretch>: il contenuto dell'oggetto <xref:System.Windows.Shapes.Shape> viene allungato il più possibile per riempire completamente lo spazio del layout mantenendo le proporzioni originali.  
  
 Si noti che, quando il contenuto di un oggetto <xref:System.Windows.Shapes.Shape> viene allungato, la struttura dell'oggetto <xref:System.Windows.Shapes.Shape> viene disegnata dopo l'allungamento.  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Shapes.Polygon> per disegnare un triangolo molto piccolo da \(0,0\) a \(0,1\) a \(1,1\).  Le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> dell'oggetto <xref:System.Windows.Shapes.Polygon> vengono impostate su 100 e la proprietà Stretch viene impostata su Fill.  Di conseguenza, il contenuto dell'oggetto <xref:System.Windows.Shapes.Polygon> \(triangolo\) viene allungato per riempire lo spazio più ampio.  
  
```  
...  
<Polygon  
  Points="0,0 0,1 1,1"  
  Fill="Blue"  
  Width="100"  
  Height="100"  
  Stretch="Fill"  
  Stroke="Black"  
  StrokeThickness="2" />  
...  
```  
  
```  
...  
PointCollection myPointCollection = new PointCollection();  
myPointCollection.Add(new Point(0,0));  
myPointCollection.Add(new Point(0,1));  
myPointCollection.Add(new Point(1,1));  
  
Polygon myPolygon = new Polygon();  
myPolygon.Points = myPointCollection;  
myPolygon.Fill = Brushes.Blue;  
myPolygon.Width = 100;  
myPolygon.Height = 100;  
myPolygon.Stretch = Stretch.Fill;  
myPolygon.Stroke = Brushes.Black;  
myPolygon.StrokeThickness = 2;  
...  
```  
  
<a name="transforms"></a>   
## Trasformazione degli oggetti Shape  
 La classe <xref:System.Windows.Media.Transform> fornisce i mezzi per trasformare le forme su un piano bidimensionale.  I diversi tipi di trasformazione includono la rotazione \(<xref:System.Windows.Media.RotateTransform>\),il ridimensionamento \(<xref:System.Windows.Media.ScaleTransform>\), l'inclinazione \(<xref:System.Windows.Media.SkewTransform>\) e la traslazione \(<xref:System.Windows.Media.TranslateTransform>\).  
  
 Una trasformazione comune da applicare a una forma è una rotazione.  Per ruotare una forma, creare un oggetto <xref:System.Windows.Media.RotateTransform> e specificarne la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A>.  Una proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> pari a 45 consente di ruotare l'elemento di 45 gradi in senso orario; un angolo di rotazione pari a 90 consente di ruotare l'elemento di 90 gradi in senso orario e così via.  Impostare le proprietà <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> per controllare il punto in cui viene ruotato l'elemento.  Questi valori di proprietà sono espressi nello spazio delle coordinate dell'elemento trasformato.  <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> sono impostati sul valore predefinito 0 \(zero\).  Infine, applicare <xref:System.Windows.Media.RotateTransform> all'elemento.  Per evitare che la trasformazione influisca sul layout, impostare la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> della forma.  
  
 Nell'esempio riportato di seguito, viene utilizzato <xref:System.Windows.Media.RotateTransform> per ruotare una forma di 45 gradi rispetto all'angolo in alto a sinistra della forma stessa \(0,0\).  
  
 [!code-xml[transformssample#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#14)]  
  
 Nell'esempio successivo, un'altra forma viene ruotata di 45 gradi, ma in questo caso rispetto al punto \(25,50\).  
  
 [!code-xml[transformssample#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#15)]  
  
 Nell'immagine riportata di seguito vengono illustrati i risultati dell'applicazione delle due trasformazioni.  
  
 ![Rotazioni di 45 gradi con punti centrali diversi](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-rotatetransform45degrees.png "wcpsdk\_graphicsmm\_rotatetransform45degrees")  
  
 Negli esempi precedenti, è stata applicata una sola trasformazione a ogni oggetto Shape.  Per applicare più trasformazioni a una forma \(o a qualsiasi altro elemento dell'interfaccia utente\), utilizzare un oggetto <xref:System.Windows.Media.TransformGroup>.  
  
## Vedere anche  
 [Grafica bidimensionale e creazione di immagini](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [Cenni sul disegno con colori a tinta unita e sfumature](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)   
 [Cenni preliminari sulle classi Geometry](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)