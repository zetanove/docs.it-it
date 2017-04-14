---
title: "Cenni preliminari sulle tecniche di animazione delle propriet&#224; | Microsoft Docs"
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
  - "animazione, proprietà, metodi"
  - "proprietà, metodi per l'animazione"
ms.assetid: 74f61413-f8c0-4e75-bf04-951886426c8b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Cenni preliminari sulle tecniche di animazione delle propriet&#224;
In questo argomento vengono illustrati i diversi metodi di animazione delle proprietà: storyboard, animazioni locali, orologi e animazioni per frame.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere le funzionalità di animazione di base descritte in [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
<a name="summary"></a>   
## Diverse modalità di animazione  
 Poiché esistono diversi scenari per le proprietà di animazione, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce numerosi approcci per tali proprietà.  
  
 Per ciascun approccio, la tabella riportata di seguito indica se può essere utilizzato per istanza, negli stili, nei modelli di controllo o nei modelli di dati; se può essere utilizzato in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e se consente di controllare l'animazione in modo interattivo.  "Per istanza" si riferisce alla tecnica di applicare un'animazione o uno storyboard direttamente a istanze di un oggetto, piuttosto che in uno stile, un modello di controllo o un modello di dati.  
  
|Tecnica di animazione|Scenari|Supporta XAML|Controllabile in modo interattivo|  
|---------------------------|-------------|-------------------|---------------------------------------|  
|Animazione storyboard|Per istanza, <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, <xref:System.Windows.DataTemplate>|Sì|Sì|  
|Animazione locale|Per istanza|No|No|  
|Animazione orologio|Per istanza|No|Sì|  
|Animazione per frame|Per istanza|No|N\/D|  
  
<a name="storyboard_animations"></a>   
## Animazioni storyboard  
 Utilizzare uno <xref:System.Windows.Media.Animation.Storyboard> per definire e applicare le animazioni in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], per controllare in modo interattivo le animazioni dopo l'avvio, per creare una struttura ad albero complessa di animazioni o per eseguire animazioni in uno <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate> o <xref:System.Windows.DataTemplate>.  Perché un oggetto sia animato da uno <xref:System.Windows.Media.Animation.Storyboard>, è necessario che sia <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> oppure deve essere utilizzato per impostare <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>.  Per ulteriori informazioni, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
 Uno <xref:System.Windows.Media.Animation.Storyboard> è un tipo di contenitore <xref:System.Windows.Media.Animation.Timeline> speciale che fornisce informazioni sulla destinazione delle animazioni che contiene.  Per eseguire animazioni con uno <xref:System.Windows.Media.Animation.Storyboard>, è necessario completare i tre passaggi riportati di seguito.  
  
1.  Dichiarare uno <xref:System.Windows.Media.Animation.Storyboard> e una o più animazioni.  
  
2.  Utilizzare le proprietà associate <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> [](GTMT)per specificare l'oggetto di destinazione e la proprietà di ciascuna animazione.  
  
3.  \(Solo codice\) Definire un oggetto <xref:System.Windows.NameScope> per <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>.  Registrare i nomi degli oggetti da animare con <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>.  
  
4.  Iniziare lo <xref:System.Windows.Media.Animation.Storyboard>.  
  
 L'inizio di uno <xref:System.Windows.Media.Animation.Storyboard> consente di applicare le animazioni alle proprietà animate e di avviarle.  Sono disponibili due modalità di inizio di uno <xref:System.Windows.Media.Animation.Storyboard>: è possibile utilizzare il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> fornito dalla classe <xref:System.Windows.Media.Animation.Storyboard> oppure utilizzare un'azione <xref:System.Windows.Media.Animation.BeginStoryboard>.  L'unico modo per eseguire le animazioni in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] è di utilizzare un'azione <xref:System.Windows.Media.Animation.BeginStoryboard>. Un'azione <xref:System.Windows.Media.Animation.BeginStoryboard> può essere utilizzata in un oggetto <xref:System.Windows.EventTrigger>, <xref:System.Windows.Trigger> della proprietà o <xref:System.Windows.DataTrigger>.  
  
 Nella tabella seguente sono riportate le diverse posizioni in cui è supportata la tecnica di inizio di ciascuno <xref:System.Windows.Media.Animation.Storyboard>: per istanza, stile, modello di controllo e modello di dati.  
  
