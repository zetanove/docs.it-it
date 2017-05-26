---
title: Controlli | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- controls [WPF], about WPF controls
ms.assetid: 3f255a8a-35a8-4712-9065-472ff7d75599
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 7652a2e64cdc107546ac3ea51178a3542606bd43
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="controls"></a>Controlli
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] viene fornito con molti dei più comuni componenti dell'interfaccia utente usati in quasi tutte le applicazioni Windows, ad esempio              <xref:System.Windows.Controls.Button>,              <xref:System.Windows.Controls.Label>,              <xref:System.Windows.Controls.TextBox>,              <xref:System.Windows.Controls.Menu> e              <xref:System.Windows.Controls.ListBox>. In passato, questi oggetti sono stati indicati come controlli. Mentre              [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] SDK continua a usare il termine "controllo" per indicare in modo generico qualsiasi classe che rappresenta un oggetto visibile in un'applicazione, è importante notare che una classe non deve necessariamente ereditare dalla              classe <xref:System.Windows.Controls.Control> per avere una presenza visibile. Le classi che ereditano dalla              classe <xref:System.Windows.Controls.Control> contengono un              oggetto <xref:System.Windows.Controls.ControlTemplate>, che consente al consumer di un controllo di modificare radicalmente l'aspetto del controllo stesso senza dover creare una nuova sottoclasse.  Questo argomento illustra in che modo i controlli (sia quelli che ereditano dalla              classe <xref:System.Windows.Controls.Control> che quelli che non ereditano da tale classe) vengono comunemente usati in              [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 
  
