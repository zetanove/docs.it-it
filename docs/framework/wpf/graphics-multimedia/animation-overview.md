---
title: "Cenni preliminari sull&#39;animazione | Microsoft Docs"
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
  - "Storyboard [WPF], animazioni"
  - "Panoramica, animazioni [WPF]"
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
caps.latest.revision: 73
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 73
---
# Cenni preliminari sull&#39;animazione
<a name="introduction"></a>[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un potente set di elementi grafici e layout funzionalità che consentono di creare interfacce utente e documenti accattivanti. Animazione può rendere un'interfaccia utente ancora più spettacolare e utilizzabile. Applicando semplicemente l'animazione di un colore di sfondo oppure utilizzando un oggetto animato <xref:System.Windows.Media.Transform>, è possibile creare transizioni significativo sullo schermo o fornire utili segnali visivi.  
  
 In questa panoramica vengono fornite informazioni introduttive per la [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sistema animazione e temporizzazione. Affronta principalmente argomenti quali l'animazione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] oggetti tramite storyboard.  

<a name="introducinganimations"></a>   
## <a name="introducing-animations"></a>Introduzione alle animazioni  
 L'animazione è un effetto ottico creata scorrendo rapidamente una serie di immagini, ognuna leggermente diverse dall'ultima. Il cervello percepisce il gruppo di immagini come un'unica scena a modifica. Nei film questa illusione viene creata utilizzando fotocamere che registrano molti fotografie, oppure i frame al secondo. Quando i fotogrammi vengono riprodotti con un proiettore, il pubblico vede un'immagine in movimento.  
  
 Animazione in un computer è simile. Ad esempio, un programma che esegue il disegno di un rettangolo dissolvenza fuori della visualizzazione potrebbe funzionare come indicato di seguito.  
  
-   Il programma crea un timer.  
  
-   Viene verificato il timer a intervalli prestabiliti per visualizzare la quantità di tempo.  
  
-   Ogni volta che viene verificato il timer, calcola il valore di opacità del rettangolo in base alle quantità di tempo.  
  
-   Il programma quindi aggiorna il rettangolo con il nuovo valore e lo ridisegna.  
  
 Prima di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] gli sviluppatori dovevano creare e gestire i propri sistemi di temporizzazione o utilizzare speciali librerie personalizzate.                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]include un efficiente sistema di temporizzazione esposto tramite codice gestito e [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e che è integrato nella [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] framework.                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]animazione rende più facile applicare animazioni ai controlli e altri oggetti grafici.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]gestisce tutte le attività di gestione di un sistema di temporizzazione e aggiornamento dello schermo in modo efficiente. Fornisce classi di temporizzazione che consentono di concentrarsi sugli effetti che si desidera creare, anziché i meccanismi di raggiungimento di tali effetti.                  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]Inoltre è semplice per creare il proprio animazioni esponendo le classi di animazione base da cui possono ereditare le classi, per produrre animazioni personalizzate. Queste animazioni personalizzate ottengono molti dei vantaggi delle prestazioni delle classi di animazione standard.  
  
<a name="thewpftimingsystem"></a>   
## <a name="wpf-property-animation-system"></a>Sistema di animazione di proprietà WPF  
 Se si comprende alcuni concetti importanti sul sistema di temporizzazione, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] animazioni possono essere più facile da utilizzare. Più importante è che, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], si animare oggetti applicando l'animazione alle relative proprietà. Ad esempio, per ingrandire un elemento del framework, si anima la <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> proprietà. Per fare un oggetto dalla visualizzazione, si anima la <xref:System.Windows.UIElement.Opacity%2A> proprietà.  
  
 Per una proprietà per disporre di funzionalità di animazione, deve soddisfare i tre requisiti seguenti:  
  
-   Deve essere una proprietà di dipendenza.  
  
-   Deve appartenere a una classe che eredita da <xref:System.Windows.DependencyObject> e implementa il <xref:System.Windows.Media.Animation.IAnimatable> interfaccia.  
  
-   Deve essere disponibile un tipo di animazione compatibile. (Se [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non viene fornito, è possibile creare. Vedere il [Cenni preliminari sulle animazioni personalizzate](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md).)  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]contiene molti oggetti che dispongono di <xref:System.Windows.Media.Animation.IAnimatable> proprietà. Controlli, ad esempio <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.TabControl>, nonché <xref:System.Windows.Controls.Panel> e <xref:System.Windows.Shapes.Shape> oggetti ereditano da <xref:System.Windows.DependencyObject>. La maggior parte delle relative proprietà sono proprietà di dipendenza.  
  
 È possibile utilizzare le animazioni quasi ovunque, che include gli stili e modelli di controllo. Le animazioni non debbano essere visive. è possibile animare oggetti che non fanno parte dell'interfaccia utente se soddisfano i criteri descritti in questa sezione.  
  
