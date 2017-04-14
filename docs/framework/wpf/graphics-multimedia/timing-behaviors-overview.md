---
title: "Cenni preliminari sui comportamenti temporali | Microsoft Docs"
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
  - "comportamenti, temporizzazione"
  - "comportamenti di temporizzazione"
ms.assetid: 5b714d46-bd46-48b8-b467-b4be89ba3091
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Cenni preliminari sui comportamenti temporali
In questo argomento vengono descritti i comportamenti temporali delle animazioni e di altri oggetti <xref:System.Windows.Media.Animation.Timeline>.  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## Prerequisiti  
 Per comprendere questo argomento, è necessario conoscere le funzionalità di base dell'animazione.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
<a name="timelinetypes"></a>   
## Tipi di sequenza temporale  
 Un oggetto <xref:System.Windows.Media.Animation.Timeline> rappresenta un intervallo di tempo.  Fornisce proprietà che consentono di specificare la lunghezza dell'intervallo, il momento di inizio, il numero di ripetizioni, la velocità di avanzamento dell'intervallo e così via.  
  
 Le classi che ereditano dalla classe della sequenza temporale offrono funzionalità aggiuntive, ad esempio la riproduzione di animazioni e contenuti multimediali.  In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili forniti i seguenti tipi di oggetto <xref:System.Windows.Media.Animation.Timeline>.  
  
|Tipo di sequenza temporale|Descrizione|  
|--------------------------------|-----------------|  
|<xref:System.Windows.Media.Animation.AnimationTimeline>|Classe base astratta per oggetti <xref:System.Windows.Media.Animation.Timeline> che generano valori di output per l'animazione delle proprietà.|  
|<xref:System.Windows.Media.MediaTimeline>|Genera output da un file multimediale.|  
|<xref:System.Windows.Media.Animation.ParallelTimeline>|Tipo di <xref:System.Windows.Media.Animation.TimelineGroup> che raggruppa e controlla oggetti <xref:System.Windows.Media.Animation.Timeline> figlio.|  
|<xref:System.Windows.Media.Animation.Storyboard>|Tipo di <xref:System.Windows.Media.Animation.ParallelTimeline> che fornisce informazioni di destinazione per gli oggetti Timeline che contiene.|  
|<xref:System.Windows.Media.Animation.Timeline>|Classe base astratta che definisce i comportamenti temporali.|  
|<xref:System.Windows.Media.Animation.TimelineGroup>|Classe astratta per oggetti <xref:System.Windows.Media.Animation.Timeline> che possono contenere altri oggetti <xref:System.Windows.Media.Animation.Timeline>.|  
  
<a name="propertiesthatcontroltimelinelength"></a>   
## Proprietà che controllano la lunghezza di una sequenza temporale  
 Un oggetto <xref:System.Windows.Media.Animation.Timeline> rappresenta un intervallo di tempo. La lunghezza di una sequenza temporale può essere descritta in modi diversi.  Nella tabella riportata di seguito vengono definiti vari termini per la descrizione della lunghezza di una sequenza temporale.  
  
|Termine|Descrizione|Proprietà||||  
|-------------|-----------------|---------------|-|-|-|  
|Durata semplice|Periodo di tempo impiegato da una sequenza temporale per compiere una sola iterazione in avanti.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>||||  
|Una ripetizione|Periodo di tempo impiegato da una sequenza temporale per essere riprodotta una volta e, se la proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> è true, per essere riprodotta una volta in senso inverso.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>||||  
|Periodo attivo|Periodo di tempo impiegato da una sequenza temporale per completare tutte le ripetizioni specificate dalla relativa proprietà <xref:System.Windows.Media.Animation.RepeatBehavior>.|<xref:System.Windows.Media.Animation.Timeline.Duration%2A>, <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>, <xref:System.Windows.Media.Animation.RepeatBehavior>||||  
  
