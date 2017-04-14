---
title: "Cenni preliminari sulle animazioni From/To/By | Microsoft Docs"
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
  - "animazione, From/To/By"
  - "From/To/By (animazione)"
ms.assetid: 516fce0a-e7f8-49b8-b018-53b3d409a8a3
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# Cenni preliminari sulle animazioni From/To/By
In questo argomento viene descritto come utilizzare le animazioni From\/To\/By per animare le [proprietà di dipendenza](GTMT).  Un'animazione From\/To\/By crea una transizione tra due valori.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prereq"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario avere familiarità con le funzionalità di animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per un'introduzione alle funzionalità di animazione, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
<a name="whatisanimation"></a>   
## Descrizione di un'animazione From\/To\/By  
 Un'animazione From\/To\/By è un tipo di oggetto <xref:System.Windows.Media.Animation.AnimationTimeline> che crea una transizione tra un valore iniziale e un valore finale.  Il tempo necessario per completare la transizione è determinato dalla proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> di tale animazione.  
  
 È possibile applicare un'animazione From\/To\/By a una proprietà utilizzando un oggetto <xref:System.Windows.Media.Animation.Storyboard> nel markup e nel codice o utilizzando il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> nel codice.  È inoltre possibile utilizzare un'animazione From\/To\/By per creare un oggetto <xref:System.Windows.Media.Animation.AnimationClock> e applicarlo a una o più proprietà.  Per ulteriori informazioni sui diversi metodi per l'applicazione delle animazioni, vedere [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
 Le animazioni From\/To\/By non possono avere più di due valori di destinazione.  Se è necessaria un'animazione con più di due valori di destinazione, utilizzare un'animazione basata su fotogrammi chiave.  Per informazioni sulle animazioni basate su fotogrammi chiave, vedere [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
<a name="animation_types"></a>   
## Tipi di animazione From\/To\/By  
 Poiché le animazioni generano valori di proprietà, sono disponibili tipi di animazione diversi per i diversi tipi di proprietà.  Per animare una proprietà che accetta un oggetto <xref:System.Double>, ad esempio la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di un elemento, utilizzare un'animazione che produce valori <xref:System.Double>.  Per animare una proprietà che accetta un oggetto <xref:System.Windows.Point>, utilizzare un'animazione che produce valori <xref:System.Windows.Point> e così via.  
  
 Le classi di animazioni From\/To\/By appartengono allo spazio dei nomi <xref:System.Windows.Media.Animation> e utilizzano la convenzione di denominazione seguente:  
  
 *\<Tipo\>* `Animation`  
  
 Dove *\<Tipo\>* è il tipo di valore animato dalla classe.  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili le classi di animazioni From\/To\/By seguenti.  
  
|Tipo proprietà|Classe di animazione From\/To\/By corrispondente|  
|--------------------|------------------------------------------------------|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimation>|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimation>|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16Animation>|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32Animation>|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64Animation>|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimation>|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimation>|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimation>|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimation>|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimation>|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimation>|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimation>|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimation>|  
  
<a name="anim_values"></a>   
## Valori di destinazione  
 Un'animazione From\/To\/By crea una transizione tra due valori di destinazione.  In genere, si specificano un valore iniziale \(impostarlo tramite la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> \) e un valore finale \(impostarlo tramite la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> \).  È tuttavia possibile specificare solo un valore iniziale, un valore di destinazione o un valore di offset.  In questi casi, l'animazione ottiene il valore di destinazione mancante dalla proprietà a cui viene applicata.  Nell'elenco seguente sono descritte le diverse modalità per specificare i valori di destinazione di un'animazione.  
  
-   **Valore iniziale**  
  
     Utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> quando si desidera specificare in modo esplicito il valore iniziale di un'animazione.  È possibile utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> da sola o con la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> o <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.  Se si specifica solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, l'animazione esegue la transizione da tale valore al valore di base della proprietà animata.  
  
-   **Valore finale**  
  
     Per specificare un valore finale di un'animazione, utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>.  Se si utilizza solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, l'animazione ottiene il valore iniziale dalla proprietà a cui viene applicata o dall'output di un'altra animazione applicata alla stessa proprietà.  È possibile utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> con la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> per specificare in modo esplicito i valori iniziale e finale dell'animazione.  
  
-   **Valore di offset**  
  
     La proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> consente di specificare un offset anziché un valore iniziale o finale esplicito dell'animazione.  La proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> di un'animazione specifica di quanto un valore viene modificato dall'animazione nel corso della durata.  È possibile utilizzare la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> da sola o con la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>.  Se si specifica solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>, l'animazione aggiunge il valore di offset al valore di base della proprietà o all'output di un'altra animazione.  
  
<a name="examples"></a>   
## Utilizzo di valori From\/To\/By  
 Nelle sezioni seguenti viene descritto come utilizzare le proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> insieme o singolarmente.  
  
 In ogni esempio di questa sezione viene utilizzato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>, ossia un tipo di animazione From\/To\/By, per animare la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle>, caratterizzato da un'altezza di 10 [Device Independent Pixel](GTMT) e da una larghezza di 100 [Device Independent Pixel](GTMT).  
  
 Benché ogni esempio utilizzi un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>, le proprietà From, To e By di tutte le animazioni From\/To\/By si comportano allo stesso modo.  Sebbene ognuno di questi esempi utilizzi un oggetto <xref:System.Windows.Media.Animation.Storyboard>, è possibile utilizzare le animazioni From\/To\/By in altri modi.  Per ulteriori informazioni, vedere [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
### From\/To  
 Quando si impostano i valori <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> insieme, l'animazione avanza dal valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> al valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>.  
  
 Nell'esempio riportato di seguito viene impostata su 50 la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> e su 300 la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>.  Di conseguenza, la proprietà <xref:System.Windows.FrameworkElement.Width%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> viene animata da 50 a 300.  
  
 [!code-csharp[basicvalues_snip#FromToAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromtoanimationinline)]
 [!code-vb[basicvalues_snip#FromToAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromtoanimationinline)]  
  
### Per  
 Quando si imposta solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>, l'animazione avanza dal valore di base della proprietà animata, o dall'output di un'animazione in composizione applicata in precedenza alla stessa proprietà, al valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>.  
  
 Per animazione in composizione si intende un'animazione <xref:System.Windows.Media.Animation.ClockState> o <xref:System.Windows.Media.Animation.ClockState> applicata in precedenza alla stessa proprietà e ancora attiva quando l'animazione corrente viene applicata utilizzando il comportamento di handoff di <xref:System.Windows.Media.Animation.HandoffBehavior>.  
  
 Nell'esempio riportato di seguito viene impostata su 300 solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>.  Poiché non è stato specificato alcun valore iniziale, l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> utilizza il valore di base \(100\) della proprietà <xref:System.Windows.FrameworkElement.Width%2A> come valore iniziale.  La proprietà <xref:System.Windows.FrameworkElement.Width%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> viene animata da 100 al valore di destinazione dell'animazione pari a 300.  
  
 [!code-csharp[basicvalues_snip#ToAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#toanimationinline)]
 [!code-vb[basicvalues_snip#ToAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#toanimationinline)]  
  
### Utente  
 Quando si imposta solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> di un'animazione, l'animazione avanza dal valore di base della proprietà animata, o dall'output di un'animazione in composizione, alla somma di tale valore e del valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.  
  
 Nell'esempio riportato di seguito viene impostata su 300 solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>.  Poiché nell'esempio non viene specificato un valore iniziale, l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> utilizza il valore di base della proprietà <xref:System.Windows.FrameworkElement.Width%2A>, 100, come valore iniziale.  Il valore finale, 400, è determinato dall'aggiunta del valore della proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> dell'animazione, 300, al valore iniziale, 100.  Di conseguenza, la proprietà <xref:System.Windows.FrameworkElement.Width%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> viene animata da 100 a 400.  
  
 [!code-csharp[basicvalues_snip#ByAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#byanimationinline)]
 [!code-vb[basicvalues_snip#ByAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#byanimationinline)]  
  
### From\/By  
 Quando si impostano le proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> di un'animazione, l'animazione avanza dal valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, al valore specificato dalla somma delle proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.  
  
 Nell'esempio riportato di seguito viene impostata su 50 la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> e su 300 la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>.  Il valore finale, 350, è determinato dall'aggiunta del valore della proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> dell'animazione, 300, al valore iniziale, 50.  Di conseguenza, la proprietà <xref:System.Windows.FrameworkElement.Width%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> viene animata da 50 a 350.  
  
 [!code-csharp[basicvalues_snip#FromByAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#frombyanimationinline)]
 [!code-vb[basicvalues_snip#FromByAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#frombyanimationinline)]  
  
### Da  
 Quando si specifica solo il valore della proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> di un'animazione, l'animazione avanza dal valore specificato dalla proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>, al valore di base della proprietà animata o all'output di un'animazione in composizione.  
  
 Nell'esempio riportato di seguito viene impostata su 50 solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>.  Poiché non è stato specificato alcun valore finale, l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> utilizza il valore di base della proprietà <xref:System.Windows.FrameworkElement.Width%2A>, 100, come valore iniziale.  La proprietà <xref:System.Windows.FrameworkElement.Width%2A> dell'oggetto <xref:System.Windows.Shapes.Rectangle> viene animata da 50 al valore di base della proprietà <xref:System.Windows.FrameworkElement.Width%2A>, 100.  
  
 [!code-csharp[basicvalues_snip#FromAnimationInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromanimationinline)]
 [!code-vb[basicvalues_snip#FromAnimationInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromanimationinline)]  
  
### To\/By  
 Se si impostano entrambe le proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> e <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> di un'animazione, la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> viene ignorata.  
  
<a name="otheranimationtypes"></a>   
## Altri tipi di animazione  
 Le animazioni From\/To\/By non sono l'unico tipo di animazioni disponibili in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Vengono inoltre fornite animazioni basate su fotogrammi chiave e animazioni percorso.  
  
-   Un'animazione basata su fotogrammi chiave si applica a un numero qualsiasi di valori di destinazione, descritti utilizzando i fotogrammi chiave.  Per ulteriori informazioni, vedere [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
-   Un'animazione percorso genera valori di output da un oggetto <xref:System.Windows.Media.PathGeometry>.  Per ulteriori informazioni, vedere [Panoramica sulle animazioni percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md).  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è inoltre possibile creare tipi di animazione personalizzati.  Per ulteriori informazioni, vedere [Cenni preliminari sulle animazioni personalizzate](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.Animation.Timeline>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Cenni preliminari sulle animazioni con fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)   
 [Panoramica sulle animazioni percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)   
 [Cenni preliminari sulle animazioni personalizzate](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)   
 [Esempio di valori di destinazione dell'animazione From\/To\/By](http://go.microsoft.com/fwlink/?LinkID=159988)