---
title: "Creazione di un controllo dall&#39;aspetto personalizzabile | Microsoft Docs"
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
  - "controlli [WPF], personalizzazione"
  - "controlli [WPF], definizione della struttura visiva e del comportamento"
  - "ControlTemplate [WPF], personalizzazione dell'aspetto"
  - "personalizzazione dell'aspetto [WPF], ControlTemplate"
  - "gestione degli stati dei controlli [WPF], VisualStateManager"
  - "VisualStateManager [WPF], procedura consigliata"
  - "VisualStateManager [WPF], gestione dello stato di un controllo"
ms.assetid: 9e356d3d-a3d0-4b01-a25f-2d43e4d53fe5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Creazione di un controllo dall&#39;aspetto personalizzabile
<a name="introduction"></a> In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è possibile creare un controllo dall'aspetto personalizzabile.  È ad esempio possibile modificare l'aspetto di un oggetto <xref:System.Windows.Controls.CheckBox> ben oltre le possibilità offerte dall'impostazione delle proprietà creando un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate>.  Nella figura seguente viene illustrato un oggetto <xref:System.Windows.Controls.CheckBox> che utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> predefinito e un oggetto <xref:System.Windows.Controls.CheckBox> che utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> personalizzato.  
  
 ![Casella di controllo con il modello di controllo predefinito.](../../../../docs/framework/wpf/controls/media/ndp-checkboxdefault.png "NDP\_CheckBoxDefault")  
Oggetto CheckBox che utilizza il modello di controllo predefinito  
  
 ![Casella di controllo con un modello di controllo personalizzato.](../../../../docs/framework/wpf/controls/media/ndp-checkboxcustom.png "NDP\_CheckBoxCustom")  
Oggetto CheckBox che utilizza un modello di controllo personalizzato  
  
 Se durante la creazione di un controllo si segue il modello delle parti e degli stati, l'aspetto del controllo risulterà personalizzabile.  Alcuni strumenti di progettazione, ad esempio quali Microsoft Expression Blend, supportano il modello delle parti e degli stati e pertanto l'utilizzo di questo modello renderà personalizzabile il controllo in tali tipi di applicazioni.  In questo argomento viene illustrato il modello delle parti e degli stati e viene spiegato come utilizzarlo quando si crea il controllo personalizzato.  Per illustrare la filosofia di questo modello, in questo argomento è incluso un esempio di controllo personalizzato, ovvero `NumericUpDown`.  Il controllo `NumericUpDown` consente di visualizzare un valore numerico che un utente può aumentare o ridurre facendo clic sui pulsanti del controllo.  Nell'immagine seguente viene illustrato il controllo `NumericUpDown` descritto in questo argomento.  
  
 ![Controllo personalizzato NumericUpDown.](../../../../docs/framework/wpf/controls/media/ndp-numericupdown.png "NDP\_NumericUPDown")  