<a name="storyboardwalkthrough"></a>   
## <a name="example-make-an-element-fade-in-and-out-of-view"></a>Esempio: Rendere un elemento una dissolvenza o disattivare la visualizzazione  
 In questo esempio viene illustrato come utilizzare un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] animazione per animare il valore di una proprietà di dipendenza. Usa un <xref:System.Windows.Media.Animation.DoubleAnimation>, che è un tipo di animazione che viene generato l'errore <xref:System.Double> valori, eseguire l'animazione di <xref:System.Windows.UIElement.Opacity%2A> proprietà di un <xref:System.Windows.Shapes.Rectangle>. Di conseguenza, il <xref:System.Windows.Shapes.Rectangle> dissolvenza o disattivare la visualizzazione.  
  
 La prima parte dell'esempio crea un <xref:System.Windows.Shapes.Rectangle> elemento. I passaggi che seguono viene illustrato come creare un'animazione e applicarla al rettangolo <xref:System.Windows.UIElement.Opacity%2A> proprietà.  
  
 Di seguito è illustrato come creare un <xref:System.Windows.Shapes.Rectangle> elemento in un <xref:System.Windows.Controls.StackPanel> in XAML.  
  
 [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]  
  
 Di seguito è illustrato come creare un <xref:System.Windows.Shapes.Rectangle> elemento in un <xref:System.Windows.Controls.StackPanel> nel codice.  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]  
  
<a name="opacity_animation_step1"></a>   
### <a name="part-1-create-a-doubleanimation"></a>Parte 1: Creare un oggetto DoubleAnimation  
 Per creare un elemento menu tramite dissolvenza o disattivare la visualizzazione, è possibile animare il <xref:System.Windows.UIElement.Opacity%2A> proprietà. Poiché il <xref:System.Windows.UIElement.Opacity%2A> proprietà è di tipo <xref:System.Double>, è necessaria un'animazione che produce valori double. Oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> è un'animazione di questo tipo. Oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> crea una transizione tra due valori double. Per specificare il valore iniziale, impostare il relativo <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> proprietà. Per specificare il valore finale, impostare il relativo <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> proprietà.  
  
1.  Un valore di opacità `1.0` rende completamente opaco l'oggetto e un valore di opacità `0.0` rende completamente invisibile. To make the animation transition from                                  `1.0` to                                  `0.0` you set its                                  <xref:System.Windows.Media.Animation.DoubleAnimation.From%2A> property to                                  `1.0` and its                                  <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> property to                                  `0.0`. Di seguito è illustrato come creare un <xref:System.Windows.Media.Animation.DoubleAnimation> in XAML.  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]  
  
     Di seguito è illustrato come creare un <xref:System.Windows.Media.Animation.DoubleAnimation> nel codice.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]  
  
2.  Successivamente, è necessario specificare un <xref:System.Windows.Media.Animation.Timeline.Duration%2A>. Il <xref:System.Windows.Media.Animation.Timeline.Duration%2A> di un'animazione specifica il tempo impiegato per passare dal valore iniziale al valore di destinazione. Di seguito è illustrato come impostare il <xref:System.Windows.Media.Animation.Timeline.Duration%2A> a cinque secondi in XAML.  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]  
  
     Di seguito è illustrato come impostare il <xref:System.Windows.Media.Animation.Timeline.Duration%2A> a cinque secondi nel codice.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]  
  
3.  Il codice precedente è stato illustrato un'animazione che passa da `1.0` a `0.0`, in modo che l'elemento di destinazione applicare la dissolvenza da completamente opaco a completamente invisibile. Per fare l'elemento alla visualizzazione una volta che torni, impostare il <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> proprietà dell'animazione `true`. Per rendere l'animazione ripetuta all'infinito, impostare il relativo <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> proprietà <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>. Di seguito è illustrato come impostare il <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> e <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> proprietà in XAML.  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]  
  
     Di seguito è illustrato come impostare il <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> e <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> proprietà nel codice.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]  
  
<a name="opacity_animation_step2"></a>   
### <a name="part-2-create-a-storyboard"></a>Parte 2: Creare uno Storyboard  
 Per applicare un'animazione a un oggetto, si crea un <xref:System.Windows.Media.Animation.Storyboard> e utilizzare il <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> collegato le proprietà per specificare l'oggetto e proprietà per aggiungere un'animazione.  
  
