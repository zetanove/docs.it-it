---
title: "Cenni preliminari sugli storyboard | Microsoft Docs"
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
  - "storyboard (sintassi)"
  - "sintassi, Storyboard"
  - "sequenze temporali"
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# Cenni preliminari sugli storyboard
In questo argomento viene illustrato come utilizzare gli oggetti <xref:System.Windows.Media.Animation.Storyboard> per organizzare e applicare animazioni.  Viene illustrato come modificare in modo interattivo gli oggetti <xref:System.Windows.Media.Animation.Storyboard> e come utilizzare la sintassi indiretta relativa alle proprietà.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere i diversi tipi di animazione e le relative funzionalità di base.  Per un'introduzione alle animazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  È inoltre consigliabile conoscere le modalità di utilizzo delle proprietà collegate.  Per ulteriori informazioni sulle proprietà collegate, vedere [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
<a name="whatisatimeline"></a>   
## Definizione di storyboard  
 Le animazioni non sono l'unico tipo utile di sequenza temporale.  Vengono fornite altre classi di sequenze temporali per organizzare insiemi di sequenze e per applicare sequenze alle proprietà.  Le sequenze temporali contenitore derivano dalla classe <xref:System.Windows.Media.Animation.TimelineGroup> e includono <xref:System.Windows.Media.Animation.ParallelTimeline> e <xref:System.Windows.Media.Animation.Storyboard>.  
  
 Uno <xref:System.Windows.Media.Animation.Storyboard> è un tipo di sequenza temporale contenitore che fornisce informazioni per le sequenze in essa contenute.  Uno storyboard può contenere qualsiasi tipo di <xref:System.Windows.Media.Animation.Timeline>, incluse altre animazioni e altre sequenze temporali contenitore.  Gli oggetti <xref:System.Windows.Media.Animation.Storyboard> consentono di combinare sequenze temporali che influiscono su numerosi oggetti e proprietà in una singola struttura ad albero di sequenze, semplificando l'organizzazione e il controllo di comportamenti di temporizzazione complessi.  Si supponga, ad esempio, di voler disporre di un pulsante avente le tre caratteristiche riportate di seguito.  
  
-   Aumentare di volume e cambiare colore quando viene selezionato.  
  
-   Ridursi e tornare nuovamente alle dimensioni originali quando viene fatto clic su di esso.  
  
-   Comprimersi e perdere il 50% di opacità quando viene disabilitato.  
  
 In questo caso, si dispone di più set di animazioni applicabili allo stesso oggetto e si desidera eseguirli in momenti diversi, a seconda dello stato del pulsante.  Gli oggetti <xref:System.Windows.Media.Animation.Storyboard> consentono di organizzare le animazioni e di applicarle in gruppi a uno o più oggetti.  
  
<a name="wherecanyouuseastoryboard"></a>   
## Dove utilizzare uno storyboard  
 Un oggetto <xref:System.Windows.Media.Animation.Storyboard> può essere utilizzato per animare le [proprietà di dipendenza](GTMT) di classi che supportano l'animazione. Per ulteriori informazioni sul supporto delle classi per le animazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)\).  Poiché lo storyboard è una funzionalità a livello di framework, l'oggetto deve appartenere all'oggetto <xref:System.Windows.NameScope> di <xref:System.Windows.FrameworkElement> o di <xref:System.Windows.FrameworkContentElement>.  
  
 È ad esempio possibile utilizzare uno <xref:System.Windows.Media.Animation.Storyboard> per eseguire le operazioni riportate di seguito:  
  
-   Animare un oggetto <xref:System.Windows.Media.SolidColorBrush> \(elemento non framework\) che consente di disegnare lo sfondo di un pulsante \(un tipo di <xref:System.Windows.FrameworkElement>\)  
  
