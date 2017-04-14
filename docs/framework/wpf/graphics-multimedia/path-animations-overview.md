---
title: "Panoramica sulle animazioni percorso | Microsoft Docs"
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
  - "animazione, i percorsi"
  - "animazioni di percorso"
ms.assetid: 979c732c-df74-47a6-be96-8e07b3707d53
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Panoramica sulle animazioni percorso
<a name="introduction"></a>Questo argomento vengono presentate le animazioni di percorso, che consentono di utilizzare un percorso geometrico per generare valori di output. Le animazioni di percorso sono utili per lo spostamento e rotazione di oggetti lungo percorsi complessi.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] le funzionalità di animazione. Per un'introduzione alle funzionalità di animazione, vedere il [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Poiché si utilizza un <xref:System.Windows.Media.PathGeometry> oggetto per definire un'animazione percorso, è inoltre necessario avere familiarità con <xref:System.Windows.Media.PathGeometry> e i diversi tipi di <xref:System.Windows.Media.PathSegment> oggetti. Per ulteriori informazioni, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
<a name="what_is_a_path_animation"></a>   
## <a name="what-is-a-path-animation"></a>Che cos'è un'animazione percorso?  
 Un'animazione percorso è un tipo di <xref:System.Windows.Media.Animation.AnimationTimeline> che utilizza un <xref:System.Windows.Media.PathGeometry> come input. Anziché impostare a da, o dalla proprietà (come avviene per From/To/By animazione) o utilizzando i fotogrammi chiave (come si utilizza per un'animazione con fotogrammi chiave), si definisce un percorso geometrico e utilizzarlo per impostare il `PathGeometry` proprietà dell'animazione percorso. Man mano che procede l'animazione percorso, legge la x, y e informazioni sull'angolo dal percorso e le informazioni vengono utilizzate per generare l'output.  
  
 Le animazioni di percorso sono molto utili per animare un oggetto lungo un percorso complesso. Per spostare un oggetto lungo un percorso consiste nell'utilizzare un <xref:System.Windows.Media.MatrixTransform> e <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> per trasformare un oggetto lungo un percorso complesso. Nell'esempio seguente viene illustrata questa tecnica utilizzando il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> oggetto per animare il <xref:System.Windows.Media.MatrixTransform.Matrix%2A> proprietà di un <xref:System.Windows.Media.MatrixTransform>. Il <xref:System.Windows.Media.MatrixTransform> viene applicato a un pulsante e determina lo spostamento lungo un percorso curvo. Poiché il <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> è impostata su `true`, il rettangolo ruota lungo la tangente del percorso.  
  
 [!code-xml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 Per ulteriori informazioni sulla sintassi del percorso che viene utilizzata per la [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] esempio, vedere il [sintassi di Markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) Panoramica. Per l'esempio completo, vedere [esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028).  
  
 È possibile applicare un'animazione percorso a una proprietà utilizzando un <xref:System.Windows.Media.Animation.Storyboard> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e nel codice o tramite il <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> metodo nel codice. È inoltre possibile utilizzare un'animazione percorso per creare un <xref:System.Windows.Media.Animation.AnimationClock> e applicarla a una o più proprietà. Per ulteriori informazioni sui diversi metodi per l'applicazione di animazioni, vedere [Cenni preliminari sulle tecniche di animazione di proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
<a name="animation_types"></a>   
## <a name="path-animation-types"></a>Tipi di animazione percorso  
 Poiché le animazioni generano valori di proprietà, esistono diversi tipi di animazione per diversi tipi di proprietà. Per animare una proprietà che accetta un <xref:System.Double> (ad esempio il <xref:System.Windows.Media.TranslateTransform.X%2A> proprietà di un <xref:System.Windows.Media.TranslateTransform>), si utilizza un'animazione che produce <xref:System.Double> valori. Per animare una proprietà che accetta un <xref:System.Windows.Point>, si utilizza un'animazione che produce <xref:System.Windows.Point> valori e così via.  
  
 Classi di animazione percorso appartengono al <xref:System.Windows.Media.Animation> dello spazio dei nomi e utilizzano la convenzione di denominazione seguente:  
  
 *<>\>*`AnimationUsingPath`  
  
 Dove * <> \> * è il tipo di valore animato dalla classe.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]fornisce il percorso seguente classi di animazione.  
  