1.  Creare il <xref:System.Windows.Media.Animation.Storyboard> e aggiungere l'animazione al relativo elemento figlio. Di seguito è illustrato come creare il <xref:System.Windows.Media.Animation.Storyboard> in XAML.  
  
     <!-- TODO: review snippet reference [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]  -->  
  
     Per creare il <xref:System.Windows.Media.Animation.Storyboard> nel codice, dichiarare un <xref:System.Windows.Media.Animation.Storyboard> variabile a livello di classe.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]  
  
     Inizializzare quindi il <xref:System.Windows.Media.Animation.Storyboard> e aggiungere l'animazione al relativo elemento figlio.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]  
  
2.  Il <xref:System.Windows.Media.Animation.Storyboard> deve conoscere la posizione in cui applicare l'animazione. Utilizzare il <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=fullName> proprietà associata per specificare l'oggetto per aggiungere un'animazione. Di seguito è illustrato come impostare il nome di destinazione di <xref:System.Windows.Media.Animation.DoubleAnimation> a `MyRectangle` in XAML.  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]  
  
     Di seguito è illustrato come impostare il nome di destinazione di <xref:System.Windows.Media.Animation.DoubleAnimation> a `MyRectangle` nel codice.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]  
  
3.  Utilizzare il <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> proprietà associata per specificare la proprietà per aggiungere un'animazione. Nell'esempio seguente viene illustrato come configurare l'animazione di destinazione di <xref:System.Windows.UIElement.Opacity%2A> proprietà del <xref:System.Windows.Shapes.Rectangle> in XAML.  
  
     [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]  
  
     Nell'esempio seguente viene illustrato come configurare l'animazione di destinazione di <xref:System.Windows.UIElement.Opacity%2A> proprietà del <xref:System.Windows.Shapes.Rectangle> nel codice.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]  
  
 Per ulteriori informazioni su <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> sintassi e per altri esempi, vedere il [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
<a name="opacity_animation_step3"></a>   
### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>Parte 3 (XAML): Associare lo Storyboard a un Trigger  
 Il modo più semplice per applicare e avviare un <xref:System.Windows.Media.Animation.Storyboard> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] consiste nell'utilizzare un trigger di evento.                          In questa sezione viene illustrato come associare il <xref:System.Windows.Media.Animation.Storyboard> con un trigger in XAML.  
  
1.  Creare un <xref:System.Windows.Media.Animation.BeginStoryboard> dell'oggetto e associare lo storyboard. Oggetto <xref:System.Windows.Media.Animation.BeginStoryboard> è un tipo di <xref:System.Windows.TriggerAction> che applica e avvia un <xref:System.Windows.Media.Animation.Storyboard>.  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]  
  
2.  Creare un <xref:System.Windows.EventTrigger> e aggiungere il <xref:System.Windows.Media.Animation.BeginStoryboard> al relativo <xref:System.Windows.EventTrigger.Actions%2A> insieme. Impostare il <xref:System.Windows.EventTrigger.RoutedEvent%2A> proprietà del <xref:System.Windows.EventTrigger> per l'evento indirizzato che si desidera avviare il <xref:System.Windows.Media.Animation.Storyboard>. (Per ulteriori informazioni sugli eventi indirizzati, vedere il [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).)  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]  
  
3.  Aggiungere il <xref:System.Windows.EventTrigger> per il <xref:System.Windows.FrameworkElement.Triggers%2A> insieme del rettangolo.  
  
     [!code-xml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]  
  
<a name="opacity_animation_step3code"></a>   
### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>Parte 3 (codice): Associare lo Storyboard a un gestore eventi  
 Il modo più semplice per applicare e avviare un <xref:System.Windows.Media.Animation.Storyboard> nel codice consiste nell'utilizzare un gestore eventi. In questa sezione viene illustrato come associare il <xref:System.Windows.Media.Animation.Storyboard> con un gestore eventi nel codice.  
  
1.  Registrazione per il <xref:System.Windows.FrameworkElement.Loaded> evento del rettangolo.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]  
  
2.  Dichiarare il gestore dell'evento. Nel gestore eventi, utilizzare il <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> metodo per applicare lo storyboard.  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]  
  
