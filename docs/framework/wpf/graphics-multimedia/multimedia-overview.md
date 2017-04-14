---
title: "Panoramica delle funzionalit&#224; multimediali | Microsoft Docs"
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
  - "supporto"
  - "elementi multimediali"
ms.assetid: feb25b15-d741-4ac3-818f-1b19f63a3562
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Panoramica delle funzionalit&#224; multimediali
In questo argomento vengono introdotte le funzionalità multimediali in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], che consentono di integrare audio e video nelle applicazioni, in modo da migliorare l'esperienza utente.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="mediaapi"></a>   
## API multimediali  
 Le classi <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Media.MediaPlayer> sono utilizzate per presentare contenuto audio o video.  Queste classi possono essere controllate in modo interattivo oppure tramite un orologio.  È possibile utilizzare queste classi sul controllo [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 per la riproduzione di contenuti multimediali. La classe utilizzata dipende dallo scenario.  
  
 <xref:System.Windows.Controls.MediaElement> è una classe <xref:System.Windows.UIElement> supportata dal [Layout](../../../../docs/framework/wpf/advanced/layout.md) e può essere utilizzata in un gran numero di controlli.  È inoltre utilizzabile in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e nel codice. <xref:System.Windows.Media.MediaPlayer>, d'altra parte, è progettato per oggetti <xref:System.Windows.Media.Drawing> e non include il supporto del layout.  I contenuti multimediali caricati mediante <xref:System.Windows.Media.MediaPlayer> possono essere presentati unicamente utilizzando una classe <xref:System.Windows.Media.VideoDrawing> o tramite l'interazione diretta con una classe <xref:System.Windows.Media.DrawingContext>.  La classe <xref:System.Windows.Media.MediaPlayer> non può essere utilizzata in XAML.  
  
 Per ulteriori informazioni sugli oggetti e sul contesto di disegno, vedere [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md).  
  
> [!NOTE]
>  Quando si distribuiscono contenuti multimediali con l'applicazione, non è possibile utilizzare un file multimediale come risorsa di progetto.  Invece, è necessario impostare il tipo di contenuti multimediali su `Content` nel file del progetto e `CopyToOutputDirectory` su `PreserveNewest` o su `Always`.  
  
<a name="mediaplaybackmodes"></a>   
## Modalità di riproduzione di contenuti multimediali  
  
> [!NOTE]
>  <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Media.MediaPlayer> dispongono di membri simili.  I collegamenti di questa sezione si riferiscono ai membri della classe <xref:System.Windows.Controls.MediaElement>.  A meno che non sia indicato in modo specifico, i membri collegati nella classe <xref:System.Windows.Controls.MediaElement> sono reperibili anche nella classe <xref:System.Windows.Media.MediaPlayer>.  
  
 Per comprendere la riproduzione di contenuti multimediali in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], è necessario conoscere le diverse modalità che è possibile utilizzare per riprodurre questo tipo di contenuti.  <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Media.MediaPlayer> possono essere utilizzate entrambe in due modalità multimediali diverse, vale a dire la modalità indipendente e la modalità orologio.  La modalità multimediale è determinata dalla proprietà <xref:System.Windows.Controls.MediaElement.Clock%2A>.  Se la proprietà <xref:System.Windows.Controls.MediaElement.Clock%2A> è `null`, l'oggetto multimediale si trova nella modalità indipendente.  Se, invece, il valore della proprietà <xref:System.Windows.Controls.MediaElement.Clock%2A> è diverso da null, l'oggetto multimediale si trova nella modalità orologio.  Per impostazione predefinita, gli oggetti multimediali si trovano nella modalità indipendente.  
  
### Modalità indipendente  
 In modalità indipendente, la riproduzione dei contenuti multimediali dipende dai contenuti stessi.  Questa modalità consente le possibilità indicate di seguito:  
  
-   È possibile specificare direttamente l'<xref:System.Uri> dei contenuti multimediali.  
  
-   È possibile controllare direttamente la riproduzione dei contenuti multimediali.  
  
