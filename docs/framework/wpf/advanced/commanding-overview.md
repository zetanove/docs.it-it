---
title: "Cenni preliminari sull&#39;esecuzione di comandi | Microsoft Docs"
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
  - "classi, CommandBinding"
  - "libreria di comandi"
  - "CommandBindings"
  - "esecuzione di comandi"
  - "CommandManager"
  - "comandi, definizione"
  - "ICommandSource (interfacce)"
  - "interfacce, ICommandSource"
ms.assetid: bc208dfe-367d-426a-99de-52b7e7511e81
caps.latest.revision: 35
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# Cenni preliminari sull&#39;esecuzione di comandi
<a name="introduction"></a> L'esecuzione di comandi è un meccanismo di input di [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] che fornisce la gestione di input a un livello semantico maggiore rispetto all'input del dispositivo.  Le operazioni **Copia**, **Taglia** e **Incolla** presenti in molte applicazioni sono esempi di comandi.  
  
 In questi cenni preliminari vengono definiti i comandi presenti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], le classi che fanno parte del modello di esecuzione di comandi e la modalità di utilizzo e di creazione di comandi all'interno delle applicazioni.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Definizione dei comandi](#commands_at_10000_feet)  
  
-   [Esempio di comando semplice in WPF](#simple_command)  
  
-   [Quattro concetti principali relativi all'esecuzione di comandi in WPF](#Four_main_Concepts)  
  
-   [Libreria dei comandi](#Command_Library)  
  
-   [Creazione di comandi personalizzati](#creating_commands)  
  
<a name="commands_at_10000_feet"></a>   
## Definizione dei comandi  
 I comandi hanno diversi scopi.  Il primo scopo è di separare la semantica e l'oggetto che richiama un comando dalla logica che esegue il comando.  In questo modo, più codici sorgente diversi possono richiamare la stessa logica di comando che pertanto può essere personalizzata per obiettivi differenti.  Le operazioni di modifica **Copia**, **Taglia** e **Incolla**, ad esempio, disponibili in molte applicazioni, possono essere richiamate utilizzando azioni dell'utente diverse se vengono implementati tramite i comandi.  Un'applicazione potrebbe consentire a un utente di tagliare gli oggetti o il testo selezionato facendo clic su un pulsante, scegliendo una voce da un menu o utilizzando una combinazione di tasti, ad esempio CTRL\+X.  Utilizzando i comandi, è possibile associare ogni tipo di azione utente alla stessa logica.  
  
 Un altro scopo dei comandi è di indicare se un'azione è disponibile.  Per continuare con l'esempio in cui viene tagliato un oggetto o un testo, l'azione ha senso solo quando viene selezionato un elemento.  Se un utente tenta di tagliare un oggetto o un testo senza avere selezionato alcun elemento, non viene eseguita alcuna operazione.  Per indicarlo all'utente, in molte applicazioni vengono disabilitati i pulsanti e le voci di menu in modo che l'utente sappia se è possibile eseguire un'azione.  Un comando può indicare se un'azione è possibile implementando il metodo <xref:System.Windows.Input.ICommand.CanExecute%2A>.  Un pulsante può sottoscrivere l'evento <xref:System.Windows.Input.ICommand.CanExecuteChanged> ed essere disabilitato se <xref:System.Windows.Input.ICommand.CanExecute%2A> restituisce `false` oppure essere abilitato se <xref:System.Windows.Input.ICommand.CanExecute%2A> restituisce `true`.  
  
 La semantica di un comando può essere coerente tra le applicazioni e le classi, tuttavia la logica dell'azione è specifica dell'oggetto particolare su cui si agisce.  La combinazione di tasti CTRL\+X richiama il comando **Taglia** nelle classi di testo, nelle classi di immagine e nei Web browser, tuttavia la logica effettiva per l'esecuzione dell'operazione **Taglia** viene definita dall'applicazione in cui si esegue l'operazione di taglio.  Un oggetto <xref:System.Windows.Input.RoutedCommand> consente ai client di implementare la logica.  Un oggetto testo può tagliare il testo selezionato negli Appunti, mentre un oggetto immagine può tagliare l'immagine selezionata.  Quando un'applicazione gestisce l'evento <xref:System.Windows.Input.CommandManager.Executed>, dispone di accesso alla destinazione del comando e può eseguire l'azione appropriata in base al tipo della destinazione.  
  
<a name="simple_command"></a>   
## Esempio di comando semplice in WPF  
 Il modo più semplice per utilizzare un comando in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste nell'utilizzo di un oggetto <xref:System.Windows.Input.RoutedCommand> predefinito di una delle classi della libreria dei comandi; nell'utilizzare un controllo che dispone del supporto nativo per gestire il comando; nell'utilizzare un controllo che dispone del supporto nativo per richiamare un comando.  Il comando <xref:System.Windows.Input.ApplicationCommands.Paste%2A> è uno dei comandi predefiniti della classe <xref:System.Windows.Input.ApplicationCommands>.  Il controllo <xref:System.Windows.Controls.TextBox> dispone di una logica incorporata per la gestione del comando <xref:System.Windows.Input.ApplicationCommands.Paste%2A>.  La classe <xref:System.Windows.Controls.MenuItem> dispone del supporto nativo per richiamare i comandi.  
  
 Nell'esempio seguente viene mostrato come configurare un oggetto <xref:System.Windows.Controls.MenuItem> in modo che, una volta selezionato, richiami il comando <xref:System.Windows.Input.ApplicationCommands.Paste%2A> su un oggetto <xref:System.Windows.Controls.TextBox>, presupponendo che l'oggetto <xref:System.Windows.Controls.TextBox> disponga dello stato attivo.  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewSimpleCommand](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewsimplecommand)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Four_main_Concepts"></a>   
## Quattro concetti principali relativi all'esecuzione di comandi in WPF  
 Il modello di comando indirizzato di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] può essere suddiviso in quattro concetti principali: il comando, l'origine comando, la destinazione comando e l'associazione comando:  
  
-   Il *comando* è l'azione da eseguire.  
  
-   L'*origine comando* è l'oggetto che richiama il comando.  
  
-   La *destinazione comando* è l'oggetto sul quale il comando viene eseguito.  
  
-   L'*associazione comando* è l'oggetto che esegue il mapping della logica di comando al comando.  
  
 Nell'esempio precedente, il comando <xref:System.Windows.Input.ApplicationCommands.Paste%2A> rappresenta il comando, l'oggetto <xref:System.Windows.Controls.MenuItem> rappresenta l'origine comando, l'oggetto <xref:System.Windows.Controls.TextBox> rappresenta la destinazione comando e l'associazione comando viene fornita dal controllo <xref:System.Windows.Controls.TextBox>.  È importante notare che non sempre l'oggetto <xref:System.Windows.Input.CommandBinding> viene fornito dal controllo che rappresenta la classe di destinazione comando.  Spesso, l'oggetto <xref:System.Windows.Input.CommandBinding> deve essere creato dallo sviluppatore di applicazioni oppure può essere associato a un predecessore della destinazione comando.  
  
<a name="Commands"></a>   
### Comandi  
 I comandi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] vengono creati implementando l'interfaccia <xref:System.Windows.Input.ICommand>.  <xref:System.Windows.Input.ICommand> espone due metodi, <xref:System.Windows.Input.ICommand.Execute%2A> e <xref:System.Windows.Input.ICommand.CanExecute%2A>, e un evento, <xref:System.Windows.Input.ICommand.CanExecuteChanged>.  <xref:System.Windows.Input.ICommand.Execute%2A> esegue le azioni associate al comando. <xref:System.Windows.Input.ICommand.CanExecute%2A> determina se sia possibile eseguirlo sulla destinazione corrente.  Viene generato <xref:System.Windows.Input.ICommand.CanExecuteChanged>se il gestore che centralizza le operazioni di comando rileva una modifica nell'origine del comando che potrebbe invalidare un comando generato ma non ancora eseguito dall'associazione del comando.  L'implementazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dell'oggetto <xref:System.Windows.Input.ICommand> è la classe <xref:System.Windows.Input.RoutedCommand> e rappresenta l'oggetto di discussione principale di questi cenni preliminari.  
  
 Le origini di input principali di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono il mouse, la tastiera, l'input penna e i comandi indirizzati.  La maggior parte degli input orientati al dispositivo utilizzano un oggetto <xref:System.Windows.RoutedEvent> per notificare agli oggetti di una pagina dell'applicazione che si è verificato un evento di input.  Un oggetto <xref:System.Windows.Input.RoutedCommand> non è diverso.  I metodi <xref:System.Windows.Input.RoutedCommand.Execute%2A> e <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> di un oggetto <xref:System.Windows.Input.RoutedCommand> non contengono la logica dell'applicazioni per il comando, piuttosto generano eventi indirizzati che effettuano il tunneling e il bubbling della struttura ad albero dell'elemento, finché non incontrano un oggetto con <xref:System.Windows.Input.CommandBinding>.  Nell'oggetto <xref:System.Windows.Input.CommandBinding> sono contenuti i gestori di questi eventi, i quali eseguono il comando.  Per ulteriori informazioni sul routing degli eventi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 Il metodo <xref:System.Windows.Input.RoutedCommand.Execute%2A> di un oggetto <xref:System.Windows.Input.RoutedCommand> genera gli eventi <xref:System.Windows.Input.CommandManager.PreviewExecuted> e <xref:System.Windows.Input.CommandManager.Executed> sulla destinazione comando.  Il metodo <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> di un oggetto <xref:System.Windows.Input.RoutedCommand> genera gli eventi <xref:System.Windows.Input.CommandManager.CanExecute> e <xref:System.Windows.Input.CommandManager.PreviewCanExecute> sulla destinazione comando.  Tali eventi eseguono il tunneling e il bubbling nella struttura ad albero dell'elemento finché non incontrano un oggetto che dispone di un oggetto <xref:System.Windows.Input.CommandBinding> per quel particolare comando.  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornito un set di comandi indirizzati comuni contenuti in più classi: <xref:System.Windows.Input.MediaCommands>, <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.ComponentCommands> e <xref:System.Windows.Documents.EditingCommands>.  Queste classi sono costituite solo da oggetti <xref:System.Windows.Input.RoutedCommand> e non dalla logica di implementazione del comando.  La logica di implementazione è responsabilità dell'oggetto sul quale il comando viene eseguito.  
  
<a name="Command_Sources"></a>   
### Origini comando  
 Un origine comando è l'oggetto che richiama il comando.  <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.Button> e <xref:System.Windows.Input.KeyGesture> sono esempi di origini comando.  
  
 In genere, le origini comando di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] implementano l'interfaccia <xref:System.Windows.Input.ICommandSource>.  
  
 L'oggetto <xref:System.Windows.Input.ICommandSource> espone tre proprietà: <xref:System.Windows.Input.ICommandSource.Command%2A>, <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> e <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>:  
  