### <a name="complete-example"></a>Esempio completo  
 Di seguito viene illustrato come creare un rettangolo che si visualizza in XAML.  
  
 [!code-xml[animation_ovws2#RectangleOpacityFadeExampleXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]  
  
 Di seguito viene illustrato come creare un rettangolo che si visualizza nel codice.  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]  
  
<a name="animationtypes"></a>   
## <a name="animation-types"></a>Tipi di animazione  
 Poiché le animazioni generano valori di proprietà, per diversi tipi di proprietà diversi tipi di animazione. Per animare una proprietà che accetta un <xref:System.Double>, ad esempio il <xref:System.Windows.FrameworkElement.Width%2A> proprietà di un elemento, utilizzare un'animazione che produce <xref:System.Double> valori. Per animare una proprietà che accetta un <xref:System.Windows.Point>, utilizzare un'animazione che produce <xref:System.Windows.Point> valori e così via. A causa del numero di diversi tipi di proprietà, sono disponibili diverse classi di animazione nel <xref:System.Windows.Media.Animation> dello spazio dei nomi. Fortunatamente, seguono una convenzione di denominazione rigorosa che rende più semplice distinguere tra di essi:  
  
-   \<                         *Tipo*> animazione  
  
     Nota come "From/To/By" o "basic" animazione, viene applicata tra un valore di inizio e di destinazione, oppure aggiungendo un valore di offset al valore iniziale.  
  
    -   Per specificare un valore iniziale, impostare la proprietà From dell'animazione.  
  
    -   Per specificare un valore finale, impostare la proprietà To dell'animazione.  
  
    -   Per specificare un valore di offset, impostare la proprietà By dell'animazione.  
  
     Negli esempi inclusi in questa panoramica vengono utilizzate queste animazioni, perché sono più semplici da utilizzare. Le animazioni From/To/By sono descritti dettagliatamente i cenni preliminari sulle animazioni From/To/By.  
  
-   \<                         *Tipo*> AnimationUsingKeyFrames  
  
     Animazioni con fotogrammi chiave sono più potenti delle animazioni From/To/By perché è possibile specificare qualsiasi numero di valori di destinazione e controllarne il metodo di interpolazione. Alcuni tipi possono essere animati solo con animazioni con fotogrammi chiave. Animazioni con fotogrammi chiave sono descritte dettagliatamente le [Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md).  
  
-   \<                         *Tipo*> AnimationUsingPath  
  
     Le animazioni di percorso consentono di utilizzare un percorso geometrico per produrre valori animati.  
  
-   \<                         *Tipo*> AnimationBase  
  
     Classe astratta che, quando viene implementata, anima un <> \</> *tipo*> valore. Questa classe funge da classe base per <> \</> *tipo*> animazione e <> \</> *tipo*> classi AnimationUsingKeyFrames. È necessario gestire direttamente queste classi solo se si desidera creare animazioni personalizzate. In caso contrario, utilizzare un <> \</> *tipo*> Animation o KeyFrame<>*tipo*> animazione.  
  
 Nella maggior parte dei casi, si utilizzerà il <> \</> *tipo*> classi di animazione, ad esempio <xref:System.Windows.Media.Animation.DoubleAnimation> e <xref:System.Windows.Media.Animation.ColorAnimation>.  
  
 Nella tabella seguente mostra diversi tipi di animazione comuni e alcune proprietà con cui vengono utilizzati.  
  
|Tipo di proprietà|Animazione di base (From/To/By) corrispondente|Animazioni con fotogrammi chiave corrispondente|Animazione percorso corrispondente|Esempio di utilizzo|  
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|Nessuna|Animate the                                  <xref:System.Windows.Media.SolidColorBrush.Color%2A> of a                                  <xref:System.Windows.Media.SolidColorBrush> or a                                  <xref:System.Windows.Media.GradientStop>.|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|Animate the                                  <xref:System.Windows.FrameworkElement.Width%2A> of a                                  <xref:System.Windows.Controls.DockPanel> or the                                  <xref:System.Windows.FrameworkElement.Height%2A> of a                                  <xref:System.Windows.Controls.Button>.|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|Animare il <xref:System.Windows.Media.EllipseGeometry.Center%2A> posizione di un <xref:System.Windows.Media.EllipseGeometry>.|  
|<xref:System.String>|Nessuna|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|Nessuna|Animate the                                  <xref:System.Windows.Controls.TextBlock.Text%2A> of a                                  <xref:System.Windows.Controls.TextBlock> or the                                  <xref:System.Windows.Controls.ContentControl.Content%2A> of a                                  <xref:System.Windows.Controls.Button>.|  
  
<a name="animationsaretimelines"></a>   
### <a name="animations-are-timelines"></a>Le animazioni sono sequenze temporali  
 Tutti i tipi di animazione ereditano il <xref:System.Windows.Media.Animation.Timeline> classe; pertanto, tutte le animazioni sono tipi speciali di sequenze temporali. Oggetto <xref:System.Windows.Media.Animation.Timeline> definisce un intervallo di tempo. È possibile specificare il *comportamenti di temporizzazione* di una sequenza temporale: relativo <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, quante volte è ripetuto e tempo la velocità di avanzamento del.  
  
 Poiché un'animazione è un <xref:System.Windows.Media.Animation.Timeline>, rappresenta inoltre un intervallo di tempo. Un'animazione vengono inoltre calcolati i valori di output durante il relativo avanzamento nell'intervallo di tempo specificato (o <xref:System.Windows.Media.Animation.Timeline.Duration%2A>). Come l'animazione avanza, o "riproduzione", viene aggiornata la proprietà che è associato.  
  
 Le tre proprietà temporali utilizzate più frequentemente sono <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, e <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>.  
  
#### <a name="the-duration-property"></a>La proprietà di durata  
 Come accennato in precedenza, una sequenza temporale rappresenta un intervallo di tempo. La lunghezza del segmento di è il <xref:System.Windows.Media.Animation.Timeline.Duration%2A> della sequenza temporale, in genere specificata tramite un <xref:System.Windows.Duration.TimeSpan%2A> valore. Quando una sequenza temporale raggiunge la fine della durata, il completamento di un'iterazione.  
  
 Utilizza un'animazione relativa <xref:System.Windows.Media.Animation.Timeline.Duration%2A> proprietà per determinare il valore corrente. Se non si specifica un <xref:System.Windows.Media.Animation.Timeline.Duration%2A> valore per un'animazione, viene utilizzato il valore predefinito di 1 secondo.  
  
 La sintassi seguente viene illustrata una versione semplificata di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] attributo sintassi per la <xref:System.Windows.Media.Animation.Timeline.Duration%2A> proprietà.  
  
