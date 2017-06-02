---
title: "Cenni preliminari sulla modifica di controlli | Microsoft Docs"
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
  - "cenni preliminari sulla creazione di controlli"
  - "controlli, cenni preliminari sulla creazione"
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# Cenni preliminari sulla modifica di controlli
L'estensibilità del modello di controlli [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] riduce notevolmente l'esigenza di creare un nuovo controllo.  Tuttavia, in certi casi può ancora essere necessario creare un controllo personalizzato.  In questo argomento vengono illustrate le funzionalità che riducono al minimo l'esigenza di creare un controllo personalizzato e i diversi modelli di modifica dei controlli in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  In questo argomento viene inoltre illustrato come creare un nuovo controllo.  
  
   
  
<a name="when_to_write_a_new_control"></a>   
## Alternative alla scrittura di un nuovo controllo  
 In precedenza, per ottenere un'esperienza personalizzata da un controllo esistente, le modifiche erano limitate alle proprietà standard del controllo, ad esempio colore di sfondo, larghezza dei bordi e dimensioni del carattere.  Per estendere l'aspetto o il comportamento di un controllo oltre tali parametri predefiniti era necessario creare un nuovo controllo, generalmente ereditando da un controllo esistente ed eseguendo l'override del metodo responsabile della creazione del controllo.  Sebbene ciò sia ancora possibile, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente di personalizzare i controlli esistenti mediante un modello di contenuto dettagliato, stili, modelli e trigger.  Nell'elenco riportato di seguito vengono forniti alcuni esempi di utilizzo di tali funzionalità per la creazione di esperienze coerenti e personalizzate senza la necessità di creare un nuovo controllo.  
  
-   **Contenuto dettagliato** Molti controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] standard supportano il contenuto dettagliato.  La proprietà di contenuto di <xref:System.Windows.Controls.Button>, ad esempio, è di tipo <xref:System.Object>. In teoria, pertanto, in <xref:System.Windows.Controls.Button> è possibile visualizzare qualsiasi tipo di oggetto.  Per visualizzare testo e immagini in un pulsante, è possibile aggiungere un'immagine e un oggetto <xref:System.Windows.Controls.TextBlock> a <xref:System.Windows.Controls.StackPanel> e assegnare <xref:System.Windows.Controls.StackPanel> alla proprietà <xref:System.Windows.Controls.ContentControl.Content%2A>.  Poiché i controlli sono in grado di visualizzare elementi visivi e dati arbitrari di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vi è una minore esigenza di creare un nuovo controllo o di modificarne uno esistente per supportare una visualizzazione complessa.  Per ulteriori informazioni sul modello di contenuto per <xref:System.Windows.Controls.Button> e su altri modelli di contenuto in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Modello di contenuto WPF](../../../../docs/framework/wpf/controls/wpf-content-model.md).  
  
-   **Stili** <xref:System.Windows.Style> è una raccolta di valori che rappresentano le proprietà di un controllo.  Utilizzando gli stili, è possibile creare una rappresentazione riutilizzabile dell'aspetto e del comportamento di un controllo desiderato senza scrivere un nuovo controllo.  Si supponga ad esempio che si desideri applicare a tutti i controlli <xref:System.Windows.Controls.TextBlock> il carattere Arial di colore rosso con una dimensione pari a 14.  È possibile creare uno stile come risorsa e impostare di conseguenza le proprietà appropriate.  Ogni oggetto <xref:System.Windows.Controls.TextBlock> aggiunto all'applicazione avrà quindi lo stesso aspetto.  
  
-   **Modelli di dati** <xref:System.Windows.DataTemplate> consente di personalizzare la modalità di visualizzazione dei dati in un controllo.  È ad esempio possibile utilizzare <xref:System.Windows.DataTemplate> per specificare la modalità di visualizzazione dei dati in <xref:System.Windows.Controls.ListBox>.  Per un esempio, vedere [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md).  Oltre alla personalizzazione dell'aspetto dei dati, in <xref:System.Windows.DataTemplate> possono essere inclusi elementi di interfaccia utente. Tale caratteristica aumenta la flessibilità nella personalizzazione dell'interfaccia utente stessa.  Mediante <xref:System.Windows.DataTemplate>, ad esempio, è possibile creare un oggetto <xref:System.Windows.Controls.ComboBox> in cui ogni elemento contiene una casella di controllo.  
  