<a name="duration"></a>   
### Proprietà Duration  
 Come accennato in precedenza, un oggetto Timeline rappresenta un intervallo di tempo.  La lunghezza di tale intervallo è determinata dalla proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> della sequenza temporale.  Quando una sequenza temporale raggiunge la fine della propria durata, la riproduzione viene interrotta.  Se la sequenza temporale ha sequenze temporali figlie, anche la loro riproduzione viene interrotta.  Nel caso di un'animazione, la proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> specifica il tempo impiegato dall'animazione per la transizione dal valore iniziale a quello finale.  In alcuni casi, la durata di una sequenza temporale è detta *durata semplice*, per distinguere tra la durata di una singola iterazione e il periodo di tempo totale impiegato dalla riproduzione dell'animazione, incluse le ripetizioni.  È possibile specificare una durata utilizzando un valore temporale finito o il valore speciale <xref:System.Windows.Duration.Automatic%2A> o <xref:System.Windows.Duration.Forever%2A>.  La durata di un'animazione deve restituire un valore <xref:System.Windows.Duration.TimeSpan%2A>, in modo da poter eseguire la transizione tra valori.  
  
 Nell'esempio riportato di seguito viene illustrato un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> con una proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> di cinque secondi.  
  
  
  
 Le sequenze temporali del contenitore, ad esempio <xref:System.Windows.Media.Animation.Storyboard> e <xref:System.Windows.Media.Animation.ParallelTimeline>, hanno una durata predefinita di <xref:System.Windows.Duration.Automatic%2A>, che implica che tali sequenze temporali terminano automaticamente quando viene interrotta la riproduzione dell'ultima sequenza figlio.  Nell'esempio riportato di seguito viene illustrato un oggetto <xref:System.Windows.Media.Animation.Storyboard> la cui proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> restituisce cinque secondi, il periodo di tempo richiesto per il completamento di tutti gli oggetti <xref:System.Windows.Media.Animation.DoubleAnimation> figlio.  
  
  
  
 L'impostazione della proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> di una sequenza temporale contenitore su un valore <xref:System.Windows.Duration.TimeSpan%2A> consente di imporre una riproduzione più lunga o più breve rispetto a quella degli oggetti <xref:System.Windows.Media.Animation.Timeline> figlio.  Se si imposta <xref:System.Windows.Media.Animation.Timeline.Duration%2A> su un valore inferiore alla lunghezza degli oggetti <xref:System.Windows.Media.Animation.Timeline> figlio della sequenza temporale contenitore, la riproduzione degli oggetti <xref:System.Windows.Media.Animation.Timeline> figlio viene interrotta al termine della sequenza temporale contenitore.  Nell'esempio riportato di seguito viene impostata su tre secondi la proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> dell'oggetto <xref:System.Windows.Media.Animation.Storyboard> degli esempi precedenti.  Di conseguenza, l'avanzamento del primo oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene interrotto dopo tre secondi, quando è stata eseguita l'animazione della larghezza del rettangolo di destinazione per un valore pari a 60.  
  
  
  