||  
|-|  
|*hours* `:` *minutes* `:` *seconds*|  
  
 Nella tabella seguente vengono mostrate diverse <xref:System.Windows.Duration> impostazioni e i relativi valori risultanti.  
  
|Impostazione|Valore risultante|  
|-------------|---------------------|  
|0:0:5.5|5.5 secondi.|  
|0:30:5.5|30 minuti e 5,5 secondi.|  
|1:30:5.5|1 ora, 30 minuti e 5,5 secondi.|  
  
 Per specificare un <xref:System.Windows.Duration> nel codice consiste nell'utilizzare il <xref:System.TimeSpan.FromSeconds%2A> metodo per creare un <xref:System.TimeSpan>, quindi dichiarare una nuova <xref:System.Windows.Duration> struttura utilizzando tale <xref:System.TimeSpan>.  
  
 Per ulteriori informazioni su <xref:System.Windows.Duration> valori e completo [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] sintassi, vedere il <xref:System.Windows.Duration> struttura.  
  
#### <a name="autoreverse"></a>AutoReverse  
 Il <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> proprietà specifica se una sequenza temporale viene riprodotto con le versioni precedenti, quando viene raggiunta la fine del relativo <xref:System.Windows.Media.Animation.Timeline.Duration%2A>. Se si imposta questa proprietà di animazione su `true`, un'animazione viene riprodotta una volta raggiunta la fine del relativo <xref:System.Windows.Media.Animation.Timeline.Duration%2A>, ossia dal valore iniziale al valore iniziale. Per impostazione predefinita, questa proprietà è `false`.  
  
#### <a name="repeatbehavior"></a>RepeatBehavior  
 Il <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> proprietà specifica quante volte viene riprodotto una sequenza temporale. Per impostazione predefinita, le sequenze temporali presentano un conteggio di iterazioni di `1.0`, vale a dire che vengono riprodotti una sola volta e non vengono ripetuti.  
  
 Per ulteriori informazioni su queste e altre proprietà, vedere il [Cenni preliminari sui comportamenti di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md).  
  
<a name="applyanimationstoproperty"></a>   
## <a name="applying-an-animation-to-a-property"></a>Applicare un'animazione a una proprietà  
 Nelle sezioni precedenti vengono descritti i diversi tipi di animazioni e le relative proprietà temporali. In questa sezione viene illustrato come applicare l'animazione alla proprietà che si desidera aggiungere un'animazione.                  <xref:System.Windows.Media.Animation.Storyboard> oggetti forniscono un modo per applicare animazioni alle proprietà. Oggetto <xref:System.Windows.Media.Animation.Storyboard> è un *sequenza temporale contenitore* che fornisce informazioni per le animazioni che contiene.  
  