-   Animare un oggetto <xref:System.Windows.Media.SolidColorBrush> \(elemento non framework\) che consente di disegnare il riempimento di un oggetto <xref:System.Windows.Media.GeometryDrawing> \(elemento non framework\) visualizzato tramite un oggetto <xref:System.Windows.Controls.Image> \(<xref:System.Windows.FrameworkElement>\).  
  
-   Nel codice, animare un oggetto <xref:System.Windows.Media.SolidColorBrush> dichiarato da una classe che contiene anche un oggetto <xref:System.Windows.FrameworkElement>, se l'oggetto <xref:System.Windows.Media.SolidColorBrush> ha registrato il relativo nome con <xref:System.Windows.FrameworkElement>.  
  
 Non è tuttavia possibile utilizzare uno <xref:System.Windows.Media.Animation.Storyboard> per animare un oggetto <xref:System.Windows.Media.SolidColorBrush> che non ha registrato il proprio nome con <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> oppure che non è stato utilizzato per impostare una proprietà di un oggetto <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>.  
  
<a name="applyanimationswithastoryboard"></a>   
## Come applicare animazioni con uno storyboard  
 Per utilizzare uno <xref:System.Windows.Media.Animation.Storyboard> per organizzare e applicare animazioni, è necessario aggiungere le animazioni come sequenze temporali figlio dello <xref:System.Windows.Media.Animation.Storyboard>.  La classe <xref:System.Windows.Media.Animation.Storyboard> fornisce le proprietà collegate <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A?displayProperty=fullName>.  Queste proprietà devono essere impostate su un'animazione per specificare la proprietà e l'oggetto di destinazione relativi.  
  
 Per applicare animazioni alle relative destinazioni, dare inizio allo <xref:System.Windows.Media.Animation.Storyboard> utilizzando un'azione trigger o un metodo.  In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], utilizzare un oggetto <xref:System.Windows.Media.Animation.BeginStoryboard> con <xref:System.Windows.EventTrigger>, <xref:System.Windows.Trigger> o <xref:System.Windows.DataTrigger>.  Nel codice, è anche possibile utilizzare il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>.  
  
 Nella tabella seguente sono riportate le diverse posizioni in cui è supportata la tecnica di inizio di ciascuno <xref:System.Windows.Media.Animation.Storyboard>: per istanza, stile, modello di controllo e modello di dati.    Per istanza" si riferisce alla tecnica di applicare un'animazione o uno storyboard direttamente a istanze di un oggetto, piuttosto che in uno stile, un modello di controllo o un modello di dati.  
  