-   La proprietà <xref:System.Windows.Input.ICommandSource.Command%2A> è il comando da eseguire quando viene richiamata l'origine comando.  
  
-   La proprietà <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> è l'oggetto su cui eseguire il comando.  È importante notare che in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la proprietà <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> di <xref:System.Windows.Input.ICommandSource> può essere applicata solo quando l'oggetto <xref:System.Windows.Input.ICommand> è un oggetto <xref:System.Windows.Input.RoutedCommand>.  Se l'oggetto <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> viene impostato su <xref:System.Windows.Input.ICommandSource> e il comando corrispondente non è un oggetto <xref:System.Windows.Input.RoutedCommand>, la destinazione comando viene ignorata.  Se la proprietà <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> non viene impostata, l'elemento con lo stato attivo sarà la destinazione comando.  
  
-   L'oggetto <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> è un tipo di dati definito dall'utente utilizzato per passare informazioni ai gestori che implementano il comando.  
  
 Le classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che implementano l'oggetto <xref:System.Windows.Input.ICommandSource> sono: <xref:System.Windows.Controls.Primitives.ButtonBase>, <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Documents.Hyperlink> e <xref:System.Windows.Input.InputBinding>.  Gli oggetti <xref:System.Windows.Controls.Primitives.ButtonBase>, <xref:System.Windows.Controls.MenuItem> e <xref:System.Windows.Documents.Hyperlink> richiamano un comando quando vengono selezionati, mentre l'oggetto <xref:System.Windows.Input.InputBinding> richiama un comando quando viene eseguito l'oggetto <xref:System.Windows.Input.InputGesture> associato.  
  
 Nell'esempio seguente viene illustrato come utilizzare <xref:System.Windows.Controls.MenuItem> in <xref:System.Windows.Controls.ContextMenu> come un'origine comando per il comando <xref:System.Windows.Input.ApplicationCommands.Properties%2A>.  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewCmdSourceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcmdsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCmdSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcmdsource)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCmdSource](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcmdsource)]  
  
 In genere, un'origine comando resterà in ascolto dell'evento <xref:System.Windows.Input.RoutedCommand.CanExecuteChanged>.  Tale evento informa l'origine comando relativamente alla probabile modifica della capacità del comando di essere eseguito sulla destinazione comando corrente.  L'origine comando può eseguire una query sullo stato corrente dell'oggetto <xref:System.Windows.Input.RoutedCommand> utilizzando il metodo <xref:System.Windows.Input.RoutedCommand.CanExecute%2A>.  L'origine comando può quindi disabilitarsi, se l'esecuzione del comando non riesce.  Un esempio viene fornito dal fatto che l'oggetto <xref:System.Windows.Controls.MenuItem> diventa di colore grigio quando non è possibile eseguire un comando.  
  
 Un oggetto <xref:System.Windows.Input.InputGesture> può essere utilizzato come origine comando.  Gli oggetti <xref:System.Windows.Input.KeyGesture> e <xref:System.Windows.Input.MouseGesture> sono due tipi di movimento di input di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È possibile considerare un oggetto <xref:System.Windows.Input.KeyGesture> come un tasto di scelta rapida, ad esempio CTRL\+C.  Un oggetto <xref:System.Windows.Input.KeyGesture> è costituito da un oggetto <xref:System.Windows.Input.Key> e da un insieme di oggetti <xref:System.Windows.Input.ModifierKeys>.  Un oggetto <xref:System.Windows.Input.MouseGesture> è costituito da un oggetto <xref:System.Windows.Input.MouseAction> e da un insieme facoltativo di oggetti <xref:System.Windows.Input.ModifierKeys>.  
  
 Affinché un oggetto <xref:System.Windows.Input.InputGesture> funzioni come origine comando, deve essere associato a un comando.  Questa operazione può essere eseguita in diversi modi.  Uno di questi consiste nell'utilizzare un oggetto <xref:System.Windows.Input.InputBinding>.  
  
 Nell'esempio seguente viene illustrato come creare un oggetto <xref:System.Windows.Input.KeyBinding> tra un oggetto <xref:System.Windows.Input.KeyGesture> e un oggetto <xref:System.Windows.Input.RoutedCommand>.  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewXAMLKeyBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlkeybinding)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeybinding)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeybinding)]  
  
 Un altro modo per associare un oggetto <xref:System.Windows.Input.InputGesture> a un oggetto <xref:System.Windows.Input.RoutedCommand> consiste nell'aggiungere <xref:System.Windows.Input.InputGesture> all'oggetto <xref:System.Windows.Input.InputGestureCollection> nell'oggetto <xref:System.Windows.Input.RoutedCommand>.  
  
 Nell'esempio seguente viene illustrato come aggiungere un oggetto <xref:System.Windows.Input.KeyGesture> all'oggetto <xref:System.Windows.Input.InputGestureCollection> di un oggetto <xref:System.Windows.Input.RoutedCommand>.  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeygestureoncmd)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeygestureoncmd)]  
  