<a name="repeatinganimations"></a>   
### Proprietà RepeatBehavior  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> determina il numero di ripetizioni della durata semplice di una sequenza temporale.  Utilizzando la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>, è possibile specificare il numero di volte in cui la sequenza temporale viene riprodotta \(proprietà <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> di iterazione\) oppure il periodo di tempo totale di esecuzione \(proprietà <xref:System.Windows.Media.Animation.RepeatBehavior.Duration%2A> di ripetizione\).  In entrambi i casi, l'animazione viene eseguita dall'inizio alla fine per il numero di volte necessario per completare il conteggio o la durata richiesta.  Per impostazione predefinita, le sequenze temporali presentano un conteggio di iterazioni pari a `1.0`, il che significa che vengono riprodotte una sola volta senza ripetizioni.  
  
 Nell'esempio riportato di seguito viene utilizzata la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> per riprodurre due volte la durata semplice di un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> specificando un conteggio di iterazioni.  
  
  
  
 Nell'esempio successivo viene utilizzata la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> per riprodurre l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> per metà della relativa durata semplice.  
  
  
  
 L'impostazione della proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> su <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A> determina la ripetizione di <xref:System.Windows.Media.Animation.Timeline> finché non viene interrotto in modo interattivo o da parte del sistema di temporizzazione.  Nell'esempio riportato di seguito viene utilizzata la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> per riprodurre <xref:System.Windows.Media.Animation.DoubleAnimation> in modo illimitato.  
  
  
  
 Per un altro esempio, vedere [Ripetere un'animazione](../../../../docs/framework/wpf/graphics-multimedia/how-to-repeat-an-animation.md).  
  
<a name="autoreverseproperty"></a>   
### Proprietà AutoReverse  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> specifica se un oggetto <xref:System.Windows.Media.Animation.Timeline> verrà riprodotto in senso inverso alla fine di ogni iterazione in avanti.  Nell'esempio riportato di seguito la proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> di un oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene impostata su `true`; di conseguenza l'oggetto viene animato da zero a 100 e, successivamente, da 100 a zero.  La riproduzione ha una durata totale di 10 secondi.  
  
  
  
 Quando si utilizza un valore <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> per specificare la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> di un oggetto <xref:System.Windows.Media.Animation.Timeline> e la proprietà <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A> di <xref:System.Windows.Media.Animation.Timeline> è `true`, una sola ripetizione è costituita da un'iterazione in avanti seguita da un'iterazione in senso inverso.  Nell'esempio riportato di seguito la proprietà <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> dell'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> dell'esempio precedente viene impostata su una proprietà <xref:System.Windows.Media.Animation.RepeatBehavior.Count%2A> pari a due.  Di conseguenza, l'oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene riprodotto per 20 secondi: in avanti per cinque secondi, in senso inverso per cinque secondi, nuovamente in avanti per cinque secondi, quindi in senso inverso per cinque secondi.  
  
  
  
 Se una sequenza temporale contenitore ha oggetti <xref:System.Windows.Media.Animation.Timeline> figlio, questi vengono invertiti in corrispondenza dell'inversione della sequenza temporale contenitore.  Per ulteriori esempi, vedere [Specificare se una sequenza temporale viene invertita automaticamente](../../../../docs/framework/wpf/graphics-multimedia/how-to-specify-whether-a-timeline-automatically-reverses.md).  
  
<a name="timelinebegin"></a>   
## Proprietà BeginTime  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> consente di specificare il momento di avvio di una sequenza temporale.  Il momento di avvio di una sequenza temporale è relativo alla sequenza temporale padre.  Un momento di avvio pari a zero secondi indica che la sequenza temporale viene avviata all'avvio della sequenza padre. Qualsiasi altro valore crea un offset tra il momento di avvio della riproduzione della sequenza temporale padre e quello della sequenza temporale figlio.  Ad esempio, un momento di avvio di due secondi indica che la riproduzione della sequenza temporale viene avviata quando la sequenza temporale padre ha raggiunto un valore di due secondi.  Per impostazione predefinita, il momento di avvio di tutte le sequenze temporali è pari a zero secondi.  È inoltre possibile impostare il momento di avvio di una sequenza temporale su `null`, per impedire l'avvio della sequenza temporale.  In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], specificare null tramite l'[Estensione del markup x:Null](../../../../docs/framework/xaml-services/x-null-markup-extension.md).  
  
 Si noti che il momento di avvio non viene applicato a ogni ripetizione di una sequenza temporale a causa dell'impostazione di <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>.  Se si crea un'animazione con una proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> pari a 10 secondi e un oggetto <xref:System.Windows.Media.Animation.RepeatBehavior> di <xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>, si ha un ritardo di 10 secondi prima della prima riproduzione dell'animazione, ma non a ogni successiva ripetizione.  Tuttavia, se la sequenza temporale padre dell'animazione venisse riavviata o ripetuta, verrebbe applicato il ritardo di 10 secondi.  
  
 La proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> è utile per scaglionare le sequenze temporali.  Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Media.Animation.Storyboard> con due oggetti <xref:System.Windows.Media.Animation.DoubleAnimation> figlio.  La proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> della prima animazione è pari a cinque secondi, mentre la proprietà <xref:System.Windows.Media.Animation.Timeline.Duration%2A> della seconda è pari a tre secondi.  Nell'esempio la proprietà <xref:System.Windows.Media.Animation.Timeline.BeginTime%2A> del secondo oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene impostata su cinque secondi, per consentire l'avvio della riproduzione alla fine di quella del primo oggetto <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
  
  
<a name="fillbehaviorproperty"></a>   
## Proprietà FillBehavior  
 Quando un oggetto <xref:System.Windows.Media.Animation.Timeline> raggiunge la fine della durata attiva totale, la proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> specifica se tale oggetto viene interrotto o se mantiene l'ultimo valore.  Un'animazione con una proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> pari a <xref:System.Windows.Media.Animation.FillBehavior> mantiene il valore di output, ovvero la proprietà animata conserva l'ultimo valore dell'animazione.  Con un valore pari a <xref:System.Windows.Media.Animation.FillBehavior> viene interrotto l'effetto dell'animazione sulla proprietà di destinazione al termine della riproduzione.  
  
 Nell'esempio riportato di seguito viene creato un oggetto <xref:System.Windows.Media.Animation.Storyboard> con due oggetti <xref:System.Windows.Media.Animation.DoubleAnimation> figlio.  Entrambi gli oggetti <xref:System.Windows.Media.Animation.DoubleAnimation> animano la proprietà <xref:System.Windows.FrameworkElement.Width%2A> di un oggetto <xref:System.Windows.Shapes.Rectangle> da 0 a 100.  Gli elementi <xref:System.Windows.Shapes.Rectangle> hanno valori <xref:System.Windows.FrameworkElement.Width%2A> non animati pari a 500 [pixel indipendenti dal dispositivo](GTMT).  
  
-   La proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> del primo oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene impostata su <xref:System.Windows.Media.Animation.FillBehavior>, ovvero sul valore predefinito.  Di conseguenza, la larghezza del rettangolo mantiene il valore di 100 al termine della riproduzione di <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
-   La proprietà <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A> del secondo oggetto <xref:System.Windows.Media.Animation.DoubleAnimation> viene impostata su <xref:System.Windows.Media.Animation.FillBehavior>.  Di conseguenza, la proprietà <xref:System.Windows.FrameworkElement.Width%2A> del secondo oggetto <xref:System.Windows.Shapes.Rectangle> ritorna a 500 al termine della riproduzione di <xref:System.Windows.Media.Animation.DoubleAnimation>.  
  
  
  
<a name="speedproperties"></a>   
## Proprietà che controllano la velocità di una sequenza temporale  
 La classe <xref:System.Windows.Media.Animation.Timeline> fornisce tre proprietà per la specifica della velocità:  
  
-   <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A>: specifica la velocità, relativa alla sequenza padre, alla quale avanza il tempo per un oggetto <xref:System.Windows.Media.Animation.Timeline>.  I valori superiori a uno aumentano la velocità di <xref:System.Windows.Media.Animation.Timeline> e dei relativi oggetti <xref:System.Windows.Media.Animation.Timeline> figlio, mentre i valori compresi tra zero e uno la rallentano.  Un valore pari a uno indica che <xref:System.Windows.Media.Animation.Timeline> avanza alla stessa velocità della sequenza padre.  L'impostazione di <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> per una sequenza temporale contenitore ha effetto anche su tutti i relativi oggetti <xref:System.Windows.Media.Animation.Timeline> figlio.  
  
-   <xref:System.Windows.Media.Animation.Timeline.AccelerationRatio%2A>: specifica la percentuale di <xref:System.Windows.Media.Animation.Timeline.Duration%2A> impiegata da una sequenza temporale per l'accelerazione.  Per un esempio, vedere [Accelerare o decelerare un'animazione](../../../../docs/framework/wpf/graphics-multimedia/how-to-accelerate-or-decelerate-an-animation.md).  
  
-   <xref:System.Windows.Media.Animation.Timeline.DecelerationRatio%2A>: specifica la percentuale di <xref:System.Windows.Media.Animation.Timeline.Duration%2A> impiegata da una sequenza temporale per la decelerazione.  Per un esempio, vedere [Accelerare o decelerare un'animazione](../../../../docs/framework/wpf/graphics-multimedia/how-to-accelerate-or-decelerate-an-animation.md).  
  
## Vedere anche  
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)   
 [Cenni preliminari sull'animazione e sul sistema di temporizzazione](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-system-overview.md)   
 [Cenni preliminari sugli eventi di tempo](../../../../docs/framework/wpf/graphics-multimedia/timing-events-overview.md)   
 [Procedure relative](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)   
 [Esempio di comportamento temporale di un'animazione](http://go.microsoft.com/fwlink/?LinkID=159970)