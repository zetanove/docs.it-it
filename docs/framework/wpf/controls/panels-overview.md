---
title: "Cenni preliminari sugli elementi Panel | Microsoft Docs"
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
  - "controlli, Pannello"
  - "Panel (controllo) [WPF], informazioni"
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
caps.latest.revision: 48
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 45
---
# Cenni preliminari sugli elementi Panel
Gli elementi <xref:System.Windows.Controls.Panel> sono componenti che controllano il rendering degli elementi, vale a dire le dimensioni, la posizione e la disposizione del contenuto figlio.  In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene fornita una serie di elementi <xref:System.Windows.Controls.Panel> predefiniti, nonché la possibilità di costruire elementi <xref:System.Windows.Controls.Panel> personalizzati.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento.  
  
-   [La classe Panel](#Panels_view_from_10000_feet)  
  
-   [Membri comuni alla classe Panel](#Panels_declared_members)  
  
-   [Elementi Panel derivati](#Panels_derived_elements)  
  
-   [Elementi Panel dell'interfaccia utente](#Panels_main_UI_elements)  
  
-   [Elementi Panel annidati](#Panels_nested_panel_elements)  
  
-   [Elementi Panel personalizzati](#Panels_custom_panel_elements)  
  
-   [Supporto di localizzazione\/globalizzazione](#Panels_global_localization)  
  
-   [Argomenti correlati](#seeAlsoToggle)  
  
<a name="Panels_view_from_10000_feet"></a>   
## La classe Panel  
 <xref:System.Windows.Controls.Panel> è la classe base per tutti gli elementi che forniscono un supporto layout in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  Gli elementi <xref:System.Windows.Controls.Panel> derivati vengono utilizzati per posizionare e disporre elementi in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] e nel codice.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] include un insieme completo di implementazioni Panel derivate che abilitano numerosi layout complessi.  Tali classi derivate espongono proprietà e metodi che abilitano la maggior parte degli scenari [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] standard.  Gli sviluppatori che non riescono a trovare un comportamento di disposizione degli elementi figlio adatto alle loro esigenze possono creare nuovi layout eseguendo l'override dei metodi <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> e <xref:System.Windows.FrameworkElement.MeasureOverride%2A>.  Per ulteriori informazioni sui comportamenti di layout personalizzati, vedere [Elementi Panel personalizzati](#Panels_custom_panel_elements).  
  
<a name="Panels_declared_members"></a>   
## Membri comuni alla classe Panel  
 Tutti gli elementi <xref:System.Windows.Controls.Panel> supportano le proprietà di ridimensionamento e posizionamento di base definite in <xref:System.Windows.FrameworkElement>, incluse <xref:System.Windows.FrameworkElement.Height%2A>, <xref:System.Windows.FrameworkElement.Width%2A>, <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A> e <xref:System.Windows.FrameworkElement.LayoutTransform%2A>.  Per ulteriori informazioni sulle proprietà di posizionamento definite in <xref:System.Windows.FrameworkElement>, vedere [Panoramica su allineamento, margini e spaziatura interna](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md).  
  
 <xref:System.Windows.Controls.Panel> espone delle proprietà aggiuntive di importanza cruciale per la comprensione e l'utilizzo del layout.  La proprietà <xref:System.Windows.Controls.Panel.Background%2A> viene utilizzata per riempire l'area compresa all'interno dei limiti di un elemento Panel derivato con <xref:System.Windows.Media.Brush>.  <xref:System.Windows.Controls.Panel.Children%2A> rappresenta la raccolta di elementi figlio di cui è composto l'elemento <xref:System.Windows.Controls.Panel>.  <xref:System.Windows.Controls.Panel.InternalChildren%2A> rappresenta il contenuto della raccolta <xref:System.Windows.Controls.Panel.Children%2A>, più i membri generati dall'associazione dati.  Entrambi sono costituiti da un oggetto <xref:System.Windows.Controls.UIElementCollection> di elementi figlio ospitati all'interno dell'elemento <xref:System.Windows.Controls.Panel> padre.  
  
 Panel espone inoltre una proprietà associata <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> che può essere utilizzata per ottenere un ordine stratificato in un elemento <xref:System.Windows.Controls.Panel> derivato.  I membri di una raccolta <xref:System.Windows.Controls.Panel.Children%2A> Panel con un valore di <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> più elevato vengono posizionati prima di quelli con un valore di <xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> minore.  Si tratta di una proprietà particolarmente utile per elementi Panel quali <xref:System.Windows.Controls.Canvas> e <xref:System.Windows.Controls.Grid>, che consentono agli elementi figlio di condividere lo spazio delle coordinate.  
  
 <xref:System.Windows.Controls.Panel> definisce inoltre il metodo <xref:System.Windows.Controls.Panel.OnRender%2A>, che consente di eseguire l'override del comportamento di presentazione predefinito di un elemento <xref:System.Windows.Controls.Panel>.  
  
#### Proprietà associate  
 Gli elementi Panel derivati utilizzano in modo diffuso le [proprietà associate](GTMT).  Una proprietà associata è un tipo specializzato di [proprietà di dipendenza](GTMT) che non dispone della proprietà "wrapper" [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] convenzionale.  Le proprietà associate presentano una sintassi specializzata in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)], illustrata in molti degli esempi seguenti.  
  
 Una delle funzioni di una proprietà associata consiste nel consentire agli elementi figlio di archiviare valori univoci di una proprietà definita da un elemento padre.  Dall'applicazione di questa funzionalità consegue che gli elementi figlio comunicano all'elemento padre il modo in cui devono essere presentati nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]. Questa operazione risulta estremamente utile per il layout dell'applicazione.  Per ulteriori informazioni, vedere [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
<a name="Panels_derived_elements"></a>   
## Elementi Panel derivati  
 Molti oggetti sono derivati da <xref:System.Windows.Controls.Panel>, ma non tutti vengono utilizzati come provider di layout radice.  Esistono sei classi Panel definite \(<xref:System.Windows.Controls.Canvas>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.VirtualizingStackPanel> e <xref:System.Windows.Controls.WrapPanel>\), progettate specificamente per la creazione dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dell'applicazione.  
  
 Ciascun elemento Panel incapsula la propria particolare funzionalità, come mostrato nella seguente tabella.  
  
|Nome elemento|Panel dell'interfaccia utente?|Descrizione|  
|-------------------|------------------------------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|Sì|Definisce un'area nella quale è possibile posizionare in modo esplicito gli elementi figlio utilizzando coordinate relative all'area <xref:System.Windows.Controls.Canvas>.|  
|<xref:System.Windows.Controls.DockPanel>|Sì|Definisce un'area all'interno della quale è possibile disporre gli elementi figlio orizzontalmente o verticalmente l'uno rispetto all'altro.|  
|<xref:System.Windows.Controls.Grid>|Sì|Definisce un'area flessibile della griglia costituita da colonne e righe.  Gli elementi figlio di <xref:System.Windows.Controls.Grid> possono essere posizionati con precisione utilizzando la proprietà <xref:System.Windows.FrameworkElement.Margin%2A>.|  
|<xref:System.Windows.Controls.StackPanel>|Sì|Dispone gli elementi figlio in una singola riga che può essere orientata orizzontalmente o verticalmente.|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|No|Gestisce il layout dei pulsanti scheda di un oggetto <xref:System.Windows.Controls.TabControl>.|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|No|Dispone il contenuto all'interno di un controllo <xref:System.Windows.Controls.ToolBar>.|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|No|<xref:System.Windows.Controls.Primitives.UniformGrid> viene utilizzato per disporre gli elementi figlio in una griglia con tutte le celle di uguali dimensioni.|  
|<xref:System.Windows.Controls.VirtualizingPanel>|No|Fornisce una classe base per gli elementi Panel in grado di "virtualizzare" la relativa raccolta di elementi figlio.|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|Sì|Dispone e virtualizza il contenuto su una singola riga orientata orizzontalmente o verticalmente.|  
|<xref:System.Windows.Controls.WrapPanel>|Sì|<xref:System.Windows.Controls.WrapPanel> posiziona gli elementi figlio in sequenza da sinistra verso destra, interrompendo il contenuto quando viene raggiunto il bordo della casella contenitore e facendolo ripartire dalla riga successiva.  Successivamente l'ordinamento in sequenza procede dall’alto verso il basso o da destra verso sinistra, a seconda del valore della proprietà <xref:System.Windows.Controls.WrapPanel.Orientation%2A>.|  
  
<a name="Panels_main_UI_elements"></a>   
## Elementi Panel dell'interfaccia utente  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili sei classi Panel ottimizzate per supportare gli scenari dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]: <xref:System.Windows.Controls.Canvas>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.VirtualizingStackPanel> e <xref:System.Windows.Controls.WrapPanel>.  Questi elementi Panel sono semplici da utilizzare, versatili ed estendibili per la maggior parte delle applicazioni.  
  
 Ciascun elemento <xref:System.Windows.Controls.Panel> considera i vincoli di ridimensionamento in modo diverso.  La comprensione della modalità con cui un elemento <xref:System.Windows.Controls.Panel> gestisce i vincoli in direzione sia verticale, sia orizzontale consente di prevedere con più precisione il layout.  
  
|**Nome elemento Panel**|**Dimensione x**|**Dimensione y**|  
|-----------------------------|----------------------|----------------------|  
|<xref:System.Windows.Controls.Canvas>|Vincolato al contenuto|Vincolato al contenuto|  
|<xref:System.Windows.Controls.DockPanel>|Vincolato|Vincolato|  
|<xref:System.Windows.Controls.StackPanel> \(con orientamento verticale\)|Vincolato|Vincolato al contenuto|  
|<xref:System.Windows.Controls.StackPanel> \(con orientamento orizzontale\)|Vincolato al contenuto|Vincolato|  
|<xref:System.Windows.Controls.Grid>|Vincolato|Vincolato, ad eccezione dei casi in cui si applica <xref:System.Windows.GridUnitType> a righe e colonne|  
|<xref:System.Windows.Controls.WrapPanel>|Vincolato al contenuto|Vincolato al contenuto|  
  
 Di seguito vengono riportate descrizioni più dettagliate ed esempi di utilizzo di questi elementi.  
  
<a name="Panels_overview_Canvas_subsection"></a>   
### Controllo Canvas  
 L'elemento <xref:System.Windows.Controls.Canvas> consente il posizionamento del contenuto in base a coordinate *x* e *y* assolute.  Gli elementi possono essere disegnati in una posizione univoca oppure, se occupano le stesse coordinate, l'ordine in cui verranno disegnati sarà determinato in base all'ordine di visualizzazione nel markup.  
  
 <xref:System.Windows.Controls.Canvas> fornisce il supporto di layout più flessibile rispetto a qualsiasi altro elemento <xref:System.Windows.Controls.Panel>.  Le proprietà Height e Width vengono utilizzate per definire l'area dell'elemento Canvas e agli elementi inclusi vengono assegnate coordinate in relazione all'area dell'elemento <xref:System.Windows.Controls.Canvas> padre.  Quattro proprietà associate, <xref:System.Windows.Controls.Canvas.Left%2A?displayProperty=fullName>, <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=fullName>, <xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=fullName> e <xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=fullName>, consentono un controllo accurato sul posizionamento all'interno dell'elemento <xref:System.Windows.Controls.Canvas>; in tal modo, lo sviluppatore può posizionare e disporre gli elementi sullo schermo in maniera precisa.  
  
#### La proprietà ClipToBounds di un oggetto Canvas  
 Con <xref:System.Windows.Controls.Canvas> è possibile posizionare gli elementi figlio in qualsiasi punto dello schermo, perfino in corrispondenza di coordinate esterne alle relative proprietà<xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> definite.  Inoltre, le dimensioni degli elementi figlio non influiscono su<xref:System.Windows.Controls.Canvas>.  Pertanto, è possibile che un elemento figlio estenda altri elementi all'esterno del rettangolo di delimitazione dell'elemento <xref:System.Windows.Controls.Canvas> padre.  Il comportamento predefinito di un elemento <xref:System.Windows.Controls.Canvas> prevede che gli elementi figlio possano essere disegnati esternamente ai limiti <xref:System.Windows.Controls.Canvas>.  Se si desidera modificare questo comportamento, è possibile impostare la proprietà <xref:System.Windows.UIElement.ClipToBounds%2A> su `true`.  In questo modo, <xref:System.Windows.Controls.Canvas> viene ritagliato in base alle relative dimensioni.  In questo modo, <xref:System.Windows.Controls.Canvas> è l'unico elemento di layout che consente di disegnare gli elementi figlio esternamente ai propri limiti.  
  
 Questo comportamento viene illustrato graficamente in [Esempio di confronto di proprietà Width](http://go.microsoft.com/fwlink/?LinkID=160050).  
  
#### Definizione e utilizzo di un elemento Canvas  
 È possibile creare un'istanza di un elemento <xref:System.Windows.Controls.Canvas> semplicemente tramite [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] o codice.  Nell'esempio seguente viene mostrato l'utilizzo di <xref:System.Windows.Controls.Canvas> per il posizionamento assoluto del contenuto.  Questo codice produce tre quadrati da 100 pixel.  Il primo di essi è rosso e la posizione \(*x, y*\) del relativo angolo superiore sinistro è specificata come \(0, 0\).  Il secondo è verde, con la posizione dell'angolo superiore sinistro impostata su \(100, 100\), ossia al di sotto e a destra rispetto al primo quadrato.  Il terzo è blu, con la posizione dell'angolo superiore sinistro impostata su \(50, 50\) e ingloba pertanto il quadrante inferiore destro del primo quadrato e quello superiore sinistro del secondo quadrato.  Poiché il terzo quadrato è stato disposto per ultimo, sembra posizionato sopra agli altri due; di conseguenza, le porzioni sovrapposte assumono il colore del terzo quadrato.  
  
 [!code-csharp[CanvasOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xml[CanvasOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Tipico elemento Canvas](../../../../docs/framework/wpf/controls/media/panel-intro-canvas.png "panel\_intro\_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>   
### DockPanel  
 L'elemento <xref:System.Windows.Controls.DockPanel> utilizza la proprietà <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> associata impostata negli elementi di contenuto figlio per posizionare il contenuto lungo i bordi di un contenitore.  Quando <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> è impostato su <xref:System.Windows.Controls.Dock> o <xref:System.Windows.Controls.Dock>, gli elementi figlio vengono posizionati l'uno sopra o sotto l'altro.  Quando <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> è impostato su <xref:System.Windows.Controls.Dock> o <xref:System.Windows.Controls.Dock>, gli elementi figlio vengono posizionati l'uno a destra o a sinistra dell'altro.  La proprietà <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> determina la posizione dell'elemento finale aggiunto come elemento figlio di <xref:System.Windows.Controls.DockPanel>.  
  
 È possibile utilizzare <xref:System.Windows.Controls.DockPanel> per posizionare un gruppo di controlli correlati, ad esempio una serie di pulsanti.  È anche possibile utilizzarlo per creare un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] con riquadri, simile a quella disponibile in [!INCLUDE[TLA#tla_outlook](../../../../includes/tlasharptla-outlook-md.md)].  
  
#### Ridimensionamento in base al contenuto  
 Se le proprietà <xref:System.Windows.FrameworkElement.Height%2A> e <xref:System.Windows.FrameworkElement.Width%2A> non sono specificate, <xref:System.Windows.Controls.DockPanel> esegue il ridimensionamento in base al contenuto.  Le dimensioni possono essere aumentate o diminuite in modo da contenere quelle degli elementi figlio.  Tuttavia, se tali proprietà sono impostate e lo spazio non è sufficiente a contenere il successivo elemento figlio specificato, in <xref:System.Windows.Controls.DockPanel> quell'elemento figlio o quelli successivi non saranno visualizzati, né misurati.  
  
#### LastChildFill  
 Per impostazione predefinita, l'ultimo elemento figlio di un elemento <xref:System.Windows.Controls.DockPanel> "riempie" lo spazio rimanente non allocato.  Se si desidera modificare questo comportamento, è possibile impostare la proprietà <xref:System.Windows.Controls.DockPanel.LastChildFill%2A> su `false`.  
  
#### Definizione e utilizzo di un elemento DockPanel  
 Nell'esempio seguente viene illustrata la partizione dello spazio tramite <xref:System.Windows.Controls.DockPanel>.  Vengono aggiunti cinque elementi <xref:System.Windows.Controls.Border> come elementi figlio di un elemento <xref:System.Windows.Controls.DockPanel> padre.  Ciascuno utilizza una diversa proprietà di posizionamento di <xref:System.Windows.Controls.DockPanel> per la partizione dello spazio.  L'elemento finale "riempie" lo spazio rimanente non allocato.  
  
 [!code-cpp[DockPanelOvwSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xml[DockPanelOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Tipo scenario DockPanel](../../../../docs/framework/wpf/controls/media/panel-intro-dockpanel.png "panel\_intro\_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>   
### Grid  
 L'elemento <xref:System.Windows.Controls.Grid> combina le funzionalità di posizionamento assoluto e controllo dati tabulari.  <xref:System.Windows.Controls.Grid> consente di posizionare facilmente gli elementi e applicare uno stile.  Con <xref:System.Windows.Controls.Grid> è possibile definire raggruppamenti flessibili di righe e colonne e viene fornito inoltre un meccanismo per la condivisione delle informazioni di ridimensionamento tra più elementi <xref:System.Windows.Controls.Grid>.  
  
#### Differenze tra l'elemento Grid e l'elemento Table  
 Gli elementi <xref:System.Windows.Documents.Table> e <xref:System.Windows.Controls.Grid> condividono alcune funzionalità comuni, ma ciascuno di essi si rivela più adatto per scenari diversi.  Un elemento <xref:System.Windows.Documents.Table> è progettato per l'utilizzo all'interno del contenuto di flusso \(per ulteriori informazioni sul contenuto di flusso, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)\).  Gli elementi Grid vengono utilizzati con maggior efficacia all'interno di form \(in generale all'esterno del contenuto di flusso\).  All'interno di un oggetto <xref:System.Windows.Documents.FlowDocument>, un elemento <xref:System.Windows.Documents.Table> supporta comportamenti del contenuto di flusso come impaginazione, riflusso di colonne e selezione di contenuto, a differenza di un elemento <xref:System.Windows.Controls.Grid>.  Un elemento <xref:System.Windows.Controls.Grid> viene invece utilizzato con maggior efficacia all'esterno di un oggetto <xref:System.Windows.Documents.FlowDocument> per diversi motivi, incluso il fatto che l'elemento <xref:System.Windows.Controls.Grid> aggiunge gli elementi in base a un indice di riga e di colonna, a differenza di <xref:System.Windows.Documents.Table>.  L'elemento <xref:System.Windows.Controls.Grid> consente la sovrapposizione di contenuti figlio, permettendo la presenza di più di un elemento all'interno di un'unica "cella". L'elemento <xref:System.Windows.Documents.Table> non supporta la sovrapposizione.  Gli elementi figlio di un elemento <xref:System.Windows.Controls.Grid> possono essere posizionati in modo assoluto rispetto all'area della relativa "cella".  <xref:System.Windows.Documents.Table> non supporta questa funzionalità.  Infine, un elemento <xref:System.Windows.Controls.Grid> è più semplice rispetto a un elemento <xref:System.Windows.Documents.Table>.  
  
#### Comportamento di ridimensionamento di colonne e righe  
 Le colonne e le righe definite all'interno di un oggetto <xref:System.Windows.Controls.Grid> possono sfruttare il ridimensionamento <xref:System.Windows.GridUnitType> per distribuire proporzionalmente lo spazio rimanente.  Quando è selezionato <xref:System.Windows.GridUnitType> per l'altezza o la larghezza di una riga o di una colonna, tale colonna o tale riga riceve una proporzione ponderata dello spazio disponibile rimanente.  Al contrario, <xref:System.Windows.GridUnitType> distribuirà uniformemente lo spazio in base alla dimensione del contenuto che si trova all'interno di una colonna o di una riga.  Questo valore è espresso come `*` o `2*` quando si utilizza la sintassi [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Nel primo caso, la riga o la colonna riceverebbe una volta lo spazio disponibile, mentre nel secondo caso due volte e così via.  Combinando questa tecnica per distribuire proporzionalmente lo spazio con i valori <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> e <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> di `Stretch`, è possibile suddividere lo spazio di layout come percentuale dello spazio dello schermo,  <xref:System.Windows.Controls.Grid> è l'unico riquadro del layout in grado di distribuire lo spazio in questo modo.  
  
#### Definizione e utilizzo di un elemento Grid  
 Nell'esempio seguente viene illustrata la compilazione di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] analoga a quella della finestra di dialogo Esegui, disponibile nel menu Start di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  
  
 [!code-csharp[GridRunDialog#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Tipico elemento Grid](../../../../docs/framework/wpf/controls/media/avalon-run-dialog.png "avalon\_run\_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>   
### StackPanel  
 Un oggetto <xref:System.Windows.Controls.StackPanel> consente di disporre in uno stack gli elementi assegnando una direzione.  La direzione predefinita dello stack è verticale.  La proprietà <xref:System.Windows.Controls.StackPanel.Orientation%2A> può essere utilizzata per controllare il flusso del contenuto.  
  
#### StackPanel eDockPanel  
 Sebbene sia possibile utilizzare <xref:System.Windows.Controls.DockPanel> per disporre gli elementi figlio in uno stack, <xref:System.Windows.Controls.DockPanel> e <xref:System.Windows.Controls.StackPanel> non producono risultati analoghi in alcuni scenari di utilizzo.  Ad esempio, l'ordine degli elementi figlio può influire sulle relative dimensioni in un oggetto <xref:System.Windows.Controls.DockPanel>, ma non in un oggetto <xref:System.Windows.Controls.StackPanel>.  Questa differenza è dovuta al fatto che <xref:System.Windows.Controls.StackPanel> considera le misure nella direzione dello stack a <xref:System.Double.PositiveInfinity>, mentre <xref:System.Windows.Controls.DockPanel> misura solo le dimensioni disponibili.  
  
 Nell'esempio seguente viene illustrata questa differenza fondamentale.  
  
 [!code-cpp[StackPanelOvw4#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xml[StackPanelOvw4#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 In questa immagine è possibile notare il diverso comportamento di rendering.  
  
 ![Schermata: StackPanel e DockPanel a confronto](../../../../docs/framework/wpf/controls/media/layout-smiley-stackpanel.png "layout\_smiley\_stackpanel")  
  
#### Definizione e utilizzo di un elemento StackPanel  
 Nell'esempio seguente viene mostrato l'utilizzo di un elemento <xref:System.Windows.Controls.StackPanel> per creare una serie di pulsanti posizionati verticalmente.  Per il posizionamento orizzontale, impostare la proprietà <xref:System.Windows.Controls.StackPanel.Orientation%2A> su <xref:System.Windows.Controls.Orientation>.  
  
 [!code-csharp[StackPanel_ovw2#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Tipico elemento StackPanel](../../../../docs/framework/wpf/controls/media/panel-intro-stackpanel.png "panel\_intro\_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>   
#### VirtualizingStackPanel  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è disponibile anche una variante dell'elemento <xref:System.Windows.Controls.StackPanel> che "virtualizza" automaticamente il contenuto figlio con associazione a dati.  In questo contesto, il termine "virtualizzare" si riferisce a una tecnica grazie alla quale, a partire da un gran numero di elementi dei dati, viene generato un sottoinsieme di elementi in base agli elementi visibili sullo schermo.  Generare un elevato numero di elementi dell'interfaccia utente, quando solo alcuni possono essere visualizzati sullo schermo in un dato momento, richiede un intenso consumo di risorse sia in termini di memoria che di processore.  <xref:System.Windows.Controls.VirtualizingStackPanel>, tramite le funzionalità disponibili in <xref:System.Windows.Controls.VirtualizingPanel>, calcola gli elementi visibili e utilizza l'elemento <xref:System.Windows.Controls.ItemContainerGenerator> di un oggetto <xref:System.Windows.Controls.ItemsControl> \(ad esempio <xref:System.Windows.Controls.ListBox> o <xref:System.Windows.Controls.ListView>\) per creare elementi solo per gli elementi visibili.  
  
 L'elemento <xref:System.Windows.Controls.VirtualizingStackPanel> viene impostato automaticamente come host degli elementi per controlli quali <xref:System.Windows.Controls.ListBox>.  Quando viene ospitata una raccolta con associazione a dati, il contenuto viene virtualizzato automaticamente, purché il contenuto sia incluso all'interno dei limiti di <xref:System.Windows.Controls.ScrollViewer>.  In questo modo le prestazioni ottenute durante l'hosting di molti elementi figlio vengono sensibilmente migliorate.  
  
 Nel seguente markup viene illustrato l'utilizzo di <xref:System.Windows.Controls.VirtualizingStackPanel> come host di elementi.  Per eseguire la virtualizzazione, la [proprietà associata](GTMT) <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> deve essere impostata su `true` \(impostazione predefinita\).  
  
 [!code-xml[VirtualizingStackPanel_Intro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>   
### WrapPanel  
 <xref:System.Windows.Controls.WrapPanel> viene utilizzato per posizionare gli elementi figlio in sequenza da sinistra verso destra, interrompendo il contenuto quando viene raggiunto il bordo del contenitore padre e facendolo ripartire dalla riga successiva.  Il contenuto può essere orientato orizzontalmente o verticalmente.  <xref:System.Windows.Controls.WrapPanel> è utile negli scenari dell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  È possibile utilizzarlo inoltre per applicare un ridimensionamento uniforme a tutti i relativi elementi figlio.  
  
 Nell'esempio seguente viene illustrato il modo in cui creare un oggetto <xref:System.Windows.Controls.WrapPanel> per visualizzare controlli <xref:System.Windows.Controls.Button> che eseguono il wrapping una volta raggiunto il bordo del relativo contenitore.  
  
 [!code-cpp[WrapPanel_Intro#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xml[WrapPanel_Intro#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Tipico elemento WrapPanel](../../../../docs/framework/wpf/controls/media/wrappanel-element.png "WrapPanel\_Element")  
  
<a name="Panels_nested_panel_elements"></a>   
## Elementi Panel annidati  
 È possibile annidare gli elementi <xref:System.Windows.Controls.Panel> l'uno all'interno dell'altro in modo da produrre layout complessi.  Questo annidamento può risultare molto utile in situazioni in cui un elemento <xref:System.Windows.Controls.Panel> è ideale per una porzione di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], ma potrebbe non rispondere ai requisiti necessari per un'altra porzione dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  
  
 Non esistono limiti effettivi al livello di annidamento che l'applicazione è in grado di supportare; tuttavia, è preferibile restringere l'utilizzo dei pannelli a quelli realmente necessari per il layout desiderato.  In molti casi è possibile utilizzare un elemento <xref:System.Windows.Controls.Grid> al posto dei pannelli annidati a causa della flessibilità di tale elemento come contenitore di layout.  Questo può accrescere le prestazioni dell'applicazione, evitando di inserire elementi inutili nella struttura ad albero.  
  
 Nell'esempio seguente viene illustrato il modo in cui creare un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che sfrutta gli elementi <xref:System.Windows.Controls.Panel> annidati per ottenere un determinato layout.  In questo particolare caso, un elemento <xref:System.Windows.Controls.DockPanel> viene utilizzato per fornire la struttura dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], mentre elementi <xref:System.Windows.Controls.StackPanel> annidati, un elemento <xref:System.Windows.Controls.Grid> e un elemento <xref:System.Windows.Controls.Canvas> vengono utilizzati per posizionare gli elementi figlio con precisione all'interno dell'elemento padre <xref:System.Windows.Controls.DockPanel>.  
  
 [!code-csharp[Nested_Panels#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 L'applicazione compilata produce una nuova [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] simile alla seguente.  
  
 ![Interfaccia utente che usa panelli annidati](../../../../docs/framework/wpf/controls/media/nested-panels.png "nested\_panels")  
  
<a name="Panels_custom_panel_elements"></a>   
## Elementi Panel personalizzati  
 Mentre in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornita una matrice di controlli layout flessibili, è possibile ottenere comportamenti di layout personalizzati anche eseguendo l'override dei metodi <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> e <xref:System.Windows.FrameworkElement.MeasureOverride%2A>.  Il ridimensionamento e il posizionamento personalizzati possono essere eseguiti tramite la definizione di nuovi comportamenti di posizionamento all'interno di questi metodi di override.  
  
 Analogamente, è possibile definire comportamenti di layout personalizzati \(ad esempio <xref:System.Windows.Controls.Canvas> o <xref:System.Windows.Controls.Grid>\) eseguendo l'override dei relativi metodi <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> e <xref:System.Windows.FrameworkElement.MeasureOverride%2A>.  
  
 Nel seguente markup viene illustrata la procedura per la creazione di un elemento <xref:System.Windows.Controls.Panel> personalizzato.  Questo nuovo elemento <xref:System.Windows.Controls.Panel>, definito `PlotPanel`, supporta il posizionamento degli elementi figlio mediante l'utilizzo di coordinate *x\-* e *y\-* hardcoded.  In questo esempio, un elemento <xref:System.Windows.Shapes.Rectangle> \(non visualizzato\) viene posizionato in corrispondenza del punto 50 \(*x*\) e 50 \(*y*\).  
  
 [!code-cpp[PlotPanel#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 Per visualizzare un'implementazione di pannelli personalizzati più complessa, vedere [Esempio di creazione di un elemento Panel personalizzato con ritorno a capo del contenuto](http://go.microsoft.com/fwlink/?LinkID=159979) \(la pagina potrebbe essere in inglese\).  
  
<a name="Panels_global_localization"></a>   
## Supporto di localizzazione\/globalizzazione  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono supportate numerose funzionalità che facilitano la creazione di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] localizzabile.  
  
 Tutti gli elementi Panel supportano a livello nativo la proprietà <xref:System.Windows.FrameworkElement.FlowDirection%2A>, che può essere utilizzata per consentire un nuovo flusso dinamico del contenuto in base alle impostazioni locali o di lingua dell'utente.  Per ulteriori informazioni, vedere <xref:System.Windows.FrameworkElement.FlowDirection%2A>.  
  
 La proprietà <xref:System.Windows.Window.SizeToContent%2A> fornisce un meccanismo che consente agli sviluppatori di applicazioni di prevedere le esigenze di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] localizzata.  Utilizzando il valore <xref:System.Windows.SizeToContent> di tale proprietà, un elemento <xref:System.Windows.Window> padre viene sempre ridimensionato in modo dinamico in modo da adattarlo al contenuto e non è vincolato da restrizioni artificiali di altezza o larghezza.  
  
 <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Grid> e <xref:System.Windows.Controls.StackPanel> rappresentano tutti opzioni appropriate per un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] localizzabile.  <xref:System.Windows.Controls.Canvas> invece non rappresenta un'opzione ideale, poiché determina il posizionamento assoluto del contenuto, che risulterà pertanto difficile da localizzare.  
  
 Per ulteriori informazioni sulla creazione di applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] localizzabili, vedere [Cenni preliminari sull'utilizzo del layout automatico](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md).  
  
## Vedere anche  
 [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)   
 [Esempio di raccolte di layout WPF](http://go.microsoft.com/fwlink/?LinkID=160054)   
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)   
 [Esempio di raccolta di controlli WPF](http://go.microsoft.com/fwlink/?LinkID=160053)   
 [Panoramica su allineamento, margini e spaziatura interna](../../../../docs/framework/wpf/advanced/alignment-margins-and-padding-overview.md)   
 [Esempio di creazione di un elemento Panel personalizzato con ritorno a capo del contenuto](http://go.microsoft.com/fwlink/?LinkID=159979)   
 [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)   
 [Cenni preliminari sull'utilizzo del layout automatico](../../../../docs/framework/wpf/advanced/use-automatic-layout-overview.md)   
 [Layout e progettazione](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)