<a name="Command_Binding"></a>   
### CommandBinding  
 Un oggetto <xref:System.Windows.Input.CommandBinding> associa un comando ai gestori eventi che implementano il comando.  
  
 La classe <xref:System.Windows.Input.CommandBinding> contiene una proprietà <xref:System.Windows.Input.CommandBinding.Command%2A> e gli eventi <xref:System.Windows.Input.CommandBinding.PreviewExecuted>, <xref:System.Windows.Input.CommandBinding.Executed>, <xref:System.Windows.Input.CommandBinding.PreviewCanExecute> e <xref:System.Windows.Input.CommandBinding.CanExecute>.  
  
 L'oggetto <xref:System.Windows.Input.CommandBinding.Command%2A> è il comando a cui è associato l'oggetto <xref:System.Windows.Input.CommandBinding>.  I gestori eventi associati agli eventi <xref:System.Windows.Input.CommandBinding.PreviewExecuted> e <xref:System.Windows.Input.CommandBinding.Executed> implementano la logica di comando.  I gestori eventi associati agli eventi <xref:System.Windows.Input.CommandBinding.PreviewCanExecute> e <xref:System.Windows.Input.CommandBinding.CanExecute> determinano se il comando può essere eseguito nella destinazione comando corrente.  
  
 Nell'esempio seguente viene mostrato come creare un oggetto <xref:System.Windows.Input.CommandBinding> nella radice <xref:System.Windows.Window> di un'applicazione.  L'oggetto <xref:System.Windows.Input.CommandBinding> associa il comando <xref:System.Windows.Input.ApplicationCommands.Open%2A> ai gestori <xref:System.Windows.Input.CommandManager.Executed> e <xref:System.Windows.Input.CommandBinding.CanExecute>.  
  
 [!code-xml[commandwithhandler#CommandHandlerCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
 Successivamente, vengono creati gli oggetti <xref:System.Windows.Input.ExecutedRoutedEventHandler> e <xref:System.Windows.Input.CanExecuteRoutedEventHandler>.  <xref:System.Windows.Input.ExecutedRoutedEventHandler> consente di aprire un oggetto <xref:System.Windows.MessageBox> nel quale viene visualizzata una stringa che conferma l'esecuzione del comando.  L'oggetto <xref:System.Windows.Input.CanExecuteRoutedEventHandler> imposta la proprietà <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> su `true`.  
  
 [!code-csharp[commandwithhandler#CommandHandlerExecutedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerexecutedhandler)]
 [!code-vb[commandwithhandler#CommandHandlerExecutedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerexecutedhandler)]  
  
 [!code-csharp[commandwithhandler#CommandHandlerCanExecuteHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlercanexecutehandler)]
 [!code-vb[commandwithhandler#CommandHandlerCanExecuteHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlercanexecutehandler)]  
  
 Un oggetto <xref:System.Windows.Input.CommandBinding> viene associato a un oggetto specifico, ad esempio la radice <xref:System.Windows.Window> dell'applicazione o di un controllo.  L'oggetto a cui è associato l'oggetto <xref:System.Windows.Input.CommandBinding> definisce l'ambito dell'associazione.  Ad esempio, un oggetto <xref:System.Windows.Input.CommandBinding> associato a un predecessore della destinazione comando può essere raggiunto dall'evento <xref:System.Windows.Input.CommandBinding.Executed>, mentre un oggetto <xref:System.Windows.Input.CommandBinding> associato a un discendente della destinazione comando non può essere raggiunto.  Si tratta di una conseguenza diretta del modo in cui un oggetto <xref:System.Windows.RoutedEvent> effettua il tunneling e il bubbling dall'oggetto che genera l'evento.  
  
 In alcune situazioni, l'oggetto <xref:System.Windows.Input.CommandBinding> viene associato alla destinazione comando stessa, ad esempio con la classe <xref:System.Windows.Controls.TextBox> e i comandi <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.ApplicationCommands.Copy%2A>e <xref:System.Windows.Input.ApplicationCommands.Paste%2A>.  Tuttavia, spesso è consigliabile associare l'oggetto <xref:System.Windows.Input.CommandBinding> a un predecessore della destinazione comando, ad esempio l'oggetto <xref:System.Windows.Window> principale o l'oggetto Application, specialmente se lo stesso oggetto <xref:System.Windows.Input.CommandBinding> può essere utilizzato per più destinazioni comando.  Si tratta di decisioni di progettazione di cui tenere conto quando si crea l'infrastruttura di esecuzione dei comandi.  
  
<a name="Commane_Target"></a>   
### Destinazione comando  
 La destinazione comando è l'elemento sul quale viene eseguito il comando.  Per quanto riguarda un oggetto <xref:System.Windows.Input.RoutedCommand>, la destinazione comando è l'elemento a partire dal quale viene avviato il routing degli eventi <xref:System.Windows.Input.CommandManager.Executed> e <xref:System.Windows.Input.CommandManager.CanExecute>.  Come indicato in precedenza, in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la proprietà <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> dell'oggetto <xref:System.Windows.Input.ICommandSource> può essere applicata solo se l'oggetto <xref:System.Windows.Input.ICommand> è un oggetto <xref:System.Windows.Input.RoutedCommand>.  Se l'oggetto <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> viene impostato su <xref:System.Windows.Input.ICommandSource> e il comando corrispondente non è un oggetto <xref:System.Windows.Input.RoutedCommand>, la destinazione comando viene ignorata.  
  
 L'origine comando può impostare in modo esplicito la destinazione comando.  Se quest'ultima non viene definita, l'elemento con lo stato attivo sarà utilizzato come destinazione comando.  Uno dei vantaggi dell'utilizzo dell'elemento con lo stato attivo come destinazione comando consiste nel fatto che consente allo sviluppatore di applicazioni di utilizzare la stessa origine comando per richiamare un comando su più destinazioni senza tenere traccia della destinazione comando.  Se, ad esempio, l'oggetto <xref:System.Windows.Controls.MenuItem> richiama il comando **Incolla** in un'applicazione che dispone di un controllo <xref:System.Windows.Controls.TextBox> e di un controllo <xref:System.Windows.Controls.PasswordBox>, la destinazione può essere l'oggetto <xref:System.Windows.Controls.TextBox> oppure l'oggetto <xref:System.Windows.Controls.PasswordBox>, in base al controllo che dispone dello stato attivo.  
  
 Nell'esempio seguente viene mostrato come impostare in modo esplicito la destinazione comando nel markup e nel code behind.  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewXAMLCommandTarget](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlcommandtarget)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Command_Manager"></a>   
### CommandManager  
 L'oggetto <xref:System.Windows.Input.CommandManager> è utile per molte funzioni relative ai comandi.  Rende disponibile un insieme di metodi statici per aggiungere e rimuovere i gestori eventi <xref:System.Windows.Input.CommandManager.PreviewExecuted>, <xref:System.Windows.Input.CommandManager.Executed>, <xref:System.Windows.Input.CommandManager.PreviewCanExecute> e <xref:System.Windows.Input.CommandManager.CanExecute> da un elemento specifico nonché  un modo per registrare gli oggetti <xref:System.Windows.Input.CommandBinding> e <xref:System.Windows.Input.InputBinding> in una classe specifica.  L'oggetto <xref:System.Windows.Input.CommandManager> fornisce inoltre un modo, tramite l'evento <xref:System.Windows.Input.CommandManager.RequerySuggested>, per notificare a un comando il momento in cui deve generare l'evento <xref:System.Windows.Input.ICommand.CanExecuteChanged>.  
  
 Il metodo <xref:System.Windows.Input.CommandManager.InvalidateRequerySuggested%2A> forza l'oggetto <xref:System.Windows.Input.CommandManager> di generare l'evento <xref:System.Windows.Input.CommandManager.RequerySuggested>.  Ciò è utile per le condizioni che richiedono l'abilitazione o la disabilitazione di un comando ma che l'oggetto <xref:System.Windows.Input.CommandManager> non è in grado di rilevare.  
  
<a name="Command_Library"></a>   
## Libreria dei comandi  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornito un insieme di comandi predefiniti.  La libreria dei comandi include le classi seguenti: <xref:System.Windows.Input.ApplicationCommands>, <xref:System.Windows.Input.NavigationCommands>, <xref:System.Windows.Input.MediaCommands>, <xref:System.Windows.Documents.EditingCommands> e <xref:System.Windows.Input.ComponentCommands>.  Tali classi forniscono comandi, quali <xref:System.Windows.Input.ApplicationCommands.Cut%2A>, <xref:System.Windows.Input.NavigationCommands.BrowseBack%2A> e <xref:System.Windows.Input.NavigationCommands.BrowseForward%2A>, <xref:System.Windows.Input.MediaCommands.Play%2A>, <xref:System.Windows.Input.MediaCommands.Stop%2A> e <xref:System.Windows.Input.MediaCommands.Pause%2A>.  
  
 Molti di questi comandi includono un insieme di associazioni di input predefinite.  Se, ad esempio, si specifica che l'applicazione gestisce il comando di copia, si ottiene automaticamente l'associazione di tastiera "CTRL \+ C". Si ottengono inoltre associazioni per altri dispositivi di input, quali i movimenti della penna [!INCLUDE[TLA2#tla_tpc](../../../../includes/tla2sharptla-tpc-md.md)] e informazioni sulle funzioni vocali.  
  
 Quando si fa riferimento ai comandi delle diverse librerie dei comandi utilizzando [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], in genere è possibile omettere il nome classe della classe di libreria che espone la proprietà del comando statico.  Di solito i nomi dei comandi sono stringhe non ambigue ed esistono tipi proprietari che forniscono un raggruppamento logico di comandi, ma che non sono necessari per la risoluzione dell'ambiguità.  È possibile, ad esempio, specificare `Command="Cut"` anziché l'oggetto `Command="ApplicationCommands.Cut"` più dettagliato.  Si tratta di un meccanismo utile incorporato nel processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per i comandi \(più precisamente, si tratta di un comportamento del convertitore dei tipi di <xref:System.Windows.Input.ICommand> al quale il processore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fa riferimento in fase di caricamento\).  
  
<a name="creating_commands"></a>   
## Creazione di comandi personalizzati  
 Se i comandi delle classi della libreria dei comandi non soddisfano le proprie esigenze, è possibile creare comandi personalizzati.  Questa operazione può essere eseguita in due modi.  Il primo prevede la progettazione da zero e l'implementazione dell'interfaccia <xref:System.Windows.Input.ICommand>.  Il secondo, che costituisce l'approccio più comune, consiste nel creare un oggetto <xref:System.Windows.Input.RoutedCommand> o un oggetto <xref:System.Windows.Input.RoutedUICommand>.  
  
 Per un esempio di creazione di un oggetto <xref:System.Windows.Input.RoutedCommand> personalizzato, vedere [Esempio di creazione di un RoutedCommand personalizzato](http://go.microsoft.com/fwlink/?LinkID=159980) \(la pagina potrebbe essere in inglese\).  
  
## Vedere anche  
 <xref:System.Windows.Input.RoutedCommand>   
 <xref:System.Windows.Input.CommandBinding>   
 <xref:System.Windows.Input.InputBinding>   
 <xref:System.Windows.Input.CommandManager>   
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [Implementare l'oggetto ICommandSource](../../../../docs/framework/wpf/advanced/how-to-implement-icommandsource.md)   
 [How to: Add a Command to a MenuItem](http://msdn.microsoft.com/it-it/013d68a0-5373-4a68-bd91-5de574307370)   
 [Creare un esempio RoutedCommand personalizzato](http://go.microsoft.com/fwlink/?LinkID=159980)