|Storyboard iniziato utilizzando…|Per istanza|Stile|Modello di controllo|Modello di dati|Esempio|  
|--------------------------------------|-----------------|-----------|--------------------------|---------------------|-------------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.EventTrigger>|Sì|Sì|Sì|Sì|[Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.Trigger> della proprietà|No|Sì|Sì|Sì|[Attivare un'animazione quando il valore di una proprietà viene modificato](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.DataTrigger>|No|Sì|Sì|Sì|[How to: Trigger an Animation When Data Changes](http://msdn.microsoft.com/it-it/a736bb3a-2ae5-479a-a33a-75a27055d863)|  
|Metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>|Sì|No|No|No|[Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 Nell'esempio riportato di seguito viene utilizzato uno <xref:System.Windows.Media.Animation.Storyboard> per animare la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di un elemento <xref:System.Windows.Shapes.Rectangle> e la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per disegnare quel <xref:System.Windows.Shapes.Rectangle>.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]  
  
 Nelle sezioni riportate di seguito vengono descritte più dettagliatamente le proprietà collegate <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A>.  
  
<a name="targetingelementsandfreezables"></a>   
## Elementi del framework, elementi di contenuto del framework e oggetti Freezable  
 Nella sezione precedente è stato specificato che per trovare la relativa destinazione un'animazione deve conoscere il nome e la proprietà da animare relativi.  Per specificare la proprietà da animare,è sufficiente impostare la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A?displayProperty=fullName> con il nome della proprietà da animare.  Specificare il nome dell'oggetto di cui animare la proprietà impostando la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName> sull'animazione.  
  
 Affinché la proprietà <xref:System.Windows.Setter.TargetName%2A> sia funzionante, l'oggetto di destinazione deve avere un nome.  La procedura di assegnazione di un nome a un oggetto <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] non corrisponde a quella utilizzata per assegnare un nome a un oggetto <xref:System.Windows.Freezable>.  
  
 Gli elementi del framework sono classi che ereditano dalla classe <xref:System.Windows.FrameworkElement>.  Elementi del framework di questo tipo sono rappresentati ad esempio da <xref:System.Windows.Window>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Button> e <xref:System.Windows.Shapes.Rectangle>.  Praticamente tutte le finestre, i pannelli e i controlli sono elementi.  Gli elementi di contenuto del framework sono classi che ereditano dalla classe <xref:System.Windows.FrameworkContentElement>.  Elementi di contenuto del framework di questo tipo sono rappresentati ad esempio da <xref:System.Windows.Documents.FlowDocument> e <xref:System.Windows.Documents.Paragraph>.  Se non si è in grado di stabilire se un tipo è un elemento del framework o un elemento di contenuto del framework, verificare se dispone della proprietà Name.  In caso affermativo, si tratta probabilmente di un elemento del framework o di un elemento di contenuto del framework.  Per avere la certezza, controllare la sezioneGerarchia di ereditarietà della pagina relativa al tipo.  
  
 Per utilizzare come destinazione un elemento del framework o un elemento di contenuto del framework in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], impostare la relativa proprietà <xref:System.Windows.FrameworkElement.Name%2A>.  Nel codice è inoltre necessario utilizzare il metodo <xref:System.Windows.NameScope.RegisterName%2A> per registrare il nome dell'elemento con l'elemento per il quale è stato creato un oggetto <xref:System.Windows.NameScope>.  
  
 Nell'esempio riportato di seguito, ricavato dall'esempio precedente, viene assegnato il nome `MyRectangle` a <xref:System.Windows.Shapes.Rectangle>, un tipo di <xref:System.Windows.FrameworkElement>.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]  
  
 Dopo l'assegnazione del nome all'elemento, è possibile animare una proprietà.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#105](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]  
  
 I tipi <xref:System.Windows.Freezable> sono classi che ereditano dalla classe <xref:System.Windows.Freezable>.  Esempi di oggetti <xref:System.Windows.Freezable> includono <xref:System.Windows.Media.SolidColorBrush>, <xref:System.Windows.Media.RotateTransform> e <xref:System.Windows.Media.GradientStop>.  
  
 Per utilizzare come destinazione un oggetto <xref:System.Windows.Freezable> tramite un'animazione in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], utilizzare [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) per assegnare ad esso un nome.  Nel codice è necessario utilizzare il metodo <xref:System.Windows.NameScope.RegisterName%2A> per registrare il suo nome con l'elemento per il quale è stato creato un oggetto <xref:System.Windows.NameScope>.  
  
 Nell'esempio riportato di seguito viene assegnato un nome all'oggetto <xref:System.Windows.Freezable>.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]  
  
 L'oggetto può essere impostato come destinazione di un'animazione.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#107](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]  
  
 Gli oggetti <xref:System.Windows.Media.Animation.Storyboard> utilizzano ambiti di nomi per risolvere la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>.  Per ulteriori informazioni sugli ambiti di nomi WPF, vedere [NameScope XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md).  Se si omette la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>, l'animazione considera come destinazione l'elemento su cui è stata definita o, nel caso di stili, l'elemento con stile.  
  
 Talvolta non è possibile assegnare un nome a un oggetto <xref:System.Windows.Freezable>.  Se, ad esempio, un oggetto <xref:System.Windows.Freezable> viene dichiarato come una risorsa o utilizzato per impostare un valore di proprietà in uno stile, non è possibile assegnare ad esso un nome.  Poiché non dispone di un nome, non può essere impostato direttamente come destinazione, ma solo indirettamente.  Nelle sezioni riportate di seguito viene illustrato come impostare indirettamente le destinazioni.  
  
