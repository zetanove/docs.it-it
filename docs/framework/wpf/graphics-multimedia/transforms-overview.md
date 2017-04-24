---
title: "Cenni preliminari sulle trasformazioni | Microsoft Docs"
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
  - "2D (classi di trasformazione)"
  - "classi, 2-D transform"
  - "FrameworkElement (oggetti), rotazione"
  - "FrameworkElement (oggetti), adattamento"
  - "FrameworkElement (oggetti), inclinazione"
  - "FrameworkElement (oggetti), conversione"
  - "trasformazione (classi), 2D"
  - "trasformazioni, informazioni sulle trasformazioni"
  - "Trasformazioni, informazioni sulle trasformazioni"
ms.assetid: 8f153d5e-ed61-4aa5-a7cd-286f0c427a13
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Cenni preliminari sulle trasformazioni
In questo argomento viene descritto come utilizzare le classi <xref:System.Windows.Media.Transform> [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)] per ruotare, ridimensionare, spostare \(traslare\) e inclinare oggetti <xref:System.Windows.FrameworkElement>.  
  
   
  
<a name="whatIsATransformSection"></a>   
## Definizione di trasformazione  
 Un oggetto <xref:System.Windows.Media.Transform> definisce come eseguire il mapping dei punti, ovvero trasformare i punti, da uno spazio di coordinate a un altro spazio di coordinate.  Questo mapping è descritto da un oggetto <xref:System.Windows.Media.Matrix> di trasformazione, che è una raccolta di tre righe con tre colonne di valori <xref:System.Double>.  
  
> [!NOTE]
>  In [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] vengono utilizzate matrici ordinate in base alla riga.  I vettori sono espressi come vettori di riga anziché come vettori di colonna.  
  
 Nella tabella seguente viene illustrata la struttura di una matrice [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Matrice di trasformazione 2D  
  
||||  
|-|-|-|  
|<xref:System.Windows.Media.Matrix.M11%2A><br /><br /> Valore predefinito: 1,0|<xref:System.Windows.Media.Matrix.M12%2A><br /><br /> Valore predefinito: 0,0|0.0|  
|<xref:System.Windows.Media.Matrix.M21%2A><br /><br /> Valore predefinito: 0,0|<xref:System.Windows.Media.Matrix.M22%2A><br /><br /> Valore predefinito: 1,0|0.0|  
|<xref:System.Windows.Media.Matrix.OffsetX%2A><br /><br /> Valore predefinito: 0,0|<xref:System.Windows.Media.Matrix.OffsetY%2A><br /><br /> Valore predefinito: 0,0|1.0|  
  
 Modificando i valori della matrice, è possibile ruotare, ridimensionare, inclinare e spostare \(traslare\) un oggetto.  Ad esempio, se si modifica il valore nella prima colonna della terza riga \(il valore <xref:System.Windows.Media.Matrix.OffsetX%2A>\) in 100, è possibile utilizzarlo per spostare un oggetto di 100 unità lungo l'asse x.  Se si imposta il valore nella seconda colonna della seconda riga su 3, è possibile utilizzarlo per allungare un oggetto fino a un'altezza tre volte superiore a quella corrente.  Se si modificano entrambi i valori, si sposta l'oggetto di 100 unità lungo l'asse x e se ne aumenta l'altezza di un fattore di 3.  Poiché in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] vengono supportate solo le trasformazioni affini, i valori nella colonna di destra sono sempre 0, 0, 1.  
  
 Anche se in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] è possibile modificare direttamente i valori della matrice, vengono comunque fornite diverse classi <xref:System.Windows.Media.Transform> che permettono di trasformare un oggetto senza conoscere la configurazione della struttura della matrice sottostante.  Ad esempio, la classe <xref:System.Windows.Media.ScaleTransform> consente di ridimensionare un oggetto impostando le relative proprietà <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> e <xref:System.Windows.Media.ScaleTransform.ScaleY%2A>, anziché modificando una matrice di trasformazione.  Analogamente, la classe <xref:System.Windows.Media.RotateTransform> consente di ruotare un oggetto impostando semplicemente la relativa proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A>.  
  
