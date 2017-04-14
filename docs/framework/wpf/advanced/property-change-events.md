---
title: "Eventi di modifica delle propriet&#224; | Microsoft Docs"
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
  - "eventi di modifica [WPF], proprietà"
  - "creazione di trigger di proprietà [WPF]"
  - "proprietà di dipendenza [WPF], eventi di modifica"
  - "eventi [WPF], modifica dei valori delle proprietà"
  - "identificazione di eventi di proprietà modificate [WPF]"
  - "eventi di modifica proprietà [WPF]"
  - "eventi di modifica proprietà [WPF], tipi"
  - "trigger di proprietà [WPF]"
  - "trigger di proprietà [WPF], definizione"
  - "modifiche dei valori di proprietà [WPF]"
ms.assetid: 0a7989df-9674-4cc1-bc50-5d8ef5d9c055
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Eventi di modifica delle propriet&#224;
In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] vengono definiti diversi eventi generati in risposta a una modifica nel valore di una proprietà.  Spesso la proprietà è una [proprietà di dipendenza](GTMT).  L'evento stesso è in alcuni casi un [evento indirizzato](GTMT) e in altri casi un evento [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] standard.  La definizione dell'evento varia a seconda dello scenario, poiché alcune modifiche delle proprietà sono inviate in modo ottimale tramite una struttura ad albero dell'elemento, mentre altre interessano in genere solo l'oggetto in cui viene modificata la proprietà.  
  
## Identificazione di un evento di modifica delle proprietà  
 Non tutti gli eventi che segnalano una modifica delle proprietà sono identificati in modo esplicito come eventi di modifica delle proprietà, per mezzo di un pattern di firma o di nome.  In genere, la descrizione dell'evento nella documentazione di [!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] indica se l'evento è direttamente collegato a una modifica del valore di una proprietà e fornisce riferimenti incrociati tra la proprietà e l'evento.  
  
### Eventi RoutedPropertyChanged  
 In alcuni eventi vengono utilizzati un tipo di dati di evento e un delegato utilizzati in modo esplicito per gli eventi di modifica delle proprietà.  Il tipo di dati di evento è <xref:System.Windows.RoutedPropertyChangedEventArgs%601> e il delegato è <xref:System.Windows.RoutedPropertyChangedEventHandler%601>.  I dati di evento e il delegato dispongono entrambi di un parametro di tipo generico utilizzato per specificare il tipo effettivo della proprietà modificata quando si definisce il gestore.  I dati di evento contengono due proprietà, <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A> e <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>, entrambe passate come argomento di tipo nei dati di evento.  
  
 Il termine "Routed" del nome indica che l'evento di proprietà modificata è registrato come evento indirizzato.  Il vantaggio che si ottiene nell'indirizzare un evento di proprietà modificata è dato dal fatto che il livello superiore di un controllo può ricevere eventi di proprietà modificata se vengono modificati i valori delle proprietà sugli elementi figlio \(parti composite del controllo\).  Ad esempio, è possibile creare un controllo che incorpora un controllo <xref:System.Windows.Controls.Primitives.RangeBase>, ad esempio <xref:System.Windows.Controls.Slider>.  Se il valore della proprietà <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> viene modificato sulla parte del dispositivo di scorrimento, è necessario gestire tale modifica sul controllo padre anziché sulla parte.  
  
 Poiché si dispone di un valore vecchio e di un valore nuovo, può sembrare opportuno utilizzare questo gestore eventi come validator per il valore della proprietà.  Tuttavia, questo utilizzo non rientra negli intenti di progettazione della maggior parte degli eventi di proprietà modificata.  In genere, i valori vengono forniti per consentire di eseguire azioni su di essi in altre aree logiche del codice, ma la modifica dei valori dall'interno del gestore eventi non è consigliabile e può causare ricorsione non intenzionale a seconda della modalità di implementazione del gestore.  
  
 Se la proprietà è una proprietà di dipendenza personalizzata o si sta utilizzando una classe derivata in cui è stato definito il codice di creazione di un'istanza, nel sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è incorporato un meccanismo più efficiente per tenere traccia delle modifiche delle proprietà, ovvero i callback del sistema di proprietà <xref:System.Windows.CoerceValueCallback> e <xref:System.Windows.PropertyChangedCallback>.  Per informazioni dettagliate sulla modalità di utilizzo del sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per la convalida e la coercizione, vedere [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md) e [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