|Tipo di proprietà|Classe di animazione percorso corrispondente|Esempio|  
|-------------------|----------------------------------------|-------------|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|[Animare un oggetto lungo un percorso (animazione Double)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-double-animation.md)|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>|[Animare un oggetto lungo un percorso (animazione Matrix)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-matrix-animation.md)|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|[Animare un oggetto lungo un percorso (animazione Point)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-an-object-along-a-path-point-animation.md)|  
  
 Oggetto <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> genera <xref:System.Windows.Media.Matrix> i valori relativi <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.PathGeometry%2A>. Quando si utilizza un <xref:System.Windows.Media.MatrixTransform>, <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> possibile spostare un oggetto lungo un percorso. Se si imposta la <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A> proprietà del <xref:System.Windows.Media.Animation.MatrixAnimationUsingPath> a `true`, viene anche ruotato lungo le curve del percorso dell'oggetto.  
  
 Oggetto <xref:System.Windows.Media.Animation.PointAnimationUsingPath> genera <xref:System.Windows.Point> valori dalle coordinate x e y della relativa <xref:System.Windows.Media.Animation.PointAnimationUsingPath.PathGeometry%2A>. Utilizzando un <xref:System.Windows.Media.Animation.PointAnimationUsingPath> per animare una proprietà che accetta <xref:System.Windows.Point> valori, è possibile spostare un oggetto lungo un percorso. Oggetto <xref:System.Windows.Media.Animation.PointAnimationUsingPath> Impossibile ruotare gli oggetti.  
  
 Oggetto <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> genera <xref:System.Double> i valori relativi <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>. Impostando il <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.Source%2A> proprietà, è possibile specificare se il <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> utilizza la coordinata x, coordinata y o l'angolo del percorso come output. È possibile utilizzare un <xref:System.Windows.Media.Animation.DoubleAnimationUsingPath> per ruotare un oggetto o spostarlo lungo l'asse x o asse y.  
  
<a name="pathanimationinput"></a>   
## <a name="path-animation-input"></a>Input dell'animazione percorso  
 Ogni classe di animazione percorso fornisce un <xref:System.Windows.Media.PathGeometry> proprietà per specificare il relativo input. L'animazione percorso utilizza il <xref:System.Windows.Media.PathGeometry> per generare i valori di output. Il <xref:System.Windows.Media.PathGeometry> classe consente di descrivere più figure complesse costituite da linee, curve e archi.  
  
 Il fulcro di un <xref:System.Windows.Media.PathGeometry> è una raccolta di <xref:System.Windows.Media.PathFigure> oggetti; questi oggetti vengono denominati in questo modo perché ogni figura descrive una forma discreta nel <xref:System.Windows.Media.PathGeometry>. Ogni <xref:System.Windows.Media.PathFigure> è costituito da uno o più <xref:System.Windows.Media.PathSegment> oggetti, ognuno dei quali descrive un segmento della figura.  
  
 Esistono molti tipi di segmenti.  
  
|Tipo di segmento|Descrizione|  
|------------------|-----------------|  
|<xref:System.Windows.Media.ArcSegment>|Crea un arco ellittico tra due punti.|  
|<xref:System.Windows.Media.BezierSegment>|Crea una curva di Bezier cubica tra due punti.|  
|<xref:System.Windows.Media.LineSegment>|Crea una linea tra due punti.|  
|<xref:System.Windows.Media.PolyBezierSegment>|Crea una serie di curve di Bézier cubiche.|  
|<xref:System.Windows.Media.PolyLineSegment>|Crea una serie di righe.|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|Crea una serie di curve di Bezier quadratiche.|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|Crea una curva di Bezier quadratica.|  
  
 I segmenti in un <xref:System.Windows.Media.PathFigure> vengono combinati in una singola forma geometrica, che utilizza il punto finale di un segmento come punto iniziale del segmento successivo. Il <xref:System.Windows.Media.PathFigure.StartPoint%2A> proprietà di un <xref:System.Windows.Media.PathFigure> specifica il punto da cui viene disegnato il primo segmento. Ogni segmento successivo inizia in corrispondenza del punto finale del segmento precedente. Ad esempio, una linea verticale da `10,50` a `10,150` può essere definito impostando il <xref:System.Windows.Media.PathFigure.StartPoint%2A> proprietà `10,50` e la creazione di un <xref:System.Windows.Media.LineSegment> con un <xref:System.Windows.Media.LineSegment.Point%2A> impostazione della proprietà `10,150`.  
  
 Per ulteriori informazioni su <xref:System.Windows.Media.PathGeometry> degli oggetti, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
 In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è inoltre possibile utilizzare una sintassi abbreviata speciale per impostare il <xref:System.Windows.Media.PathGeometry.Figures%2A> proprietà di un <xref:System.Windows.Media.PathGeometry>. Per ulteriori informazioni, vedere [sintassi del Markup percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) Panoramica.  
  
 Per ulteriori informazioni sulla sintassi del percorso che viene utilizzata per la [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] esempio, vedere il [sintassi di Markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md) Panoramica.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di animazione percorso](http://go.microsoft.com/fwlink/?LinkID=160028)   
 [Sintassi di Markup del percorso](../../../../docs/framework/wpf/graphics-multimedia/path-markup-syntax.md)   
 [Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle tecniche di animazione di proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)