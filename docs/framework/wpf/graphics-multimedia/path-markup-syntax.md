---
title: "Sintassi di markup del percorso | Microsoft Docs"
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
  - "PathGeometry (classe)"
  - "utilizzo degli attributi in XAML"
  - "Utilizzo dell'attributo XAML"
  - "classi, PathGeometry"
  - "grafica, PathGeometry (classe)"
  - "Utilizzo dell'elemento oggetto XAML"
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Sintassi di markup del percorso
Vengono illustrati i percorsi in [forme e disegno di base di WPF Overview](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md) e [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md), tuttavia, questo argomento viene descritto in dettaglio il potente e complesso mini linguaggio consente di specificare in modo più compatto usando le geometrie percorso [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere le funzionalità di base <xref:System.Windows.Media.Geometry> oggetti. Per ulteriori informazioni, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
<a name="abouthisdocument"></a>   
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>StreamGeometry e PathFigureCollection Mini-lingue  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]sono disponibili due classi che forniscono mini-lingue per descrivere percorsi geometrici: <xref:System.Windows.Media.StreamGeometry> e <xref:System.Windows.Media.PathFigureCollection>.  
  
-   Utilizzare il <xref:System.Windows.Media.StreamGeometry> mini linguaggio quando si imposta una proprietà di tipo <xref:System.Windows.Media.Geometry>, ad esempio il <xref:System.Windows.UIElement.Clip%2A> proprietà di un <xref:System.Windows.UIElement> o <xref:System.Windows.Shapes.Path.Data%2A> proprietà di un <xref:System.Windows.Shapes.Path> elemento. Nell'esempio seguente viene utilizzata la sintassi degli attributi per creare un <xref:System.Windows.Media.StreamGeometry>.  
  
     [!code-xml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
-   Utilizzare il <xref:System.Windows.Media.PathFigureCollection> mini linguaggio durante l'impostazione di <xref:System.Windows.Media.PathGeometry.Figures%2A> proprietà di un <xref:System.Windows.Media.PathGeometry>. Nell'esempio seguente utilizza una sintassi di attributo per creare un <xref:System.Windows.Media.PathFigureCollection> per un <xref:System.Windows.Media.PathGeometry>.  
  
     [!code-xml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 Come si può notare dagli esempi precedenti, i due linguaggi mini sono molto simili. È sempre possibile utilizzare un <xref:System.Windows.Media.PathGeometry> in qualsiasi situazione in cui è possibile utilizzare un <xref:System.Windows.Media.StreamGeometry>; in questo caso quello è necessario utilizzare? Utilizzare un <xref:System.Windows.Media.StreamGeometry> quando non è necessario modificare il percorso dopo averlo creato; utilizzare un <xref:System.Windows.Media.PathGeometry> se è necessario modificare il percorso.  
  
 Per ulteriori informazioni sulle differenze tra <xref:System.Windows.Media.PathGeometry> e <xref:System.Windows.Media.StreamGeometry> degli oggetti, vedere il [Geometry Overview](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md).  
  
### <a name="a-note-about-white-space"></a>Nota sugli spazi vuoti  
 Per brevità, uno spazio singolo viene illustrato nelle sezioni che seguono la sintassi, ma più spazi sono anche quando viene visualizzato uno spazio singolo.  
  
 Due numeri non è necessario essere separati da virgole o spazi vuoti, ma ciò può essere eseguita solo quando la stringa risulta è ambigua. Ad esempio, `2..3` è composta da due numeri: "2". E ".&3;". Analogamente, `2-3` è "2" e "-3". Gli spazi non sono necessari prima o dopo i comandi di.  
  
### <a name="syntax"></a>Sintassi  
 Il [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] attributo sintassi di utilizzo di un <xref:System.Windows.Media.StreamGeometry> è composto da un parametro facoltativo <xref:System.Windows.Media.FillRule> valore e uno o più descrizioni di figure.  
  
|Utilizzo dell'attributo XAML StreamGeometry|  
|-----------------------------------------|  
|`<`*object* *property* `="`[                                         `fillRule`]                                          `figureDescription`[                                         `figureDescription`]*`" ... />`|  
  
 Il [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] attributo sintassi di utilizzo di un <xref:System.Windows.Media.PathFigureCollection> è composto da uno o più descrizioni di figure.  
  
|Utilizzo dell'attributo XAML PathFigureCollection|  
|-----------------------------------------------|  
|`<`*object* *property* `="` `figureDescription`[                                         `figureDescription`]*`" ... />`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=fullName><br /><br /> Specifica se il <xref:System.Windows.Media.StreamGeometry> utilizza il <xref:System.Windows.Media.FillRule> o <xref:System.Windows.Media.FillRule><xref:System.Windows.Media.PathGeometry.FillRule%2A>.<br /><br /> -   `F0`Specifica il <xref:System.Windows.Media.FillRule> regola di riempimento.<br />-   `F1`Specifica il <xref:System.Windows.Media.FillRule> regola di riempimento.<br /><br /> Se si omette questo comando, il percorso secondario utilizzerà il comportamento predefinito, ovvero <xref:System.Windows.Media.FillRule>. Se si specifica questo comando, è necessario inserire prima.|  
|*figureDescription*|Figura costituita da un comando di spostamento, creare comandi e un comando di chiuso facoltativo.<br /><br /> `moveCommand` `drawCommands`  `[` `closeCommand` `]`|  
|*moveCommand*|Un comando di spostamento che specifica il punto iniziale della figura. Vedere il [comando Sposta](#themovecommand) sezione.|  
|*drawCommands*|Uno o più comandi di disegno che descrivono il contenuto della figura. Vedere il [comandi Draw](#drawcommands) sezione.|  
|*closeCommand*|Comando close facoltativo che figura viene chiusa. Vedere il [comando Close](#closecommand) sezione.|  
  
<a name="themovecommand"></a>   
## <a name="move-command"></a>Comando di spostamento  
 Specifica il punto di inizio di una nuova figura.  
  
|Sintassi|  
|------------|  
|`M`*startPoint*<br /><br /> -oppure-<br /><br /> `m`*startPoint*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*punto iniziale*|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Il punto di inizio di una nuova figura.|  
  
 Un carattere maiuscolo `M` indica che `startPoint` è un valore assoluto; una minuscola `m` indica che `startPoint` è un offset al punto precedente, oppure (0,0) se non ne esiste nessuno. Se si elencano più punti dopo il comando di spostamento, una linea viene tracciata in quei punti anche se è specificata la riga di comando.  
  
<a name="drawcommands"></a>   
## <a name="draw-commands"></a>Comandi di disegno  
 Un comando di disegno può essere costituito da diversi comandi di forma. Sono disponibili i seguenti comandi di forma: riga, linea orizzontale, verticale, curva di Bezier cubica, curva di Bezier quadratica, curva di Bezier cubica smooth, curva di Bezier quadratica e arco ellittico.  
  
 Ogni comando immesso utilizzando maiuscola o minuscola: lettere maiuscole indicano valori assoluti e relativi valori indicano le lettere minuscole: i punti di controllo per il segmento sono rispetto al punto di fine dell'esempio precedente. Quando si immette in sequenza più comandi dello stesso tipo, è possibile omettere l'immissione del comando duplicati; ad esempio, `L 100,200 300,400` equivale a `L 100,200 L 300,400`. Nella tabella seguente vengono descritti il **spostare** e **disegnare** comandi.  
  
### <a name="line-command"></a>Riga di comando  
 Crea una linea retta tra il punto corrente e il punto finale specificato.                           `l 20 30`e `L 20,30` sono esempi di valido **riga** comandi.  
  
|Sintassi|  
|------------|  
|`L`*endPoint*<br /><br /> -oppure-<br /><br /> `l`*endPoint*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*endPoint*|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto finale della linea.|  
  
### <a name="horizontal-line-command"></a>Orizzontale della riga di comando  
 Crea una riga orizzontale tra il punto corrente e la coordinata x specificata.                          `H 90`è un esempio di un comando di linea orizzontale valido.  
  
|Sintassi|  
|------------|  
|`H`  *x*<br /><br /> -oppure-<br /><br /> `h`  *x*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=fullName><br /><br /> Coordinata x del punto finale della linea.|  
  
### <a name="vertical-line-command"></a>Verticale della riga di comando  
 Crea una linea verticale tra il punto corrente e la coordinata y specificata.                          `v 90`è un esempio di comando di linea verticale valido.  
  
|Sintassi|  
|------------|  
|`V`  *y*<br /><br /> -oppure-<br /><br /> `v`  *y*|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=fullName><br /><br /> Coordinata y del punto finale della linea.|  
  
### <a name="cubic-bezier-curve-command"></a>Comando curva di Bezier cubica  
 Crea una curva di Bezier cubica tra il punto corrente e il punto finale specificato utilizzando i due punti di controllo ( `controlPoint`1 e `controlPoint`2).                          `C 100,200 200,400 300,200`è un esempio di comando di curva valido.  
  
|Sintassi|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> -oppure-<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Il primo punto di controllo della curva, che determina la tangente iniziale della curva.|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Secondo punto di controllo della curva, che determina la tangente finale della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="quadratic-bezier-curve-command"></a>Comando curva di Bezier quadratica  
 Crea una curva di Bezier quadratica tra il punto corrente e il punto finale specificato utilizzando il punto di controllo ( `controlPoint`).                          `q 100,200 300,200`è un esempio di comando di curva di Bezier quadratica valido.  
  
|Sintassi|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> -oppure-<br /><br /> `q` `controlPoint` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Il punto di controllo della curva, che determina l'inizio e fine tangenti della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>Curva di Bezier cubica Smooth comando  
 Crea una curva di Bezier cubica tra il punto corrente e il punto finale specificato. Il primo punto di controllo verrà considerato reflection del secondo punto di controllo del comando precedente rispetto al punto corrente. Se non esiste alcun comando precedente o se il comando precedente non è un comando di curva di Bezier cubica o un comando curva di Bezier cubica, si supponga che il primo punto di controllo è coinciderà con il punto corrente. Il secondo punto di controllo, il punto di controllo per l'entità finale della curva, specificato da `controlPoint`2. Ad esempio, `S 100,200 200,300` è un comando di curva di Bezier cubico continua valido.  
  
|Sintassi|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> -oppure-<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Il punto di controllo della curva, che determina la tangente finale della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>Curva di Bezier quadratica Smooth comando  
 Crea una curva di Bezier quadratica tra il punto corrente e il punto finale specificato. Il punto di controllo è considerato la reflection del punto di controllo del comando precedente rispetto al punto corrente. Se non esiste alcun comando precedente o se il comando precedente non è un comando di curva di Bezier quadratica o un comando di curva di Bezier quadratica continua, il punto di controllo coinciderà con il punto corrente.  
  
|Sintassi|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> -oppure-<br /><br /> `t` `controlPoint` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Il punto di controllo della curva, che determina l'inizio e di tangente della curva.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto verso il quale viene disegnata la curva.|  
  
### <a name="elliptical-arc-command"></a>Comando arco ellittico  
 Crea un arco ellittico tra il punto corrente e il punto finale specificato.  
  
|Sintassi|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> -oppure-<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=fullName><br /><br /> Raggio x e raggio y dell'arco.|  
|`rotationAngle`|<xref:System.Double?displayProperty=fullName><br /><br /> La rotazione dell'ellisse, in gradi.|  
|`isLargeArcFlag`|Impostare su 1 se l'angolo dell'arco deve essere di 180 gradi o superiore; in caso contrario, impostare su 0.|  
|`sweepDirectionFlag`|Impostare su 1 se l'arco viene disegnato in una direzione angolo positivo; in caso contrario, impostare su 0.|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> Punto verso cui viene disegnata l'arco.|  
  
<a name="closecommand"></a>   
## <a name="the-close-command"></a>Il comando Close  
 Termina la figura corrente e viene creata una riga che connette il punto corrente e il punto iniziale della figura. Questo comando crea un join riga (angolo) tra l'ultimo segmento e il primo segmento della figura.  
  
|Sintassi|  
|------------|  
|`Z`<br /><br /> -oppure-<br /><br /> `z`|  
  
<a name="pointsyntax"></a>   
## <a name="point-syntax"></a>Sintassi del punto  
 Descrive le coordinate x e y di un punto.  
  
|Sintassi|  
|------------|  
|`x` `,` `y`<br /><br /> -oppure-<br /><br /> `x` `y`|  
  
|Termine|Descrizione|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=fullName><br /><br /> Coordinata x del punto.|  
|`y`|<xref:System.Double?displayProperty=fullName><br /><br /> Coordinata y del punto.|  
  
<a name="specialvalues"></a>   
## <a name="special-values"></a>Valori speciali  
 Anziché un valore numerico standard, è inoltre possibile utilizzare i seguenti valori speciali. Questi valori tra maiuscole e minuscole.  
  
 Infinito  
 Rappresenta <xref:System.Double.PositiveInfinity?displayProperty=fullName>.  
  
 -Infinito  
 Rappresenta <xref:System.Double.NegativeInfinity?displayProperty=fullName>.  
  
 NaN  
 Rappresenta <xref:System.Double.NaN?displayProperty=fullName>.  
  
 È inoltre possibile utilizzare la notazione scientifica. Ad esempio, `+1.e17` è un valore valido.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.StreamGeometry>   
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Media.PathFigureCollection>   
 [Disegno di base di WPF Overview e forme](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Panoramica di geometria](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [Procedure](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)