### Eventi DependencyPropertyChanged  
 Un'altra coppia di tipi appartenente allo scenario degli eventi di proprietà modificata è costituita da <xref:System.Windows.DependencyPropertyChangedEventArgs> e <xref:System.Windows.DependencyPropertyChangedEventHandler>.  Gli eventi per queste modifiche delle proprietà non sono eventi indirizzati, bensì eventi di [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] standard.  <xref:System.Windows.DependencyPropertyChangedEventArgs> è un tipo di segnalazione dei dati di evento non consueto, poiché non deriva da <xref:System.EventArgs>. <xref:System.Windows.DependencyPropertyChangedEventArgs> è una struttura, non una classe.  
  
 Gli eventi che utilizzano <xref:System.Windows.DependencyPropertyChangedEventArgs> e <xref:System.Windows.DependencyPropertyChangedEventHandler> sono un po' più comuni degli eventi `RoutedPropertyChanged`.  Un esempio di evento che utilizza questi tipi è <xref:System.Windows.UIElement.IsMouseCapturedChanged>.  
  
 Come <xref:System.Windows.RoutedPropertyChangedEventArgs%601>, anche <xref:System.Windows.DependencyPropertyChangedEventArgs> riporta un valore vecchio e un valore nuovo per la proprietà.  Inoltre, a questo evento si applicano le stesse considerazioni relative all'utilizzo dei valori. In genere, è sconsigliabile tentare di modificare nuovamente i valori sul mittente in risposta all'evento.  
  
## Trigger di proprietà  
 Un concetto correlato strettamente a un evento di proprietà modificata è quello di trigger di proprietà.  Un trigger di proprietà viene creato all'interno di uno stile o di un modello e consente di creare un comportamento condizionale basato sul valore della proprietà a cui il trigger è assegnato.  
  
 La proprietà per un trigger di proprietà deve essere una proprietà di dipendenza.  Può trattarsi, come spesso accade, di una proprietà di dipendenza di sola lettura.  Un ottimo indicatore del fatto che una proprietà di dipendenza esposta da un controllo sia progettata almeno parzialmente come trigger di proprietà è la presenza del termine "Is" nel nome della proprietà.  Proprietà con questo nome sono spesso proprietà di dipendenza booleane di sola lettura il cui scenario primario è la segnalazione dello stato di un controllo che può avere conseguenze sull'interfaccia utente in tempo reale ed essere pertanto un candidato di trigger di proprietà.  
  
 Alcune di queste proprietà dispongono inoltre di un evento di proprietà modificata dedicato.  Ad esempio, la proprietà <xref:System.Windows.UIElement.IsMouseCaptured%2A> ha un evento di proprietà modificata <xref:System.Windows.UIElement.IsMouseCapturedChanged>.  La proprietà stessa è di sola lettura, con il relativo valore regolato dal sistema di input, e <xref:System.Windows.UIElement.IsMouseCapturedChanged> viene generato dal sistema di input a ogni modifica in tempo reale.  
  
 Rispetto a un evento di proprietà modificata effettivo, l'utilizzo di un trigger di proprietà per gestire una modifica di proprietà presenta alcune limitazioni.  
  
 I trigger di proprietà funzionano in base a una logica di corrispondenze esatte.  Vengono specificati una proprietà e un valore che indica il valore specifico per il quale interviene il trigger.  Ad esempio, `<Setter Property="IsMouseCaptured" Value="true"> ... </Setter>`.  A causa di questa limitazione, nella maggior parte dei casi i trigger di proprietà vengono utilizzati per le proprietà booleane, o proprietà che accettano un valore di enumerazione dedicato, in cui l'intervallo di valori possibili è sufficientemente gestibile per consentire la definizione di un trigger per ogni caso.  In alternativa, i trigger di proprietà possono essere utilizzati solo per valori speciali, ad esempio nel caso un conteggio di elementi raggiunga zero, senza trigger che tengano conto dei casi in cui il valore della proprietà viene modificato su un numero diverso da zero \(anziché disporre di trigger per tutti i casi, in questo caso potrebbe essere necessario un gestore eventi di codice o un comportamento predefinito per ripristinare lo stato del trigger quando il valore è diverso da zero\).  
  
 La sintassi del trigger di proprietà è analoga a un'istruzione "if" nella programmazione.  Se la condizione del trigger è true, viene eseguito il corpo del trigger di proprietà.  Il corpo di un trigger di proprietà non è codice, ma markup.  Tale markup è limitato all'utilizzo di uno o più elementi <xref:System.Windows.Setter> per impostare altre proprietà dell'oggetto a cui si applica lo stile o il modello.  
  
 Per compensare la condizione "if" di un trigger di proprietà con un'ampia varietà di valori possibili, è in genere consigliabile utilizzare un'impostazione predefinita per lo stesso valore di proprietà tramite <xref:System.Windows.Setter>.  In questo modo, il metodo di impostazione contenuto in <xref:System.Windows.Trigger> avrà la precedenza quando la condizione del trigger è true, mentre l'oggetto <xref:System.Windows.Setter> che non è all'interno di <xref:System.Windows.Trigger> avrà la precedenza ogni volta che la condizione del trigger è false.  
  
 I trigger di proprietà sono generalmente adatti negli scenari in cui una o più proprietà dell'aspetto devono essere modificate, in base allo stato di un'altra proprietà sullo stesso elemento.  
  
 Per ulteriori informazioni sui trigger di proprietà, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
## Vedere anche  
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)