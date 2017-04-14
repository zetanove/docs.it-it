---
title: "Suggerimenti sulle animazioni | Microsoft Docs"
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
  - "animazione di oggetti [WPF], risoluzione dei problemi"
  - "suggerimenti sulle animazioni [WPF]"
  - "animazioni [WPF], FillBehavior (proprietà)"
  - "animazioni [WPF], utilizzo di risorse di sistema"
  - "risoluzione dei problemi relativi alle prestazioni [WPF], animazione"
  - "suggerimenti [WPF], animazione"
  - "risoluzione dei problemi [WPF], animazione"
  - "risoluzione dei problemi di animazione [WPF]"
ms.assetid: e467796b-d5d4-45a6-a108-8c5d7ff69a0f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Suggerimenti sulle animazioni
Quando si utilizzano animazioni in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], sono disponibili numerosi suggerimenti che ne migliorano le prestazioni e ne riducono le difficoltà di impiego.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="generalissuessection"></a>   
## Esempi generali  
  
### Animazione della posizione di una barra di scorrimento o di un dispositivo di scorrimento bloccata  
 Se si anima la posizione di una barra di scorrimento o di un dispositivo di scorrimento mediante un'animazione che possiede un oggetto <xref:System.Windows.Media.Animation.FillBehavior> di <xref:System.Windows.Media.Animation.FillBehavior> \(valore predefinito\), l'utente non sarà più in grado di spostare la barra di scorrimento o il dispositivo di scorrimento.  Ciò è dovuto al fatto che, anche se l'animazione è terminata, è ancora in corso l'override del valore di base della proprietà di destinazione.  Per interrompere l'animazione dall'override del valore corrente della proprietà, rimuoverla o fornirle un oggetto <xref:System.Windows.Media.Animation.FillBehavior> di <xref:System.Windows.Media.Animation.FillBehavior>.  Per ulteriori informazioni e un esempio, vedere [Impostare una proprietà dopo averla animata con uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md).  
  
### Animazione dell'output di un'animazione senza alcun effetto  
 Non è possibile animare a un oggetto che rappresenta l'output di un'altra animazione.  Ad esempio, se si utilizza <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames> per animare <xref:System.Windows.Shapes.Shape.Fill%2A> di <xref:System.Windows.Shapes.Rectangle> da <xref:System.Windows.Media.RadialGradientBrush> a <xref:System.Windows.Media.SolidColorBrush>, non è possibile animare tutte le proprietà di <xref:System.Windows.Media.RadialGradientBrush> o <xref:System.Windows.Media.SolidColorBrush>.  
  
### Impossibile modificare il valore di una proprietà dopo l'aggiunta di un'animazione  
 In alcuni casi, potrebbe sembrare che non sia possibile modificare il valore di una proprietà dopo che è stata animata, anche dopo la conclusione dell'animazione.  Ciò è dovuto al fatto che, anche se l'animazione è terminata, è ancora in corso l'override del valore di base della proprietà.  Per interrompere l'animazione dall'override del valore corrente della proprietà, rimuoverla o fornirle un oggetto <xref:System.Windows.Media.Animation.FillBehavior> di <xref:System.Windows.Media.Animation.FillBehavior>.  Per ulteriori informazioni e un esempio, vedere [Impostare una proprietà dopo averla animata con uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-set-a-property-after-animating-it-with-a-storyboard.md).  
  
### Modifica della sequenza temporale senza alcun effetto  
 Sebbene la maggior parte delle proprietà <xref:System.Windows.Media.Animation.Timeline> possa animare e possa essere associata a dati, la modifica dei valori delle proprietà di un oggetto <xref:System.Windows.Media.Animation.Timeline> attivo non produce alcun effetto.  Ciò è dovuto al fatto che, una volta iniziato <xref:System.Windows.Media.Animation.Timeline>, il sistema di temporizzazione consente di effettuare una copia di <xref:System.Windows.Media.Animation.Timeline> ed utilizzarla per creare un oggetto <xref:System.Windows.Media.Animation.Clock>.  La modifica dell'originale non ha alcun effetto sulla copia del sistema.  
  
 Affinché <xref:System.Windows.Media.Animation.Timeline> rifletta le modifiche, il clock deve essere rigenerato e utilizzato per sostituire quello creato in precedenza.  I clock non vengono rigenerati automaticamente.  Di seguito vengono riportate le diverse modalità per applicare le modifiche alla sequenza temporale:  
  