<a name="creating_an_instance_of_a_control"></a>   
## <a name="creating-an-instance-of-a-control"></a>Creazione dell'istanza di un controllo  
 È possibile aggiungere un controllo a un'applicazione usando [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] o il codice.  L'esempio seguente illustra come creare una semplice applicazione che chiede all'utente di indicare il nome e cognome.  In questo esempio vengono creati sei controlli: due etichette, due caselle di testo e due pulsanti in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. È possibile creare tutti i controlli in modo analogo.  
  
 [!code-xml[ControlsOverview#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#1)]  
  
 Nell'esempio seguente viene creata la stessa applicazione nel codice. Per brevità, la creazione di                  <xref:System.Windows.Controls.Grid>,                  `grid1`, è stata esclusa dall'esempio.                   `grid1` presenta le stesse definizioni di colonna e riga illustrate nell'esempio [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] precedente.  
  
 [!code-csharp[ControlsOverview#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#2)] [!code-vb[ControlsOverview#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#2)]  
  
<a name="changing_the_appearance_of_a_control"></a>   
## <a name="changing-the-appearance-of-a-control"></a>Modifica dell'aspetto di un controllo  
 È spesso necessario modificare l'aspetto di un controllo per adattarlo all'aspetto dell'applicazione. Per modificare l'aspetto di un controllo, è possibile adottare una delle procedure seguenti, a seconda del risultato che si intende ottenere:  
  
-   Modificare il valore di una proprietà del controllo.  
  
-   Creare un                          oggetto <xref:System.Windows.Style> per il controllo.  
  
-   Creare un nuovo                          oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo.  
  
### <a name="changing-a-controls-property-value"></a>Modifica di un valore della proprietà del controllo  
 Esistono proprietà che consentono di modificare l'aspetto del controllo, ad esempio la                          proprietà <xref:System.Windows.Controls.Control.Background%2A> di un                          controllo <xref:System.Windows.Controls.Button>. È possibile impostare il valore delle proprietà sia in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che nel codice. Nell'esempio seguente vengono impostate le                          proprietà <xref:System.Windows.Controls.Control.Background%2A>,                          <xref:System.Windows.Controls.Control.FontSize%2A> e                          <xref:System.Windows.Controls.Control.FontWeight%2A> di un controllo                          <xref:System.Windows.Controls.Button> in                          [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[ControlsOverview#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#3)]  
  
 Nell'esempio seguente vengono impostate le stesse proprietà nel codice.  
  
 [!code-csharp[ControlsOverview#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#4)] [!code-vb[ControlsOverview#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#4)]  
  
### <a name="creating-a-style-for-a-control"></a>Creazione di uno stile per un controllo  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente di specificare l'aspetto dei controlli a livello globale, anziché impostare le proprietà per ogni istanza dell'applicazione, creando un                          oggetto <xref:System.Windows.Style>.                           Nell'esempio seguente                          viene creato un                          oggetto <xref:System.Windows.Style> che viene applicato a ogni                          controllo <xref:System.Windows.Controls.Button> nell'applicazione.                          Le definizioni <xref:System.Windows.Style> vengono in genere specificate in                          [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in un                          oggetto <xref:System.Windows.ResourceDictionary>, ad esempio la                          proprietà <xref:System.Windows.FrameworkElement.Resources%2A> dell'oggetto                          <xref:System.Windows.FrameworkElement>.  
  
 [!code-xml[ControlsOverview#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#5)]  
  
 È anche possibile applicare uno stile solo a determinati controlli di un tipo specifico assegnando una chiave allo stile e specificando tale chiave nella proprietà `Style` del controllo.  Per altre informazioni sugli stili, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
### <a name="creating-a-controltemplate"></a>Creazione di un ControlTemplate  
 Un                          oggetto <xref:System.Windows.Style> consente di impostare le proprietà per più controlli contemporaneamente, ma a volte può essere necessario personalizzare l'aspetto di                          <xref:System.Windows.Controls.Control> più di quanto sia possibile ottenere creando un                          oggetto <xref:System.Windows.Style>. Le classi che ereditano dalla                          classe <xref:System.Windows.Controls.Control> dispongono di un                          oggetto <xref:System.Windows.Controls.ControlTemplate>, che definisce la struttura e l'aspetto di un                          oggetto <xref:System.Windows.Controls.Control>. La                          proprietà <xref:System.Windows.Controls.Control.Template%2A> di un                          <xref:System.Windows.Controls.Control> è pubblica, pertanto è possibile assegnare a un                          <xref:System.Windows.Controls.Control> un                          <xref:System.Windows.Controls.ControlTemplate> diverso da quello predefinito. Spesso è possibile specificare un nuovo                          oggetto <xref:System.Windows.Controls.ControlTemplate> per                           <xref:System.Windows.Controls.Control> anziché ereditare da un controllo per personalizzare l'aspetto di                          <xref:System.Windows.Controls.Control>.  
  
 Si consideri un controllo molto comune, ad esempio                          <xref:System.Windows.Controls.Button>.  Il comportamento principale di                           <xref:System.Windows.Controls.Button> consiste nel consentire a un'applicazione di eseguire qualche azione quando l'utente fa clic su di esso.  Per impostazione predefinita, l'oggetto                          <xref:System.Windows.Controls.Button> in                          [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene visualizzato come un rettangolo in rilievo.  Quando si sviluppa un'applicazione, è possibile usufruire del comportamento di                          <xref:System.Windows.Controls.Button>, ovvero gestendo l'evento click del pulsante, ma è possibile modificare l'aspetto del pulsante più di quanto si possa fare modificando le proprietà del pulsante stesso.  In questo caso, è possibile creare un nuovo                          <xref:System.Windows.Controls.ControlTemplate>.  
  
 Nell'esempio seguente viene creato un                          <xref:System.Windows.Controls.ControlTemplate> per un                          controllo <xref:System.Windows.Controls.Button>.  Il                          <xref:System.Windows.Controls.ControlTemplate> crea un                          controllo <xref:System.Windows.Controls.Button> con angoli arrotondati e uno sfondo sfumato.  Il                          <xref:System.Windows.Controls.ControlTemplate> contiene un                          <xref:System.Windows.Controls.Border> la cui proprietà                          <xref:System.Windows.Controls.Border.Background%2A> è                           <xref:System.Windows.Media.LinearGradientBrush> con due                          oggetti <xref:System.Windows.Media.GradientStop>.  Il primo                          oggetto <xref:System.Windows.Media.GradientStop> usa l'associazione dati per associare la                          proprietà <xref:System.Windows.Media.GradientStop.Color%2A> di                          <xref:System.Windows.Media.GradientStop> al colore dello sfondo del pulsante.  Quando si imposta la                          proprietà <xref:System.Windows.Controls.Control.Background%2A> del                          controllo <xref:System.Windows.Controls.Button>, il colore di tale valore verrà usato come primo                          <xref:System.Windows.Media.GradientStop>. Per altre informazioni sul data binding, vedere [Panoramica sul data binding](../../../../docs/framework/wpf/data/data-binding-overview.md). Nell'esempio viene inoltre creato un                          oggetto <xref:System.Windows.Trigger> che modifica l'aspetto del                          controllo <xref:System.Windows.Controls.Button> quando                          <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> è                          `true`.  
  
 [!code-xml[ControlsOverview#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#6)]  
[!code-xml[ControlsOverview#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml#7)]  
  
> [!NOTE]
>  Affinché l'esempio funzioni correttamente, la                             proprietà <xref:System.Windows.Controls.Control.Background%2A> del                              controllo <xref:System.Windows.Controls.Button> deve essere impostata su                              <xref:System.Windows.Media.SolidColorBrush>.  
  
<a name="subscribing_to_events"></a>   
## <a name="subscribing-to-events"></a>Sottoscrizione di eventi  
 È possibile sottoscrivere un evento del controllo utilizzando [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o il codice, ma si può gestire solo un evento nel codice.  Nell'esempio seguente viene illustrato come sottoscrivere l'evento                  `Click` di un                  controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[ControlsOverview#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/Window1.xaml#10)]  
  
 [!code-csharp[ControlsOverview#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#8)] [!code-vb[ControlsOverview#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#8)]  
  
 Nell'esempio seguente viene gestito l'evento                  `Click` di un                  controllo <xref:System.Windows.Controls.Button>.  
  
 [!code-csharp[ControlsOverview#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlsOverview/CSharp/AppInCode.xaml.cs#9)] [!code-vb[ControlsOverview#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ControlsOverview/VisualBasic/AppInCode.xaml.vb#9)]  
  
<a name="rich_content_in_controls"></a>   
## <a name="rich-content-in-controls"></a>Contenuto avanzato dei controlli  
 La maggior parte delle classi che eredita dalla                  classe <xref:System.Windows.Controls.Control> può contenere contenuto completo. Ad esempio, un                  oggetto <xref:System.Windows.Controls.Label> può contenere qualsiasi oggetto, ad esempio una stringa, un                  controllo <xref:System.Windows.Controls.Image> o un                  controllo <xref:System.Windows.Controls.Panel>.  Le classi seguenti supportano contenuto avanzato e fungono da classi di base per la maggior parte dei controlli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   <xref:System.Windows.Controls.ContentControl>-- Alcuni esempi di classi che ereditano da questa classe sono                          <xref:System.Windows.Controls.Label>,                          <xref:System.Windows.Controls.Button> e                          <xref:System.Windows.Controls.ToolTip>.  
  
-   <xref:System.Windows.Controls.ItemsControl>-- Alcuni esempi di classi che ereditano da questa classe sono                          <xref:System.Windows.Controls.ListBox>,                          <xref:System.Windows.Controls.Menu> e                          <xref:System.Windows.Controls.Primitives.StatusBar>.  
  
-   <xref:System.Windows.Controls.HeaderedContentControl>-- Alcuni esempi di classi che ereditano da questa classe sono                          <xref:System.Windows.Controls.TabItem>,                          <xref:System.Windows.Controls.GroupBox> e                          <xref:System.Windows.Controls.Expander>.  
  
-   <xref:System.Windows.Controls.HeaderedItemsControl>--Alcuni esempi di classi che ereditano da questa classe sono                          <xref:System.Windows.Controls.MenuItem>,                          <xref:System.Windows.Controls.TreeViewItem> e                          <xref:System.Windows.Controls.ToolBar>.  
  
-  
  
 Per altre informazioni su queste classi di base, vedere [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Controlli per categoria](../../../../docs/framework/wpf/controls/controls-by-category.md)   
 [Libreria di controlli](../../../../docs/framework/wpf/controls/control-library.md)   
 [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Input](../../../../docs/framework/wpf/advanced/input-wpf.md)   
 [Attivare un comando](../../../../docs/framework/wpf/advanced/how-to-enable-a-command.md)   
 [Procedure dettagliate: creazione di un pulsante personalizzato a cui è stata aggiunta un'animazione](../../../../docs/framework/wpf/controls/walkthroughs-create-a-custom-animated-button.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)