Controllo NumericUpDown personalizzato  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Prerequisiti](#prerequisites)  
  
-   [Modello delle parti e degli stati](#parts_and_states_model)  
  
-   [Definizione della struttura e del comportamento visuali di un controllo in un oggetto ControlTemplate](#defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate)  
  
-   [Utilizzo di parti dell'oggetto ControlTemplate nel codice](#using_parts_of_the_controltemplate_in_code)  
  
-   [Disponibilità del contratto di controllo](#providing_the_control_contract)  
  
-   [Esempio completo](#complete_example)  
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si suppone che l'utente sia in grado di creare un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> per un controllo esistente, che abbia familiarità con gli elementi di un contratto di controllo e che abbia compreso i concetti illustrati in [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
> [!NOTE]
>  Per creare un controllo di cui sia possibile personalizzare l'aspetto, è necessario creare un controllo che erediti dalla classe <xref:System.Windows.Controls.Control> o da una delle relative sottoclassi diverse da <xref:System.Windows.Controls.UserControl>.  Un controllo che eredita da <xref:System.Windows.Controls.UserControl> è un controllo che può essere creato con rapidità, ma poiché non utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> non è possibile personalizzarne l'aspetto.  
  
<a name="parts_and_states_model"></a>   
## Modello delle parti e degli stati  
 Il modello delle parti e degli stati specifica come definire la struttura visuale e il comportamento visivo di un controllo.  L'adesione al modello delle parti e degli stati comporta l'esecuzione delle operazioni seguenti:  
  
-   Definizione della struttura visuale e del comportamento visivo nell'oggetto <xref:System.Windows.Controls.ControlTemplate> di un controllo.  
  
-   Adesione a determinate procedure consigliate quando la logica del controllo interagisce con parti del modello di controllo.  
  
-   Disponibilità di un contratto di controllo per la specifica degli elementi da includere nell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
 Quando si definiscono la struttura e il comportamento visuali nell'oggetto <xref:System.Windows.Controls.ControlTemplate> di un controllo, gli autori delle applicazioni possono modificare la struttura visuale e il comportamento visivo del controllo creando un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> anziché scrivendo codice.  È necessario fornire un contratto di controllo che indichi agli autori delle applicazioni quali oggetti <xref:System.Windows.FrameworkElement> e stati devono essere definiti nell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  Quando si interagisce con le parti incluse nell'oggetto <xref:System.Windows.Controls.ControlTemplate>, è necessario utilizzare alcune procedure consigliate, in modo che il controllo sia in grado di gestire correttamente un oggetto <xref:System.Windows.Controls.ControlTemplate> incompleto.  Se si seguono questi tre principi, gli autori delle applicazioni saranno in grado di creare un oggetto <xref:System.Windows.Controls.ControlTemplate> per il controllo con la stessa facilità con cui è possibile crearlo per i controlli forniti con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Ogni suggerimento viene descritto in dettaglio nella sezione seguente.  
  
<a name="defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate"></a>   
## Definizione della struttura e del comportamento visuali di un controllo in un oggetto ControlTemplate  
 La creazione del controllo personalizzato mediante il modello delle parti e degli stati comporta la definizione della struttura visuale e del comportamento visivo del controllo nel relativo oggetto <xref:System.Windows.Controls.ControlTemplate> anziché nella logica corrispondente.  La struttura visuale di un controllo è formata dagli oggetti <xref:System.Windows.FrameworkElement> che costituiscono il controllo.  Il comportamento visivo è il modo in cui il controllo viene visualizzato quando si trova in un determinato stato.  Per ulteriori informazioni sulla creazione di un oggetto <xref:System.Windows.Controls.ControlTemplate> che specifica la struttura visuale e il comportamento visivo di un controllo, vedere [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
 Nell'esempio del controllo `NumericUpDown` la struttura visuale include due controlli <xref:System.Windows.Controls.Primitives.RepeatButton> e un oggetto <xref:System.Windows.Controls.TextBlock>.  L'aggiunta questi controlli nel codice del controllo `NumericUpDown`, ad esempio nel relativo costruttore, determinerebbe l'impossibilità di modificare le posizioni di tali controlli.  Anziché definire la struttura visuale e il comportamento visivo del controllo nel relativo codice, è necessario definirli nell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  Poiché l'oggetto <xref:System.Windows.Controls.ControlTemplate> può essere sostituito, uno sviluppatore di applicazioni può personalizzare la posizione dei pulsanti e dell'oggetto <xref:System.Windows.Controls.TextBlock> e specificare quale comportamento si verifica quando `Value` è negativo.  
  
 Nell'esempio seguente viene illustrata la struttura visuale del controllo `NumericUpDown` che include un oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> per aumentare `Value`, un oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> per ridurre `Value` e un oggetto <xref:System.Windows.Controls.TextBlock> per visualizzare `Value`.  
  
 [!code-xml[VSMCustomControl#VisualStructure](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#visualstructure)]  
  
 Un comportamento visivo del controllo `NumericUpDown` prevede che il valore venga visualizzato con un tipo di carattere rosso quando è negativo.  Se si modifica la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> dell'oggetto <xref:System.Windows.Controls.TextBlock> nel codice quando `Value` è negativo, `NumericUpDown` visualizzerà sempre un valore negativo di colore rosso.  Il comportamento visivo del controllo nell'oggetto <xref:System.Windows.Controls.ControlTemplate> viene specificato aggiungendo oggetti <xref:System.Windows.VisualState> all'oggetto <xref:System.Windows.Controls.ControlTemplate>.  Nell'esempio seguente vengono illustrati gli oggetti <xref:System.Windows.VisualState> per gli stati `Positive` e `Negative`.  `Positive` e `Negative` si escludono a vicenda \(lo stato del controllo corrisponde sempre a uno dei due\) e pertanto nell'esempio gli oggetti <xref:System.Windows.VisualState> vengono inseriti in un unico oggetto <xref:System.Windows.VisualStateGroup>.  Quando il controllo passa nello stato `Negative`, la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> dell'oggetto <xref:System.Windows.Controls.TextBlock> diventa di colore rosso.  Quando il controllo è nello stato `Positive`, la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> ritorna al valore originale.  La definizione di oggetti <xref:System.Windows.VisualState> in un oggetto <xref:System.Windows.Controls.ControlTemplate> viene discussa ulteriormente in [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md).  
  
> [!NOTE]
>  Assicurarsi di impostare la proprietà associata <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> sulla radice <xref:System.Windows.FrameworkElement> dell'oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
 [!code-xml[VSMCustomControl#ValueStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]  
  
<a name="using_parts_of_the_controltemplate_in_code"></a>   
## Utilizzo di parti dell'oggetto ControlTemplate nel codice  
 Un autore di <xref:System.Windows.Controls.ControlTemplate> potrebbe omettere oggetti <xref:System.Windows.FrameworkElement> o <xref:System.Windows.VisualState> intenzionalmente o per errore, ma per il corretto funzionamento è possibile che la logica del controllo necessiti di tali parti.  Il modello delle parti e degli stati specifica che il controllo deve essere resiliente a un oggetto <xref:System.Windows.Controls.ControlTemplate> in cui mancano oggetti <xref:System.Windows.FrameworkElement> o <xref:System.Windows.VisualState>.  Il controllo non deve generare un'eccezione o segnalare un errore se un oggetto <xref:System.Windows.FrameworkElement>, <xref:System.Windows.VisualState> o <xref:System.Windows.VisualStateGroup> risulta mancante da <xref:System.Windows.Controls.ControlTemplate>.  In questa sezione vengono illustrate le procedure consigliate per l'interazione con gli oggetti <xref:System.Windows.FrameworkElement> e la gestione degli stati.  
  
### Prevedere la mancanza di oggetti FrameworkElement  
 Quando si definiscono oggetti <xref:System.Windows.FrameworkElement> in <xref:System.Windows.Controls.ControlTemplate>, la logica del controllo potrebbe dover interagire con alcuni questi oggetti.  Ad esempio, il controllo `NumericUpDown` sottoscrive l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> dei pulsanti per aumentare o diminuire `Value` e imposta la proprietà <xref:System.Windows.Controls.TextBlock.Text%2A> dell'oggetto <xref:System.Windows.Controls.TextBlock> su `Value`.  Se un oggetto <xref:System.Windows.Controls.ControlTemplate> personalizzato omette <xref:System.Windows.Controls.TextBlock> o i pulsanti, è plausibile che il controllo perda alcuna delle relative funzionalità, ma è necessario verificare che il controllo non causi un errore.  Ad esempio, se un oggetto <xref:System.Windows.Controls.ControlTemplate> non contiene i pulsanti per la modifica di `Value`, `NumericUpDown` perderà tale funzionalità, ma un'applicazione che utilizza <xref:System.Windows.Controls.ControlTemplate> continuerà a essere in esecuzione.  
  
 L'utilizzo delle procedure seguenti garantirà che il controllo risponda correttamente agli oggetti <xref:System.Windows.FrameworkElement> mancanti:  
  
1.  Impostare l'attributo `x:Name` per ogni oggetto <xref:System.Windows.FrameworkElement> a cui è necessario fare riferimento nel codice.  
  
2.  Definire proprietà private per ogni oggetto <xref:System.Windows.FrameworkElement> con cui è necessario interagire.  
  
3.  Sottoscrivere e annullare la sottoscrizione di qualsiasi evento gestito dal controllo nella funzione di accesso set della proprietà dell'oggetto <xref:System.Windows.FrameworkElement>.  
  
4.  Impostare le proprietà dell'oggetto <xref:System.Windows.FrameworkElement> di cui è stata effettuata la definizione nel passaggio 2 nel metodo <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A>.  Si tratta del primo oggetto <xref:System.Windows.FrameworkElement> in <xref:System.Windows.Controls.ControlTemplate> disponibile per il controllo.  Utilizzare l'attributo `x:Name` dell'oggetto <xref:System.Windows.FrameworkElement> per ottenere il valore corrispondente da <xref:System.Windows.Controls.ControlTemplate>.  
  
5.  Verificare che il valore di <xref:System.Windows.FrameworkElement> non sia `null` prima dell'accesso ai relativi membri.  Se è `null`, non segnalare un errore.  
  
 Negli esempi seguenti viene illustrata l'interazione del controllo `NumericUpDown` con gli oggetti <xref:System.Windows.FrameworkElement> in base ai suggerimenti riportati nell'elenco precedente.  
  
 Nell'esempio che definisce la struttura visuale del controllo `NumericUpDown` nell'oggetto <xref:System.Windows.Controls.ControlTemplate> l'oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> che determina l'aumento di `Value` dispone dell'attributo `x:Name` impostato su `UpButton`.  Nell'esempio seguente viene dichiarata una proprietà denominata `UpButtonElement` che rappresenta l'oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> dichiarato in <xref:System.Windows.Controls.ControlTemplate>.  La funzione di accesso `set` annulla innanzitutto la sottoscrizione dell'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante se `UpDownElement` non è `null`, quindi imposta la proprietà e infine sottoscrive l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click>.  Viene inoltre definita una proprietà, non illustrata in questo esempio, per l'altro oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> denominato `DownButtonElement`.  
  
 [!code-csharp[VSMCustomControl#UpButtonProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#upbuttonproperty)]
 [!code-vb[VSMCustomControl#UpButtonProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#upbuttonproperty)]  
  
 Nell'esempio seguente viene illustrato il metodo <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> per il controllo `NumericUpDown`.  Nell'esempio viene utilizzato il metodo <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> per ottenere gli oggetti <xref:System.Windows.FrameworkElement> da <xref:System.Windows.Controls.ControlTemplate>.  Si noti che nell'esempio viene evitato che si verifichino casi in cui il metodo <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> trova un oggetto <xref:System.Windows.FrameworkElement> con il nome specificato che non corrisponde al tipo previsto.  La procedura consigliata prevede inoltre di ignorare gli elementi che dispongono dell'attributo `x:Name` ma che sono del tipo non corretto.  
  
 [!code-csharp[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
 [!code-vb[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]  
  
 L'utilizzo delle procedure illustrate nell'esempio precedente assicura che il controllo continuerà a essere eseguito quando da <xref:System.Windows.Controls.ControlTemplate> risulta mancante un oggetto <xref:System.Windows.FrameworkElement>.  
  
### Utilizzare l'oggetto VisualStateManager per gestire gli stati  
 L'oggetto <xref:System.Windows.VisualStateManager> consente di tenere traccia degli stati di un controllo e di eseguire la logica necessaria per la transizione tra gli stati.  L'aggiunta di oggetti <xref:System.Windows.VisualState> a <xref:System.Windows.Controls.ControlTemplate> comporta la loro aggiunta a un oggetto <xref:System.Windows.VisualStateGroup> e l'aggiunta dell'oggetto <xref:System.Windows.VisualStateGroup> alla proprietà collegata <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> in modo che <xref:System.Windows.VisualStateManager> disponga dell'accesso a tali oggetti.  
  
 Nell'esempio seguente viene ripetuto l'esempio precedente in cui vengono illustrati gli oggetti <xref:System.Windows.VisualState> che corrispondono agli stati `Positive` e `Negative` del controllo.  L'oggetto <xref:System.Windows.Media.Animation.Storyboard> nell'oggetto <xref:System.Windows.VisualState> `Negative` trasforma in rosso la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> dell'oggetto <xref:System.Windows.Controls.TextBlock>.  Quando il controllo `NumericUpDown` è nello stato `Negative`, lo storyboard nello stato `Negative` viene avviato.  L'oggetto <xref:System.Windows.Media.Animation.Storyboard> nello stato `Negative` viene quindi interrotto quando il controllo torna allo stato `Positive`.  Non è necessario che l'oggetto <xref:System.Windows.VisualState> `Positive` contenga un oggetto <xref:System.Windows.Media.Animation.Storyboard>, poiché quando <xref:System.Windows.Media.Animation.Storyboard> per lo stato `Negative` viene interrotto, la proprietà <xref:System.Windows.Controls.TextBlock.Foreground%2A> ritorna al relativo colore originale.  
  
 [!code-xml[VSMCustomControl#ValueStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]  
  
 Si noti che all'oggetto <xref:System.Windows.Controls.TextBlock> viene assegnato un nome, ma <xref:System.Windows.Controls.TextBlock> non è incluso nel contratto di controllo per `NumericUpDown` poiché la logica del controllo non fa mai riferimento a <xref:System.Windows.Controls.TextBlock>.  Gli elementi a cui viene fatto riferimento in <xref:System.Windows.Controls.ControlTemplate> dispongono di nomi, ma non devono far parte del contratto di controllo, poiché un nuovo <xref:System.Windows.Controls.ControlTemplate> per il controllo potrebbe non avere necessità di fare riferimento a tale elemento.  Ad esempio, l'autore di un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> per `NumericUpDown` potrebbe decidere di non indicare che `Value` è negativo mediante la modifica di <xref:System.Windows.Controls.Control.Foreground%2A>.  In tal caso, né il codice né l'oggetto <xref:System.Windows.Controls.ControlTemplate> fanno riferimento a <xref:System.Windows.Controls.TextBlock> in base al nome.  
  
 La logica del controllo è responsabile della modifica dello stato del controllo.  Nell'esempio seguente viene illustrata la chiamata del controllo `NumericUpDown` al metodo <xref:System.Windows.VisualStateManager.GoToState%2A> per il passaggio allo stato `Positive` quando `Value` è 0 o maggiore e allo stato `Negative` quando `Value` è minore di 0.  
  
 [!code-csharp[VSMCustomControl#ValueStateChange](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#valuestatechange)]
 [!code-vb[VSMCustomControl#ValueStateChange](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#valuestatechange)]  
  
 Il metodo <xref:System.Windows.VisualStateManager.GoToState%2A> esegue la logica necessaria per avviare e interrompere lo storyboard in modo appropriato.  Quando un controllo chiama il metodo <xref:System.Windows.VisualStateManager.GoToState%2A> per modificare il relativo stato, l'oggetto <xref:System.Windows.VisualStateManager> effettua le operazioni seguenti:  
  
-   Se l'oggetto <xref:System.Windows.VisualState> di destinazione del controllo dispone di un oggetto <xref:System.Windows.Media.Animation.Storyboard>, lo storyboard verrà avviato.  Quindi, se l'oggetto <xref:System.Windows.VisualState> da cui il controllo proviene dispone di un oggetto <xref:System.Windows.Media.Animation.Storyboard>, lo storyboard verrà interrotto.  
  
-   Se il controllo è già nello stato specificato, <xref:System.Windows.VisualStateManager.GoToState%2A> non eseguirà alcuna azione e restituirà `true`.  
  
-   Se lo stato specificato non esiste nell'oggetto <xref:System.Windows.Controls.ControlTemplate> di `control`, il metodo <xref:System.Windows.VisualStateManager.GoToState%2A> non eseguirà alcuna azione e restituirà `false`.  
  
#### Procedure consigliate per l'utilizzo dell'oggetto VisualStateManager  
 Per gestire gli stati del controllo, è consigliabile effettuare le operazioni seguenti:  
  
-   Utilizzare le proprietà per tenere traccia dello stato corrispondente.  
  
-   Creare un metodo di supporto per la transizione tra gli stati.  
  
 Il controllo `NumericUpDown` utilizza la proprietà `Value` corrispondente per tenere traccia dello stato `Positive` o `Negative`.  Il controllo `NumericUpDown` definisce inoltre gli stati `Focused` e `UnFocused` che consentono di tenere traccia della proprietà <xref:System.Windows.UIElement.IsFocused%2A>.  Se si utilizzano stati che non corrispondono per natura a una proprietà del controllo, sarà possibile definire una proprietà privata per tenere traccia dello stato.  
  
 Un singolo metodo che aggiorna tutti gli stati consente di centralizzare le chiamate a <xref:System.Windows.VisualStateManager> e di mantenere gestibile il codice.  Nell'esempio seguente viene illustrato il metodo di supporto del controllo `NumericUpDown`, ovvero `UpdateStates`.  Quando `Value` è maggiore o uguale a 0, <xref:System.Windows.Controls.Control> è nello stato `Positive`.  Quando `Value` è minore di 0, il controllo è nello stato `Negative`.  Quando <xref:System.Windows.UIElement.IsFocused%2A> è `true`, il controllo è nello stato `Focused`. In caso contrario, è nello stato `Unfocused`.  Il controllo può chiamare `UpdateStates` quando è necessario modificare lo stato, indipendentemente dallo stato che viene modificato.  
  
 [!code-csharp[VSMCustomControl#UpdateStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#updatestates)]
 [!code-vb[VSMCustomControl#UpdateStates](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#updatestates)]  
  
 Se si passa un nome di stato a <xref:System.Windows.VisualStateManager.GoToState%2A> quando il controllo è già in tale stato, <xref:System.Windows.VisualStateManager.GoToState%2A> non eseguirà alcuna operazione e non sarà quindi necessario verificare lo stato corrente del controllo.  Ad esempio, se `Value` cambia da un numero negativo a un altro numero negativo, lo storyboard per lo stato `Negative` non verrà interrotto e il controllo visualizzato all'utente non presenterà alcuna modifica.  
  
 <xref:System.Windows.VisualStateManager> utilizza oggetti <xref:System.Windows.VisualStateGroup> per determinare quale stato disattivare quando si chiama <xref:System.Windows.VisualStateManager.GoToState%2A>.  Il controllo è sempre in un unico stato per ogni <xref:System.Windows.VisualStateGroup> definito nel relativo <xref:System.Windows.Controls.ControlTemplate> e uno stato viene disattivato solo quando il controllo passa in un altro stato dallo stesso <xref:System.Windows.VisualStateGroup>.  Ad esempio, l'oggetto <xref:System.Windows.Controls.ControlTemplate> del controllo `NumericUpDown` definisce gli oggetti <xref:System.Windows.VisualState> con gli stati `Positive` e `Negative` in un oggetto <xref:System.Windows.VisualStateGroup> e gli oggetti <xref:System.Windows.VisualState> con gli stati `Focused` e `Unfocused` in un altro.  È possibile osservare `Focused` e `Unfocused`<xref:System.Windows.VisualState> definiti nella sezione [Esempio completo](#complete_example) di questo argomento. Quando il controllo passa dallo stato `Positive` allo stato `Negative` o viceversa, il controllo rimane nello stato `Focused` o `Unfocused`.  
  
 Lo stato di un controllo può cambiare nelle tre situazioni tipiche seguenti:  
  
-   Quando l'oggetto <xref:System.Windows.Controls.ControlTemplate> viene applicato a <xref:System.Windows.Controls.Control>.  
  
-   Quando il valore di una proprietà cambia.  
  
-   Quando si verifica un evento.  
  
 Negli esempi seguenti viene illustrato l'aggiornamento dello stato del controllo `NumericUpDown` nei casi descritti.  
  
 È necessario aggiornare lo stato del controllo nel metodo <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> in modo che il controllo venga visualizzato nello stato corretto quando <xref:System.Windows.Controls.ControlTemplate> viene applicato.  Nell'esempio seguente viene chiamato `UpdateStates` nel metodo <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> per assicurarsi che il controllo sia negli stati appropriati.  Si supponga, ad esempio, di creare un controllo `NumericUpDown`, quindi di impostarne la proprietà <xref:System.Windows.Controls.Control.Foreground%2A> su verde e `Value` su \-5.  Se non si chiama `UpdateStates` quando l'oggetto <xref:System.Windows.Controls.ControlTemplate> viene applicato al controllo `NumericUpDown`, lo stato del controllo non sarà `Negative` e il valore sarà verde anziché rosso.  Per fare in modo che il controllo passi nello stato `Negative`, è necessario chiamare `UpdateStates`.  
  
 [!code-csharp[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
 [!code-vb[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]  
  
 È spesso necessario aggiornare gli stati di un controllo quando il valore di una proprietà cambia.  Nell'esempio seguente viene illustrato l'intero metodo `ValueChangedCallback`.  Poiché viene chiamato `ValueChangedCallback` quando `Value` cambia, il metodo chiama `UpdateStates` nel caso in cui `Value` cambia da positivo a negativo o viceversa.  È possibile chiamare `UpdateStates` quando `Value` cambia ma rimane positivo o negativo, in quanto in tal caso il controllo non modificherà gli stati.  
  
 [!code-csharp[VSMCustomControl#EntireValueChangedCallback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#entirevaluechangedcallback)]
 [!code-vb[VSMCustomControl#EntireValueChangedCallback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#entirevaluechangedcallback)]  
  
 Potrebbe inoltre essere necessario aggiornare gli stati quando si verifica un evento.  Nell'esempio seguente viene illustrata la chiamata a `UpdateStates` da parte di `NumericUpDown` sull'oggetto <xref:System.Windows.Controls.Control> per gestire l'evento <xref:System.Windows.UIElement.GotFocus>.  
  
 [!code-csharp[VSMCustomControl#OnGotFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#ongotfocus)]
 [!code-vb[VSMCustomControl#OnGotFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#ongotfocus)]  
  
 L'oggetto <xref:System.Windows.VisualStateManager> consente di gestire gli stati del controllo.  Tramite l'oggetto <xref:System.Windows.VisualStateManager> è possibile garantire la transizione corretta del controllo tra gli stati.  Se si seguono i suggerimenti descritti in questa sezione per l'utilizzo dell'oggetto <xref:System.Windows.VisualStateManager>, il codice del controllo risulterà leggibile e gestibile.  
  
<a name="providing_the_control_contract"></a>   
## Disponibilità del contratto di controllo  
 Un contratto di controllo viene reso disponibile in modo che gli autori dell'oggetto <xref:System.Windows.Controls.ControlTemplate> siano a conoscenza degli elementi da inserire nel modello.  In un contratto di controllo sono disponibili tre elementi:  
  
-   Gli elementi visivi utilizzati dalla logica del controllo.  
  
-   Gli stati del controllo e il gruppo al quale appartiene ogni stato.  
  
-   Le proprietà pubbliche che influiscono a livello visivo sul controllo.  
  
 Quando si crea un nuovo oggetto <xref:System.Windows.Controls.ControlTemplate> è necessario conoscere gli oggetti <xref:System.Windows.FrameworkElement> utilizzati dalla logica del controllo, il tipo di ogni oggetto e il relativo nome.  Un autore di <xref:System.Windows.Controls.ControlTemplate> deve inoltre conoscere il nome di ogni possibile stato del controllo e lo stato in cui si trova l'oggetto <xref:System.Windows.VisualStateGroup>.  
  
 Nell'esempio precedente relativo a `NumericUpDown` il controllo prevede che l'oggetto <xref:System.Windows.Controls.ControlTemplate> contenga gli oggetti <xref:System.Windows.FrameworkElement> seguenti:  
  
-   Oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> denominato `UpButton`.  
  
-   Oggetto <xref:System.Windows.Controls.Primitives.RepeatButton> denominato `DownButton.`  
  
 Il controllo può essere negli stati seguenti:  
  
-   In `ValueStates` <xref:System.Windows.VisualStateGroup>  
  
    -   `Positive`  
  
    -   `Negative`  
  
-   In `FocusStates` <xref:System.Windows.VisualStateGroup>  
  
    -   `Focused`  
  
    -   `Unfocused`  
  
 Per specificare gli oggetti <xref:System.Windows.FrameworkElement> previsti dal controllo, utilizzare l'oggetto <xref:System.Windows.TemplatePartAttribute> che specifica il nome e il tipo degli elementi previsti.  Per specificare gli stati possibili di un controllo, utilizzare l'oggetto <xref:System.Windows.TemplateVisualStateAttribute> che specifica il nome dello stato e l'oggetto <xref:System.Windows.VisualStateGroup> a cui appartiene.  Inserire gli oggetti <xref:System.Windows.TemplatePartAttribute> e <xref:System.Windows.TemplateVisualStateAttribute> nella definizione di classe del controllo.  
  
 Qualsiasi proprietà pubblica che influisce sull'aspetto del controllo fa anche parte del contratto di controllo.  
  
 Nell'esempio seguente vengono specificati l'oggetto <xref:System.Windows.FrameworkElement> e gli stati per il controllo `NumericUpDown`.  
  
 [!code-csharp[VSMCustomControl#ControlContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controlcontract)]
 [!code-vb[VSMCustomControl#ControlContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controlcontract)]  
  
<a name="complete_example"></a>   
## Esempio completo  
 Nell'esempio seguente viene illustrato l'oggetto <xref:System.Windows.Controls.ControlTemplate> completo per il controllo `NumericUpDown`.  
  
 [!code-xml[VSMCustomControl#NUDTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/themes/generic.xaml#nudtemplate)]  
  
 Nell'esempio seguente viene illustrata la logica per `NumericUpDown`.  
  
 [!code-csharp[VSMCustomControl#ControlLogic](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controllogic)]
 [!code-vb[VSMCustomControl#ControlLogic](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controllogic)]  
  
## Vedere anche  
 [Personalizzazione dell'aspetto di un controllo esistente mediante la creazione di un oggetto ControlTemplate](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)