|Storyboard iniziato utilizzando…|Per istanza|Stile|Modello di controllo|Modello di dati|Esempio|  
|--------------------------------------|-----------------|-----------|--------------------------|---------------------|-------------|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.EventTrigger>|Sì|Sì|Sì|Sì|[Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.Trigger> della proprietà|No|Sì|Sì|Sì|[Attivare un'animazione quando il valore di una proprietà viene modificato](../../../../docs/framework/wpf/graphics-multimedia/how-to-trigger-an-animation-when-a-property-value-changes.md)|  
|<xref:System.Windows.Media.Animation.BeginStoryboard> e <xref:System.Windows.DataTrigger>|No|Sì|Sì|Sì|[How to: Trigger an Animation When Data Changes](http://msdn.microsoft.com/it-it/a736bb3a-2ae5-479a-a33a-75a27055d863)|  
|Metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>|Sì|No|No|No|[Animare una proprietà utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)|  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Animation.Storyboard>, vedere [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
## Animazioni locali  
 Le animazioni locali costituiscono un comodo mezzo per animare una [proprietà di dipendenza](GTMT) di qualsiasi oggetto <xref:System.Windows.Media.Animation.Animatable>.  È possibile utilizzare le animazioni locali per applicare una singola animazione a una proprietà, senza bisogno di controllare in modo interattivo l'animazione dopo l'avvio.  A differenza di un'animazione <xref:System.Windows.Media.Animation.Storyboard>, un'animazione locale può animare un oggetto non associato a <xref:System.Windows.FrameworkElement> o a <xref:System.Windows.FrameworkContentElement>.  Inoltre, non è necessario definire un oggetto <xref:System.Windows.NameScope> per questo tipo di animazione.  
  
 Le animazioni locali possono essere utilizzate solo nel codice e non possono essere definite negli stili, nei modelli di controllo o nei modelli di dati.  Un'animazione locale non può essere controllata in modo interattivo dopo l'avvio.  
  
 Per animare utilizzando un'animazione locale, è necessario completare i passaggi riportati di seguito.  
  
1.  Creare un oggetto <xref:System.Windows.Media.Animation.AnimationTimeline>.  
  
2.  Utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> dell'oggetto che si desidera animare per applicare <xref:System.Windows.Media.Animation.AnimationTimeline> alla proprietà specificata.  
  
 Nell'esempio seguente viene illustrato come animare la larghezza e il colore di sfondo di un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-cpp[animateproperty#11](../../../../samples/snippets/cpp/VS_Snippets_Wpf/animateproperty/CPP/LocalAnimationExample.cpp#11)]
 [!code-csharp[animateproperty#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animateproperty/CSharp/LocalAnimationExample.cs#11)]
 [!code-vb[animateproperty#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animateproperty/VisualBasic/LocalAnimationExample.vb#11)]  
  
## Animazioni orologio  
 Utilizzare gli oggetti <xref:System.Windows.Media.MediaPlayer.Clock%2A> quando si desidera eseguire animazioni senza utilizzare uno <xref:System.Windows.Media.Animation.Storyboard> e si desidera creare complesse strutture ad albero delle temporizzazioni o controllare in modo interattivo le animazioni dopo l'avvio.  È possibile utilizzare gli oggetti Clock per animare una [proprietà di dipendenza](GTMT) di qualsiasi oggetto <xref:System.Windows.Media.Animation.Animatable>.  
  
 Non è possibile utilizzare direttamente gli oggetti <xref:System.Windows.Media.Animation.Clock> per eseguire l'animazione negli stili, nei modelli di controllo o nei modelli di dati.  \(Il sistema di animazione e di temporizzazione utilizza effettivamente gli oggetti <xref:System.Windows.Media.Animation.Clock> per l'animazione negli stili, nei modelli di controllo e di dati ma questi oggetti <xref:System.Windows.Media.Animation.Clock> devono essere creati appositamente da uno <xref:System.Windows.Media.Animation.Storyboard>.  Per ulteriori informazioni sulla relazione tra gli oggetti <xref:System.Windows.Media.Animation.Storyboard> e gli oggetti <xref:System.Windows.Media.Animation.Clock>, vedere [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).\)  
  
 Per applicare un singolo oggetto <xref:System.Windows.Media.Animation.Clock> a una proprietà, è necessario completare i passaggi riportati di seguito.  
  
1.  Creare un oggetto <xref:System.Windows.Media.Animation.AnimationTimeline>.  
  
2.  Utilizzare il metodo <xref:System.Windows.Media.Animation.AnimationTimeline.CreateClock%2A> di <xref:System.Windows.Media.Animation.AnimationTimeline> per creare un oggetto <xref:System.Windows.Media.Animation.AnimationClock>.  
  
3.  Utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> dell'oggetto che si desidera animare per applicare <xref:System.Windows.Media.Animation.AnimationClock> alla proprietà specificata.  
  
 Nell'esempio riportato di seguito viene illustrato come creare un oggetto <xref:System.Windows.Media.Animation.AnimationClock> e come applicarlo a due proprietà simili.  
  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/AnimationClockExample.cs#graphicsmmcreateanimationclockwholeclass)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMCreateAnimationClockWholeClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/animationclockexample.vb#graphicsmmcreateanimationclockwholeclass)]  
  
 Per creare una struttura ad albero delle temporizzazioni e utilizzarne le proprietà animate, è necessario completare i passaggi riportati di seguito.  
  
1.  Utilizzare gli oggetti <xref:System.Windows.Media.Animation.ParallelTimeline> e <xref:System.Windows.Media.Animation.AnimationTimeline> per creare la struttura ad albero delle temporizzazioni.  
  
2.  Utilizzare <xref:System.Windows.Media.Animation.TimelineGroup.CreateClock%2A> di <xref:System.Windows.Media.Animation.ParallelTimeline> radice per creare un oggetto <xref:System.Windows.Media.Animation.ClockGroup>.  
  
3.  Scorrere <xref:System.Windows.Media.Animation.ClockGroup.Children%2A> di <xref:System.Windows.Media.Animation.ClockGroup> e applicare i relativi oggetti <xref:System.Windows.Media.Animation.Clock> figlio.  Per ciascun <xref:System.Windows.Media.Animation.AnimationClock> figlio, utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%2A> dell'oggetto che si desidera animare per applicare <xref:System.Windows.Media.Animation.AnimationClock> alla proprietà specificata.  
  
 Per ulteriori informazioni sugli oggetti Clock, vedere [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
## Animazione per frame: ignorare il sistema di animazione e di temporizzazione  
 Utilizzare questo approccio quando è necessario ignorare completamente il sistema di animazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Uno scenario di questo approccio è rappresentato dalle animazioni fisiche, dove ciascun passaggio dell'animazione richiede che gli oggetti siano ricalcolati in base all'ultima serie di interazioni dell'oggetto.  
  
 Le animazioni per frame non possono essere definite negli stili, nei modelli di controllo o nei modelli di dati.  
  
 Per l'animazione frame per frame, è necessario eseguire la registrazione per l'evento <xref:System.Windows.Media.CompositionTarget.Rendering> dell'oggetto che contiene gli oggetti da animare.  Questo metodo per la gestione eventi viene chiamato una volta per ciascun frame.  Ogni volta che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esegue il marshalling dei dati di rendering permanenti della [struttura ad albero visuale](GTMT) nella struttura ad albero della composizione, viene chiamato il metodo per la gestione eventi.  
  
 Nel gestore eventi, eseguire i calcoli necessari per l'effetto di animazione e impostare le proprietà degli oggetti da animare con tali valori.  
  
 Per ottenere l'ora di presentazione del frame corrente, è possibile eseguire il cast dell'oggetto <xref:System.EventArgs> associato a questo evento come <xref:System.Windows.Media.RenderingEventArgs> che fornisce una proprietà <xref:System.Windows.Media.RenderingEventArgs.RenderingTime%2A> utilizzabile per ottenere l'ora di rendering del frame corrente.  
  
 Per ulteriori informazioni, vedere la pagina <xref:System.Windows.Media.CompositionTarget.Rendering>.  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)   
 [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)