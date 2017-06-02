---
title: "Eventi di durata degli oggetti | Microsoft Docs"
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
  - "Activated (eventi)"
  - "Application (oggetti), eventi durata"
  - "classi, Frame"
  - "classi, NavigationWindow"
  - "Closed (eventi)"
  - "Closing (eventi)"
  - "ContentRendered (eventi)"
  - "Deactivated (eventi)"
  - "eventi, Activated"
  - "eventi, Chiuso"
  - "eventi, Closing"
  - "eventi, ContentRendered"
  - "eventi, Deactivated"
  - "eventi, Inizializzato"
  - "eventi, Caricato"
  - "eventi, Scaricato"
  - "eventi di uscita"
  - "Frame (classe)"
  - "Initialized (evento)"
  - "eventi durata degli oggetti"
  - "Loaded (eventi)"
  - "NavigationWindow (classe)"
  - "eventi durata degli oggetti"
  - "eventi di avvio"
  - "Unloaded (eventi)"
ms.assetid: face6fc7-465b-4502-bfe5-e88d2e729a78
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Eventi di durata degli oggetti
In questo argomento vengono descritti gli eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] specifici che denotano le fasi della durata di un oggetto in termini di creazione, utilizzo e distruzione.  
  
   
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la conoscenza delle [proprietà di dipendenza](GTMT) dal punto di vista di un consumer di proprietà di dipendenza esistenti nelle classi [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], nonché la lettura dell'argomento [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Per seguire gli esempi illustrati in questo argomento, è necessaria inoltre la comprensione di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] \(vedere [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)\) e della modalità di scrittura delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="intro"></a>   
## Eventi di durata degli oggetti  
 Tutti gli oggetti nel codice gestito [!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] attraversano un insieme simile di fasi di vita, creazione, utilizzo e distruzione.  Per molti oggetti la fase di finalizzazione della vita si verifica come parte della fase di distruzione.  Gli oggetti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], più specificamente gli oggetti visivi che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] identifica come elementi, hanno una serie comune di fasi di vita dell'oggetto.  I modelli di programmazione e applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] espongono queste fasi come una serie di eventi.  Esistono quattro tipi principali di oggetti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in relazione agli eventi di durata: gli elementi in generale, gli elementi finestra, gli host di navigazione e gli oggetti applicazione.  Le finestre e gli host di navigazione fanno parte anche del più ampio raggruppamento di oggetti visivi \(elementi\).  In questo argomento vengono descritti gli eventi di durata che sono comuni a tutti gli elementi; vengono quindi introdotti quelli più specifici che si applicano alle definizioni dell'applicazione, alle finestre o agli host di navigazione.  
  
<a name="common_events"></a>   
## Eventi di durata comuni degli elementi  
 Tutti gli elementi a [livello di framework WPF](GTMT) \(ossia gli oggetti derivanti da <xref:System.Windows.FrameworkElement> o da <xref:System.Windows.FrameworkContentElement>\) hanno in comune tre eventi di durata: <xref:System.Windows.FrameworkElement.Initialized>, <xref:System.Windows.FrameworkElement.Loaded> e <xref:System.Windows.FrameworkElement.Unloaded>.  
  
