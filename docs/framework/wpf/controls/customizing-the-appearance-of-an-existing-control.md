---
title: "Personalizzazione dell&#39;aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate | Microsoft Docs"
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
  - "contratto di controllo [WPF]"
  - "controlli [WPF], aspetto specificato dallo stato"
  - "controlli [WPF], modifiche della struttura visiva"
  - "ControlTemplate [WPF], personalizzazione di controlli esistenti"
  - "creazione di interfacce di controlli [WPF]"
  - "modelli [WPF], personalizzazione di controlli esistenti"
ms.assetid: 678dd116-43a2-4b8c-82b5-6b826f126e31
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Personalizzazione dell&#39;aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate
<a name="introduction"></a> Un oggetto <xref:System.Windows.Controls.ControlTemplate> specifica la struttura visuale e il comportamento visivo di un controllo.  È possibile personalizzare l'aspetto di un controllo assegnando al controllo un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate>.  La creazione di un oggetto <xref:System.Windows.Controls.ControlTemplate> determina la sostituzione dell'aspetto di un controllo esistente senza tuttavia modificarne le funzionalità.  È ad esempio possibile creare pulsanti dell'applicazione rotondi anziché con la forma quadrata predefinita, ma il pulsante genererà comunque l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  
  
 In questo argomento vengono descritte le diverse parti di un oggetto <xref:System.Windows.Controls.ControlTemplate>, viene spiegato come creare un oggetto <xref:System.Windows.Controls.ControlTemplate> semplice per <xref:System.Windows.Controls.Button> e come comprendere il contratto di controllo di un controllo in modo da personalizzarne l'aspetto.  Poiché si crea un oggetto <xref:System.Windows.Controls.ControlTemplate> in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], è possibile modificare l'aspetto di un controllo senza ricorrere alla scrittura di codice.  È inoltre possibile utilizzare una finestra di progettazione, quale Microsoft Expression Blend, per creare modelli di controllo personalizzato.  In questo argomento vengono illustrati esempi in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] che consentono di personalizzare l'aspetto di un oggetto <xref:System.Windows.Controls.Button>. Alla fine dell'argomento viene inoltre riportato l'esempio completo.  Per ulteriori informazioni sull'utilizzo di Expression Blend, vedere [Applicazione di stili a un controllo che supporta modelli](http://go.microsoft.com/fwlink/?LinkId=161153).  
  
 Nelle immagini seguenti viene illustrato un oggetto <xref:System.Windows.Controls.Button> che utilizza l'oggetto <xref:System.Windows.Controls.ControlTemplate> creato in questo argomento.  
  
 ![Pulsante con un modello di controllo personalizzato.](../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP\_ButtonNormal")  
Pulsante che utilizza un modello di controllo personalizzato  
  
 ![Pulsante con un bordo rosso.](../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP\_ButtonMouseOver")  
Pulsante che utilizza un modello di controllo personalizzato sul quale è posizionato il puntatore del mouse  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si suppone che l'utente sia in grado di creare e utilizzare controlli e stili come descritto in [Controlli](../../../../docs/framework/wpf/controls/index.md).  I concetti presentati in questo argomento si applicano agli elementi che ereditano dalla classe <xref:System.Windows.Controls.Control>, tranne per l'oggetto <xref:System.Windows.Controls.UserControl>.  Non è possibile applicare <xref:System.Windows.Controls.ControlTemplate> a un oggetto <xref:System.Windows.Controls.UserControl>.  
  
<a name="when_you_should_create_a_controltemplate"></a>   
## Quando è necessario creare un oggetto ControlTemplate  
 I controlli dispongono di molte proprietà, ad esempio <xref:System.Windows.Controls.Border.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A> e <xref:System.Windows.Controls.Control.FontFamily%2A>, che è possibile impostare per specificare aspetti diversi del controllo, sebbene l'impostazione di queste proprietà consenta tuttavia di apportare modifiche limitate.  È ad esempio possibile impostare la proprietà <xref:System.Windows.Controls.Control.Foreground%2A> su blu e <xref:System.Windows.Controls.Control.FontStyle%2A> su corsivo in un oggetto <xref:System.Windows.Controls.CheckBox>.  
  
 Senza la possibilità di creare un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> per i controlli, tutti i controlli di tutte le applicazioni basate su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] avrebbero lo stesso aspetto generale, condizione che non permetterebbe di creare un'applicazione con aspetto personalizzato.  Per impostazione predefinita, tutti gli oggetti <xref:System.Windows.Controls.CheckBox> hanno caratteristiche simili.  Il contenuto di <xref:System.Windows.Controls.CheckBox> è ad esempio sempre a destra dell'indicatore di selezione e il segno di spunta viene sempre utilizzato per indicare che l'oggetto <xref:System.Windows.Controls.CheckBox> è selezionato.  
  
 Un oggetto <xref:System.Windows.Controls.ControlTemplate> viene creato quando si desidera personalizzare ulteriormente l'aspetto del controllo rispetto a quanto è consentito dall'impostazione delle altre proprietà.  Nell'esempio di <xref:System.Windows.Controls.CheckBox> si supponga che si desideri posizionare il contenuto della casella di controllo sopra l'indicatore di selezione e che si desideri utilizzare una X per indicare che l'oggetto <xref:System.Windows.Controls.CheckBox> è selezionato.  È possibile specificare queste modifiche nell'oggetto <xref:System.Windows.Controls.ControlTemplate> dell'oggetto <xref:System.Windows.Controls.CheckBox>.  
  
 Nell'immagine seguente viene illustrato un oggetto <xref:System.Windows.Controls.CheckBox> che utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito.  
  
 ![Casella di controllo con il modello di controllo predefinito.](../../../../docs/framework/wpf/controls/media/ndp-checkboxdefault.png "NDP\_CheckBoxDefault")  
Oggetto CheckBox che utilizza il modello di controllo predefinito  
  
 Nell'immagine seguente viene illustrato un oggetto <xref:System.Windows.Controls.CheckBox> che utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> personalizzato per posizionare il contenuto dell'oggetto <xref:System.Windows.Controls.CheckBox> sopra l'indicatore di selezione e visualizzare una X quando l'oggetto <xref:System.Windows.Controls.CheckBox> è selezionato.  
  
 ![Casella di controllo con un modello di controllo personalizzato.](../../../../docs/framework/wpf/controls/media/ndp-checkboxcustom.png "NDP\_CheckBoxCustom")  
Oggetto CheckBox che utilizza un modello di controllo personalizzato  
  
 L'oggetto <xref:System.Windows.Controls.ControlTemplate> per l'oggetto <xref:System.Windows.Controls.CheckBox> di questo esempio è relativamente complesso, pertanto in questo argomento verrà utilizzato un esempio di creazione di <xref:System.Windows.Controls.ControlTemplate> più semplice per <xref:System.Windows.Controls.Button>.  
  
<a name="changing_the_visual_structure_of_a_control"></a>   
## Modifica della struttura visuale di un controllo  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] un controllo è spesso costituito da oggetti <xref:System.Windows.FrameworkElement> compositi.  Quando si crea un oggetto <xref:System.Windows.Controls.ControlTemplate>, gli oggetti <xref:System.Windows.FrameworkElement> vengono combinati in modo da compilare un singolo controllo.  Un oggetto <xref:System.Windows.Controls.ControlTemplate> deve disporre di un solo <xref:System.Windows.FrameworkElement> come elemento radice corrispondente.  L'elemento radice contiene in genere altri oggetti <xref:System.Windows.FrameworkElement>.  La combinazione di oggetti costituisce la struttura visuale del controllo.  
  
 Nell'esempio seguente viene creato un oggetto <xref:System.Windows.Controls.ControlTemplate> personalizzato per <xref:System.Windows.Controls.Button>.  <xref:System.Windows.Controls.ControlTemplate> crea la struttura visuale di <xref:System.Windows.Controls.Button>.  In questo esempio l'aspetto del pulsante non cambia quando si posiziona il puntatore del mouse o si fa clic su di esso.  La modifica dell'aspetto del pulsante quando il pulsante si trova in uno stato diverso viene illustrata più avanti in questo argomento.  
  
 In questo esempio la struttura visuale consiste nelle parti seguenti:  
  
-   Un oggetto <xref:System.Windows.Controls.Border> denominato `RootElement` che ha la funzione di oggetto <xref:System.Windows.FrameworkElement> radice del modello.  
  
-   Un oggetto <xref:System.Windows.Controls.Grid> figlio di `RootElement`.  
  
-   Un oggetto <xref:System.Windows.Controls.ContentPresenter> che visualizza il contenuto del pulsante.  <xref:System.Windows.Controls.ContentPresenter> consente la visualizzazione di qualsiasi tipo di oggetto.  
  
 [!code-xml[VSMButtonTemplate#BasicTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#basictemplate)]  
  
### Mantenimento delle funzionalità delle proprietà di un controllo tramite TemplateBinding  
 Quando si crea un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate>, è possibile che si desideri continuare a utilizzare le proprietà pubbliche per modificare l'aspetto del controllo.  L'estensione di markup [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) associa una proprietà di un elemento in <xref:System.Windows.Controls.ControlTemplate> a una proprietà pubblica definita dal controllo.  Quando si utilizza [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md), si consente alle proprietà sul controllo di fungere da parametri per il modello.  Ossia, quando viene impostata una proprietà di un controllo, tale valore viene passato all'elemento che presenta [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md).  
  
 Nell'esempio seguente viene ripetuta la parte dell'esempio precedente in cui viene utilizzata l'estensione di markup [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) per associare le proprietà degli elementi in <xref:System.Windows.Controls.ControlTemplate> a proprietà pubbliche definite dal pulsante.  
  
 [!code-xml[VSMButtonTemplate#TemplateBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#templatebinding)]  
  
 In questo esempio la proprietà <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=fullName> dell'oggetto <xref:System.Windows.Controls.Grid> è associata a <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> tramite un modello.  Poiché la proprietà <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=fullName> è associata al modello, è possibile creare più pulsanti che utilizzano lo stesso oggetto <xref:System.Windows.Controls.ControlTemplate> e impostare <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> su valori diversi per ogni pulsante.  Se <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> non fosse associata tramite un modello a una proprietà di un elemento in <xref:System.Windows.Controls.ControlTemplate>, l'impostazione della proprietà <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> di un pulsante non determinerebbe alcun effetto sull'aspetto del pulsante.  
  
 Si noti che non è necessario che i nomi delle due proprietà siano identici.  Nell'esempio precedente la proprietà <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=fullName> dell'oggetto <xref:System.Windows.Controls.Button> è associata alla proprietà <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=fullName> dell'oggetto <xref:System.Windows.Controls.ContentPresenter> tramite un modello.  In questo modo il contenuto del pulsante può essere posizionato orizzontalmente.  <xref:System.Windows.Controls.ContentPresenter> non dispone di una proprietà denominata `HorizontalContentAlignment`, ma la proprietà <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=fullName> può essere associata a <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=fullName>.  Quando si associa una proprietà tramite un modello, verificare che le proprietà di destinazione e di origine siano dello stesso tipo.  
  
 La classe <xref:System.Windows.Controls.Control> definisce diverse proprietà che devono essere utilizzate dal modello del controllo per produrre un effetto sul controllo quando vengono impostate.  La modalità di utilizzo della proprietà da parte di <xref:System.Windows.Controls.ControlTemplate> dipende dalla proprietà.  L'oggetto <xref:System.Windows.Controls.ControlTemplate> deve utilizzare la proprietà in uno dei modi seguenti:  
  
-   Un elemento incluso nel modello <xref:System.Windows.Controls.ControlTemplate> viene associato alla proprietà.  
  
-   Un elemento incluso nel modello <xref:System.Windows.Controls.ControlTemplate> eredita la proprietà da un oggetto <xref:System.Windows.FrameworkElement> padre.  
  
 Nella tabella seguente vengono elencate le proprietà visive ereditate da un controllo dalla classe <xref:System.Windows.Controls.Control>.  Viene inoltre indicato se il modello predefinito di un controllo utilizza il valore della proprietà ereditato o se deve essere associato a un modello.  
  
|Proprietà|Metodo di utilizzo|  
|---------------|------------------------|  
|<xref:System.Windows.Controls.Control.Background%2A>|Associazione al modello|  
|<xref:System.Windows.Controls.Control.BorderThickness%2A>|Associazione al modello|  
|<xref:System.Windows.Controls.Control.BorderBrush%2A>|Associazione al modello|  
|<xref:System.Windows.Controls.Control.FontFamily%2A>|Ereditarietà della proprietà o associazione al modello|  
|<xref:System.Windows.Controls.Control.FontSize%2A>|Ereditarietà della proprietà o associazione al modello|  
|<xref:System.Windows.Controls.Control.FontStretch%2A>|Ereditarietà della proprietà o associazione al modello|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|Ereditarietà della proprietà o associazione al modello|  
|<xref:System.Windows.Controls.Control.Foreground%2A>|Ereditarietà della proprietà o associazione al modello|  
|<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>|Associazione al modello|  
|<xref:System.Windows.Controls.Control.Padding%2A>|Associazione al modello|  
|<xref:System.Windows.Controls.Control.VerticalContentAlignment%2A>|Associazione al modello|  
  
 Nella tabella sono elencate solo le proprietà visive ereditate da un controllo dalla classe <xref:System.Windows.Controls.Control>.  Fatta eccezione per le proprietà elencate nella tabella, un controllo può inoltre ereditare le proprietà <xref:System.Windows.FrameworkElement.DataContext%2A>, <xref:System.Windows.FrameworkElement.Language%2A> e <xref:System.Windows.Controls.TextBlock.TextDecorations%2A> dall'elemento del framework padre.  
  
 Inoltre, se <xref:System.Windows.Controls.ContentPresenter> è incluso nell'oggetto <xref:System.Windows.Controls.ControlTemplate> di un oggetto <xref:System.Windows.Controls.ContentControl>, <xref:System.Windows.Controls.ContentPresenter> verrà associato automaticamente alle proprietà <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> e <xref:System.Windows.Controls.ContentControl.Content%2A>.  In modo analogo, un oggetto <xref:System.Windows.Controls.ItemsPresenter> incluso nell'oggetto <xref:System.Windows.Controls.ControlTemplate> di <xref:System.Windows.Controls.ItemsControl> verrà associato automaticamente alle proprietà <xref:System.Windows.Controls.ItemsControl.Items%2A> e <xref:System.Windows.Controls.ItemsPresenter>.  
  
 Nell'esempio seguente vengono creati due pulsanti che utilizzano l'oggetto <xref:System.Windows.Controls.ControlTemplate> definito nell'esempio precedente.  Nell'esempio vengono impostate le proprietà <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Foreground%2A> e <xref:System.Windows.Controls.Control.FontSize%2A> su ogni pulsante.  L'impostazione della proprietà <xref:System.Windows.Controls.Control.Background%2A> ha effetto poiché è associata al modello in <xref:System.Windows.Controls.ControlTemplate>.  Anche se le proprietà <xref:System.Windows.Controls.Control.Foreground%2A> e <xref:System.Windows.Controls.Control.FontSize%2A> non sono associate al modello, la loro impostazione ha effetto in quanto i valori corrispondenti vengono ereditati.  
  
 [!code-xml[VSMButtonTemplate#ButtonDeclaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#buttondeclaration)]  
  
 L'output generato nell'esempio precedente è simile a quello illustrato nell'immagine seguente.  
  
 ![Due pulsanti, uno blu e uno viola.](../../../../docs/framework/wpf/controls/media/ndp-buttontwo.png "NDP\_ButtonTwo")  
Due pulsanti con colori di sfondo diversi  
  
<a name="changing_the_appearance_of_a_control_depending_on_its_state"></a>   
## Modifica dell'aspetto di un controllo a seconda del relativo stato  
 La differenza tra un pulsante con l'aspetto predefinito e il pulsante dell'esempio precedente risiede nel fatto che il primo cambia leggermente quando si trova in stati diversi.  L'aspetto del pulsante predefinito cambia ad esempio quando il pulsante viene premuto o quando si posiziona il puntatore del mouse su di esso.  <xref:System.Windows.Controls.ControlTemplate> non modifica la funzionalità di un controllo, ma modifica il comportamento visivo del controllo.  Il comportamento visivo descrive l'aspetto del controllo quando si trova in un determinato stato.  Per capire la differenza tra la funzionalità e il comportamento visivo di un controllo, si consideri l'esempio del pulsante.  La funzionalità del pulsante consiste nel generare l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> quando si fa clic sul pulsante, mentre il comportamento visivo del pulsante consiste nel cambiare aspetto quando l'utente posiziona il mouse sul pulsante o preme il pulsante.  
  
 Per specificare l'aspetto di un controllo quando il controllo si trova in un determinato stato si utilizzano oggetti <xref:System.Windows.VisualState>.  Un oggetto <xref:System.Windows.VisualState> contiene un oggetto <xref:System.Windows.Media.Animation.Storyboard> che modifica l'aspetto degli elementi che si trovano in <xref:System.Windows.Controls.ControlTemplate>.  Per ottenere questo risultato non è necessario ricorrere alla scrittura di codice, in quanto la logica del controllo modifica lo stato tramite <xref:System.Windows.VisualStateManager>.  Quando il controllo assume lo stato specificato dalla proprietà <xref:System.Windows.VisualState.Name%2A?displayProperty=fullName>, <xref:System.Windows.Media.Animation.Storyboard> viene avviato.  Quando il controllo non è più nello stato specificato, <xref:System.Windows.Media.Animation.Storyboard> viene interrotto.  
  
 Nell'esempio seguente viene illustrato l'oggetto <xref:System.Windows.VisualState> che modifica l'aspetto di un oggetto <xref:System.Windows.Controls.Button> quando si posiziona il puntatore del mouse su di esso.  <xref:System.Windows.Media.Animation.Storyboard> modifica il colore del bordo del pulsante modificando il colore di `BorderBrush`.  Se si fa riferimento all'esempio di <xref:System.Windows.Controls.ControlTemplate> presentato all'inizio di questo argomento, si ricorderà che `BorderBrush` è il nome dell'oggetto <xref:System.Windows.Media.SolidColorBrush> assegnato all'oggetto <xref:System.Windows.Controls.Border.Background%2A> di <xref:System.Windows.Controls.Border>.  
  
 [!code-xml[VSMButtonTemplate#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#4)]  
  
 Il controllo è responsabile della definizione degli stati come parte del relativo contratto, che viene illustrato in modo dettagliato in [Personalizzazione di altri controlli sulla base del contratto di controllo](#customizing_other_controls_by_understanding_the_control_contract) più avanti in questo argomento.  Nella tabelle seguente sono elencati gli stati specificati per <xref:System.Windows.Controls.Button>.  
  
|Nome VisualState|Nome VisualStateGroup|Descrizione|  
|----------------------|---------------------------|-----------------|  
|Normal|CommonStates|Stato predefinito.|  
|MouseOver|CommonStates|Il puntatore del mouse è posizionato sul controllo.|  
|Pressed|CommonStates|Il controllo viene premuto.|  
|Disabled|CommonStates|Il controllo è disabilitato.|  
|Focused|FocusStates|Il controllo ha lo stato attivo.|  
|Unfocused|FocusStates|Il controllo non ha lo stato attivo.|  
  
 L'oggetto <xref:System.Windows.Controls.Button> definisce due gruppi di stato. Il gruppo `CommonStates` contiene gli stati `Normal`, `MouseOver`, `Pressed` e `Disabled`.  Il gruppo `FocusStates` contiene gli stati `Focused` e `Unfocused`.  Gli stati nello stesso gruppo di stato si escludono a vicenda.  Il controllo si trova sempre in un solo stato per ogni gruppo.  Ad esempio, un oggetto <xref:System.Windows.Controls.Button> può avere lo stato attivo anche se il puntatore si trova in un'altra posizione, pertanto un oggetto <xref:System.Windows.Controls.Button> nello stato `Focused` può essere nello stato `MouseOver`, `Pressed` o `Normal`.  
  
 Gli oggetti <xref:System.Windows.VisualState> vengono aggiunti a oggetti <xref:System.Windows.VisualStateGroup>.  Aggiungere gli oggetti <xref:System.Windows.VisualStateGroup> alla proprietà associata <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName>.  Nell'esempio seguente vengono definiti gli oggetti <xref:System.Windows.VisualState> per gli stati `Normal`, `MouseOver` e `Pressed`, che si trovano tutti nel gruppo `CommonStates`.  L'oggetto <xref:System.Windows.VisualState.Name%2A> di ogni <xref:System.Windows.VisualState> corrisponde al nome riportato nella tabella precedente.  Lo stato `Disabled` e gli stati del gruppo `FocusStates` vengono omessi dall'esempio per motivi di brevità, ma sono inclusi nell'esempio completo disponibile alla fine di questo argomento.  
  
> [!NOTE]
>  Assicurarsi di impostare la proprietà associata <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> sulla radice <xref:System.Windows.FrameworkElement> dell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
 [!code-xml[VSMButtonTemplate#VisualStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualstates)]  
  
 L'output generato nell'esempio precedente è simile a quello illustrato nelle immagini seguenti.  
  
 ![Pulsante con un modello di controllo personalizzato.](../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP\_ButtonNormal")  
Pulsante che utilizza un modello di controllo personalizzato nello stato Normal  
  
 ![Pulsante con un bordo rosso.](../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP\_ButtonMouseOver")  
Pulsante che utilizza un modello di controllo personalizzato nello stato MouseOver  
  
 ![Il bordo è trasparente in un pulsante premuto.](../../../../docs/framework/wpf/controls/media/ndp-buttonpressed.png "NDP\_ButtonPressed")  
Pulsante che utilizza un modello di controllo personalizzato nello stato Pressed  
  
 Per trovare gli stati di visualizzazione per i controlli inclusi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md).  
  
<a name="specifying_the_behavior_of_a_control_when_it_transitions_between_states"></a>   
## Definizione del comportamento di un controllo durante le transizioni tra gli stati  
 Nell'esempio precedente l'aspetto del pulsante cambia anche quando l'utente fa clic su di esso, ma l'effetto non è visibile all'utente a meno che il pulsante non venga premuto per un intero secondo.  Per impostazione predefinita, l'esecuzione di un'animazione impiega un secondo.  Poiché è probabile che gli utenti facciano clic e rilascino un pulsante in un tempo molto più breve, il feedback visivo non sarà efficace se si lascia <xref:System.Windows.Controls.ControlTemplate> nello stato predefinito.  
  
 È possibile specificare il tempo necessario per l'esecuzione di un'animazione per una transizione graduale di un controllo da uno stato a un altro mediante l'aggiunta di oggetti <xref:System.Windows.VisualTransition> a <xref:System.Windows.Controls.ControlTemplate>.  Quando si crea un oggetto <xref:System.Windows.VisualTransition>, è necessario specificare uno o più degli elementi seguenti:  
  
-   Tempo necessario per effettuare una transizione tra gli stati.  
  
-   Modifiche aggiuntive nell'aspetto del controllo che si verificano al momento della transizione.  
  
-   Stati ai quali viene applicato l'oggetto <xref:System.Windows.VisualTransition>.  
  
### Definizione della durata di una transizione  
 È possibile specificare la durata di una transizione impostando la proprietà <xref:System.Windows.VisualTransition.GeneratedDuration%2A>.  Nell'esempio precedente è incluso un oggetto <xref:System.Windows.VisualState> che specifica che il bordo di un pulsante diventa trasparente quando il pulsante viene premuto, ma se il pulsante viene premuto e rilasciato troppo velocemente, l'animazione impiegherà troppo tempo per essere visibile.  È possibile utilizzare un oggetto <xref:System.Windows.VisualTransition> per specificare il tempo necessario per la transizione del controllo allo stato di pressione.  Nell'esempio seguente viene specificato che il controllo impiega un centesimo di secondo per passare allo stato di pressione.  
  
 [!code-xml[VSMButtonTemplate#PressedTransition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#pressedtransition)]  
  
### Definizione delle modifiche da apportare all'aspetto del controllo durante una transizione  
 <xref:System.Windows.VisualTransition> contiene un oggetto <xref:System.Windows.Media.Animation.Storyboard> che viene avviato quando il controllo passa da uno stato a un altro.  È ad esempio possibile specificare l'esecuzione di una determinata animazione quando il controllo passa dallo stato `MouseOver` allo stato `Normal`.  Nell'esempio seguente viene creato un oggetto <xref:System.Windows.VisualTransition> che specifica che quando l'utente allontana il puntatore del mouse dal pulsante, il bordo del pulsante diventa blu, quindi giallo e infine nero nell'arco di 1,5 secondi.  
  
 [!code-xml[VSMButtonTemplate#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#8)]  
  
### Definizione del momento per l'applicazione di VisualTransition  
 Un oggetto <xref:System.Windows.VisualTransition> può essere applicato solo a determinati stati o in qualsiasi momento in cui il controllo passa da uno stato a un altro.  Nell'esempio precedente <xref:System.Windows.VisualTransition> viene applicato quando il controllo passa dallo stato `MouseOver` allo stato `Normal`, mentre nell'esempio che lo precede <xref:System.Windows.VisualTransition> viene applicato quando il controllo passa allo stato `Pressed`.  Per limitare l'applicazione di un oggetto <xref:System.Windows.VisualTransition>, è necessario impostare le proprietà <xref:System.Windows.VisualTransition.To%2A> e <xref:System.Windows.VisualTransition.From%2A>.  Nella tabella riportata di seguito vengono descritti i livelli di restrizione, dal più al meno elevato.  
  
|Tipo di restrizione|Valore di From|Valore di To|  
|-------------------------|--------------------|------------------|  
|Da uno stato specificato a un altro stato specificato|Nome di un oggetto <xref:System.Windows.VisualState>.|Nome di un oggetto <xref:System.Windows.VisualState>.|  
|Da qualsiasi stato a uno stato specificato|Non impostato|Nome di un oggetto <xref:System.Windows.VisualState>.|  
|Da uno stato specificato a uno stato qualsiasi|Nome di un oggetto <xref:System.Windows.VisualState>.|Non impostato|  
|Da uno stato qualsiasi a un altro stato qualsiasi|Non impostato|Non impostato|  
  
 È possibile includere più oggetti <xref:System.Windows.VisualTransition> in un oggetto <xref:System.Windows.VisualStateGroup> che fanno riferimento allo stesso stato, ma tali oggetti verranno utilizzati nell'ordine specificato nella tabella precedente.  Nell'esempio seguente sono presenti due oggetti <xref:System.Windows.VisualTransition>.  Quando il controllo passa dallo stato `Pressed` allo stato `MouseOver`, viene utilizzato l'oggetto <xref:System.Windows.VisualTransition> che dispone delle proprietà <xref:System.Windows.VisualTransition.From%2A> e <xref:System.Windows.VisualTransition.To%2A> entrambe impostate.  Quando il controllo passa da uno stato diverso da `Pressed` allo stato `MouseOver`, viene utilizzato l'altro stato.  
  
 [!code-xml[VSMButtonTemplate#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#7)]  
  
 L'oggetto <xref:System.Windows.VisualStateGroup> dispone di una proprietà <xref:System.Windows.VisualStateGroup.Transitions%2A> contenente gli oggetti <xref:System.Windows.VisualTransition> che si applicano agli oggetti <xref:System.Windows.VisualState> in <xref:System.Windows.VisualStateGroup>.  L'autore di <xref:System.Windows.Controls.ControlTemplate> ha la possibilità di includere tutti gli oggetti <xref:System.Windows.VisualTransition> desiderati.  Tuttavia, se le proprietà <xref:System.Windows.VisualTransition.To%2A> e <xref:System.Windows.VisualTransition.From%2A> sono impostate su nomi di stato non presenti in <xref:System.Windows.VisualStateGroup>, l'oggetto <xref:System.Windows.VisualTransition> verrà ignorato.  
  
 Nell'esempio seguente viene illustrato l'oggetto <xref:System.Windows.VisualStateGroup> per `CommonStates`.  Nell'esempio viene definito un oggetto <xref:System.Windows.VisualTransition> per ciascuna delle transizioni seguenti del pulsante.  
  
-   Allo stato `Pressed`.  
  
-   Allo stato `MouseOver`.  
  
-   Dallo stato `Pressed` allo stato `MouseOver`.  
  
-   Dallo stato `MouseOver` allo stato `Normal`.  
  
 [!code-xml[VSMButtonTemplate#VisualTransitions](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualtransitions)]  
  
<a name="customizing_other_controls_by_understanding_the_control_contract"></a>   
## Personalizzazione di altri controlli sulla base del contratto di controllo  
 Un controllo che utilizza <xref:System.Windows.Controls.ControlTemplate> per specificare la struttura visuale \(tramite oggetti <xref:System.Windows.FrameworkElement>\) e il comportamento visivo \(tramite oggetti <xref:System.Windows.VisualState>\) utilizza il modello di controllo delle parti.  Questo modello viene utilizzato da molti controlli inclusi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 4.  Le parti di cui un autore di <xref:System.Windows.Controls.ControlTemplate> deve essere consapevole sono riportate nel contratto del controllo.  La conoscenza delle parti di un contratto di controllo consente di personalizzare l'aspetto di qualsiasi controllo che utilizza il modello di controllo delle parti.  
  
 In un contratto di controllo sono disponibili tre elementi:  
  
-   Gli elementi visivi utilizzati dalla logica del controllo.  
  
-   Gli stati del controllo e il gruppo al quale appartiene ogni stato.  
  
-   Le proprietà pubbliche che influiscono a livello visivo sul controllo.  
  
### Elementi visivi del contratto di controllo  
 La logica di un controllo può talvolta interagire con un oggetto <xref:System.Windows.FrameworkElement> che si trova in <xref:System.Windows.Controls.ControlTemplate>.  È ad esempio possibile che il controllo gestisca un evento di uno dei relativi elementi.  Quando è previsto che un controllo trovi un determinato oggetto <xref:System.Windows.FrameworkElement> in <xref:System.Windows.Controls.ControlTemplate>, tali informazioni devono essere fornite all'autore di <xref:System.Windows.Controls.ControlTemplate>.  Il controllo utilizza <xref:System.Windows.TemplatePartAttribute> per fornire il tipo di elemento e il nome dell'elemento previsti.  Nel contratto del controllo <xref:System.Windows.Controls.Button> non sono incluse parti <xref:System.Windows.FrameworkElement>, che sono invece presenti nel contratto di altri controlli, ad esempio <xref:System.Windows.Controls.ComboBox>.  
  
 Nell'esempio seguente vengono illustrati gli oggetti <xref:System.Windows.TemplatePartAttribute> specificati nella classe <xref:System.Windows.Controls.ComboBox>.  La logica di <xref:System.Windows.Controls.ComboBox> prevede che un oggetto <xref:System.Windows.Controls.TextBox> denominato `PART_EditableTextBox` e un oggetto <xref:System.Windows.Controls.Primitives.Popup> denominato `PART_Popup` vengano individuati nel relativo oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
 [!code-csharp[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#comboboxcontract)]
 [!code-vb[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#comboboxcontract)]  
  
 Nell'esempio seguente viene illustrato un oggetto <xref:System.Windows.Controls.ControlTemplate> semplificato per l'oggetto <xref:System.Windows.Controls.ComboBox> che include gli elementi specificati dagli oggetti <xref:System.Windows.TemplatePartAttribute> nella classe <xref:System.Windows.Controls.ComboBox>.  
  
 [!code-xml[VSMButtonTemplate#ComboBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/window1.xaml#comboboxtemplate)]  
  
### Stati nel contratto di controllo  
 Anche gli stati di un controllo fanno parte del contratto di controllo.  Nell'esempio di creazione di un oggetto <xref:System.Windows.Controls.ControlTemplate> per un oggetto <xref:System.Windows.Controls.Button> viene illustrato come specificare l'aspetto di un oggetto <xref:System.Windows.Controls.Button> a seconda del relativo stato.  A tale scopo, creare un oggetto <xref:System.Windows.VisualState> per ogni stato specificato e inserire tutti gli oggetti <xref:System.Windows.VisualState> che condividono un oggetto <xref:System.Windows.TemplateVisualStateAttribute.GroupName%2A> in <xref:System.Windows.VisualStateGroup>, come illustrato in [Modifica dell'aspetto di un controllo a seconda del relativo stato](#changing_the_appearance_of_a_control_depending_on_its_state) più indietro in questo argomento.  I controlli di terze parti devono specificare gli stati utilizzando <xref:System.Windows.TemplateVisualStateAttribute>, che consente agli strumenti di progettazione, ad esempio Expression Blend, per esporre gli stati del controllo per la creazione di modelli di controllo.  
  
 Per trovare il contratto di controllo per i controlli inclusi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Stili e modelli di Control](../../../../docs/framework/wpf/controls/control-styles-and-templates.md).  
  
### Proprietà nel contratto di controllo  
 Nel contratto di controllo sono inoltre incluse le proprietà pubbliche che influiscono a livello visivo sul controllo.  È possibile impostare queste proprietà affinché venga modificato l'aspetto del controllo senza creare un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate>.  È inoltre possibile utilizzare l'estensione di markup [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) per associare proprietà di elementi in <xref:System.Windows.Controls.ControlTemplate> a proprietà pubbliche definite dall'oggetto <xref:System.Windows.Controls.Button>.  
  
 Nell'esempio seguente viene illustrato il contratto di controllo per il pulsante.  
  
 [!code-csharp[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#buttoncontract)]
 [!code-vb[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#buttoncontract)]  
  
 Quando si crea un oggetto <xref:System.Windows.Controls.ControlTemplate>, è spesso più facile partire da un oggetto <xref:System.Windows.Controls.ControlTemplate> esistente e modificarlo.  Per modificare un oggetto <xref:System.Windows.Controls.ControlTemplate> esistente, è possibile effettuare una delle operazioni seguenti:  
  
-   Utilizzare uno strumento di progettazione, ad esempio Expression Blend, che fornisce un'interfaccia utente grafica per la creazione di modelli di controllo.  Per ulteriori informazioni, vedere [Applicazione di stili a un controllo che supporta modelli](http://go.microsoft.com/fwlink/?LinkId=161153).  
  
-   Ottenere l'oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito e modificarlo.  Per trovare i modelli di controllo inclusi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Temi WPF predefiniti](http://go.microsoft.com/fwlink/?LinkID=158252).  
  
<a name="complete_example"></a>   
## Esempio completo  
 Di seguito viene illustrato l'esempio completo relativo a <xref:System.Windows.Controls.Button><xref:System.Windows.Controls.ControlTemplate> di cui si è trattato in questo argomento.  
  
 [!code-xml[VSMButtonTemplate#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#3)]  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)