-   È possibile modificare le proprietà <xref:System.Windows.Controls.MediaElement.Position%2A> e <xref:System.Windows.Controls.MediaElement.SpeedRatio%2A> dei contenuti multimediali.  
  
 I contenuti multimediali vengono caricati impostando la proprietà <xref:System.Windows.Controls.MediaElement.Source%2A> dell'oggetto <xref:System.Windows.Controls.MediaElement> oppure chiamando il metodo <xref:System.Windows.Media.MediaPlayer.Open%2A>dell'oggetto <xref:System.Windows.Media.MediaPlayer>.  
  
 Per controllare la riproduzione di contenuti multimediali in modalità indipendente, è possibile utilizzare i metodi di controllo dell'oggetto multimediale.  I metodi di controllo disponibili sono <xref:System.Windows.Controls.MediaElement.Play%2A>, <xref:System.Windows.Controls.MediaElement.Pause%2A>, <xref:System.Windows.Controls.MediaElement.Close%2A> e <xref:System.Windows.Controls.MediaElement.Stop%2A>.  Per <xref:System.Windows.Controls.MediaElement>, il controllo interattivo mediante questi metodi è disponibile solo quando la proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> è impostata su <xref:System.Windows.Controls.MediaState>.  Questi metodi non sono disponibili quando l'oggetto multimediale è in modalità orologio.  
  
 Per un esempio della modalità indipendente, vedere [Controllare un oggetto MediaElement \(riproduzione, sospensione, interruzione, volume e velocità\)](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-play-pause-stop-volume-and-speed.md).  
  
### Modalità orologio  
 In modalità orologio, la riproduzione di contenuti multimediali dipende da una classe <xref:System.Windows.Media.MediaTimeline>.  La modalità orologio presenta le seguenti caratteristiche:  
  
-   L'<xref:System.Uri> dei contenuti multimediali è impostato in modo indiretto tramite una classe <xref:System.Windows.Media.MediaTimeline>.  
  
-   La riproduzione dei contenuti multimediali può essere controllata mediante l'orologio.  Non è possibile utilizzare i metodi di controllo dell'oggetto multimediale.  
  