-   Se la sequenza temporale è o appartiene a un oggetto <xref:System.Windows.Media.Animation.Storyboard>, è possibile far sì che rifletta le modifiche tramite una nuova applicazione dello storyboard, utilizzando un oggetto <xref:System.Windows.Media.Animation.BeginStoryboard> o il metodo <xref:System.Windows.Media.Animation.Storyboard.Begin%2A>.  Ciò ha come effetto collaterale il riavvio dell'animazione.  Nel codice è possibile utilizzare il metodo <xref:System.Windows.Media.Animation.Storyboard.Seek%2A> per riportare lo storyboard alla posizione precedente.  
  
-   Se un'animazione è stata applicata direttamente a una proprietà utilizzando il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>, chiamare nuovamente il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> e passare l'animazione che è stata modificata.  
  
-   Se si lavora direttamente a livello di clock, creare e applicare un nuovo insieme di clock e utilizzarli per sostituire l'insieme di clock generati in precedenza.  
  
 Per ulteriori informazioni sui clock e sulle sequenze temporali, vedere la sezione [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
### Funzionamento imprevisto di FillBehavior.Stop  
 In alcuni casi può sembrare che l'impostazione della proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> su <xref:System.Windows.Media.Animation.FillBehavior> non abbia alcun effetto, ad esempio quando un'animazione viene restituita a un'altra in quanto ha l'impostazione <xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A> di <xref:System.Windows.Media.Animation.HandoffBehavior>.  
  
 Nell'esempio che segue vengono creati un oggetto <xref:System.Windows.Controls.Canvas>, un oggetto <xref:System.Windows.Shapes.Rectangle> e un oggetto <xref:System.Windows.Media.TranslateTransform>.  <xref:System.Windows.Media.TranslateTransform> verrà animato per spostare l'oggetto <xref:System.Windows.Shapes.Rectangle> intorno a <xref:System.Windows.Controls.Canvas>.  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipAnimatedObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipanimatedobject)]  
  
 Negli esempi riportati in questa sezione vengono utilizzati gli oggetti precedenti per illustrare numerosi casi in cui il funzionamento della proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> non è quello previsto.  
  
#### FillBehavior\="Stop" e HandoffBehavior con animazioni multiple  
 Talvolta si ha l'impressione che un'animazione ignori la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> corrispondente quando sostituita da una seconda animazione.  Nell'esempio seguente vengono creati due oggetti <xref:System.Windows.Media.Animation.Storyboard> utilizzati per animare lo stesso oggetto <xref:System.Windows.Media.TranslateTransform> illustrato nell'esempio precedente.  
  
 Il primo <xref:System.Windows.Media.Animation.Storyboard>, `B1` aggiunge un'animazione alla proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> dell'oggetto <xref:System.Windows.Media.TranslateTransform> da 0 a 350, che consente di spostare il rettangolo di 350 pixel a destra.  Quando l'animazione raggiunge la fine della durata e si interrompe, viene ripristinato il valore originale della proprietà <xref:System.Windows.Media.TranslateTransform.X%2A>, cioè 0.  Di conseguenza, il rettangolo si sposta a destra di 350 pixel, quindi torna alla posizione originale.  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB1Button](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb1button)]  
  
 Anche il secondo <xref:System.Windows.Media.Animation.Storyboard>, `B2` anima la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> dello stesso oggetto <xref:System.Windows.Media.TranslateTransform>.  Dal momento che solo la proprietà <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> dell'animazione in <xref:System.Windows.Media.Animation.Storyboard> è impostata, l'animazione utilizza i valori correnti della proprietà che anima come valore iniziale.  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB2Button](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb2button)]  
  
 Se si fa clic sul secondo pulsante mentre il primo oggetto <xref:System.Windows.Media.Animation.Storyboard> è in fase di riproduzione, si può prevedere il seguente funzionamento:  
  
1.  Il primo storyboard termina e invia di nuovo il rettangolo alla relativa posizione originale, dal momento che l'animazione possiede un oggetto <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> di <xref:System.Windows.Media.Animation.FillBehavior>.  
  
