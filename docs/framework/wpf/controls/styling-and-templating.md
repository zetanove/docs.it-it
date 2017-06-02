---
title: "Applicazione di stili e modelli | Microsoft Docs"
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
  - "trigger"
  - "stili di riferimento"
  - "trigger di eventi"
  - "stili, prerequisiti"
  - "stili, dichiarazione"
  - "gli stili, panoramica"
  - "stili, estensione"
  - "stili, i trigger"
  - "stili, i trigger di evento"
ms.assetid: 481765e5-5467-4a75-9f7b-e10e2ac410d9
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Applicazione di stili e modelli
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]stili e modelli fa riferimento a un insieme di funzionalità (stili, modelli, trigger e storyboard) che consentono agli sviluppatori e progettisti per creare effetti visivamente accattivanti e per creare un aspetto coerenza per il prodotto. Anche se gli sviluppatori e progettisti possono personalizzare l'aspetto in modo esteso in modo da applicazioni, un modello di stili e modelli sicuro è necessario consentire la condivisione dell'aspetto all'interno e tra applicazioni e manutenzione. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]fornisce il modello.  
  
 Un'altra funzionalità del [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] stile modello consiste nella separazione della presentazione dalla logica. Ciò significa che i progettisti possono lavorare sull'aspetto di un'applicazione utilizzando solo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] allo stesso tempo che gli sviluppatori lavorano sulla logica di programmazione mediante c# o Visual Basic.  
  
 In questo argomento è incentrato sugli aspetti di stili e modelli dell'applicazione e non vengono illustrati i concetti qualsiasi associazione dati. Per informazioni sull'associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Inoltre, è importante conoscere le risorse, che consentono il riutilizzo dei modelli e stili. Per ulteriori informazioni sulle risorse, vedere [risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
   
  
<a name="styling_and_templating_sample"></a>   
## <a name="styling-and-templating-sample"></a>Applicazione di stili e modelli  
 Gli esempi di codice utilizzati in questa panoramica sono basati su un esempio semplice foto illustrato nella figura seguente:  
  
 ![Stile del controllo ListView](../../../../docs/framework/wpf/controls/media/stylingintro-triggers.png "StylingIntro_triggers")  
  
 Questo semplice esempio di foto utilizza stili e modelli per creare un'esperienza utente visivamente accattivanti. L'esempio include due <xref:System.Windows.Controls.TextBlock> elementi e un <xref:System.Windows.Controls.ListBox> controllo associato a un elenco di immagini. Per l'esempio completo, vedere [Introduzione agli stili e modelli](http://go.microsoft.com/fwlink/?LinkID=160010).  
  
<a name="styling_basics"></a>   
## <a name="style-basics"></a>Nozioni fondamentali sullo stile  
 È possibile considerare un <xref:System.Windows.Style> come un modo pratico per applicare un set di valori di proprietà per più di un elemento. Ad esempio, tenere presente quanto segue <xref:System.Windows.Controls.TextBlock> elementi e il relativo aspetto predefinito:  
  
 [!code-xml[StylingIntroSample_snippet#TextBlocks](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#textblocks)]  
  
 ![Schermata dell'esempio Styling](../../../../docs/framework/wpf/controls/media/stylingintro-textblocksbefore.png "StylingIntro_TextBlocksBefore")  
  
 È possibile modificare l'aspetto predefinito impostando le proprietà, ad esempio <xref:System.Windows.Controls.Control.FontSize%2A> e <xref:System.Windows.Controls.Control.FontFamily%2A>, in ogni <xref:System.Windows.Controls.TextBlock> direttamente l'elemento. Tuttavia, se si desidera che il <xref:System.Windows.Controls.TextBlock> elementi condividano alcune proprietà, è possibile creare un <xref:System.Windows.Style> nel `Resources` sezione del [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file, come illustrato di seguito:  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#tb1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#tb1)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 Quando si imposta la <xref:System.Windows.Style.TargetType%2A> dello stile per il <xref:System.Windows.Controls.TextBlock> tipo, lo stile applicato a tutti i <xref:System.Windows.Controls.TextBlock> elementi nella finestra.  
  
 A questo punto il <xref:System.Windows.Controls.TextBlock> gli elementi vengono visualizzati come segue:  
  
 ![Schermata dell'esempio Styling](../../../../docs/framework/wpf/controls/media/stylingintro-textblocksbasestyle.png "StylingIntro_TextBlocksBaseStyle")  
  
### <a name="extending-styles"></a>Estensione degli stili  
 Probabilmente si desidera che i due <xref:System.Windows.Controls.TextBlock> elementi condividano alcuni valori delle proprietà, ad esempio il <xref:System.Windows.Controls.Control.FontFamily%2A> e centrato <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, ma anche che il testo "My Pictures" abbia alcune proprietà aggiuntive. È possibile farlo creando un nuovo stile basato sul primo stile, come illustrato di seguito:  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#tb2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#tb2)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 Si noti che lo stile precedente viene assegnato un `x:Key`. Per applicare lo stile, impostare il <xref:System.Windows.FrameworkElement.Style%2A> proprietà di <xref:System.Windows.Controls.TextBlock> per il `x:Key` valore, come illustrato di seguito:  
  
 [!code-xml[StylingIntroSnippet#UIText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#uitext)]  
  
 Questo <xref:System.Windows.Controls.TextBlock> dispone ora di stile un <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> valore <xref:System.Windows.HorizontalAlignment>, un <xref:System.Windows.Controls.TextBlock.FontFamily%2A> valore `Comic Sans MS`, un <xref:System.Windows.Controls.TextBlock.FontSize%2A> valore pari a 26 e un <xref:System.Windows.Controls.TextBlock.Foreground%2A> valore impostato il <xref:System.Windows.Media.LinearGradientBrush> illustrato nell'esempio. Si noti che viene eseguito l'override di <xref:System.Windows.Controls.Control.FontSize%2A> valore dello stile di base. Se è presente più di un <xref:System.Windows.Setter> impostano la stessa proprietà un <xref:System.Windows.Style>, <xref:System.Windows.Setter> che è dichiarato ultima ha la precedenza.  
  
 Di seguito viene illustrato cosa il <xref:System.Windows.Controls.TextBlock> come appaiono ora elementi:  
  
 ![Stile TextBlock](../../../../docs/framework/wpf/controls/media/stylingintro-textblocks.png "StylingIntro_TextBlocks")  
  
 Questo `TitleText` stile estende lo stile che è stato creato per il <xref:System.Windows.Controls.TextBlock> tipo. È anche possibile estendere uno stile che ha un `x:Key` utilizzando il `x:Key` valore. Per un esempio, vedere l'esempio fornito per il <xref:System.Windows.Style.BasedOn%2A> proprietà.  
  
### <a name="relationship-of-the-targettype-property-and-the-xkey-attribute"></a>Relazione della proprietà TargetType e l'attributo X:Key  
 Come illustrato nel primo esempio, l'impostazione di <xref:System.Windows.Style.TargetType%2A> proprietà `TextBlock` senza assegnare un `x:Key` determina lo stile da applicare a tutti <xref:System.Windows.Controls.TextBlock> elementi. In questo caso, il `x:Key` è impostato in modo implicito su `{x:Type TextBlock}`. Ciò significa che se si imposta in modo esplicito il `x:Key` su un valore diverso da `{x:Type TextBlock}`, <xref:System.Windows.Style> non viene applicata a tutti <xref:System.Windows.Controls.TextBlock> elementi automaticamente. In alternativa, è necessario applicare lo stile (utilizzando il `x:Key` valore) per il <xref:System.Windows.Controls.TextBlock> elementi in modo esplicito. Se lo stile si trova nella sezione delle risorse e non si imposta la <xref:System.Windows.Style.TargetType%2A> proprietà di stile, sarà necessario fornire un `x:Key`.  
  
 Oltre a fornire un valore predefinito per il `x:Key`, <xref:System.Windows.Style.TargetType%2A> proprietà specifica il tipo a cui vengono applicate le proprietà. Se non si specifica un <xref:System.Windows.Style.TargetType%2A>, è necessario qualificare le proprietà di <xref:System.Windows.Setter> oggetti con un nome di classe utilizzando la sintassi `Property="ClassName.Property"`. Ad esempio, anziché impostare `Property="FontSize"`, è necessario impostare <xref:System.Windows.Setter.Property%2A> a `"TextBlock.FontSize"` o `"Control.FontSize"`.  
  
 Si noti inoltre che molte [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controlli sono costituiti da una combinazione di altri [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controlli. Se si crea uno stile che si applica a tutti i controlli di un tipo, si potrebbero ottenere risultati imprevisti. Ad esempio, se si crea uno stile che indirizza il <xref:System.Windows.Controls.TextBlock> digitare un <xref:System.Windows.Window>, lo stile applicato a tutti <xref:System.Windows.Controls.TextBlock> controlli nella finestra anche se il <xref:System.Windows.Controls.TextBlock> fa parte di un altro controllo, ad esempio un <xref:System.Windows.Controls.ListBox>.  
  
### <a name="styles-and-resources"></a>Stili e risorse  
 È possibile utilizzare uno stile su qualsiasi elemento che deriva da <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>. È il modo più comune per dichiarare uno stile come risorsa nel `Resources` sezione un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file, come illustrato negli esempi precedenti. Poiché gli stili sono risorse, si rispettano le stesse regole di ambito che si applicano a tutte le risorse; in cui si dichiara uno stile influisce in cui può essere applicato lo stile. Ad esempio, se si dichiara lo stile nell'elemento radice della definizione di applicazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file, lo stile può essere utilizzato ovunque nell'applicazione. Se si crea un'applicazione di navigazione e lo stile in uno dell'applicazione dichiarato [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file, lo stile possono essere utilizzati solo in quel [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file. Per ulteriori informazioni sulle regole di ambito per le risorse, vedere [risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
 Inoltre, è possibile trovare ulteriori informazioni su stili e le risorse in [risorse condivise e i temi](#styling_themes) più avanti in questa panoramica.  
  
### <a name="setting-styles-programmatically"></a>Impostazione degli stili a livello di codice  
 Per assegnare uno stile denominato a un elemento a livello di codice, ottenere lo stile dalla raccolta di risorse e assegnarlo alla proprietà dell'elemento <xref:System.Windows.FrameworkElement.Style%2A> proprietà. Si noti che gli elementi in una raccolta di risorse sono di tipo <xref:System.Object>. Pertanto, è necessario eseguire il cast dello stile recuperato a un <xref:System.Windows.Style> prima di assegnarlo al <xref:System.Windows.FrameworkElement.Style%2A> proprietà. Ad esempio, per impostare l'oggetto definito `TitleText` stile in un <xref:System.Windows.Controls.TextBlock> denominato `textblock1`, eseguire le operazioni seguenti:  
  
 [!code-csharp[StylingIntroSample_snippet#Code](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml.cs#code)]
 [!code-vb[StylingIntroSample_snippet#Code](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StylingIntroSample_snippet/visualbasic/window1.xaml.vb#code)]  
  
 Si noti che dopo l'applicazione di uno stile, è sealed e non può essere modificato. Se si desidera modificare dinamicamente uno stile che è già stato applicato, è necessario creare un nuovo stile per sostituire quello esistente. Per ulteriori informazioni, vedere il <xref:System.Windows.Style.IsSealed%2A> proprietà.  
  
 È possibile creare un oggetto che sceglie uno stile da applicare in base alla logica personalizzata. Per un esempio, vedere l'esempio fornito per il <xref:System.Windows.Controls.StyleSelector> (classe).  
  
<a name="styling_binding_dynamicresource"></a>   
### <a name="bindings-dynamic-resources-and-event-handlers"></a>Associazioni, le risorse dinamiche e gestori eventi  
 Si noti che è possibile utilizzare il `Setter.Value` proprietà per specificare un [estensione di Markup Binding](../../../../docs/framework/wpf/advanced/binding-markup-extension.md) o [estensione di Markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md). Per ulteriori informazioni, vedere gli esempi forniti per il <xref:System.Windows.Setter.Value%2A?displayProperty=fullName> proprietà.  
  
 Finora, in questa panoramica vengono illustrati solo l'utilizzo di metodi per impostare il valore di proprietà. È inoltre possibile specificare i gestori eventi in uno stile. Per ulteriori informazioni, vedere <xref:System.Windows.EventSetter>.  
  
<a name="styling_datatemplates"></a>   
## <a name="data-templates"></a>Modelli di dati  
 In questa applicazione di esempio è un <xref:System.Windows.Controls.ListBox> controllo associato a un elenco di foto:  
  
 [!code-xml[StylingIntroSnippet#UIListBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#uilistbox)]  
  
 Questo <xref:System.Windows.Controls.ListBox> attualmente simile al seguente:  
  
 ![ListBox prima dell'applicazione modello](../../../../docs/framework/wpf/controls/media/stylingintro-listboxbefore.png "StylingIntro_ListBoxBefore")  
  
 La maggior parte dei controlli dispongono di un tipo di contenuto e che spesso proviene dai dati che si esegue l'associazione. In questo esempio, i dati sono l'elenco di foto. In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], si utilizza un <xref:System.Windows.DataTemplate> per definire la rappresentazione visiva dei dati. Fondamentalmente, gli elementi inseriti in un <xref:System.Windows.DataTemplate> determina l'aspetto dei dati nell'applicazione sottoposta a rendering.  
  
 Nell'applicazione di esempio, ogni personalizzato `Photo` oggetto ha un `Source` proprietà di tipo stringa che specifica il percorso del file dell'immagine. Attualmente, gli oggetti foto appaiono come percorsi di file.  
  
 Per le foto come immagini, si crea un <xref:System.Windows.DataTemplate> come risorsa:  
  
 [!code-xml[StylingIntroSnippet#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources)]  
[!code-xml[StylingIntroSnippet#DataTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#datatemplate)]  
[!code-xml[StylingIntroSnippet#Resources2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSnippet/CS/window1.xaml#resources2)]  
  
 Si noti che il <xref:System.Windows.DataTemplate.DataType%2A> proprietà è molto simile al <xref:System.Windows.Style.TargetType%2A> proprietà del <xref:System.Windows.Style>. Se il <xref:System.Windows.DataTemplate> è nella sezione delle risorse, quando si specifica il <xref:System.Windows.DataTemplate.DataType%2A> proprietà a un tipo e assegnarlo un `x:Key`, il <xref:System.Windows.DataTemplate> viene applicato ogni volta che viene visualizzato il tipo. È sempre possibile assegnare il <xref:System.Windows.DataTemplate> con un `x:Key` e quindi impostarla come un `StaticResource` per le proprietà che accettano <xref:System.Windows.DataTemplate> tipi, ad esempio il <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> proprietà o <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> proprietà.  
  
 In pratica, il <xref:System.Windows.DataTemplate> nell'esempio precedente definisce che ogni volta che è un `Photo` dell'oggetto, questo deve apparire come un <xref:System.Windows.Controls.Image> all'interno di un <xref:System.Windows.Controls.Border>. Con questo <xref:System.Windows.DataTemplate>, l'applicazione ora è simile al seguente:  
  
 ![Foto](../../../../docs/framework/wpf/controls/media/stylingintro-photosasimages.png "StylingIntro_PhotosAsImages")  
  
 Il modello di applicazione di modelli di dati fornisce altre funzionalità. Ad esempio, se si visualizzano i dati di raccolta che contiene altre raccolte tramite un <xref:System.Windows.Controls.HeaderedItemsControl> digitare ad esempio un <xref:System.Windows.Controls.Menu> o <xref:System.Windows.Controls.TreeView>, esiste il <xref:System.Windows.HierarchicalDataTemplate>. È un'altra funzionalità di <xref:System.Windows.Controls.DataTemplateSelector>, che consente di scegliere un <xref:System.Windows.DataTemplate> da utilizzare in base alla logica personalizzata. Per ulteriori informazioni, vedere [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md), che fornisce una discussione più dettagliata della funzionalità dei modelli di dati diversi.  
  
<a name="styling_controltemplates"></a>   
## <a name="control-templates"></a>Modelli di controllo  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], <xref:System.Windows.Controls.ControlTemplate> definisce l'aspetto del controllo di un controllo. È possibile modificare la struttura e l'aspetto di un controllo mediante la definizione di un nuovo <xref:System.Windows.Controls.ControlTemplate> per il controllo. In molti casi, ciò offre flessibilità sufficiente in modo che non è necessario scrivere controlli personalizzati. Per ulteriori informazioni, vedere [personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
<a name="styling_triggers"></a>   
## <a name="triggers"></a>Trigger  
 Un trigger imposta le proprietà o avvia azioni, ad esempio un'animazione, quando un valore di proprietà viene modificato o quando viene generato un evento. <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, e <xref:System.Windows.DataTemplate> hanno un `Triggers` proprietà che può contenere un set di trigger. Esistono vari tipi di trigger.  
  
### <a name="property-triggers"></a>Trigger di proprietà  
 Oggetto <xref:System.Windows.Trigger> che proprietà set di valori o avviare azioni in base al valore di una proprietà viene chiamato un trigger di proprietà.  
  
 Per illustrare come utilizzare i trigger di proprietà, è possibile rendere ogni <xref:System.Windows.Controls.ListBoxItem> parzialmente trasparente a meno che non è selezionata. Il seguente stile imposta il <xref:System.Windows.UIElement.Opacity%2A> valore di un <xref:System.Windows.Controls.ListBoxItem> a `0.5`. Quando il <xref:System.Windows.Controls.ListBoxItem.IsSelected%2A> è `true`, tuttavia, il <xref:System.Windows.UIElement.Opacity%2A> è impostato su `1.0`:  
  
 [!code-xml[StylingIntroSample_snippet#Triggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#triggers)]  
[!code-xml[StylingIntroSample_snippet#EndTriggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#endtriggers)]  
  
 Questo esempio viene utilizzato un <xref:System.Windows.Trigger> per impostare un valore della proprietà, ma si noti che il <xref:System.Windows.Trigger> classe dispone inoltre di <xref:System.Windows.TriggerBase.EnterActions%2A> e <xref:System.Windows.TriggerBase.ExitActions%2A> le proprietà che consentono a un trigger eseguire azioni.  
  
 Si noti che il <xref:System.Windows.FrameworkElement.MaxHeight%2A> di proprietà di <xref:System.Windows.Controls.ListBoxItem> è impostato su `75`. Nella figura seguente, il terzo elemento è l'elemento selezionato:  
  
 ![Stile del controllo ListView](../../../../docs/framework/wpf/controls/media/stylingintro-triggers.png "StylingIntro_triggers")  
  
### <a name="eventtriggers-and-storyboards"></a>EventTrigger e storyboard  
 Un altro tipo di trigger è il <xref:System.Windows.EventTrigger>, che avvia una serie di azioni in base all'occorrenza di un evento. Seguente, ad esempio, <xref:System.Windows.EventTrigger> oggetti specificano che quando il puntatore del mouse entra il <xref:System.Windows.Controls.ListBoxItem>, il <xref:System.Windows.FrameworkElement.MaxHeight%2A> proprietà aggiunge un'animazione a un valore di `90` su un `0.2` secondo periodo. Quando il puntatore del mouse viene spostato dall'elemento, la proprietà restituisce il valore originale in un periodo di `1` secondo. Si noti come non è necessario specificare un <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> valore per il <xref:System.Windows.ContentElement.MouseLeave> animazione. In questo modo l'animazione è in grado di tenere traccia del valore originale.  
  
 [!code-xml[StylingIntroSample_snippet#EventTriggers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StylingIntroSample_snippet/CSharp/Window1.xaml#eventtriggers)]  
  
 Per ulteriori informazioni, vedere il [Cenni preliminari sugli storyboard](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md).  
  
 Nella figura seguente, il mouse è posizionato al terzo elemento:  
  
 ![Schermata dell'esempio Styling](../../../../docs/framework/wpf/controls/media/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")  
  
### <a name="multitriggers-datatriggers-and-multidatatriggers"></a>MultiTrigger, DataTrigger e MultiDataTrigger  
 Oltre a <xref:System.Windows.Trigger> e <xref:System.Windows.EventTrigger>, esistono altri tipi di trigger. <xref:System.Windows.MultiTrigger> consente di impostare i valori delle proprietà in base a più condizioni. Utilizzare <xref:System.Windows.DataTrigger> e <xref:System.Windows.MultiDataTrigger> quando la proprietà della condizione è associato a dati.  
  
<a name="styling_themes"></a>   
## <a name="shared-resources-and-themes"></a>Risorse condivise e temi  
 Una tipica [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] applicazione potrebbe disporre di più risorse di interfaccia utente che vengono applicate in tutta l'applicazione. Complessivamente, questo set di risorse può essere considerato il tema per l'applicazione. [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]fornisce il supporto per l'assemblaggio risorse di interfaccia utente come un tema utilizzando un dizionario risorse incapsulato come il <xref:System.Windows.ResourceDictionary> (classe).  
  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]i temi sono definiti mediante il meccanismo di stili e modelli che [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] espone per personalizzare gli elementi visivi di qualsiasi elemento.  
  
 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)]le risorse del tema vengono archiviate in dizionari risorse incorporati. Questi dizionari risorse devono essere incorporati all'interno di un assembly firmato e può essere incorporato nello stesso assembly del codice o in un assembly side-by-side. Nel caso di PresentationFramework. dll, l'assembly che contiene [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] controlli, le risorse del tema sono una serie di assembly side-by-side.  
  
 Il tema diventa l'ultimo posto in cui lo stile di un elemento cercare. In genere, la ricerca verrà inizia risalendo la struttura ad albero la ricerca di una risorsa appropriata, quindi cercare nella raccolta di risorse dell'applicazione e infine eseguire query sul sistema. In questo modo gli sviluppatori di applicazioni per ridefinire lo stile per qualsiasi oggetto a livello di struttura ad albero o un'applicazione prima di raggiungere il tema.  
  
 È possibile definire i dizionari risorse come file singoli che consentono di riutilizzare un tema in più applicazioni. È inoltre possibile creare temi scambiabili definendo più dizionari risorse che forniscono gli stessi tipi di risorse ma con valori diversi. La ridefinizione di questi stili o altre risorse a livello di applicazione è l'approccio consigliato per definire l'interfaccia di un'applicazione.  
  
 Per condividere un set di risorse, inclusi gli stili e modelli, tra le applicazioni, è possibile creare un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file e definire un <xref:System.Windows.ResourceDictionary>. Ad esempio, esaminiamo l'illustrazione seguente parte di [Styling with ControlTemplates Sample](http://go.microsoft.com/fwlink/?LinkID=160041):  
  
 ![Esempi di modello di controllo](../../../../docs/framework/wpf/controls/media/stylingintro-controltemplateexamples.png "StylingIntro_ControlTemplateExamples")  
  
 Se si osserva il [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] file dell'esempio, si noterà che tutti i file dispongano i seguenti:  
  
 [!code-xml[ControlTemplateExamples#MergedDictionaries](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/button.xaml#mergeddictionaries)]  
  
 Si tratta della condivisione di `shared.xaml`, che definisce un <xref:System.Windows.ResourceDictionary> che contiene un set di risorse di stile e il pennello ai controlli nell'esempio di avere un aspetto coerente.  
  
 Per ulteriori informazioni, vedere [dizionari risorse uniti](../../../../docs/framework/wpf/advanced/merged-resource-dictionaries.md).  
  
 La creazione di un tema per il controllo personalizzato, vedere la sezione della libreria esterna di controllo della [Control Authoring Overview](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [Procedura: trovare elementi generati da un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/how-to-find-controltemplate-generated-elements.md)   
 [Trovare elementi generati da un DataTemplate](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)