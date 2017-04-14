---
title: "Cenni preliminari sui modelli di dati | Microsoft Docs"
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
  - "associazione dati, modelli"
  - "associazione dati, modelli"
  - "modelli di dati"
  - "modelli di dati"
ms.assetid: 0f4d9f8c-0230-4013-bd7b-e8e7fed01b4a
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Cenni preliminari sui modelli di dati
Il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] modello ai modelli di dati offre una notevole flessibilità per definire la presentazione dei dati. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]controlli dispongono di funzionalità incorporate per supportare la personalizzazione della presentazione dei dati. In questo argomento viene illustrato innanzitutto come definire un <xref:System.Windows.DataTemplate> e vengono presentate altre funzionalità di modello di dati, ad esempio la selezione di modelli in base a logica personalizzata e il supporto per la visualizzazione di dati gerarchici.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="Prerequisites"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 In questo argomento è incentrato sulle funzionalità dei modelli dati e non viene fornita un'introduzione dei concetti di associazione dati. Per informazioni sui concetti relativi all'associazione dati di base, vedere il [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 <xref:System.Windows.DataTemplate> riguarda la presentazione dei dati ed è una delle numerose funzionalità fornite da di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] modello di stili e modelli. Per un'introduzione di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] modello di stili e modelli, ad esempio come utilizzare un <xref:System.Windows.Style> per impostare le proprietà sui controlli, vedere il [di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md) argomento.  
  
 Inoltre, è importante comprendere `Resources`, che sono essenzialmente ciò che consentono ad esempio oggetti <xref:System.Windows.Style> e <xref:System.Windows.DataTemplate> per essere riutilizzati. Per ulteriori informazioni sulle risorse, vedere [risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
<a name="DataTemplating_Basic"></a>   
## <a name="data-templating-basics"></a>Nozioni fondamentali sui modelli di dati  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
 Per illustrare il motivo <xref:System.Windows.DataTemplate> è importante, passiamo a esaminare un esempio di associazione dati. In questo esempio, abbiamo un <xref:System.Windows.Controls.ListBox> associato a un elenco di `Task` oggetti. Ogni `Task` oggetto ha un `TaskName` (stringa), un `Description` (stringa), un `Priority` (int) e una proprietà di tipo `TaskType`, ovvero un `Enum` con valori `Home` e `Work`.  
  
 [!code-xml[DataTemplatingIntro_snip#Resources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#resources)]  
[!code-xml[DataTemplatingIntro_snip#UI1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui1)]  
[!code-xml[DataTemplatingIntro_snip#UI2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui2)]  
  
<a name="without_a_datatemplate"></a>   
### <a name="without-a-datatemplate"></a>Senza un DataTemplate  
 Senza un <xref:System.Windows.DataTemplate>, il nostro <xref:System.Windows.Controls.ListBox> attualmente è simile al seguente:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig1.png "DataTemplatingIntro_fig1")  
  
 Qual è il problema è che senza istruzioni specifiche, il <xref:System.Windows.Controls.ListBox> per impostazione predefinita chiama `ToString` quando si tenta di visualizzare gli oggetti nella raccolta. Pertanto, se il `Task` esegue l'override dell'oggetto di `ToString` (metodo), il <xref:System.Windows.Controls.ListBox> consente di visualizzare la rappresentazione di stringa di ogni oggetto di origine nella raccolta sottostante.  
  
 Ad esempio, se il `Task` classe esegue l'override di `ToString` metodo in questo modo, in cui `name` è il campo per il `TaskName` proprietà:  
  
 [!code-csharp[DataTemplatingIntro_snip#ToString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Data.cs#tostring)]
 [!code-vb[DataTemplatingIntro_snip#ToString](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/data.vb#tostring)]  
  
 Il <xref:System.Windows.Controls.ListBox> simile al seguente:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig2.png "DataTemplatingIntro_fig2")  
  
 Tuttavia, che è limitante e poco flessibile. Inoltre, se si desidera associare a [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] dati, non sarà possibile eseguire l'override `ToString`.  
  
<a name="defining_simple_datatemplate"></a>   
### <a name="defining-a-simple-datatemplate"></a>Definizione di DataTemplate semplice  
 La soluzione consiste nel definire un <xref:System.Windows.DataTemplate>. Un modo per farlo consiste nell'impostare il <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> proprietà del <xref:System.Windows.Controls.ListBox> per un <xref:System.Windows.DataTemplate>. Specificare nel <xref:System.Windows.DataTemplate> diventa la struttura visiva dell'oggetto dati. Nell'esempio <xref:System.Windows.DataTemplate> è piuttosto semplice. Vengono fornite istruzioni che ogni elemento viene visualizzato come tre <xref:System.Windows.Controls.TextBlock> elementi all'interno di un <xref:System.Windows.Controls.StackPanel>. Ogni <xref:System.Windows.Controls.TextBlock> elemento è associato a una proprietà del `Task` (classe).  
  
 [!code-xml[DataTemplatingIntro_snip#Inline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#inline)]  
  
 I dati sottostanti per gli esempi in questo argomento sono una raccolta di [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] oggetti. Se si esegue l'associazione [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] dati, i concetti fondamentali sono uguali, ma esiste una leggera differenza sintattica. Ad esempio, anziché `Path=TaskName`, è necessario impostare <xref:System.Windows.Data.Binding.XPath%2A> a `@TaskName` (se `TaskName` è un attributo del [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] nodo).  
  
 Ora il nostro <xref:System.Windows.Controls.ListBox> simile al seguente:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig3.png "DataTemplatingIntro_fig3")  
  
<a name="defining_datatemplate_as_a_resource"></a>   
### <a name="creating-the-datatemplate-as-a-resource"></a>Creazione di DataTemplate come una risorsa  
 Nell'esempio precedente è stato definito il <xref:System.Windows.DataTemplate> inline. È più comune definire nella sezione delle risorse può essere un oggetto riutilizzabile, come nell'esempio seguente:  
  
 [!code-xml[DataTemplatingIntro_snip#R1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]  
[!code-xml[DataTemplatingIntro_snip#AsResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#asresource)]  
[!code-xml[DataTemplatingIntro_snip#R2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]  
  
 Ora è possibile utilizzare `myTaskTemplate` come una risorsa, come nell'esempio seguente:  
  
 [!code-xml[DataTemplatingIntro_snip#MyTaskTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#mytasktemplate)]  
  
 Poiché `myTaskTemplate` è una risorsa, è possibile utilizzarlo in altri controlli che dispongono di una proprietà che accetta un <xref:System.Windows.DataTemplate> tipo. Come illustrato in precedenza, per <xref:System.Windows.Controls.ItemsControl> oggetti, ad esempio il <xref:System.Windows.Controls.ListBox>, è il <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> proprietà. Per <xref:System.Windows.Controls.ContentControl> oggetti, è il <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> proprietà.  
  
<a name="Styling_DataType"></a>   
### <a name="the-datatype-property"></a>La proprietà DataType  
 Il <xref:System.Windows.DataTemplate> classe dispone di un <xref:System.Windows.DataTemplate.DataType%2A> proprietà che è molto simile al <xref:System.Windows.Style.TargetType%2A> proprietà del <xref:System.Windows.Style> (classe). Pertanto, anziché specificare un `x:Key` per il <xref:System.Windows.DataTemplate> nell'esempio precedente, è possibile eseguire le operazioni seguenti:  
  
 [!code-xml[DataTemplatingIntro_snip#DataType](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#datatype)]  
  
 Questo <xref:System.Windows.DataTemplate> viene applicata automaticamente a tutti `Task` oggetti. Si noti che in questo caso il `x:Key` è impostato in modo implicito. Pertanto, se si assegna a questo <xref:System.Windows.DataTemplate> un `x:Key` valore, si esegue l'override implicita `x:Key` e <xref:System.Windows.DataTemplate> non viene applicato automaticamente.  
  
 Se si associa un <xref:System.Windows.Controls.ContentControl> a una raccolta di `Task` oggetti, il <xref:System.Windows.Controls.ContentControl> non utilizza il comando precedente <xref:System.Windows.DataTemplate> automaticamente. Infatti, l'associazione in un <xref:System.Windows.Controls.ContentControl> richiede ulteriori informazioni per distinguere se si desidera associare a un intero insieme o i singoli oggetti. Se il <xref:System.Windows.Controls.ContentControl> sta rilevando la selezione di un <xref:System.Windows.Controls.ItemsControl> tipo, è possibile impostare il <xref:System.Windows.Data.Binding.Path%2A> proprietà del <xref:System.Windows.Controls.ContentControl> associazione a "`/`" per indicare che si è interessati all'elemento corrente. Per un esempio, vedere [associare a una raccolta e visualizzare informazioni in base alla selezione](../../../../docs/framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md). In caso contrario, è necessario specificare il <xref:System.Windows.DataTemplate> in modo esplicito, impostando il <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> proprietà.  
  
 Il <xref:System.Windows.DataTemplate.DataType%2A> proprietà è particolarmente utile quando si dispone di un <xref:System.Windows.Data.CompositeCollection> di diversi tipi di oggetti dati. Per un esempio, vedere [implementare un oggetto CompositeCollection](../../../../docs/framework/wpf/data/how-to-implement-a-compositecollection.md).  
  
<a name="adding_more_to_datatemplate"></a>   
## <a name="adding-more-to-the-datatemplate"></a>Aggiunta di più a DataTemplate  
 Attualmente i dati vengono visualizzati con le informazioni necessarie, ma esiste senz'altro margine di miglioramento. Di seguito verrà migliorata la presentazione aggiungendo un <xref:System.Windows.Controls.Border>, <xref:System.Windows.Controls.Grid>e alcuni <xref:System.Windows.Controls.TextBlock> elementi che descrivono i dati da visualizzare.  
  
 [!code-xml[DataTemplatingIntro#AddingMore](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore)]  
[!code-xml[DataTemplatingIntro#AddingMore2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]  
  
 La schermata seguente mostra il <xref:System.Windows.Controls.ListBox> con questa modifica <xref:System.Windows.DataTemplate>:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig4.png "DataTemplatingIntro_fig4")  
  
 È possibile impostare <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> a <xref:System.Windows.HorizontalAlignment> sul <xref:System.Windows.Controls.ListBox> per assicurarsi che la larghezza degli elementi occupi l'intero spazio:  
  
 [!code-xml[DataTemplatingIntro_snip#Stretch](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#stretch)]  
  
 Con il <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> impostata su <xref:System.Windows.HorizontalAlignment>, <xref:System.Windows.Controls.ListBox> ora simile al seguente:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig5.png "DataTemplatingIntro_fig5")  
  
<a name="DataTrigger_to_Apply_Property_Values"></a>   
### <a name="use-datatriggers-to-apply-property-values"></a>Utilizzo di DataTrigger per applicare valori di proprietà  
 La presentazione corrente viene indicato se un `Task` è un'attività principale o un'attività di office. Tenere presente che il `Task` oggetto ha un `TaskType` proprietà di tipo `TaskType`, che costituisce un'enumerazione con i valori `Home` e `Work`.  
  
 Nell'esempio seguente, il <xref:System.Windows.DataTrigger> imposta il <xref:System.Windows.Controls.Border.BorderBrush%2A> dell'elemento denominato `border` a `Yellow` se il `TaskType` è `TaskType.Home`.  
  
 [!code-xml[DataTemplatingIntro#DT](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#dt)]  
[!code-xml[DataTemplatingIntro#DataTrigger](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#datatrigger)]  
[!code-xml[DataTemplatingIntro#AddingMore2](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]  
  
 L'applicazione ora è simile al seguente. Principali attività visualizzati con un bordo giallo e le attività di office con un bordo azzurro:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig6.png "DataTemplatingIntro_fig6")  
  
 In questo esempio il <xref:System.Windows.DataTrigger> utilizza un <xref:System.Windows.Setter> per impostare un valore della proprietà. Le classi trigger dispongono inoltre di <xref:System.Windows.TriggerBase.EnterActions%2A> e <xref:System.Windows.TriggerBase.ExitActions%2A> le proprietà che consentono di avviare un set di azioni, ad esempio animazioni. Inoltre, è inoltre disponibile un <xref:System.Windows.MultiDataTrigger> classe che consente di applicare le modifiche basate su più valori di proprietà con associazione a dati.  
  
 Un modo alternativo per ottenere lo stesso risultato consiste nell'associare il <xref:System.Windows.Controls.Border.BorderBrush%2A> proprietà per il `TaskType` proprietà e utilizzare un convertitore di valori per restituire il colore in base il `TaskType` valore. Creazione dell'effetto precedente utilizzando un convertitore è leggermente più efficiente in termini di prestazioni. Inoltre, la creazione di un convertitore personalizzato offre maggiore flessibilità poiché di fornire la logica personalizzata. In definitiva, la scelta dipende dallo scenario e le preferenze. Per informazioni su come scrivere un convertitore, vedere <xref:System.Windows.Data.IValueConverter>.  
  
<a name="what_belongs_in_datatemplate"></a>   
### <a name="what-belongs-in-a-datatemplate"></a>Cosa appartiene un DataTemplate?  
 Nell'esempio precedente, è stato inserito il trigger all'interno di <xref:System.Windows.DataTemplate> utilizzando il <xref:System.Windows.DataTemplate>.<xref:System.Windows.DataTemplate.Triggers%2A> proprietà. Il <xref:System.Windows.Setter> del trigger imposta il valore di una proprietà di un elemento (il <xref:System.Windows.Controls.Border> elemento) che si trova all'interno di <xref:System.Windows.DataTemplate>. Tuttavia, se le proprietà che il `Setters` si occupano della non sono proprietà degli elementi che sono all'interno dell'oggetto <xref:System.Windows.DataTemplate>, può essere più appropriato impostare le proprietà utilizzando un <xref:System.Windows.Style> per il <xref:System.Windows.Controls.ListBoxItem> classe (se il controllo si associa un <xref:System.Windows.Controls.ListBox>). Ad esempio, se si desidera che il <xref:System.Windows.Trigger> per animare il <xref:System.Windows.UIElement.Opacity%2A> valore dell'elemento quando si posiziona il mouse su un elemento, si definiscono trigger all'interno di un <xref:System.Windows.Controls.ListBoxItem> stile. Per un esempio, vedere il [Introduzione agli stili e modelli](http://go.microsoft.com/fwlink/?LinkID=160010).  
  
 In generale, tenere presente che il <xref:System.Windows.DataTemplate> viene applicata a ogni oggetto generato <xref:System.Windows.Controls.ListBoxItem> (per ulteriori informazioni su come e dove viene effettivamente applicato, vedere il <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> pagina.). Il <xref:System.Windows.DataTemplate> riguarda esclusivamente la presentazione e l'aspetto degli oggetti dati. Nella maggior parte dei casi, tutti gli altri aspetti della presentazione, ad esempio che cos'è un elemento simile a quando è selezionata o il <xref:System.Windows.Controls.ListBox> definisce gli elementi, non fanno parte della definizione di un <xref:System.Windows.DataTemplate>. Per un esempio, vedere il [stili e modelli di ItemsControl](#DataTemplating_ItemsControl) sezione.  
  
<a name="Styling_StyleSelection"></a>   
## <a name="choosing-a-datatemplate-based-on-properties-of-the-data-object"></a>Scelta di DataTemplate in base alle proprietà dell'oggetto dati  
 In [la proprietà DataType](#Styling_DataType) sezione discussa che è possibile definire modelli di dati diversi per gli oggetti dati diversi. Che risulta particolarmente utile quando si dispone di un <xref:System.Windows.Data.CompositeCollection> di diversi tipi o insiemi con elementi di tipi diversi. Nel [utilizzare DataTrigger per applicare valori di proprietà](#DataTrigger_to_Apply_Property_Values) sezione, è stato illustrato che se si dispone di una raccolta dello stesso tipo di oggetti dati è possibile creare un <xref:System.Windows.DataTemplate> e quindi utilizzare i trigger per applicare le modifiche in base ai valori di proprietà di ogni oggetto dati. Tuttavia, i trigger consentono di applicare i valori delle proprietà o avviare le animazioni ma non offrono la flessibilità necessaria per ricostruire la struttura degli oggetti dati. Alcuni scenari potrebbero essere necessario creare un altro <xref:System.Windows.DataTemplate> per dati gli oggetti dello stesso tipo, ma proprietà diverse.  
  
 Ad esempio, quando un `Task` oggetto ha un `Priority` valore `1`, si consiglia di fornire un aspetto completamente diverso per fungere da un avviso. In tal caso, si crea un <xref:System.Windows.DataTemplate> per la visualizzazione di priorità elevata `Task` oggetti. Aggiungere il seguente <xref:System.Windows.DataTemplate> alla sezione risorse:  
  
 [!code-xml[DataTemplatingIntro_snip#ImportantTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#importanttemplate)]  
  
 Si noti nell'esempio viene utilizzata la <xref:System.Windows.DataTemplate>.<xref:System.Windows.FrameworkTemplate.Resources%2A> proprietà. Risorse definite in questa sezione sono condivise dagli elementi all'interno di <xref:System.Windows.DataTemplate>.  
  
 Per fornire la logica per scegliere quale <xref:System.Windows.DataTemplate> da utilizzare dipende il `Priority` valore dell'oggetto dati, creare una sottoclasse di <xref:System.Windows.Controls.DataTemplateSelector> ed eseguire l'override di <xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> (metodo). Nell'esempio seguente, il <xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> metodo fornisce la logica per restituire il modello appropriato in base al valore della `Priority` proprietà. Il modello da restituire viene trovato nelle risorse di busta <xref:System.Windows.Window> elemento.  
  
 [!code-csharp[DataTemplatingIntro_snip#DTSClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/TaskListDataTemplateSelector.cs#dtsclass)]
 [!code-vb[DataTemplatingIntro_snip#DTSClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/tasklistdatatemplateselector.vb#dtsclass)]  
  
 È quindi possibile dichiarare il `TaskListDataTemplateSelector` come risorsa:  
  
 [!code-xml[DataTemplatingIntro_snip#R1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]  
[!code-xml[DataTemplatingIntro_snip#DTS](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#dts)]  
[!code-xml[DataTemplatingIntro_snip#R2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]  
  
 Per utilizzare la risorsa selettore di modello, assegnare il <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A> proprietà del <xref:System.Windows.Controls.ListBox>. Il <xref:System.Windows.Controls.ListBox> chiamate di <xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> metodo il `TaskListDataTemplateSelector` per ognuno degli elementi nella raccolta sottostante. La chiamata passa l'oggetto dati come parametro dell'elemento. Il <xref:System.Windows.DataTemplate> restituito dal metodo viene quindi applicato all'oggetto dati.  
  
 [!code-xml[DataTemplatingIntro_snip#ItemTemplateSelector](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemtemplateselector)]  
  
 Il selettore di modello sul posto, il <xref:System.Windows.Controls.ListBox> viene visualizzato come segue:  
  
 ![Esempio schermata to Data templating](../../../../docs/framework/wpf/data/media/datatemplatingintro-fig7.png "DataTemplatingIntro_fig7")  
  
 Questa operazione conclude la discussione di questo esempio. Per l'esempio completo, vedere [Introduction to Data Templating Sample](http://go.microsoft.com/fwlink/?LinkID=160009).  
  
<a name="DataTemplating_ItemsControl"></a>   
## <a name="styling-and-templating-an-itemscontrol"></a>Applicazione di stili e modelli di ItemsControl  
 Anche se il <xref:System.Windows.Controls.ItemsControl> non è l'unico tipo di controllo che è possibile utilizzare un <xref:System.Windows.DataTemplate> , è uno scenario molto comune per associare un <xref:System.Windows.Controls.ItemsControl> a una raccolta. Nel [cosa appartiene un DataTemplate](#what_belongs_in_datatemplate) sezione è stato illustrato che la definizione di <xref:System.Windows.DataTemplate> solo devono essere prese in considerazione la presentazione dei dati. Per sapere quando non è consigliabile utilizzare un <xref:System.Windows.DataTemplate> è importante comprendere le diverse proprietà di stile e modello fornite dal <xref:System.Windows.Controls.ItemsControl>. Nell'esempio seguente è progettato per illustrare la funzione di ciascuna di queste proprietà. Il <xref:System.Windows.Controls.ItemsControl> in questo esempio è associato allo stesso `Tasks` insieme come nell'esempio precedente. A scopo dimostrativo, gli stili e modelli in questo esempio sono tutti dichiarati inline.  
  
 [!code-xml[DataTemplatingIntro_snip#ItemsControlProperties](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemscontrolproperties)]  
  
 Di seguito è riportata una schermata dell'esempio quando viene sottoposto a rendering:  
  
 ![Schermata di esempio ItemsControl](../../../../docs/framework/wpf/data/media/databinding-itemscontrolproperties.png "DataBinding_ItemsControlProperties")  
  
 Si noti che invece di utilizzare il <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>, è possibile utilizzare il <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A>. Vedere la sezione precedente per un esempio. Analogamente, anziché utilizzare il <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>, è possibile utilizzare il <xref:System.Windows.Controls.ItemsControl.ItemContainerStyleSelector%2A>.  
  
 Due altre proprietà correlate allo stile di <xref:System.Windows.Controls.ItemsControl> che non sono illustrate di seguito sono <xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> e <xref:System.Windows.Controls.ItemsControl.GroupStyleSelector%2A>.  
  
<a name="DataTemplating_HeirarchicalDataTemplate"></a>   
## <a name="support-for-hierarchical-data"></a>Supporto per i dati gerarchici  
 Finora sono state analizzate unicamente associare e visualizzare una singola raccolta. A volte è necessario una raccolta che contiene altre raccolte. Il <xref:System.Windows.HierarchicalDataTemplate> classe è progettata per essere utilizzato con <xref:System.Windows.Controls.HeaderedItemsControl> tipi per visualizzare tali dati. Nell'esempio seguente, `ListLeagueList` è un elenco di `League` oggetti. Ogni `League` oggetto ha un `Name` e una raccolta di `Division` oggetti. Ogni `Division` ha un `Name` e una raccolta di `Team` oggetti e ogni `Team` oggetto ha un `Name`.  
  
 [!code-xml[HierarchicalDataTemplateSnippet#HDT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HierarchicalDataTemplateSnippet/CS/window1.xaml#hdt)]  
  
 Nell'esempio viene illustrato che con l'utilizzo di <xref:System.Windows.HierarchicalDataTemplate>, è possibile visualizzare facilmente i dati dell'elenco che contiene altri elenchi. Di seguito è riportata una schermata dell'esempio.  
  
 ![Schermata di esempio HierarchicalDataTemplate](../../../../docs/framework/wpf/data/media/databinding-hierarchicaldatatemplate.png "DataBinding_HierarchicalDataTemplate")  
  
## <a name="see-also"></a>Vedere anche  
 [Associazione dati](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [Trovare elementi generati da un DataTemplate](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)   
 [Stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Cenni preliminari sui modelli e stili di intestazione di colonna GridView](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md)