-   I contenuti multimediali vengono caricati impostando la proprietà <xref:System.Windows.Media.MediaTimeline.Source%2A> di un oggetto <xref:System.Windows.Media.MediaTimeline>, creando l'orologio dalla sequenza temporale e assegnandolo all'oggetto multimediale.  I contenuti multimediali vengono inoltre caricati in questo modo quando una classe <xref:System.Windows.Media.MediaTimeline> all'interno di un oggetto <xref:System.Windows.Media.Animation.Storyboard> ha come destinazione <xref:System.Windows.Controls.MediaElement>.  
  
 Per controllare la riproduzione di contenuti multimediali in modalità orologio, è necessario utilizzare i metodi di controllo della classe <xref:System.Windows.Media.Animation.ClockController>.  Un oggetto <xref:System.Windows.Media.Animation.ClockController> si ottiene dalla proprietà <xref:System.Windows.Media.Animation.ClockController> della classe <xref:System.Windows.Media.MediaClock>.  Se si tenta di utilizzare i metodi di controllo di un oggetto <xref:System.Windows.Controls.MediaElement> o <xref:System.Windows.Media.MediaPlayer> in modalità orologio, verrà generata un'eccezione <xref:System.InvalidOperationException>.  
  
 Per ulteriori informazioni sugli orologi e sulle sequenze temporali, vedere la sezione [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Per un esempio della modalità orologio, vedere [Controllare un MediaElement utilizzando uno storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-control-a-mediaelement-by-using-a-storyboard.md).  
  
<a name="mediaelement"></a>   
## Classe MediaElement  
 Per aggiungere contenuti multimediali a un'applicazione è sufficiente aggiungere un controllo <xref:System.Windows.Controls.MediaElement> all'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] dell'applicazione e fornire un <xref:System.Uri> ai contenuti multimediali che si desidera includere.  Tutti i tipi di contenuti multimediali supportati da [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 10 sono supportati in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]. Nell'esempio seguente viene illustrato un utilizzo semplice di <xref:System.Windows.Controls.MediaElement> in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
 [!code-xml[MediaElement_snip#SimpleMediaElementUsageWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MediaElement_snip/CSharp/SimpleUsage.xaml#simplemediaelementusagewholepage)]  
  
 Nell'esempio, i contenuti multimediali vengono riprodotti automaticamente appena vengono caricati.  Al termine della riproduzione, i contenuti multimediali vengono chiusi e tutte le risorse multimediali rilasciate \(inclusa la memoria video\).  Quello appena descritto è il comportamento predefinito dell'oggetto <xref:System.Windows.Controls.MediaElement> ed è controllato dalle proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> e <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>.  
  
### Controllo di un oggetto MediaElement  
 Le proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> e <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> consentono di controllare il comportamento dell'oggetto <xref:System.Windows.Controls.MediaElement> rispettivamente quando la proprietà <xref:System.Windows.FrameworkElement.IsLoaded%2A> è `true` oppure `false`.  Le proprietà di <xref:System.Windows.Controls.MediaState> vengono impostate per influire sul comportamento della riproduzione dei contenuti multimediali.  Ad esempio, il valore predefinito della proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> è <xref:System.Windows.Controls.MediaState>, mentre il valore predefinito della proprietà <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> è <xref:System.Windows.Controls.MediaState>.  Ciò significa che non appena l'oggetto <xref:System.Windows.Controls.MediaElement> viene caricato e il [preroll](GTMT) è completo, la riproduzione dei contenuti multimediali ha inizio.  Al termine della riproduzione, i contenuti multimediali vengono chiusi e tutte le risorse multimediali rilasciate.  
  
 Le proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> e <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> non rappresentano l'unico modo per controllare la riproduzione dei contenuti multimediali.  In modalità orologio, l'oggetto <xref:System.Windows.Controls.MediaElement> può essere controllato dall'orologio oppure dai metodi di controllo interattivi, se la proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> è impostata su <xref:System.Windows.Controls.MediaState>.  La scelta tra i due metodi viene gestita dall'oggetto <xref:System.Windows.Controls.MediaElement> mediante la valutazione delle seguenti proprietà.  
  
1.  <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A>.  Disponibile quando vengono scaricati i contenuti multimediali.  In tal modo viene garantito che tutte le risorse multimediali siano rilasciate per impostazione predefinita, anche quando un oggetto <xref:System.Windows.Media.MediaClock> è associato all'oggetto <xref:System.Windows.Controls.MediaElement>.  
  
2.  <xref:System.Windows.Media.MediaClock>.  Disponibile quando i contenuti multimediali dispongono di una proprietà <xref:System.Windows.Controls.MediaElement.Clock%2A>.  Se i contenuti multimediali vengono scaricati, la proprietà <xref:System.Windows.Media.MediaClock> ha effetto solo se la proprietà <xref:System.Windows.Controls.MediaElement.UnloadedBehavior%2A> è impostata su <xref:System.Windows.Controls.MediaState>.  La modalità orologio esegue sempre l'override del comportamento caricato dell'oggetto <xref:System.Windows.Controls.MediaElement>.  
  
3.  <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A>.  Disponibile quando vengono caricati i contenuti multimediali.  
  
4.  Metodi di controllo interattivi.  Disponibili quando la proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> è impostata su <xref:System.Windows.Controls.MediaState>.  I metodi di controllo disponibili sono <xref:System.Windows.Controls.MediaElement.Play%2A>, <xref:System.Windows.Controls.MediaElement.Pause%2A>, <xref:System.Windows.Controls.MediaElement.Close%2A> e <xref:System.Windows.Controls.MediaElement.Stop%2A>.  
  
### Visualizzazione di un oggetto MediaElement  
 Per visualizzare un oggetto <xref:System.Windows.Controls.MediaElement>, è necessario disporre di contenuti di cui eseguire il rendering, le cui proprietà <xref:System.Windows.FrameworkElement.ActualWidth%2A> e <xref:System.Windows.FrameworkElement.ActualHeight%2A> siano impostate su zero fino a quando i contenuti non vengono caricati.  Per contenuti esclusivamente audio, il valore di queste proprietà è sempre zero.  Per contenuti video, una volta generato l'evento <xref:System.Windows.Controls.MediaElement.MediaOpened>, le proprietà <xref:System.Windows.FrameworkElement.ActualWidth%2A> e <xref:System.Windows.FrameworkElement.ActualHeight%2A> segnaleranno la dimensione dei contenuti multimediali caricati.  Pertanto, fino a quando i contenuti multimediali non vengono caricati, l'oggetto <xref:System.Windows.Controls.MediaElement> non occuperà alcuno spazio fisico nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)], a meno che non venga impostata la proprietà <xref:System.Windows.FrameworkElement.Width%2A> o <xref:System.Windows.FrameworkElement.Height%2A>.  
  
 Se le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A> vengono impostate, i contenuti multimediali occuperanno l'area destinata all'oggetto <xref:System.Windows.Controls.MediaElement>.  Per conservare le [proporzioni](GTMT) originali dei contenuti multimediali, è necessario impostare solo una tra le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>.  Se si impostano entrambe le proprietà <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.FrameworkElement.Height%2A>, il contenuto multimediale verrà presentato con una dimensione fissa, un comportamento che potrebbe non essere appropriato.  
  
 Per evitare questa situazione, [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] può effettuare il [preroll](GTMT) del contenuto multimediale.  Questa operazione viene eseguita impostando la proprietà <xref:System.Windows.Controls.MediaElement.LoadedBehavior%2A> su <xref:System.Windows.Controls.MediaState> oppure su <xref:System.Windows.Controls.MediaState>.  In uno stato <xref:System.Windows.Controls.MediaState> verrà effettuato il preroll del contenuto multimediale e verrà presentato il primo fotogramma.  In uno stato <xref:System.Windows.Controls.MediaState> verrà effettuato il [preroll](GTMT) del contenuto multimediale e verrà avviata la riproduzione.  
  
