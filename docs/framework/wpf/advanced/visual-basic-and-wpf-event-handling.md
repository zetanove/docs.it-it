---
title: "Visual Basic e la gestione degli eventi WPF | Microsoft Docs"
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
  - "gestori eventi, Visual Basic"
  - "Visual Basic, gestori eventi"
ms.assetid: ad4eb9aa-3afc-4a71-8cf6-add3fbea54a1
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Visual Basic e la gestione degli eventi WPF
Nel caso specifico del linguaggio [!INCLUDE[TLA#tla_visualbnet](../../../../includes/tlasharptla-visualbnet-md.md)], è possibile utilizzare la parola chiave `Handles` specifica del linguaggio per associare gestori eventi alle istanze, anziché collegare i gestori eventi con gli attributi o utilizzare il metodo <xref:System.Windows.UIElement.AddHandler%2A>.  Tuttavia, la tecnica `Handles` per collegare gestori alle istanze presenta alcuni limiti, in quanto la sintassi `Handles` non è in grado di supportare alcune delle funzioni degli [eventi indirizzati](GTMT) specifiche del sistema di eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
## Utilizzo di "Handles" in un'applicazione WPF  
 I gestori eventi connessi a istanze ed eventi tramite `Handles` devono essere definiti tutti all'interno della dichiarazione di classe parziale dell'istanza; ciò vale anche per i gestori eventi assegnata tramite valori di attributo negli elementi.  È possibile specificare `Handles` soltanto per un elemento della pagina che presenti un valore di proprietà <xref:System.Windows.FrameworkContentElement.Name%2A> \(o per il quale sia dichiarato [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md)\).  Tale situazione si verifica in quanto <xref:System.Windows.FrameworkContentElement.Name%2A> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] crea il riferimento all'istanza che è necessario per supportare il formato di riferimento *Istanza.Evento* richiesto dalla sintassi `Handles`.  L'unico elemento che può essere utilizzato per `Handles` senza un riferimento <xref:System.Windows.FrameworkContentElement.Name%2A> è l'istanza dell'elemento radice che definisce la classe parziale.  
  
 È possibile assegnare lo stesso gestore a più elementi separando i riferimenti *Istanza.Evento* dopo `Handles` con delle virgole.  
  
 È possibile utilizzare `Handles` per assegnare più gestori allo stesso riferimento *Istanza.Evento*.  Non attribuire alcuna importanza all'ordine in cui vengono forniti i gestori nel riferimento `Handles`; è necessario presupporre che gestori dello stesso evento possono essere richiamati in qualsiasi ordine.  
  
 Per rimuovere un gestore aggiunto con `Handles` nella dichiarazione, è possibile chiamare <xref:System.Windows.UIElement.RemoveHandler%2A>.  
  
 È possibile utilizzare `Handles` per collegare i gestori per gli [eventi indirizzati](GTMT), purché i gestori vengano collegati a istanze che definiscono l'evento gestito nelle rispettive tabelle di membri.  Per gli [eventi indirizzati](GTMT), i gestori associati con `Handles` seguono le stesse regole di routing dei gestori associati come attributi [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o con la firma comune di <xref:System.Windows.UIElement.AddHandler%2A>.  Pertanto, se l'evento è già contrassegnato come gestito \(la proprietà <xref:System.Windows.RoutedEventArgs.Handled%2A> nei dati dell'evento è `True`\), i gestori associati con `Handles` non sono richiamati in risposta all'istanza di quell'evento.  L'evento potrebbe essere contrassegnato come gestito dai gestori dell'istanza in un altro elemento della route o dalla gestione delle classi nell'elemento corrente o negli elementi precedenti della route.  Per gli eventi di input che supportano eventi accoppiati di tunneling e di bubbling, è possibile che la route di tunneling abbia contrassegnato la coppia di eventi come gestita.  Per ulteriori informazioni sugli eventi indirizzati, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
## Limitazioni di "Handles" per l'aggiunta di gestori  
 `Handles` non può fare riferimento ai gestori per gli [eventi associati](GTMT).  È necessario utilizzare il metodo della funzione di accesso `add` per quello specifico evento associato oppure gli attributi dell'evento *nometipo.nomeevento* in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Per informazioni dettagliate, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 Per gli [eventi indirizzati](GTMT), è possibile utilizzare `Handles` unicamente per assegnare gestori per le istanze in cui quell'evento è presente nella tabella dei membri dell'istanza.  Tuttavia, con gli eventi indirizzati in generale, un elemento padre può essere un listener per un evento degli elementi figlio anche se l'elemento padre non dispone di quell'evento nella relativa tabella dei membri.  Nella sintassi dell'attributo, ciò può essere specificato tramite un formato di attributo *nometipo.nomemembro* che qualifica il tipo che definisce effettivamente l'evento che si desidera gestire.  Un elemento padre, ad esempio, `Page` \(senza alcun evento `Clic` definito\) può restare in ascolto degli eventi clic del pulsante assegnando un gestore attributi nel formato `Button.Click`.  Tuttavia, `Handles` non supporta il formato *nometipo.nomemembro*, in quanto deve supportare un formato *Istanza.Evento* in conflitto.  Per informazioni dettagliate, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 `Handles` non è in grado di associare gestori richiamati per eventi che sono già contrassegnati come gestiti.  Invece, è necessario utilizzare il codice e chiamare l'overload `handledEventsToo` di <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>.  
  
> [!NOTE]
>  Non utilizzare la sintassi `Handles` nel codice [!INCLUDE[vb_current_short](../../../../includes/vb-current-short-md.md)] quando si specifica un gestore eventi per il medesimo evento in XAML.  In questo caso, il gestore eventi viene chiamato due volte.  
  
## Modalità di implementazione della funzionalità "Handles" da parte di WPF  
 Quando viene compilata una pagina [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], il file intermedio dichiara riferimenti `Friend``WithEvents` a ogni elemento della pagina in cui sia impostata una proprietà <xref:System.Windows.FrameworkContentElement.Name%2A> \(o in cui sia dichiarato [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md)\).  Ogni istanza denominata è potenzialmente un elemento che può essere assegnato a un gestore tramite la funzionalità `Handles`.  
  
> [!NOTE]
>  All'interno di [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)], [!INCLUDE[TLA2#tla_intellisense](../../../../includes/tla2sharptla-intellisense-md.md)] è in grado di mostrare il completamento per il quale sono disponibili degli elementi per un riferimento `Handles` in una pagina.  Tuttavia, tale operazione potrebbe richedere un passaggio di compilazione che consenta al file intermedio di popolare tutti i riferimenti `Friends`.  
  
## Vedere anche  
 <xref:System.Windows.UIElement.AddHandler%2A>   
 [Contrassegno degli eventi indirizzati come gestiti e gestione delle classi](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)