-   **Modelli di controllo.** Per definire la struttura e l'aspetto di molti controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], viene utilizzato <xref:System.Windows.Controls.ControlTemplate>, che separa l'aspetto di un controllo dalla relativa funzionalità. La ridefinizione di <xref:System.Windows.Controls.ControlTemplate> consente di modificare radicalmente l'aspetto di un controllo.  Si supponga, ad esempio, di voler utilizzare un controllo con l'aspetto di un semaforo.  Il controllo dispone di una funzionalità e un'interfaccia utente semplici.  È costituito da tre cerchi, che possono essere illuminati soltanto uno alla volta.  <xref:System.Windows.Controls.RadioButton> consente di fare in modo che venga selezionato un solo elemento alla volta, ma l'aspetto predefinito di <xref:System.Windows.Controls.RadioButton> non ha nulla a che fare con le luci di un semaforo.  Poiché per definire l'aspetto di <xref:System.Windows.Controls.RadioButton> viene utilizzato un modello di controllo, è possibile ridefinire facilmente <xref:System.Windows.Controls.ControlTemplate> in base ai requisiti del controllo e utilizzare pulsanti di opzione per realizzare il semaforo.  
  
    > [!NOTE]
    >  Anche se <xref:System.Windows.Controls.RadioButton> può utilizzare <xref:System.Windows.DataTemplate>, in questo esempio <xref:System.Windows.DataTemplate> non è sufficiente.  <xref:System.Windows.DataTemplate> definisce l'aspetto del contenuto di un controllo.  Nel caso di <xref:System.Windows.Controls.RadioButton>, il contenuto è costituito da qualsiasi elemento visualizzato a destra del cerchio che indica la selezione di <xref:System.Windows.Controls.RadioButton>.  Nell'esempio del semaforo, il pulsante di opzione dovrà essere costituito semplicemente da un cerchio in grado di "illuminarsi". La notevole differenza tra il requisito relativo all'aspetto del semaforo e l'aspetto predefinito di <xref:System.Windows.Controls.RadioButton> rende necessaria la ridefinizione di <xref:System.Windows.Controls.ControlTemplate>.  In genere, per la definizione del contenuto \(o dei dati\) di un controllo si utilizza <xref:System.Windows.DataTemplate>, mentre per la definizione della struttura di un controllo si utilizza <xref:System.Windows.Controls.ControlTemplate>.  
  
-   **Trigger** <xref:System.Windows.Trigger> consente di modificare in modo dinamico l'aspetto e il comportamento di un controllo senza creare un nuovo controllo.  Si supponga, ad esempio, di avere più controlli <xref:System.Windows.Controls.ListBox> nell'applicazione e che gli elementi selezionati di ciascun oggetto <xref:System.Windows.Controls.ListBox> debbano essere visualizzati in grassetto e in rosso.  La soluzione più ovvia sarebbe quella di creare una classe che eredita da <xref:System.Windows.Controls.ListBox> e di eseguire l'override del metodo <xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> per modificare l'aspetto dell'elemento selezionato. Tuttavia, un approccio migliore consiste nell'aggiunta di un trigger a uno stile di un oggetto <xref:System.Windows.Controls.ListBoxItem> che modifichi l'aspetto dell'elemento selezionato.  Un trigger consente di modificare i valori delle proprietà o di eseguire specifiche operazioni in base al valore di una proprietà.  <xref:System.Windows.EventTrigger> consente di intraprendere determinate azioni quando si verifica un evento.  
  
 Per ulteriori informazioni su stili, modelli e trigger, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
 In genere, se il controllo rispecchia la funzionalità di un controllo esistente ma si desidera che abbia un aspetto diverso, valutare innanzitutto la possibilità di utilizzare uno dei metodi descritti in questa sezione per modificare l'aspetto del controllo esistente.  
  
<a name="models_for_control_authoring"></a>   
## Modelli per la modifica dei controlli  
 Modello di contenuto dettagliato, stili, modelli e trigger riducono al minimo la necessità di creare un nuovo controllo.  Se, tuttavia, è necessario creare un nuovo controllo, è importante conoscere i diversi modelli di creazione dei controlli in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono disponibili tre modelli generali per la creazione di un controllo, ognuno dei quali offre un insieme di funzionalità e un livello di flessibilità differenti.  Le classi base dei tre modelli sono: <xref:System.Windows.Controls.UserControl>, <xref:System.Windows.Controls.Control> e <xref:System.Windows.FrameworkElement>.  
  