<a name="mediaplayer"></a>   
## Classe MediaPlayer  
 Mentre la classe <xref:System.Windows.Controls.MediaElement> è un elemento framework, la classe <xref:System.Windows.Media.MediaPlayer> è progettata per essere utilizzata negli oggetti <xref:System.Windows.Media.Drawing>.  Gli oggetti Drawing vengono utilizzati quando è possibile sacrificare le funzionalità a livello di framework per migliorare le prestazioni oppure se occorrono funzionalità <xref:System.Windows.Freezable>.  <xref:System.Windows.Media.MediaPlayer> consente di avvalersi di queste funzionalità e di fornire contenuti multimediali alle applicazioni.  Come <xref:System.Windows.Controls.MediaElement>, <xref:System.Windows.Media.MediaPlayer> può essere utilizzata in modalità indipendente oppure orologio, ma non dispone degli stati caricato e scaricato dell'oggetto <xref:System.Windows.Controls.MediaElement>.  In tal modo la complessità del controllo della riproduzione di <xref:System.Windows.Media.MediaPlayer> viene ridotta.  
  
### Controllo di un oggetto MediaPlayer  
 Dal momento che <xref:System.Windows.Media.MediaPlayer> non dispone di stati, esistono solo due modi per controllare la riproduzione dei contenuti multimediali.  
  
1.  Metodi di controllo interattivi.  Disponibili nella modalità indipendente \(proprietà `null` <xref:System.Windows.Media.MediaPlayer.Clock%2A>\).  
  
2.  <xref:System.Windows.Media.MediaClock>.  Disponibile quando i contenuti multimediali dispongono di una proprietà <xref:System.Windows.Media.MediaPlayer.Clock%2A>.  
  
### Visualizzazione di un oggetto MediaPlayer  
 Da un punto di vista tecnico, è impossibile visualizzare un oggetto <xref:System.Windows.Media.MediaPlayer>, in quanto non dispone di una rappresentazione fisica.  Tuttavia, tale oggetto può essere utilizzato per presentare contenuti multimediali in un oggetto <xref:System.Windows.Media.Drawing> mediante la classe <xref:System.Windows.Media.VideoDrawing>.  Nell'esempio riportato di seguito viene illustrato l'utilizzo di una classe <xref:System.Windows.Media.VideoDrawing> per la visualizzazione di contenuti multimediali.  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 Per ulteriori informazioni sugli oggetti <xref:System.Windows.Media.Drawing>, vedere [Cenni preliminari sugli oggetti Drawing](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md).  
  
## Vedere anche  
 <xref:System.Windows.Media.DrawingGroup>   
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/audio-and-video-how-to-topics.md)