### Initialized  
 <xref:System.Windows.FrameworkElement.Initialized> viene generato per primo e corrisponde approssimativamente all'inizializzazione dell'oggetto tramite la chiamata al relativo costruttore.  Poiché l'evento si verifica in seguito all'inizializzazione, si garantisce che tutte le proprietà dell'oggetto siano impostate.  Un'eccezione può verificarsi nei casi di utilizzo di espressioni quali risorse dinamiche o associazioni; queste saranno espressioni non valutate. Come conseguenza del requisito che impone l'impostazione di tutte le proprietà, la sequenza di eventi <xref:System.Windows.FrameworkElement.Initialized> generata dagli elementi annidati definiti nel markup viene ordinata visualizzando prima gli elementi di livello più basso nella struttura ad albero dell'elemento e quindi gli elementi padre in direzione della radice.  Questo ordine è determinato dal fatto che le relazioni padre\-figlio e il contenimento sono proprietà e pertanto l'elemento padre non può segnalare l'inizializzazione finché tutti gli elementi figlio che riempiono la proprietà non sono stati completamente inizializzati.  
  
 Durante la scrittura dei gestori in risposta all'evento <xref:System.Windows.FrameworkElement.Initialized>, è necessario considerare che non esiste alcuna garanzia che siano stati creati tutti gli altri elementi della struttura ad albero dell'elemento \(o [albero logico](GTMT) o [struttura ad albero visuale](GTMT)\) nell'area in cui è associato il gestore, in particolare gli elementi padre.  Le variabili membro possono essere null oppure le origini dati potrebbero non essere ancora popolate dall'associazione sottostante \(anche al livello dell'espressione\).  
  
### Loaded  
 <xref:System.Windows.FrameworkElement.Loaded> viene generato successivamente.  L'evento <xref:System.Windows.FrameworkElement.Loaded> viene generato prima del rendering finale, ma dopo che il sistema di layout ha calcolato tutti i valori necessari per il rendering.  <xref:System.Windows.FrameworkElement.Loaded> comporta che l'albero logico all'interno del quale è contenuto un elemento sia completo e si connetta a un'origine della presentazione che fornisce HWND e la superficie di rendering.  L'associazione dati standard \(associazione alle origini locali, ad esempio le altre proprietà o le origini dati definite in modo diretto\) sarà stata eseguita prima di <xref:System.Windows.FrameworkElement.Loaded>.  È probabile che l'associazione dati asincrona \(a origini esterne o dinamiche\) si sia verificata, ma a causa della stessa natura asincrona non è possibile averne la certezza.  
  
 Il meccanismo mediante il quale viene generato l'evento <xref:System.Windows.FrameworkElement.Loaded> è diverso rispetto a <xref:System.Windows.FrameworkElement.Initialized>.  L'evento <xref:System.Windows.FrameworkElement.Initialized> viene generato un elemento per volta, senza una coordinazione diretta da parte di una struttura ad albero dell'elemento completata.  Al contrario, l'evento <xref:System.Windows.FrameworkElement.Loaded> viene generato come operazione coordinata attraverso l'intera struttura ad albero dell'elemento \(in particolare l'[albero logico](GTMT)\).  Quando tutti gli elementi della struttura ad albero si trovano in uno stato in cui sono considerati come caricati, l'evento <xref:System.Windows.FrameworkElement.Loaded> viene generato innanzitutto sull'elemento radice.  L'evento <xref:System.Windows.FrameworkElement.Loaded> viene quindi generato successivamente in ciascun elemento figlio.  
  
> [!NOTE]
>  Questo comportamento potrebbe in apparenza essere analogo al tunneling per un [evento indirizzato](GTMT).  Tuttavia, le informazioni non vengono passate da evento a evento.  Ogni elemento ha sempre la possibilità di gestire il relativo evento <xref:System.Windows.FrameworkElement.Loaded> e contrassegnando i dati degli eventi come gestiti non si avranno effetti al di là di quell'elemento.  
  
### Unloaded  
 <xref:System.Windows.FrameworkElement.Unloaded> viene generato per ultimo e avviato tramite l'origine della presentazione o dalla rimozione del padre visuale.  Quando <xref:System.Windows.FrameworkElement.Unloaded> viene generato e gestito, l'impostazione dell'elemento corrispondente al padre dell'origine dell'evento \(determinato dalla proprietà <xref:System.Windows.FrameworkElement.Parent%2A>\) o di qualsiasi elemento specificato in un livello alto della struttura ad albero logico o visuale potrebbe già essere stata annullata; pertanto è possibile che l'associazione dati, i riferimenti alle risorse e gli stili non siano impostati sul rispettivo valore di runtime normale o sull'ultimo valore noto.  
  
<a name="application_model_elements"></a>   
## Elementi del modello di applicazione di eventi di durata  
 In base agli eventi di durata comuni per gli elementi sono previsti i seguenti elementi del modello di applicazione: <xref:System.Windows.Application>, <xref:System.Windows.Window>, <xref:System.Windows.Controls.Page>, <xref:System.Windows.Navigation.NavigationWindow> e <xref:System.Windows.Controls.Frame>.  Questi estendono gli eventi di durata comuni con eventi aggiuntivi che sono pertinenti al relativo scopo specifico  e vengono descritti in dettaglio nelle seguenti sezioni:  
  
-   <xref:System.Windows.Application>: [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
-   <xref:System.Windows.Window>: [Cenni preliminari sulle finestre WPF](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md).  
  
-   <xref:System.Windows.Controls.Page>, <xref:System.Windows.Navigation.NavigationWindow> e <xref:System.Windows.Controls.Frame>: [Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md).  
  
## Vedere anche  
 [Precedenza del valore della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)