### Derivazione dall'oggetto UserControl  
 Il modo più semplice per creare un controllo in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste nel farlo derivare da <xref:System.Windows.Controls.UserControl>.  Nella compilazione di un controllo che eredita da <xref:System.Windows.Controls.UserControl>, è possibile aggiungere componenti esistenti a <xref:System.Windows.Controls.UserControl>, denominare i componenti e fare riferimento a gestori eventi nel codice [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  Sarà quindi possibile fare riferimento agli elementi denominati e definire i gestori eventi nel codice.  Questo modello di sviluppo è molto simile al modello utilizzato per lo sviluppo di applicazioni in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Se compilato correttamente, <xref:System.Windows.Controls.UserControl> può sfruttare i vantaggi del contenuto dettagliato, degli stili e dei trigger.  Se, tuttavia, il controllo eredita da <xref:System.Windows.Controls.UserControl>, gli utenti di tale controllo non saranno in grado di utilizzare <xref:System.Windows.DataTemplate> o <xref:System.Windows.Controls.ControlTemplate> per personalizzarne l'aspetto.  Per creare un controllo personalizzato che supporti i modelli, è necessario derivare dalla classe <xref:System.Windows.Controls.Control> o da una delle relative classi derivate \(diverse da <xref:System.Windows.Controls.UserControl>\).  
  
#### Vantaggi della derivazione dall'oggetto UserControl  
 Si consideri di utilizzare la derivazione da <xref:System.Windows.Controls.UserControl> in presenza di tutte le condizioni seguenti:  
  
-   Si desidera compilare il controllo in modo analogo alla compilazione di un'applicazione.  
  
-   Il controllo è costituito esclusivamente da componenti esistenti.  
  
-   Non è necessario supportare una personalizzazione complessa.  
  
### Derivazione dall'oggetto Control  
 La derivazione dalla classe <xref:System.Windows.Controls.Control> è il modello utilizzato dalla maggior parte dei controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esistenti.  Quando si crea un controllo che eredita dalla classe <xref:System.Windows.Controls.Control>, è possibile definirne l'aspetto mediante modelli.  In tal modo, la logica operativa viene separata dalla rappresentazione visiva.  È inoltre possibile ottenere la separazione tra logica e interfaccia utente mediante l'uso di comandi e associazioni anziché di eventi, evitando laddove possibile riferimenti agli elementi di <xref:System.Windows.Controls.ControlTemplate>. Se la logica e l'interfaccia utente del controllo sono separate in modo appropriato, l'utente del controllo sarà in grado di ridefinire l'oggetto <xref:System.Windows.Controls.ControlTemplate> del controllo per personalizzarne l'aspetto. Sebbene la compilazione di un oggetto <xref:System.Windows.Controls.Control> personalizzato non sia semplice come la compilazione di <xref:System.Windows.Controls.UserControl>, un oggetto <xref:System.Windows.Controls.Control> personalizzato offre la massima flessibilità.  
  
#### Vantaggi della derivazione dall'oggetto Control  
 Si consideri di utilizzare la derivazione da <xref:System.Windows.Controls.Control> anziché la classe <xref:System.Windows.Controls.UserControl> in presenza di una qualsiasi delle condizioni seguenti:  
  
-   Si desidera che l'aspetto del controllo sia personalizzabile tramite <xref:System.Windows.Controls.ControlTemplate>.  
  
-   Si desidera che il controllo supporti temi diversi.  
  
### Derivazione dall'oggetto FrameworkElement  
 I controlli che derivano da <xref:System.Windows.Controls.UserControl> o <xref:System.Windows.Controls.Control> si basano sulla composizione di elementi esistenti.  Per molti scenari si tratta di una soluzione accettabile, poiché qualsiasi oggetto che eredita da <xref:System.Windows.FrameworkElement> può essere incluso in <xref:System.Windows.Controls.ControlTemplate>.  A volte, tuttavia, le funzionalità della composizione semplice di elementi non sono sufficienti per definire l'aspetto di un controllo.  Per questi scenari, basare un componente su <xref:System.Windows.FrameworkElement> è la scelta giusta.  
  
 Esistono due metodi standard per compilare componenti basati su <xref:System.Windows.FrameworkElement>: rendering diretto e composizione di elementi personalizzati.  Il rendering diretto comporta l'esecuzione dell'override del metodo <xref:System.Windows.UIElement.OnRender%2A> di <xref:System.Windows.FrameworkElement> e la specifica di operazioni <xref:System.Windows.Media.DrawingContext> che definiscono in modo esplicito gli elementi visivi del componente.  Questo è il metodo utilizzato da <xref:System.Windows.Controls.Image> e <xref:System.Windows.Controls.Border>.  La composizione di elementi personalizzati comporta l'utilizzo di oggetti di tipo <xref:System.Windows.Media.Visual> per comporre l'aspetto del componente.  Per un esempio, vedere [Utilizzo degli oggetti DrawingVisual](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md).  <xref:System.Windows.Controls.Primitives.Track> è un esempio di controllo di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che utilizza la composizione di elementi personalizzati.  È inoltre possibile combinare il rendering diretto e la composizione di elementi personalizzati nello stesso controllo.  
  
#### Vantaggi della derivazione dall'oggetto FrameworkElement  
 Si consideri di utilizzare la derivazione da <xref:System.Windows.FrameworkElement> in presenza di una qualsiasi delle condizioni seguenti:  
  
-   Si desidera disporre di un controllo più preciso sull'aspetto del controllo oltre a quello offerto dalla semplice composizione di elementi.  
  
-   Si desidera definire l'aspetto del controllo definendo una logica di rendering personalizzata.  
  
-   Si desidera comporre gli elementi esistenti in modalità nuove che vanno oltre le possibilità offerte da <xref:System.Windows.Controls.UserControl> e <xref:System.Windows.Controls.Control>.  
  
<a name="control_authoring_basics"></a>   
## Nozioni fondamentali sulla modifica dei controlli  
 Come illustrato in precedenza, tra le funzionalità più efficaci di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vi è la possibilità di andare oltre l'impostazione delle proprietà di base di un controllo per modificarne l'aspetto e il comportamento senza dover necessariamente creare un controllo personalizzato. Le funzionalità di applicazione di stili, associazione dati e trigger sono possibili grazie al sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e al sistema di eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Nelle sezioni seguenti vengono descritte alcune procedure che è necessario seguire, indipendentemente dal modello utilizzato per creare il controllo personalizzato, in modo che gli utenti del controllo personalizzato siano in grado di utilizzare tali funzionalità come se si trattasse di un controllo incluso in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Utilizzare proprietà di dipendenza  
 Con le proprietà di dipendenza è possibile eseguire le operazioni indicate di seguito:  
  
-   Impostare la proprietà in uno stile.  
  
-   Associare la proprietà a un'origine dati.  
  
-   Utilizzare una risorsa dinamica come valore della proprietà.  
  
-   Animare la proprietà.  
  
 Perché una proprietà del controllo supporti una di tali funzionalità, è necessario implementarla come proprietà di dipendenza.  Nell'esempio seguente viene definita una proprietà di dipendenza denominata `Value` mediante le operazioni seguenti:  
  
-   Definizione di un identificatore <xref:System.Windows.DependencyProperty> denominato `ValueProperty` come campo `static` `public` `readonly`.  
  
-   Registrazione del nome della proprietà nel sistema di proprietà mediante una chiamata a <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=fullName> per specificare gli elementi seguenti:  
  
    -   Nome della proprietà.  
  
    -   Tipo della proprietà.  
  
    -   Tipo proprietario della proprietà.  
  
    -   Metadati della proprietà.  I metadati contengono il valore predefinito della proprietà, <xref:System.Windows.CoerceValueCallback> e <xref:System.Windows.PropertyChangedCallback>.  
  
-   Definizione di una proprietà del wrapper [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] denominata `Value`, ovvero lo stesso nome utilizzato per la registrazione della proprietà di dipendenza, mediante l'implementazione delle funzioni di accesso `get` e `set` della proprietà.  Si noti che le funzioni di accesso `get` e `set` sono unicamente in grado di chiamare rispettivamente <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>.  È consigliabile che le funzioni di accesso delle proprietà di dipendenza non contengano logica aggiuntiva poiché i client e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] possono ignorare le funzioni di accesso e chiamare direttamente <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>.  Ad esempio, quando una proprietà è associata a un'origine dati, la funzione di accesso `set` della proprietà non viene chiamata.  Anziché aggiungere logica aggiuntiva alle funzioni di accesso get e set, utilizzare i delegati <xref:System.Windows.ValidateValueCallback>, <xref:System.Windows.CoerceValueCallback> e <xref:System.Windows.PropertyChangedCallback> per rispondere o controllare il valore in caso di modifica.  Per ulteriori informazioni su tali callback, vedere [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  
  
-   Definire un metodo per <xref:System.Windows.CoerceValueCallback> denominato `CoerceValue`.  `CoerceValue` garantisce che `Value` sia maggiore o uguale a `MinValue` e minore o uguale a `MaxValue`.  
  
-   Definire un metodo per <xref:System.Windows.PropertyChangedCallback> denominato `OnValueChanged`.  `OnValueChanged` crea un oggetto <xref:System.Windows.RoutedPropertyChangedEventArgs%601> e prepara la generazione dell'evento indirizzato `ValueChanged`.  Gli eventi indirizzati verranno illustrati nella sezione successiva.  
  
 [!code-csharp[UserControlNumericUpDown#DependencyProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
 [!code-vb[UserControlNumericUpDown#DependencyProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]  
  
 Per ulteriori informazioni, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
### Utilizzo di eventi indirizzati  
 Analogamente alle [proprietà di dipendenza](GTMT), che estendono il concetto di proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] con funzionalità aggiuntive, gli [eventi indirizzati](GTMT) estendono il concetto di eventi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] standard.  Quando si crea un nuovo controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è inoltre consigliabile implementare l'evento come evento indirizzato, in quanto gli eventi indirizzati supportano il comportamento seguente:  
  
-   Possibilità di gestire eventi in un elemento padre di più controlli.  Se si tratta di un evento di bubbling, un solo elemento padre nella struttura ad albero dell'elemento è in grado di sottoscrivere l'evento.  Gli autori dell'applicazione potranno quindi utilizzare un solo gestore per rispondere all'evento di più controlli.  Se, ad esempio, il controllo fa parte di ciascun elemento di <xref:System.Windows.Controls.ListBox> in quanto incluso in <xref:System.Windows.DataTemplate>, lo sviluppatore di applicazioni potrà definire il gestore eventi per l'evento del controllo in <xref:System.Windows.Controls.ListBox>.  Il gestore eventi viene chiamato ogni volta che l'evento si verifica in uno dei controlli.  
  
-   Possibilità di utilizzare eventi indirizzati in <xref:System.Windows.EventSetter>, che consente agli sviluppatori di applicazioni di specificare il gestore di un evento all'interno di uno stile.  
  
-   Possibilità di utilizzare eventi indirizzati in <xref:System.Windows.EventTrigger>, che consente l'animazione di proprietà mediante [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
 Nell'esempio seguente viene definito un evento indirizzato effettuando le operazioni seguenti:  
  
-   Definizione di un identificatore <xref:System.Windows.RoutedEvent> denominato `ValueChangedEvent` come campo `static` `public` `readonly`.  
  
-   Registrazione di un evento indirizzato mediante la chiamata al metodo <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=fullName>.  Nell'esempio vengono specificate le informazioni indicate di seguito nella chiamata a <xref:System.Windows.EventManager.RegisterRoutedEvent%2A>:  
  
    -   Il nome dell'evento è `ValueChanged`.  
  
    -   La strategia di routing è <xref:System.Windows.RoutingStrategy>: vale a dire che viene chiamato innanzitutto un gestore eventi nell'origine \(l'oggetto che genera l'evento\); vengono quindi chiamati in successione i gestori eventi negli elementi padre dell'origine, a partire dal gestore eventi nell'elemento padre più vicino.  
  
    -   Il tipo del gestore eventi è <xref:System.Windows.RoutedPropertyChangedEventHandler%601>, costruito con un tipo <xref:System.Decimal>.  
  
    -   Il tipo proprietario dell'evento è `NumericUpDown`.  
  
-   Dichiarazione di un evento pubblico denominato `ValueChanged` e inclusione di dichiarazioni delle funzioni di accesso agli eventi.  Nell'esempio viene chiamato l'oggetto <xref:System.Windows.UIElement.AddHandler%2A> nella dichiarazione della funzione di accesso `add` e <xref:System.Windows.UIElement.RemoveHandler%2A> nella dichiarazione della funzione di accesso `remove` per utilizzare i servizi eventi di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Creazione di un metodo virtuale protetto denominato `OnValueChanged` che genera l'evento `ValueChanged`.  
  
 [!code-csharp[UserControlNumericUpDown#RoutedEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
 [!code-vb[UserControlNumericUpDown#RoutedEvent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md) e [Creare un evento indirizzato personalizzato](../../../../docs/framework/wpf/advanced/how-to-create-a-custom-routed-event.md).  
  
### Utilizzare l'associazione  
 Per separare l'interfaccia utente del controllo dalla relativa logica, è possibile utilizzare l'associazione dati.  Tale operazione risulta particolarmente importante se si definisce l'aspetto del controllo mediante <xref:System.Windows.Controls.ControlTemplate>.  L'utilizzo dell'associazione dati consente di eliminare la necessità di fare riferimento a parti specifiche dell'interfaccia utente dal codice.  È consigliabile non fare riferimento a elementi presenti in <xref:System.Windows.Controls.ControlTemplate> poiché quando il codice fa riferimento a elementi presenti in <xref:System.Windows.Controls.ControlTemplate> e <xref:System.Windows.Controls.ControlTemplate> viene modificato, l'elemento a cui si fa riferimento deve essere incluso nel nuovo oggetto <xref:System.Windows.Controls.ControlTemplate>.  
  
 Nell'esempio riportato di seguito viene aggiornato l'oggetto <xref:System.Windows.Controls.TextBlock> del controllo `NumericUpDown` mediante l'assegnazione di un nome e l'uso del nome nel codice per fare riferimento alla casella di testo.  
  
 [!code-xml[UserControlNumericUpDownSimple#UIRefMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]  
  
 [!code-csharp[UserControlNumericUpDownSimple#UIRefCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
 [!code-vb[UserControlNumericUpDownSimple#UIRefCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]  
  
 Negli esempi riportati di seguito viene utilizzata l'associazione per ottenere lo stesso risultato.  
  
 [!code-xml[UserControlNumericUpDown#Binding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]  
  
 Per ulteriori informazioni sull'associazione dati, vedere [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md).  
  
### Progettare le finestre di progettazione  
 Per ottenere supporto per i controlli WPF personalizzati in [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] \(ad esempio, la modifica delle proprietà con la finestra Proprietà\), attenersi alle linee guida riportate di seguito.  Per ulteriori informazioni sullo sviluppo per [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)], vedere [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26).  
  
#### Proprietà di dipendenza  
 Implementare le funzioni di accesso [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] `get` e `set` come descritto in precedenza in "Utilizzare proprietà di dipendenza". Nelle finestre di progettazione è possibile utilizzare il wrapper per rilevare la presenza di una proprietà di dipendenza, ma, come accade per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e per i client del controllo, non è necessario chiamare le funzioni di accesso quando si ottiene o si imposta la proprietà.  
  
#### Proprietà associate  
 È necessario implementare le proprietà associate sui controlli personalizzati attenendosi alle linee guida riportate di seguito:  
  
-   Disporre di un oggetto <xref:System.Windows.DependencyProperty> `static` `public` `readonly` nel formato *NomeProprietà*`Property` creato utilizzando il metodo <xref:System.Windows.DependencyProperty.RegisterAttached%2A>.  Il nome della proprietà passato a <xref:System.Windows.DependencyProperty.RegisterAttached%2A> deve corrispondere a *NomeProprietà*.  
  
-   Implementare una coppia di metodi CLR `public``static` denominati `Set`*NomeProprietà* e `Get`*NomeProprietà*.  Entrambi i metodi devono accettare una classe derivata da <xref:System.Windows.DependencyProperty> come primo argomento.  Il metodo `Set`*NomeProprietà* accetta anche un argomento il cui tipo corrisponde al tipo di dati registrato per la proprietà.  Il metodo `Get`*NomeProprietà* deve restituire un valore dello stesso tipo.  In assenza del metodo `Set`*NomeProprietà*, la proprietà viene contrassegnata come di sola lettura.  
  
-   `Set` *NomeProprietà* e `Get`*NomeProprietà* devono essere indirizzati rispettivamente ai metodi <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A> sull'oggetto di dipendenza di destinazione in modo diretto.  Le finestre di progettazione consentono di accedere alla proprietà associata tramite chiamate rivolte al wrapper del metodo oppure tramite chiamata diretta all'oggetto di dipendenza di destinazione.  
  
 Per ulteriori informazioni sulle proprietà associate, vedere [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
### Definire e utilizzare risorse condivise  
 È possibile includere il controllo nello stesso assembly dell'applicazione o è possibile inserire il controllo in un package di un assembly separato che può essere utilizzato in più applicazioni.  Nella maggior parte dei casi, le informazioni riportate in questo argomento si applicano indipendentemente dal metodo utilizzato.  È importante tuttavia notare una differenza.  Quando si inserisce un controllo nello stesso assembly di un'applicazione, è possibile aggiungere risorse globali al file App.xaml.  Il file App.xaml non è invece disponibile per gli assembly contenenti solo controlli che non dispongono di un oggetto <xref:System.Windows.Application> associato.  
  
 Quando un'applicazione cerca una risorsa, la ricerca viene effettuata a tre livelli nell'ordine seguente:  
  
1.  Livello dell'elemento.  
  
     Il sistema inizia dall'elemento che fa riferimento alla risorsa, quindi esegue la ricerca delle risorse dell'elemento padre logico continuando fino a raggiungere l'elemento radice.  
  
2.  Livello dell'applicazione.  
  
     Risorse definite dall'oggetto <xref:System.Windows.Application>.  
  
3.  Livello del tema.  
  
     I dizionari a livello tema vengono archiviati in una sottocartella denominata Themes.  I file nella cartella Themes corrispondono ai temi.  Potrebbero ad esempio essere presenti Aero.NormalColor.xaml, Luna.NormalColor.xaml, Royale.NormalColor.xaml e così via.  È inoltre possibile disporre di un file denominato generic.xaml.  Quando il sistema cerca una risorsa a livello tema, la ricerca viene effettuata prima nel file del tema specifico e poi nel file generic.xaml.  
  
 Quando il controllo si trova in un assembly separato dall'applicazione, è necessario inserire le risorse globali a livello elemento o a livello tema.  Entrambi i metodi presentano dei vantaggi.  
  
#### Definizione di risorse al livello elemento  
 È possibile definire le risorse condivise a livello elemento creando un dizionario risorse personalizzato e unendolo al dizionario risorse del controllo.  Quando si utilizza questo metodo, è possibile assegnare un nome qualsiasi al file di risorse e posizionare il file nella stessa cartella dei controlli.  Le risorse a livello elemento possono inoltre utilizzare semplici stringhe come chiavi.  Nell'esempio seguente viene creato un file di risorse di <xref:System.Windows.Media.LinearGradientBrush> denominato Dictionary1.xaml.  
  
 [!code-xml[SharedResources#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]  
  
 Dopo aver definito il dizionario, è necessario unirlo al dizionario risorse del controllo.  A tale scopo è possibile utilizzare [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o il codice.  
  
 Nell'esempio seguente viene unito un dizionario risorse mediante [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-xml[SharedResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]  
  
 Questo approccio comporta tuttavia la creazione di un oggetto <xref:System.Windows.ResourceDictionary> ogni volta che vi si fa riferimento.  Ad esempio, se si dispone di 10 controlli personalizzati nella libreria e si uniscono i dizionari delle risorse condivise di ogni controllo mediante XAML, si creano 10 oggetti <xref:System.Windows.ResourceDictionary> identici.  È possibile evitare questo problema creando una classe statica che unisce le risorse nel codice e restituisce l'oggetto <xref:System.Windows.ResourceDictionary> risultante.  
  
 Nell'esempio seguente viene creata una classe che restituisce un oggetto <xref:System.Windows.ResourceDictionary> condiviso.  
  
 [!code-csharp[SharedResources#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]  
  
 Nell'esempio seguente viene unita la risorsa condivisa alle risorse di un controllo personalizzato nel costruttore del controllo prima che venga chiamato `InitilizeComponent`.  Poiché `SharedDictionaryManager.SharedDictionary` è una proprietà statica, l'oggetto <xref:System.Windows.ResourceDictionary> viene creato solo una volta.  Poiché il dizionario risorse è stato unito prima che venisse chiamato `InitializeComponent`, le risorse sono disponibili al controllo nel file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
 [!code-csharp[SharedResources#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]  
  
#### Definizione di risorse al livello tema  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consente di creare risorse per diversi temi di Windows.  Come autore dei controlli, è possibile definire una risorsa per un tema specifico in modo da modificare l'aspetto del controllo a seconda del tema utilizzato.  Ad esempio, l'aspetto di un oggetto <xref:System.Windows.Controls.Button> nel tema Windows Classico, ovvero il tema predefinito per Windows 2000, differisce da un oggetto <xref:System.Windows.Controls.Button> nel tema Windows Luna, ovvero il tema predefinito per Windows XP, poiché l'oggetto <xref:System.Windows.Controls.Button> utilizza un oggetto <xref:System.Windows.Controls.ControlTemplate> diverso per ogni tema.  
  
 Le risorse specifiche di un tema vengono inserite in un dizionario risorse con un nome file specifico.  Questi file devono risiedere in una cartella denominata `Themes` che è una sottocartella della cartella contenente il controllo.  Nella tabella seguente sono elencati i file del dizionario risorse e il tema associato a ogni file:  
  
|Nome del file del dizionario risorse|Tema di Windows|  
|------------------------------------------|---------------------|  
|`Classic.xaml`|Aspetto classico di Windows 9x\/2000 in Windows XP|  
|`Luna.NormalColor.xaml`|Tema blu predefinito in Windows XP|  
|`Luna.Homestead.xaml`|Tema verde oliva in Windows XP|  
|`Luna.Metallic.xaml`|Tema argento in Windows XP|  
|`Royale.NormalColor.xaml`|Tema predefinito in Windows XP Media Center Edition|  
|`Aero.NormalColor.xaml`|Tema predefinito in Windows Vista|  
  
 Non è necessario definire una risorsa per ogni tema.  Se una risorsa non è definita per un tema specifico, il controllo verifica `Classic.xaml` per tale risorsa.  Se la risorsa non è definita nel file che corrisponde al tema corrente o in `Classic.xaml`, il controllo utilizza la risorsa generica, che si trova in un file del dizionario risorse denominato `generic.xaml`.  Il file `generic.xaml` è posto nella stessa cartella dei file dei dizionari risorse specifici del tema.  Sebbene `generic.xaml` non corrisponda a un tema di Windows specifico, è ancora un dizionario a livello tema.  
  
 L'[esempio di controllo personalizzato NumericUpDown con supporto per temi e animazione interfaccia utente](http://go.microsoft.com/fwlink/?LinkID=160025) contiene due dizionari risorse per li controllo `NumericUpDown`: uno in generic.xaml e uno in Luna.NormalColor.xaml.  È possibile eseguire l'applicazione e passare dal tema argento in Windows XP a un altro tema per vedere la differenza tra i due modelli del controllo.  Se si utilizza Windows Vista, è possibile rinominare Luna.NormalColor.xaml in Aero.NormalColor.xaml e passare da un tema all'altro, ad esempio Windows Classic e il tema predefinito per Windows Vista.  
  
 Quando si inserisce un oggetto <xref:System.Windows.Controls.ControlTemplate> in uno dei file dei dizionari risorse specifici del tema, è necessario creare un costruttore statico per il controllo e chiamare il metodo <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> su <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>, come illustrato nell'esempio seguente.  
  
 [!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
 [!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]  
  
##### Definizione delle chiavi e relativo riferimento per le risorse del tema  
 Quando si definisce una risorsa a livello elemento, è possibile assegnare una stringa come chiave e accedere alla risorsa tramite la stringa.  Quando si definisce una risorsa a livello tema, è necessario utilizzare un oggetto <xref:System.Windows.ComponentResourceKey> come chiave.  Nell'esempio seguente viene definita una risorsa nel file generic.xaml.  
  
  
  
 Nell'esempio seguente viene fatto riferimento alla risorsa specificando l'oggetto <xref:System.Windows.ComponentResourceKey> come chiave.  
  
  
  
##### Specifica del percorso delle risorse del tema  
 Per trovare le risorse per un controllo, è necessario indicare all'applicazione host che l'assembly contiene risorse specifiche del controllo.  È possibile eseguire questa operazione aggiungendo l'oggetto <xref:System.Windows.ThemeInfoAttribute> all'assembly che contiene il controllo.  L'oggetto <xref:System.Windows.ThemeInfoAttribute> contiene una proprietà <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> che specifica il percorso delle risorse generiche e una proprietà <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> che specifica il percorso delle risorse specifiche del tema.  
  
 Nell'esempio seguente vengono impostate le proprietà <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> e <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> su <xref:System.Windows.ResourceDictionaryLocation>, per specificare che le risorse generiche e quelle specifiche del tema risiedono nello stesso assembly del controllo.  
  
 [!code-csharp[CustomControlNumericUpDown#ThemesSection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
 [!code-vb[CustomControlNumericUpDown#ThemesSection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]  
  
## Vedere anche  
 [WPF Designer](http://msdn.microsoft.com/it-it/c6c65214-8411-4e16-b254-163ed4099c26)   
 [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [Personalizzazione dei controlli](../../../../docs/framework/wpf/controls/control-customization.md)