<a name="transformClassesSection"></a>   
## Classi Transform  
 In [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] sono disponibili le seguenti classi <xref:System.Windows.Media.Transform> [!INCLUDE[TLA#tla_2d](../../../../includes/tlasharptla-2d-md.md)] per le comuni operazioni di trasformazione:  
  
|Classe|Descrizione|Esempio|Illustrazione|  
|------------|-----------------|-------------|-------------------|  
|<xref:System.Windows.Media.RotateTransform>|Ruota un elemento in base al valore <xref:System.Windows.Media.RotateTransform.Angle%2A> specificato.|[Ruotare un oggetto](../../../../docs/framework/wpf/graphics-multimedia/how-to-rotate-an-object.md)||  
|<xref:System.Windows.Media.ScaleTransform>|Ridimensiona un elemento in base ai valori <xref:System.Windows.Media.ScaleTransform.ScaleX%2A> e <xref:System.Windows.Media.ScaleTransform.ScaleY%2A> specificati.|[Ridimensionare un elemento](../../../../docs/framework/wpf/graphics-multimedia/how-to-scale-an-element.md)||  
|<xref:System.Windows.Media.SkewTransform>|Inclina un elemento in base ai valori <xref:System.Windows.Media.SkewTransform.AngleX%2A> e <xref:System.Windows.Media.SkewTransform.AngleY%2A> specificati.|[Inclinare un elemento](../../../../docs/framework/wpf/graphics-multimedia/how-to-skew-an-element.md)||  
|<xref:System.Windows.Media.TranslateTransform>|Sposta \(trasla\) un elemento in base ai valori <xref:System.Windows.Media.TranslateTransform.X%2A> e <xref:System.Windows.Media.TranslateTransform.Y%2A> specificati.|[Convertire un elemento](../../../../docs/framework/wpf/graphics-multimedia/how-to-translate-an-element.md)||  
  
 Per la creazione di trasformazioni più complesse, in [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] sono disponibili le due classi seguenti:  
  
|Classe|Descrizione|Esempio|  
|------------|-----------------|-------------|  
|<xref:System.Windows.Media.TransformGroup>|Raggruppa più oggetti <xref:System.Windows.Media.TransformGroup> in un unico oggetto <xref:System.Windows.Media.Transform> che è quindi possibile applicare alle proprietà di trasformazione.|[Applicare più trasformazioni a un oggetto](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-multiple-transforms-to-an-object.md)|  
|<xref:System.Windows.Media.MatrixTransform>|Crea trasformazioni personalizzate che non sono fornite dalle altre classi <xref:System.Windows.Media.Transform>.  Quando si utilizza <xref:System.Windows.Media.MatrixTransform>, si modifica direttamente una matrice.|[Utilizzare un MatrixTransform per creare trasformazioni personalizzate](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-a-matrixtransform-to-create-custom-transforms.md)|  
  
 In [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] sono inoltre disponibili le trasformazioni [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)].  Per ulteriori informazioni, vedere la classe <xref:System.Windows.Media.Media3D.Transform3D>.  
  
<a name="transformationproperties"></a>   
## Proprietà di trasformazione comuni  
 Per trasformare un oggetto, è possibile dichiarare il tipo <xref:System.Windows.Media.Transform> appropriato e applicarlo alla proprietà di trasformazione dell'oggetto.  Tipi diversi di oggetti hanno tipi diversi di proprietà di trasformazione.  Nella tabella seguente sono elencati alcuni tipi [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] comunemente utilizzati e le relative proprietà di trasformazione.  
  
|Type|Proprietà di trasformazione|  
|----------|---------------------------------|  
|<xref:System.Windows.Media.Brush>|<xref:System.Windows.Media.Brush.Transform%2A>, <xref:System.Windows.Media.Brush.RelativeTransform%2A>|  
|<xref:System.Windows.Media.ContainerVisual>|<xref:System.Windows.Media.ContainerVisual.Transform%2A>|  
|<xref:System.Windows.Media.DrawingGroup>|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|  
|<xref:System.Windows.FrameworkElement>|<xref:System.Windows.UIElement.RenderTransform%2A>, <xref:System.Windows.FrameworkElement.LayoutTransform%2A>|  
|<xref:System.Windows.Media.Geometry>|<xref:System.Windows.Media.Geometry.Transform%2A>|  
|<xref:System.Windows.Media.TextEffect>|<xref:System.Windows.Media.TextEffect.Transform%2A>|  
|<xref:System.Windows.UIElement>|<xref:System.Windows.UIElement.RenderTransform%2A>|  
  
<a name="transformcenter"></a>   
## Trasformazioni e sistemi di coordinate  
 Quando si trasforma un oggetto, non si trasforma solo l'oggetto, ma anche lo spazio di coordinate in cui esiste.  Per impostazione predefinita, una trasformazione è allineata al centro in corrispondenza dell'origine del sistema di coordinate dell'oggetto di destinazione: \(0,0\).  L'unica eccezione è <xref:System.Windows.Media.TranslateTransform>, per cui non sono disponibili proprietà di allineamento al centro da impostare, perché l'effetto di traslazione è identico indipendentemente dal punto in cui avviene l'allineamento al centro.  
  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare un elemento <xref:System.Windows.Shapes.Rectangle> \(un tipo di <xref:System.Windows.FrameworkElement>\) di 45 gradi rispetto al centro predefinito \(0,0\) dell'elemento.  Nell'immagine seguente viene illustrato l'effetto della rotazione.  
  
 ![Oggetto FrameworkElement ruotato di 45 gradi rispetto a &#40;0,0&#41;](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-fe-rotated-about-upperleft-corner.png "graphicsmm\_FE\_rotated\_about\_upperleft\_corner")  
Elemento Rectangle ruotato di 45 gradi intorno al punto \(0,0\)  
  
 [!code-xml[Transforms_snip#TransformsFERotatedAboutTopLeft](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedabouttopleft)]  
  
 Per impostazione predefinita, l'elemento ruota intorno al relativo angolo superiore sinistro, \(0, 0\).  Le classi <xref:System.Windows.Media.RotateTransform>, <xref:System.Windows.Media.ScaleTransform> e <xref:System.Windows.Media.SkewTransform> forniscono le proprietà CenterX e CenterY che consentono di specificare il punto in cui viene applicata la trasformazione.  
  
 Anche nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare di 45 gradi un elemento <xref:System.Windows.Shapes.Rectangle>, ma in questo caso le proprietà <xref:System.Windows.Media.RotateTransform.CenterX%2A> e <xref:System.Windows.Media.RotateTransform.CenterY%2A> sono impostate in modo che il centro di <xref:System.Windows.Media.RotateTransform> corrisponda a \(25, 25\).  Nell'immagine seguente viene illustrato l'effetto della rotazione.  
  
 ![Oggetto Geometry ruotato di 45 gradi rispetto a &#40;25,25&#41;](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-fe-rotated-about-center.png "graphicsmm\_FE\_rotated\_about\_center")  
Elemento Rectangle ruotato di 45 gradi intorno al punto \(25,25\)  
  
 [!code-xml[Transforms_snip#TransformsFERotatedAboutCenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/CoordinateSystemExample.xaml#transformsferotatedaboutcenter)]  
  
<a name="layoutTransformsAndRenderTransformsSection"></a>   
## Trasformazione di FrameworkElement  
 Per applicare le trasformazioni a <xref:System.Windows.FrameworkElement>, creare un oggetto <xref:System.Windows.Media.Transform> e applicarlo a una delle due proprietà rese disponibili dalla classe <xref:System.Windows.FrameworkElement>:  
  
-   <xref:System.Windows.FrameworkElement.LayoutTransform%2A>: una trasformazione applicata prima del passaggio di layout.  Dopo l'applicazione della trasformazione, il sistema di layout elabora le dimensioni e la posizione trasformate dell'elemento.  
  
-   <xref:System.Windows.UIElement.RenderTransform%2A>: una trasformazione che modifica l'aspetto dell'elemento ma viene applicata dopo il completamento del passaggio di layout.  Utilizzando la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> anziché la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A>, è possibile ottenere vantaggi nelle prestazioni.  
  
 Quale proprietà utilizzare?  Poiché offre vantaggi nelle prestazioni, utilizzare la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> laddove possibile, soprattutto quando si utilizzano oggetti <xref:System.Windows.Media.Transform> animati.  Utilizzare la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> quando si ridimensiona, ruota o inclina un elemento ed è necessario adattare il relativo elemento padre alle dimensioni trasformate.  Notare che, quando vengono utilizzati con la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A>, gli oggetti <xref:System.Windows.Media.TranslateTransform> sembrano non avere effetto sugli elementi.  Ciò è dovuto al fatto che il sistema di layout riporta l'elemento traslato nella posizione originale come parte dell'elaborazione.  
  
 Per ulteriori informazioni sul layout in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], vedere [Layout](../../../../docs/framework/wpf/advanced/layout.md).  
  
<a name="exampleRotateAnElement45degSection"></a>   
## Esempio: rotazione di un oggetto FrameworkElement di 45 gradi  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare un pulsante di 45 gradi in senso orario.  Il pulsante è contenuto in un oggetto <xref:System.Windows.Controls.StackPanel> che include altri due pulsanti.  
  
 Per impostazione predefinita, <xref:System.Windows.Media.RotateTransform> ruota intorno al punto \(0, 0\).  Poiché nell'esempio non viene specificato un valore relativo al centro, il pulsante ruota intorno al punto \(0, 0\), che corrisponde all'angolo superiore sinistro.  L'oggetto <xref:System.Windows.Media.RotateTransform> viene applicato alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A>.  Nell'immagine seguente è illustrato il risultato della trasformazione.  
  
 ![Pulsante trasformato usando RenderTransform](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformwithdefaultcenter.png "graphicsmm\_RenderTransformWithDefaultCenter")  
Rotazione di 45 gradi in senso orario rispetto all'angolo superiore sinistro  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample1)]  
  
 Anche nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Windows.Media.RotateTransform> per ruotare un pulsante di 45 gradi in senso orario, ma viene inoltre impostata la proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> del pulsante su \(0,5, 0,5\).  Il valore della proprietà <xref:System.Windows.UIElement.RenderTransformOrigin%2A> è relativo alle dimensioni del pulsante.  Di conseguenza, la rotazione viene applicata al centro del pulsante anziché nell'angolo superiore sinistro.  Nell'immagine seguente è illustrato il risultato della trasformazione.  
  
 ![Pulsante trasformato rispetto al proprio centro](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-rendertransformrelativecenter.png "graphicsmm\_RenderTransformRelativeCenter")  
Rotazione di 45 gradi in senso orario intorno al centro  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample2)]  
  
 Nell'esempio seguente viene utilizzata la proprietà <xref:System.Windows.FrameworkElement.LayoutTransform%2A> anziché la proprietà <xref:System.Windows.UIElement.RenderTransform%2A> per ruotare il pulsante.  In questo caso la trasformazione influisce sul layout del pulsante e provoca l'attivazione di un passaggio completo da parte del sistema di layout.  Di conseguenza, il pulsante viene ruotato e quindi riposizionato perché le relative dimensioni sono state modificate.  Nell'immagine seguente è illustrato il risultato della trasformazione.  
  
 ![Pulsante trasformato usando LayoutTransform](../../../../docs/framework/wpf/graphics-multimedia/media/graphicsmm-layouttransform.png "graphicsmm\_LayoutTransform")  
Utilizzo di LayoutTransform per ruotare il pulsante  
  
 [!code-xml[Transforms_snip#GraphicsMMRotateButtonExample3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonRotateTransformExample.xaml#graphicsmmrotatebuttonexample3)]  
  
<a name="animate_transforms"></a>   
## Animazione delle trasformazioni  
 Poiché ereditano dalla classe <xref:System.Windows.Media.Animation.Animatable>, le classi <xref:System.Windows.Media.Transform> possono essere animate.  Per animare un oggetto <xref:System.Windows.Media.Transform>, applicare un'animazione di un tipo compatibile alla proprietà che si desidera animare.  
  
 Nell'esempio seguente vengono utilizzati <xref:System.Windows.Media.Animation.Storyboard> e <xref:System.Windows.Media.Animation.DoubleAnimation> con <xref:System.Windows.Media.RotateTransform> per far girare un oggetto <xref:System.Windows.Controls.Button> sul posto quando viene selezionato con un clic del mouse.  
  
 [!code-xml[Transforms_snip#GraphicsMMAnimatedRotateButtonExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/ButtonAnimatedRotateTransformExample.xaml#graphicsmmanimatedrotatebuttonexamplewholepage)]  
  
 Per l'esempio completo, vedere [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252) \(la pagina potrebbe essere in inglese\).  Per ulteriori informazioni sulle animazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
<a name="freezable_features"></a>   
## Funzionalità dell'oggetto Freezable  
 Poiché eredita dalla classe <xref:System.Windows.Freezable>, la classe <xref:System.Windows.Media.Transform> fornisce diverse funzionalità speciali: gli oggetti <xref:System.Windows.Media.Transform> possono essere dichiarati come [risorse](../../../../docs/framework/wpf/advanced/xaml-resources.md), condivisi tra più oggetti, impostati in sola lettura per migliorare le prestazioni, duplicati e resi thread\-safe.  Per ulteriori informazioni sulle diverse funzionalità rese disponibili dagli oggetti <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Transform>   
 <xref:System.Windows.Media.Matrix>   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/transformations-how-to-topics.md)   
 [Esempio di trasformazioni bidimensionali](http://go.microsoft.com/fwlink/?LinkID=158252)