### <a name="targeting-objects-and-properties"></a>Proprietà e oggetti di destinazione  
 Il <xref:System.Windows.Media.Animation.Storyboard> fornisce il <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> le proprietà associate. Per impostare queste proprietà per un'animazione, si indica all'animazione che si desidera animare. Tuttavia, prima di un'animazione possibile destinazione di un oggetto, l'oggetto deve in genere essere assegnato un nome.  
  
 L'assegnazione di un nome di un <xref:System.Windows.FrameworkElement> differisce dall'assegnazione di un nome di un <xref:System.Windows.Freezable> oggetto. La maggior parte dei controlli e i pannelli sono gli elementi del framework; Tuttavia, molti oggetti esclusivamente con interfaccia grafici, ad esempio pennelli, trasformazioni e geometrie, sono oggetti freezable. Se non si è certi che un tipo sia un <xref:System.Windows.FrameworkElement> o <xref:System.Windows.Freezable>, fare riferimento a di **gerarchia di ereditarietà** sezione della documentazione di riferimento.  
  
-   Per rendere un <xref:System.Windows.FrameworkElement> la destinazione di un'animazione, occorre assegnargli un nome impostando il relativo <xref:System.Windows.FrameworkElement.Name%2A> proprietà. Nel codice, è necessario utilizzare anche il <xref:System.Windows.FrameworkElement.RegisterName%2A> metodo per registrare il nome dell'elemento con la pagina a cui appartiene.  
  
-   Per rendere un <xref:System.Windows.Freezable> oggetto di destinazione di un'animazione in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], si utilizza il [direttiva X:Name](../../../../docs/framework/xaml-services/x-name-directive.md) per assegnare un nome. Nel codice, è sufficiente utilizzare il <xref:System.Windows.FrameworkElement.RegisterName%2A> metodo per registrare l'oggetto con la pagina a cui appartiene.  
  
 Le sezioni che seguono forniscono un esempio di un elemento di denominazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e codice. Per ulteriori informazioni sulla denominazione e di destinazione, vedere il [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
### <a name="applying-and-starting-storyboards"></a>L'applicazione e avvio di storyboard  
 Per avviare uno storyboard in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], associarlo a un <xref:System.Windows.EventTrigger>. Un <xref:System.Windows.EventTrigger> è un oggetto che descrive le azioni da intraprendere quando si verifica un evento specificato. Uno di tali azioni può essere un <xref:System.Windows.Media.Animation.BeginStoryboard> azione, che consente di avviare lo storyboard. Trigger di evento sono concettualmente analoghi ai gestori eventi in quanto consentono di specificare come l'applicazione risponde a un determinato evento. A differenza dei gestori eventi, i trigger di evento possono essere descritti in modo completo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; è necessario alcun altro codice.  
  
 Per avviare un <xref:System.Windows.Media.Animation.Storyboard> nel codice, è possibile utilizzare un <xref:System.Windows.EventTrigger> oppure utilizzare il <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> metodo il <xref:System.Windows.Media.Animation.Storyboard> (classe).  
  