<a name="pathsyntaxforchangeable"></a>   
## Impostazione indiretta delle destinazioni  
 In alcuni casi, un oggetto <xref:System.Windows.Freezable> non può essere impostato direttamente come destinazione da un'animazione, ad esempio quando l'oggetto <xref:System.Windows.Freezable> viene dichiarato come una risorsa o utilizzato per impostare un valore di proprietà in uno stile.  In questi casi, anche se non è possibile impostarlo direttamente come destinazione, è ancora possibile animare l'oggetto <xref:System.Windows.Freezable>.  Anziché impostare la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> con il nome dell'oggetto <xref:System.Windows.Freezable>, assegnare ad esso il nome dell'elemento a cui "appartiene" l'oggetto <xref:System.Windows.Freezable>. Ad esempio, un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per impostare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di un elemento rettangolo appartiene a quel rettangolo.  Per animare il pennello, impostare la proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> dell'animazione con una catena di proprietà che inizia dalla proprietà dell'elemento del framework o dell'elemento di contenuto del framework impostato con l'oggetto <xref:System.Windows.Freezable> e termina con la proprietà <xref:System.Windows.Freezable> da animare.  
  
  
  
 [!code-csharp[storyboards_ovw_snip#134](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]  
  
 Se l'oggetto <xref:System.Windows.Freezable> è bloccato, viene creato un duplicato e tale duplicato verrà animato.  In questo caso, la proprietà <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> dell'oggetto originale continua a restituire `false`, perché l'oggetto originale non è effettivamente animato.  Per ulteriori informazioni sulla duplicazione, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
 Quando si impostano indirettamente le destinazioni delle proprietà, è possibile impostare come destinazioni oggetti che non esistono.  Si supponga, ad esempio, che la proprietà <xref:System.Windows.Controls.Control.Background%2A> di un pulsante sia stata impostata con un oggetto <xref:System.Windows.Media.SolidColorBrush> e si sia tentato di animare la relativa proprietà Color quando in realtà era stato utilizzato un oggetto <xref:System.Windows.Media.LinearGradientBrush> per impostare la proprietà Background del pulsante.  In questi casi, non viene generata alcuna eccezione; l'animazione non avrà un effetto visibile perché <xref:System.Windows.Media.LinearGradientBrush> non reagisce alle modifiche apportate alla proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A>.  
  
 Nelle sezioni riportate di seguito viene illustrato in dettaglio come impostare in modo indiretto le destinazioni delle proprietà.  
  
<a name="xamlsyntaxchangeableproperty"></a>   
### Impostazione indiretta della destinazione di una proprietà di un oggetto Freezable in XAML  
 Per impostare come destinazione una proprietà di un oggetto Freezable in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], utilizzare la sintassi riportata di seguito.  
  
||  
|-|  
|*ElementPropertyName*`.`*FreezablePropertyName*|  
  
 Percorso  
  
-   *ElementPropertyName* è la proprietà dell'oggetto <xref:System.Windows.FrameworkElement> impostato tramite l'oggetto <xref:System.Windows.Freezable> e  
  
-   *FreezablePropertyName* è la proprietà dell'oggetto <xref:System.Windows.Freezable> da animare.  
  
 Nel codice riportato di seguito viene illustrato come animare la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per la proprietà  
  
 <xref:System.Windows.Shapes.Shape.Fill%2A> di un elemento rettangolo.  
  
  
  
 Talvolta, è necessario impostare come destinazione un oggetto Freezable contenuto in una raccolta o in una matrice.  
  
 Per impostare come destinazione un oggetto Freezable contenuto in una raccolta, utilizzare la sintassi del percorso riportata di seguito.  
  
||  
|-|  
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|  
  
 Dove *CollectionIndex* è l'indice dell'oggetto nella matrice o nella raccolta.  
  
 Si supponga, ad esempio, che alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> di un rettangolo sia applicata una risorsa <xref:System.Windows.Media.TransformGroup> e di volere animare una delle trasformazioni in essa contenute.  
  
  
  
 Nell'esempio di codice riportato di seguito viene illustrato come animare la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> dell'oggetto <xref:System.Windows.Media.RotateTransform> illustrato nel precedente esempio.  
  
  
  
<a name="targetingpropertyofchangeableincode"></a>   
### Impostazione indiretta della destinazione di una proprietà di un oggetto Freezable nel codice  
 Nel codice creare un oggetto <xref:System.Windows.PropertyPath>.  Quando si crea l'oggetto <xref:System.Windows.PropertyPath>, si specifica una proprietà <xref:System.Windows.PropertyPath.Path%2A> e una proprietà <xref:System.Windows.PropertyPath.PathParameters%2A>.  
  
 Per creare <xref:System.Windows.PropertyPath.PathParameters%2A>, si crea una matrice di tipo <xref:System.Windows.DependencyProperty> che contiene un elenco di campi dell'identificatore di proprietà di dipendenza.  Il primo campo dell'identificatore è per la proprietà dell'oggetto <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> impostato tramite l'oggetto <xref:System.Windows.Freezable>.  Il campo dell'identificatore successivo rappresenta la proprietà dell'oggetto <xref:System.Windows.Freezable> da impostare come destinazione.  Considerarlo come una catena di proprietà che collega l'oggetto <xref:System.Windows.Freezable> all'oggetto <xref:System.Windows.FrameworkElement>.  
  
 Di seguito è riportato un esempio di una catena di proprietà di dipendenza che imposta come destinazione la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per impostare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di un elemento rettangolo.  
  
 [!code-csharp[storyboards_ovw_snip#135](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]  
  
 È inoltre necessario specificare una proprietà <xref:System.Windows.PropertyPath.Path%2A>.  <xref:System.Windows.PropertyPath.Path%2A> è un oggetto <xref:System.String> che indica alla proprietà <xref:System.Windows.PropertyPath.Path%2A> come interpretare la proprietà <xref:System.Windows.PropertyPath.PathParameters%2A>.  Viene utilizzata la seguente sintassi.  
  
||  
|-|  
|`(`*OwnerPropertyArrayIndex*`).(`*FreezablePropertyArrayIndex*`)`|  
  
 Percorso  
  
-   *OwnerPropertyArrayIndex* è l'indice della matrice <xref:System.Windows.DependencyProperty> che contiene l'identificatore della proprietà dell'oggetto <xref:System.Windows.FrameworkElement> impostato tramite <xref:System.Windows.Freezable> e  
  
-   *FreezablePropertyArrayIndex* è l'indice della matrice <xref:System.Windows.DependencyProperty> che contiene l'identificatore della proprietà da impostare come destinazione.  
  
 Nell'esempio riportato di seguito viene illustrata la proprietà <xref:System.Windows.PropertyPath.Path%2A> associata alla proprietà <xref:System.Windows.PropertyPath.PathParameters%2A> definita nel precedente esempio.  
  
 [!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]  
  
 Nell'esempio riportato di seguito viene combinato il codice degli esempi precedenti per animare la proprietà <xref:System.Windows.Media.SolidColorBrush.Color%2A> di un oggetto <xref:System.Windows.Media.SolidColorBrush> utilizzato per impostare la proprietà <xref:System.Windows.Shapes.Shape.Fill%2A> di un elemento rettangolo.  
  
 [!code-csharp[storyboards_ovw_snip#137](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]  
  
 Talvolta, è necessario impostare come destinazione un oggetto Freezable contenuto in una raccolta o in una matrice.  Si supponga, ad esempio, che alla proprietà <xref:System.Windows.UIElement.RenderTransform%2A> di un rettangolo sia applicata una risorsa <xref:System.Windows.Media.TransformGroup> e di volere animare una delle trasformazioni in essa contenute.  
  
 [!code-xml[storyboards_ovw_snip#142](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]  
  
 Per impostare come destinazione un oggetto <xref:System.Windows.Freezable> contenuto in una raccolta, utilizzare la sintassi del percorso riportata di seguito.  
  
||  
|-|  
|`(`*OwnerPropertyArrayIndex*`).(` *CollectionChildrenPropertyArrayIndex*`)` `[`*CollectionIndex* `].(`*FreezablePropertyArrayIndex*`)`|  
  
 Dove *CollectionIndex* è l'indice dell'oggetto nella matrice o nella raccolta.  
  
 Per impostare come destinazione la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> dell'oggetto <xref:System.Windows.Media.RotateTransform>, la seconda trasformazione in <xref:System.Windows.Media.TransformGroup>, utilizzare le proprietà <xref:System.Windows.PropertyPath.Path%2A> e <xref:System.Windows.PropertyPath.PathParameters%2A>.  
  
 [!code-csharp[storyboards_ovw_snip#139](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]  
  
 Nell'esempio riportato di seguito viene illustrato il codice completo per animare la proprietà <xref:System.Windows.Media.RotateTransform.Angle%2A> di un oggetto <xref:System.Windows.Media.RotateTransform> contenuto in un <xref:System.Windows.Media.TransformGroup>.  
  
 [!code-csharp[storyboards_ovw_snip#138](../../../../samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]  
  
### Impostazione indiretta della destinazione con un oggetto Freezable come punto di partenza  
 Nelle sezioni precedenti veniva illustrato come impostare indirettamente come destinazione un oggetto <xref:System.Windows.Freezable> partendo da un oggetto <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> e creando una catena di proprietà a una proprietà secondaria <xref:System.Windows.Freezable>.  È inoltre possibile utilizzare un oggetto <xref:System.Windows.Freezable> come punto di partenza e impostare indirettamente come destinazione una delle proprietà secondarie dell'oggetto <xref:System.Windows.Freezable>.  È tuttavia necessario tenere conto di un'ulteriore limitazione quando si utilizza un oggetto <xref:System.Windows.Freezable> come punto di partenza per l'impostazione indiretta delle destinazioni: l'oggetto <xref:System.Windows.Freezable> iniziale e ogni oggetto <xref:System.Windows.Freezable> presente tra esso e la proprietà secondaria impostata indirettamente come destinazione non deve essere bloccato.  
  
<a name="controllable_storyboards"></a>   
## Controllo interattivo di uno storyboard in XAML  
 Per avviare uno storyboard in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], utilizzare un'azione trigger <xref:System.Windows.Media.Animation.BeginStoryboard>.  <xref:System.Windows.Media.Animation.BeginStoryboard> distribuisce le animazioni agli oggetti e alle proprietà che vengono animati, quindi avvia lo storyboard.  Per informazioni dettagliate su questo processo, vedere [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md). Se si assegna un nome allo <xref:System.Windows.Media.Animation.BeginStoryboard> specificando la relativa proprietà <xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A>, è possibile renderlo controllabile.  È quindi possibile controllare in modo interattivo lo storyboard dopo il suo avvio.  Di seguito è riportato un elenco di azioni dello storyboard controllabili che è possibile utilizzare con trigger di evento per controllare uno storyboard.  
  
-   <xref:System.Windows.Media.Animation.PauseStoryboard>: sospende lo storyboard.  
  
-   <xref:System.Windows.Media.Animation.ResumeStoryboard>: riprende uno storyboard sospeso.  
  
-   <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>: modifica la velocità dello storyboard.  
  
-   <xref:System.Windows.Media.Animation.SkipStoryboardToFill>: sposta uno storyboard alla fine del periodo di riempimento, se presente.  
  
-   <xref:System.Windows.Media.Animation.StopStoryboard>: interrompe lo storyboard.  
  
-   <xref:System.Windows.Media.Animation.RemoveStoryboard>: rimuove lo storyboard.  
  
 Nell'esempio riportato di seguito vengono utilizzate azioni di storyboard controllabili per controllare in modo interattivo uno storyboard.  
  
 [!code-xml[animation_ovws_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]  
  
<a name="controllable_storyboards_procedural"></a>   
## Controllo interattivo di uno storyboard tramite il codice  
 Negli esempi precedenti veniva illustrato come eseguire animazioni utilizzando azioni trigger.  Nel codice, è inoltre possibile controllare uno storyboard utilizzando metodi interattivi della classe <xref:System.Windows.Media.Animation.Storyboard>.  Per rendere interattivo uno <xref:System.Windows.Media.Animation.Storyboard> nel codice, è necessario utilizzare l'overload appropriato del metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> dello storyboard e specificare `true` per renderlo controllabile.  Per ulteriori informazioni, vedere la pagina <xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29>.  
  
 Di seguito sono elencati i metodi che è possibile utilizzare per modificare uno <xref:System.Windows.Media.Animation.Storyboard> dopo il suo avvio:  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>  
  
-   <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>  
  
 Il vantaggio derivante dall'utilizzo di questi metodi è che non è necessario creare oggetti <xref:System.Windows.Trigger> o <xref:System.Windows.TriggerAction>; è sufficiente disporre di un riferimento allo <xref:System.Windows.Media.Animation.Storyboard> controllabile che si desidera modificare.  
  
 **Nota:** tutte le azioni interattive eseguite in un oggetto <xref:System.Windows.Media.Animation.Clock>, e di conseguenza in uno <xref:System.Windows.Media.Animation.Storyboard> avranno luogo in corrispondenza del tick successivo del motore di temporizzazione che precederà di poco il rendering successivo.  Ad esempio, se si utilizza il metodo <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> per passare a un altro punto di un'animazione, il valore della proprietà non cambia immediatamente, ma al tick successivo del motore di temporizzazione.  
  
 Nell'esempio riportato di seguito viene illustrato come applicare e controllare le animazioni utilizzando i metodi interattivi della classe <xref:System.Windows.Media.Animation.Storyboard>.  
  
 [!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
 [!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]  
  
<a name="usingstoryboardsinstyles"></a>   
## Animazione in uno stile  
 È possibile utilizzare gli oggetti <xref:System.Windows.Media.Animation.Storyboard> per definire animazioni in uno <xref:System.Windows.Style>.  L'esecuzione di animazioni con uno <xref:System.Windows.Media.Animation.Storyboard> in uno <xref:System.Windows.Style> presenta delle analogie con l'utilizzo di uno <xref:System.Windows.Media.Animation.Storyboard> in altre situazioni, con le tre eccezioni seguenti:  
  
-   Non si specifica una proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>; lo <xref:System.Windows.Media.Animation.Storyboard> imposta sempre come destinazione l'elemento a cui viene applicato lo <xref:System.Windows.Style>.  Per impostare come destinazione gli oggetti <xref:System.Windows.Freezable>, è necessario utilizzare la modalità indiretta.  Per ulteriori informazioni sulla modalità indiretta, vedere la sezione [Impostazione indiretta delle destinazioni](#pathsyntaxforchangeable).  
  
-   Non è possibile specificare una proprietà <xref:System.Windows.EventTrigger.SourceName%2A> per un oggetto <xref:System.Windows.EventTrigger> o <xref:System.Windows.Trigger>.  
  
-   Non è possibile utilizzare espressioni di associazione dati o riferimenti di risorsa dinamici per impostare valori di proprietà di <xref:System.Windows.Media.Animation.Storyboard> o animazioni  perché quanto contenuto in uno <xref:System.Windows.Style> deve essere thread\-safe e il sistema di temporizzazione deve utilizzare il metodo <xref:System.Windows.Freezable.Freeze%2A> sugli oggetti <xref:System.Windows.Media.Animation.Storyboard> per renderli thread\-safe.  Non è possibile bloccare uno <xref:System.Windows.Media.Animation.Storyboard> se lo storyboard stesso e le relative sequenze temporali figlio contengono espressioni di associazione dati o riferimenti di risorsa dinamici.  Per ulteriori informazioni sul blocco e su altre funzionalità <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
-   In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], non è possibile dichiarare gestori eventi per eventi animazione o <xref:System.Windows.Media.Animation.Storyboard>.  
  
 Per un esempio in cui viene illustrato come dichiarare uno storyboard in uno stile, vedere l'esempio [Aggiungere un'animazione in uno stile](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-style.md).  
  
<a name="defineAStoryboardInAControlTemplateSection"></a>   
## Animazione in un ControlTemplate  
 È possibile utilizzare gli oggetti <xref:System.Windows.Media.Animation.Storyboard> per definire animazioni in un oggetto <xref:System.Windows.Controls.ControlTemplate>.  L'esecuzione di animazioni con uno <xref:System.Windows.Media.Animation.Storyboard> in un oggetto <xref:System.Windows.Controls.ControlTemplate> presenta delle analogie con l'utilizzo di uno <xref:System.Windows.Media.Animation.Storyboard> in altre situazioni, con le due eccezioni seguenti:  
  
-   La proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> può unicamente fare riferimento agli oggetti figlio dell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  La proprietà <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> non è specificata, la destinazione dell'animazione è rappresentata dall'elemento a cui viene applicato l'oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
-   La proprietà <xref:System.Windows.EventTrigger.SourceName%2A> di un oggetto <xref:System.Windows.EventTrigger> o <xref:System.Windows.Trigger> può unicamente fare riferimento agli oggetti figlio dell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
-   Non è possibile utilizzare espressioni di associazione dati o riferimenti di risorsa dinamici per impostare valori di proprietà di <xref:System.Windows.Media.Animation.Storyboard> o animazioni  perché quanto contenuto in uno <xref:System.Windows.Controls.ControlTemplate> deve essere thread\-safe e il sistema di temporizzazione deve utilizzare il metodo <xref:System.Windows.Freezable.Freeze%2A> sugli oggetti <xref:System.Windows.Media.Animation.Storyboard> per renderli thread\-safe.  Non è possibile bloccare uno <xref:System.Windows.Media.Animation.Storyboard> se lo storyboard stesso e le relative sequenze temporali figlio contengono espressioni di associazione dati o riferimenti di risorsa dinamici.  Per ulteriori informazioni sul blocco e su altre funzionalità <xref:System.Windows.Freezable>, vedere [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md).  
  
-   In [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], non è possibile dichiarare gestori eventi per eventi animazione o <xref:System.Windows.Media.Animation.Storyboard>.  
  
 Per un esempio in cui viene illustrato come definire uno storyboard in un oggetto <xref:System.Windows.Controls.ControlTemplate>, vedere l'esempio [Eseguire un'animazione in un ControlTemplate](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-controltemplate.md).  
  
<a name="animateWhenAPropertyValueChanges"></a>   
## Esecuzione di un'animazione quando viene modificato il valore di una proprietà  
 Negli stili e nei modelli di controllo, è possibile utilizzare oggetti Trigger per avviare uno storyboard alla modifica di una proprietà.  Per i relativi esempi, vedere [Attivare un'animazione quando il valore di una proprietà viene modificato](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md) e [Eseguire un'animazione in un ControlTemplate](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-in-a-controltemplate.md).  
  
 Le animazioni applicate tramite oggetti <xref:System.Windows.Trigger> di proprietà dimostrano un comportamento più complesso rispetto alle animazioni <xref:System.Windows.EventTrigger> o a quelle avviate tramite i metodi <xref:System.Windows.Media.Animation.Storyboard>.  Vengono fornite con animazioni definite da altri oggetti <xref:System.Windows.Trigger>, ma possono essere combinate con animazioni <xref:System.Windows.EventTrigger> e con animazioni attivate tramite metodi.  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [Cenni preliminari sugli oggetti Freezable](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)