2.  Il secondo storyboard viene applicato e viene animato dalla posizione corrente che è va 0 a 500.  
  
 **Ma non è quello che si verifica.** Al contrario, il rettangolo non torna alla posizione originale ma continua a spostarsi a destra.  Ciò accade perché la seconda animazione utilizza il valore corrente della prima animazione come valore iniziale e viene eseguita da tale valore fino a 500.  Quando la seconda animazione sostituisce la prima poiché viene utilizzato <xref:System.Windows.Media.Animation.HandoffBehavior> <xref:System.Windows.Media.Animation.HandoffBehavior>, il <xref:System.Windows.Media.Animation.FillBehavior> relativo alla prima animazione non è rilevante.  
  
#### FillBehavior ed eventi completati  
 Negli esempi successivi verrà illustrato un altro scenario in cui <xref:System.Windows.Media.Animation.FillBehavior> <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> sembra non produrre alcun effetto.  Nell'esempio viene utilizzato uno storyboard per animare la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> di <xref:System.Windows.Media.TranslateTransform> da 0 a 350.  Tuttavia, in questa occasione l'esempio effettua la registrazione per l'evento <xref:System.Windows.Media.Animation.Timeline.Completed>.  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardCButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardcbutton)]  
  
 Il gestore di eventi <xref:System.Windows.Media.Animation.Timeline.Completed> avvia un altro oggetto <xref:System.Windows.Media.Animation.Storyboard> che anima la stessa proprietà a partire dal valore corrente fino a 500.  
  
 [!code-csharp[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml.cs#fillbehaviortipstoryboardc1completedhandler)]
 [!code-vb[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/VisualBasic/FillBehaviorTip.xaml.vb#fillbehaviortipstoryboardc1completedhandler)]  
  
 Di seguito viene riportato il markup che definisce il secondo <xref:System.Windows.Media.Animation.Storyboard> come risorsa.  
  
 [!code-xml[AnimationTipsAndTricksSample_snip#FillBehaviorTipResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipresources)]  
  
 Quando si esegue <xref:System.Windows.Media.Animation.Storyboard>, si prevede che la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> di <xref:System.Windows.Media.TranslateTransform> venga animata da 0 a 350, quindi venga ripristinata su 0 una volta completata \(dal momento che ha un'impostazione <xref:System.Windows.Media.Animation.FillBehavior> equivalente a <xref:System.Windows.Media.Animation.FillBehavior>\) e quindi venga animata da 0 a 500.  Al contrario, <xref:System.Windows.Media.TranslateTransform> anima da 0 a 350, quindi fino a 500.  
  
 Ciò è dovuto all'ordine in cui [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] genera eventi e ai valori della proprietà che sono memorizzati nella cache e non vengono ricalcolati, a meno che la proprietà non sia stata invalidata.  L'evento <xref:System.Windows.Media.Animation.Timeline.Completed> viene elaborato per prima in quanto attivato dalla sequenza temporale radice \(il primo <xref:System.Windows.Media.Animation.Storyboard>\).  In questa fase, la proprietà <xref:System.Windows.Media.TranslateTransform.X%2A> restituisce comunque il valore animato in quanto non è stata ancora invalidata.  Il secondo <xref:System.Windows.Media.Animation.Storyboard> utilizza il valore memorizzato nella cache come valore iniziale e inizia l'animazione.  
  
<a name="performancesection"></a>   
## Prestazioni  
  
### Continuo dell'esecuzione delle animazioni dopo lo spostamento da una pagina  
 Quando ci si sposta da <xref:System.Windows.Controls.Page> contenente animazioni in esecuzione, tali animazioni continuano la riproduzione fino a quando <xref:System.Windows.Controls.Page> non viene raccolto nel Garbage Collector.  A seconda del sistema di navigazione in uso, una pagina dalla quale ci si è spostati potrebbe rimanere in memoria per un tempo indefinito, utilizzando per tutto il tempo le risorse con le relative animazioni.  Ciò è più evidente quando una pagina contiene animazioni in esecuzione continua.  
  
 Per questo motivo si consiglia di utilizzare l'evento <xref:System.Windows.FrameworkElement.Unloaded> per rimuovere le animazioni quando ci si sposta da una pagina.  
  
 Sono disponibili diversi modi per rimuovere un'animazione.  È possibile utilizzare le tecniche riportate di seguito per rimuovere animazioni appartenenti a <xref:System.Windows.Media.Animation.Storyboard>.  
  
-   Per rimuovere <xref:System.Windows.Media.Animation.Storyboard> avviato con un trigger di evento, vedere [How to: Remove a Storyboard](http://msdn.microsoft.com/it-it/7fe39531-de2f-46a0-a69f-b783d04235ee).  
  
-   Per la rimozione di <xref:System.Windows.Media.Animation.Storyboard> mediante codice, vedere il metodo <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>.  
  
 La tecnica successiva può essere utilizzata indipendentemente dalla modalità di avviamento dell'animazione.  
  
-   Per rimuovere le animazioni da una determinata proprietà, utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29>.  Specificare la proprietà a cui si sta aggiungendo un'animazione come primo parametro e `null` come secondo.  In questo modo, tutti i clock dell'animazione verranno rimossi dalla proprietà.  
  
 Per ulteriori informazioni sulle diverse modalità di aggiunta di un'animazione alle proprietà, vedere [Cenni preliminari sulle tecniche di animazione delle proprietà](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md).  
  
### Utilizzo di Compose HandoffBehavior con risorse di sistema  
 Quando si applica un oggetto <xref:System.Windows.Media.Animation.Storyboard>, <xref:System.Windows.Media.Animation.AnimationTimeline> o <xref:System.Windows.Media.Animation.AnimationClock> a una proprietà utilizzando l'oggetto <xref:System.Windows.Media.Animation.HandoffBehavior> <xref:System.Windows.Media.Animation.HandoffBehavior>, tutti gli oggetti <xref:System.Windows.Media.Animation.Clock> precedentemente associati a tale proprietà continueranno a utilizzare risorse di sistema; il sistema di temporizzazione non rimuoverà automaticamente questi clock.  
  
 Per evitare problemi di prestazioni quando si applica un gran numero di clock utilizzando <xref:System.Windows.Media.Animation.HandoffBehavior>, è necessario rimuovere i clock di composizione dalla proprietà animata una volta completati.  Esistono diverse modalità di rimozione di un clock.  
  
-   Per rimuovere tutti i clock da una proprietà, utilizzare il metodo <xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationClock%29> o <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29> dell'oggetto a cui è stata aggiunta un'animazione.  Specificare la proprietà a cui si sta aggiungendo un'animazione come primo parametro e `null` come secondo.  In questo modo, tutti i clock dell'animazione verranno rimossi dalla proprietà.  
  
-   Per rimuovere un oggetto <xref:System.Windows.Media.Animation.AnimationClock> specifico da un elenco di clock, utilizzare la proprietà <xref:System.Windows.Media.Animation.Clock.Controller%2A> dell'oggetto <xref:System.Windows.Media.Animation.AnimationClock> per recuperare un oggetto <xref:System.Windows.Media.Animation.ClockController>, quindi chiamare il metodo <xref:System.Windows.Media.Animation.ClockController.Remove%2A> di <xref:System.Windows.Media.Animation.ClockController>.  In genere, questa operazione viene eseguita nel gestore eventi dell'oggetto <xref:System.Windows.Media.Animation.Clock.Completed> per un orologio.  Notare che solo i clock radice possono essere controllati da un oggetto <xref:System.Windows.Media.Animation.ClockController>; la proprietà <xref:System.Windows.Media.Animation.Clock.Controller%2A> di un clock figlio restituirà `null`.  Notare, inoltre, che l'evento <xref:System.Windows.Media.Animation.Clock.Completed> non verrà chiamato se la durata effettiva del clock è infinita.  In quel caso, l'utente dovrà determinare il momento in cui chiamare <xref:System.Windows.Media.Animation.ClockController.Remove%2A>.  
  
 Si tratta principalmente di un problema relativo alle animazioni su oggetti di durata lunga.  Quando un oggetto viene raccolto nel Garbage Collector, anche i clock verranno disconnessi e raccolti nel Garbage Collector.  
  
 Per ulteriori informazioni sugli oggetti clock, vedere [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md).  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)