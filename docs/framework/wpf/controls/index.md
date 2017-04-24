---
title: "Controlli | Microsoft Docs"
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
  - "controlli [WPF], informazioni sui controlli WPF"
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Controlli
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene fornito con molti dei più comuni componenti dell'interfaccia utente utilizzati in quasi ogni applicazione Windows, ad esempio <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.Menu> e <xref:System.Windows.Controls.ListBox>.  Questi oggetti sono denominati controlli.  Sebbene [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK continui a utilizzare il termine "controllo" per indicare in modo generale qualsiasi classe che rappresenta un oggetto visibile in un'applicazione, è importante notare che una classe non deve ereditare dalla classe <xref:System.Windows.Controls.Control> per essere visibilmente presente.  Le classi che ereditano dalla classe <xref:System.Windows.Controls.Control> contengono un oggetto <xref:System.Windows.Controls.ControlTemplate> che consente all'utente di un controllo di modificarne radicalmente l'aspetto senza dover creare una nuova sottoclasse.  In questo argomento viene illustrato il tipico utilizzo dei controlli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], sia quelli che ereditano dalla classe <xref:System.Windows.Controls.Control> sia gli altri.  
  
   
  
<a name="creating_an_instance_of_a_control"></a>   
## Creazione di un'istanza di un controllo  
 È possibile aggiungere un controllo a un'applicazione utilizzando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] o il codice.  Nell'esempio riportato di seguito viene illustrato come creare una semplice applicazione in cui venga chiesto all'utente di immettere il nome e il cognome.  In questo esempio vengono creati sei controlli, due etichette, due caselle di testo e due pulsanti, in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Tutti i controlli possono essere creati in modo analogo.  
  
 [!code-xml[ControlsOverview#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 Nell'esempio riportato di seguito viene creata la stessa applicazione nel codice.  Per ragioni di brevità, la creazione del controllo <xref:System.Windows.Controls.Grid>, `grid1` è stata esclusa dall'esempio.  `grid1` presenta le stesse definizioni di righe e colonne illustrate nel precedente esempio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-csharp[ControlsOverview#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)]
 [!code-vb[ControlsOverview#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>   
## Modifica dell'aspetto di un controllo  
 Modificare l'aspetto di un controllo per adattare l'aspetto dell'applicazione è un'operazione alquanto comune.  È possibile modificare l'aspetto di un controllo eseguendo una delle operazioni indicate di seguito, a seconda del risultato che si desidera ottenere:  
  
-   Modificare il valore di una proprietà del controllo.  
  
-   Creare un oggetto <xref:System.Windows.Style> per il controllo.  
  
-   Creare un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo.  
  
### Modifica del valore di una proprietà di un controllo  
 Esistono proprietà che consentono di modificare l'aspetto del controllo, ad esempio la proprietà <xref:System.Windows.Controls.Control.Background%2A> di un controllo <xref:System.Windows.Controls.Button>.  È possibile impostare le proprietà del valore in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e nel codice.  Nell'esempio riportato di seguito vengono impostate le proprietà <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.FontSize%2A> e <xref:System.Windows.Controls.Control.FontWeight%2A> di un controllo <xref:System.Windows.Controls.Button> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[ControlsOverview#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 Nell'esempio riportato di seguito vengono impostate le stesse proprietà nel codice.  
  
 [!code-csharp[ControlsOverview#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)]
 [!code-vb[ControlsOverview#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### Creazione di uno stile per un controllo  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è possibile specificare l'aspetto dei controlli a livello globale, anziché impostare proprietà in ogni istanza nell'applicazione tramite la creazione di un oggetto <xref:System.Windows.Style>.  Nell'esempio seguente viene creato un oggetto <xref:System.Windows.Style>, che viene applicato a ogni controllo <xref:System.Windows.Controls.Button> dell'applicazione. Le definizioni <xref:System.Windows.Style> vengono in genere specificate in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in un oggetto <xref:System.Windows.ResourceDictionary>, ad esempio la proprietà <xref:System.Windows.FrameworkElement.Resources%2A> dell'oggetto <xref:System.Windows.FrameworkElement>.  
  
 [!code-xml[ControlsOverview#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 È anche possibile applicare uno stile solo a determinati controlli di un tipo specifico assegnando una chiave allo stile e specificando quella chiave nella proprietà `Style` del controllo.  Per ulteriori informazioni sugli stili, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
### Creazione di un ControlTemplate  
 <xref:System.Windows.Style> consente di impostare proprietà su più controlli alla volta, anche se a volte è necessario personalizzare l'aspetto di un <xref:System.Windows.Controls.Control> in modo più esteso rispetto a quanto è possibile ottenere creando un oggetto <xref:System.Windows.Style>.  Le classi che ereditano dalla classe <xref:System.Windows.Controls.Control> dispongono di un oggetto <xref:System.Windows.Controls.ControlTemplate> che definisce la struttura e l'aspetto di un <xref:System.Windows.Controls.Control>.  La proprietà <xref:System.Windows.Controls.Control.Template%2A> di un <xref:System.Windows.Controls.Control> è pubblica, pertanto è possibile assegnare a un <xref:System.Windows.Controls.Control> un <xref:System.Windows.Controls.ControlTemplate> diverso da quello predefinito.  È spesso possibile specificare un nuovo <xref:System.Windows.Controls.ControlTemplate> per un <xref:System.Windows.Controls.Control> anziché ereditare da un controllo per personalizzare l'aspetto di un <xref:System.Windows.Controls.Control>.  
  
 Si consideri un controllo molto comune, <xref:System.Windows.Controls.Button>.  Il comportamento primario di un controllo <xref:System.Windows.Controls.Button> consiste nel consentire a un'applicazione di intraprendere una qualche azione quando l'utente fa clic su di esso.  Per impostazione predefinita, <xref:System.Windows.Controls.Button> viene visualizzato in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] come rettangolo in rilievo.  Quando si sviluppa un'applicazione, è possibile sfruttare il comportamento di un controllo <xref:System.Windows.Controls.Button>, tramite gestione dell'evento Click del pulsante, ma è possibile modificare l'aspetto del pulsante oltre a quanto è possibile fare modificando le proprietà del pulsante.  In questo caso, è possibile creare un nuovo <xref:System.Windows.Controls.ControlTemplate>.  
  
 Nell'esempio riportato di seguito viene creato un <xref:System.Windows.Controls.ControlTemplate> per un controllo <xref:System.Windows.Controls.Button>.  Tramite <xref:System.Windows.Controls.ControlTemplate> viene creato un controllo <xref:System.Windows.Controls.Button> con angoli arrotondati e uno sfondo sfumato.  <xref:System.Windows.Controls.ControlTemplate> contiene un <xref:System.Windows.Controls.Border> la cui proprietà <xref:System.Windows.Controls.Border.Background%2A> è <xref:System.Windows.Media.LinearGradientBrush> con due oggetti <xref:System.Windows.Media.GradientStop>.  Il primo oggetto <xref:System.Windows.Media.GradientStop> utilizza l'associazione dati per associare la proprietà <xref:System.Windows.Media.GradientStop.Color%2A> di <xref:System.Windows.Media.GradientStop> al colore dello sfondo del pulsante.  Quando si imposta la proprietà <xref:System.Windows.Controls.Control.Background%2A> del controllo <xref:System.Windows.Controls.Button>, il colore di quel valore verrà utilizzato come primo <xref:System.Windows.Media.GradientStop>.  Per ulteriori informazioni sull'associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  Nell'esempio viene inoltre creato un oggetto <xref:System.Windows.Trigger> che modifica l'aspetto del controllo <xref:System.Windows.Controls.Button> quando <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> è `true`.  
  
 [!code-xml[ControlsOverview#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xml[ControlsOverview#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
>  Affinché l'esempio funzioni correttamente, la proprietà <xref:System.Windows.Controls.Control.Background%2A> del controllo <xref:System.Windows.Controls.Button> deve essere impostata su <xref:System.Windows.Media.SolidColorBrush>.  
  
<a name="subscribing_to_events"></a>   
## Sottoscrizione agli eventi  
 È possibile sottoscrivere l'evento di un controllo utilizzando [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o il codice, ma è possibile gestire un evento solo nel codice.  Nell'esempio riportato di seguito viene illustrato come sottoscrivere l'evento `Click` di un controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[ControlsOverview#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)]
 [!code-vb[ControlsOverview#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 Nell'esempio riportato di seguito viene gestito l'evento `Click` di un controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-csharp[ControlsOverview#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)]
 [!code-vb[ControlsOverview#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>   
## Contenuto completo nei controlli  
 La maggior parte delle classi che eredita dalla classe <xref:System.Windows.Controls.Control> può contenere contenuto completo.  Ad esempio, un oggetto <xref:System.Windows.Controls.Label> può contenere qualsiasi oggetto, ad esempio una stringa, un controllo <xref:System.Windows.Controls.Image> o un controllo <xref:System.Windows.Controls.Panel>.  Le classi riportate di seguito supportano contenuto completo e costituiscono le classi base per la maggior parte dei controlli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   <xref:System.Windows.Controls.ContentControl>\-\-Alcuni esempi di classi che ereditano da questa classe sono <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.ToolTip>.  
  
-   <xref:System.Windows.Controls.ItemsControl>\-\-Alcuni esempi di classi che ereditano da questa classe sono <xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.Menu> e <xref:System.Windows.Controls.Primitives.StatusBar>.  
  
-   <xref:System.Windows.Controls.HeaderedContentControl>\-\-Alcuni esempi di classi che ereditano da questa classe sono <xref:System.Windows.Controls.TabItem>, <xref:System.Windows.Controls.GroupBox> e <xref:System.Windows.Controls.Expander>.  
  
-   <xref:System.Windows.Controls.HeaderedItemsControl>\-\-Alcuni esempi di classi che ereditano da questa classe sono <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.TreeViewItem> e <xref:System.Windows.Controls.ToolBar>.  
  
 Per ulteriori informazioni su queste classi di base, vedere [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md).  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Controlli per categoria](../../../../docs/framework/wpf/controls/controls-by-category.md)   
 [Libreria di controlli](../../../../docs/framework/wpf/controls/control-library.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Input](../../../../docs/framework/wpf/advanced/input-wpf.md)   
 [Attivare un comando](../../../../docs/framework/wpf/advanced/how-to-enable-a-command.md)   
 [Procedure dettagliate: creazione di un pulsante personalizzato a cui è stata aggiunta un'animazione](../../../../docs/framework/wpf/controls/walkthroughs-create-a-custom-animated-button.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)