<a name="controllingstoryboards"></a>   
## <a name="interactively-control-a-storyboard"></a>Controllare in modo interattivo uno Storyboard  
 Nell'esempio precedente è stato illustrato come avviare un <xref:System.Windows.Media.Animation.Storyboard> quando si verifica un evento. È possibile controllare anche in modo interattivo un <xref:System.Windows.Media.Animation.Storyboard> dopo l'avvio: è possibile sospendere, riprendere, arrestare, spostarlo al periodo di riempimento, cercare e rimuovere il <xref:System.Windows.Media.Animation.Storyboard>. Per ulteriori informazioni e un esempio che illustra come controllare in modo interattivo un <xref:System.Windows.Media.Animation.Storyboard>, vedere il [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
<a name="fillbehaviorsection"></a>   
## <a name="what-happens-after-an-animation-ends"></a>Che cosa accade dopo un'animazione viene terminata?  
 Il <xref:System.Windows.Media.Animation.FillBehavior> proprietà specifica il comportamento di una sequenza temporale quando termina. Per impostazione predefinita, viene avviata una sequenza temporale <xref:System.Windows.Media.Animation.ClockState> alla data di fine. Un'animazione che viene <xref:System.Windows.Media.Animation.ClockState> contiene il valore di output finale.  
  
 Il <xref:System.Windows.Media.Animation.DoubleAnimation> nell'esempio precedente non termina perché il relativo <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> è impostata su <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>. Nell'esempio seguente viene animato un rettangolo utilizzando un'animazione simile. A differenza dell'esempio precedente, il <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> e <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> proprietà di questa animazione vengono lasciate sui rispettivi valori predefiniti. Pertanto, l'animazione avanza da 1 a 0 in un intervallo di cinque secondi e quindi si arresta.  
  
 [!code-xml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]  
  
 [!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
 [!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]  
  
 Poiché il relativo <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> non è stata modificata rispetto al valore predefinito, ovvero <xref:System.Windows.Media.Animation.FillBehavior>, l'animazione mantiene il valore finale, 0, la fine. Pertanto, il <xref:System.Windows.UIElement.Opacity%2A> del rettangolo rimane impostata su 0 al termine dell'animazione termina. Se si imposta la <xref:System.Windows.UIElement.Opacity%2A> del rettangolo da un altro valore, il codice sembra non hanno alcun effetto, poiché l'animazione ancora interessa il <xref:System.Windows.UIElement.Opacity%2A> proprietà.  
  
 Per il controllo di una proprietà animata nel codice è possibile utilizzare il <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> metodo e specificare null per il <xref:System.Windows.Media.Animation.AnimationTimeline> parametro. Per ulteriori informazioni e un esempio, vedere [Set proprietà dopo l'animazione di It con uno Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md).  
  
 Si noti che, sebbene l'impostazione di un valore della proprietà che ha un <xref:System.Windows.Media.Animation.ClockState> o <xref:System.Windows.Media.Animation.ClockState> animazione sembra non avere alcun effetto, modificare il valore della proprietà. Per ulteriori informazioni, vedere il [Animation and Timing System Overview](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
<a name="databindingAndAnimatingAnimationsSection"></a>   
## <a name="data-binding-and-animating-animations"></a>Associazione dati e animazioni di animazione  
 La maggior parte delle proprietà di animazione può essere associata a dati o animate; ad esempio, è possibile animare il <xref:System.Windows.Media.Animation.Timeline.Duration%2A> proprietà di un <xref:System.Windows.Media.Animation.DoubleAnimation>. Tuttavia, a causa del funzionamento del sistema di temporizzazione, dati di animazioni associate o animate non comportarsi come gli altri dati associati o animate gli oggetti. Per comprendere questo comportamento, è utile per comprendere cosa significa applicare un'animazione a una proprietà.  
  
 Fare riferimento all'esempio nella sezione precedente che è stato illustrato come eseguire l'animazione di <xref:System.Windows.UIElement.Opacity%2A> di un rettangolo. Quando viene caricato il rettangolo nell'esempio precedente, il relativo trigger di evento applica il <xref:System.Windows.Media.Animation.Storyboard>. Il sistema di temporizzazione crea una copia di <xref:System.Windows.Media.Animation.Storyboard> e l'animazione. Queste copie sono bloccate (in sola lettura) e <xref:System.Windows.Media.Animation.Clock> vengono creati oggetti da essi. Questi orologi eseguono le operazioni effettive di animare le proprietà di destinazione.  
  
 Il sistema di temporizzazione crea un orologio per il <xref:System.Windows.Media.Animation.DoubleAnimation> e lo applica all'oggetto specificato dalla proprietà e il <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> e <xref:System.Windows.Media.Animation.Storyboard.TargetProperty%2A> del <xref:System.Windows.Media.Animation.DoubleAnimation>. In questo caso, il sistema di temporizzazione applica l'orologio per il <xref:System.Windows.UIElement.Opacity%2A> proprietà dell'oggetto denominato "MyRectangle".  
  
 Anche se viene creato un orologio anche per il <xref:System.Windows.Media.Animation.Storyboard>, l'orologio non viene applicato a tutte le proprietà. Il suo scopo è controllare l'orologio figlio, l'orologio creato per il <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
 Per un'animazione in modo da riflettere le modifiche dei dati dell'associazione o di un'animazione, è necessario rigenerare l'orologio. Orologi non vengono rigenerati automaticamente. Per rendere un'animazione a riflettere le modifiche, riapplicare il relativo storyboard utilizzando un <xref:System.Windows.Media.Animation.BeginStoryboard> o <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> metodo. Quando si utilizza uno di questi metodi, l'animazione viene riavviata. Nel codice, è possibile utilizzare il <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> eseguire il metodo per spostare lo storyboard nella posizione precedente.  
  
 Per un esempio dei dati di animazione associata, vedere [Key Spline Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160011).                  Per ulteriori informazioni sul funzionamento del sistema di animazione e temporizzazione, vedere [Animation and Timing System Overview](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
<a name="otherWaysToAnimateSection"></a>   
## <a name="other-ways-to-animate"></a>Altri modi per aggiungere un'animazione  
 Negli esempi inclusi in questa panoramica viene illustrato come aggiungere un'animazione tramite storyboard. Quando si utilizza codice, è possibile animare in molti altri modi. Per ulteriori informazioni, vedere il [Cenni preliminari sulle tecniche di animazione di proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
<a name="animation_samples"></a>   
## <a name="animation-samples"></a>Esempi di animazione  
 Negli esempi seguenti consentono di iniziare ad aggiungere animazione alle applicazioni.  
  
-   [FROM, To e dall'esempio valori di destinazione dell'animazione](http://go.microsoft.com/fwlink/?LinkID=159988)  
  
     Vengono illustrate diverse From/To/By impostazioni.  
  
-   [Esempio di comportamento](http://go.microsoft.com/fwlink/?LinkID=159970)  
  
     Illustra le varie modalità per controllare il comportamento temporale di un'animazione. In questo esempio viene inoltre illustrato come associa a dati il valore di destinazione di un'animazione.  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Animazione e temporizzazione Panoramica sistema](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)|Viene descritto l'utilizzo del sistema di temporizzazione di <xref:System.Windows.Media.Animation.Timeline> e <xref:System.Windows.Media.Animation.Clock> classi che consentono di creare animazioni.|  
|[Suggerimenti sulle animazioni](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)|Vengono elencati suggerimenti utili per la risoluzione dei problemi con animazioni, quali le prestazioni.|  
|[Cenni preliminari sulle animazioni personalizzate](../../../../docs/framework/wpf/graphics-multimedia/custom-animations-overview.md)|Viene descritto come estendere il sistema di animazione con fotogrammi chiave, le classi di animazione o callback per frame.|  
|Cenni preliminari sulle animazioni From/To/By|Viene descritto come creare un'animazione che effettua la transizione tra due valori.|  
|[Cenni preliminari sulle animazioni di fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)|Viene descritto come creare un'animazione con più valori di destinazione, inclusa la possibilità di controllare il metodo di interpolazione.|  
|[Funzioni di interpolazione](../../../../docs/framework/wpf/graphics-multimedia/easing-functions.md)|Viene descritto come applicare formule matematiche alle animazioni per ottenere un comportamento realistico, ad esempio rimbalzo.|  
|[Cenni preliminari sulle animazioni percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animations-overview.md)|Viene descritto come spostare o ruotare un oggetto lungo un percorso complesso.|  
|[Cenni preliminari sulle tecniche di animazione di proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)|Descrive le animazioni di proprietà utilizzando gli storyboard, animazioni locali, orologi e animazioni per frame.|  
|[Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)|Viene descritto come utilizzare storyboard con più sequenze temporali per creare animazioni complesse.|  
|[Cenni preliminari sui comportamenti di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/timing-behaviors-overview.md)|Viene descritto il <xref:System.Windows.Media.Animation.Timeline> tipi e le proprietà utilizzati nelle animazioni.|  
|[Cenni preliminari sugli eventi di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)|Vengono descritti gli eventi disponibili nel <xref:System.Windows.Media.Animation.Timeline> e <xref:System.Windows.Media.Animation.Clock> oggetti per l'esecuzione di codice in punti nella sequenza temporale, ad esempio avviare, sospendere, riprendere, ignorare o arrestare.|  
|[Procedure](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)|Contiene esempi di codice per l'utilizzo di animazioni e sequenze temporali nell'applicazione.|  
|[Procedure di orologi](../../../../docs/framework/wpf/graphics-multimedia/clocks-how-to-topics.md)|Contiene esempi di codice per l'utilizzo di <xref:System.Windows.Media.Animation.Clock> oggetto nell'applicazione.|  
|[Procedure relative ai fotogrammi chiave](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animation-how-to-topics.md)|Contiene esempi di codice per l'utilizzo di animazioni con fotogrammi chiave nell'applicazione.|  
|[Procedure relative all'animazione percorso](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)|Contiene esempi di codice per l'utilizzo di animazioni di percorso dell'applicazione.|  
  
<a name="reference"></a>   
## <a name="reference"></a>Riferimento  
 <xref:System.Windows.Media.Animation.Timeline>  
  
 <xref:System.Windows.Media.Animation.Storyboard>  
  
 <xref:System.Windows.Media.Animation.BeginStoryboard>  
  
 <xref:System.Windows.Media.Animation.Clock>