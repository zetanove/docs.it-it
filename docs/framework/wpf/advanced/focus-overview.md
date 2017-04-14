---
title: "Cenni preliminari sullo stato attivo | Microsoft Docs"
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
  - "applicazioni, stato attivo"
  - "stato attivo nelle applicazioni"
ms.assetid: 0230c4eb-0c8a-462b-ac4b-ae3e511659f4
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# Cenni preliminari sullo stato attivo
In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] lo stato attivo è basato su due concetti principali, lo stato attivo della tastiera e lo stato attivo logico.  Lo stato attivo della tastiera fa riferimento all'elemento che riceve l'input della tastiera, mentre lo stato attivo logico fa riferimento all'elemento di un ambito che ha ricevuto lo stato attivo.  In questi cenni preliminari verranno illustrati questi concetti.  Comprendere le differenze esistenti tra questi concetti è fondamentale per la creazione di applicazioni complesse costituite da più aree in cui è possibile ottenere lo stato attivo.  
  
 Le principali classi correlate alla gestione dello stato attivo sono <xref:System.Windows.Input.Keyboard>, <xref:System.Windows.Input.FocusManager> e le classi degli elementi di base, quali <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement>.  Per ulteriori informazioni sugli elementi di base, vedere [Cenni preliminari sugli elementi di base](../../../../docs/framework/wpf/advanced/base-elements-overview.md).  
  
 La classe <xref:System.Windows.Input.Keyboard> riguarda principalmente lo stato attivo della tastiera, mentre la classe <xref:System.Windows.Input.FocusManager> riguarda lo stato attivo logico, tuttavia tale distinzione non può essere considerata assoluta.  Un elemento con lo stato attivo della tastiera presenta anche lo stato attivo logico, mentre un elemento che ha ottenuto lo stato attivo logico non ha necessariamente lo stato attivo della tastiera.  Questo è evidente quando si utilizza la classe <xref:System.Windows.Input.Keyboard> per impostare l'elemento che ha lo stato attivo della tastiera, in quanto in tal modo viene anche impostato lo stato attivo logico.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="Keyboard_Focus"></a>   
## Stato attivo della tastiera  
 Lo stato attivo della tastiera fa riferimento all'elemento che riceve in un determinato momento l'input della tastiera.  Su un desktop un solo elemento può avere lo stato attivo della tastiera.  In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la proprietà <xref:System.Windows.IInputElement.IsKeyboardFocused%2A> dell'elemento che presenta lo stato attivo della tastiera è impostata su `true`.  La proprietà statica <xref:System.Windows.Input.Keyboard.FocusedElement%2A> nella classe <xref:System.Windows.Input.Keyboard> ottiene l'elemento che attualmente presenta lo stato attivo della tastiera.  
  
 Affinché un elemento ottenga lo stato attivo della tastiera, le proprietà <xref:System.Windows.UIElement.Focusable%2A> e <xref:System.Windows.UIElement.IsVisible%2A> sugli elementi di base devono essere impostate su `true`.  Per alcune classi, ad esempio la classe di base <xref:System.Windows.Controls.Panel>, l'impostazione predefinita di <xref:System.Windows.UIElement.Focusable%2A> è `false`. È pertanto necessario impostare <xref:System.Windows.UIElement.Focusable%2A> su `true` affinché un elemento di questo tipo possa ottenere lo stato attivo della tastiera.  
  
 Lo stato attivo della tastiera può essere ottenuto tramite interazione dell'utente con l'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], ad esempio utilizzando il tasto TAB per spostarsi su un elemento o facendo clic con il mouse su alcuni elementi.  Lo stato attivo della tastiera può anche essere ottenuto a livello di codice utilizzando il metodo <xref:System.Windows.Input.Keyboard.Focus%2A> sulla classe <xref:System.Windows.Input.Keyboard>.  Il metodo <xref:System.Windows.Input.Keyboard.Focus%2A> tenta di fornire lo stato attivo della tastiera all'elemento specificato.  L'elemento restituito è l'elemento che presenta lo stato attivo della tastiera; potrebbe non essere quello richiesto se l'oggetto stato attivo nuovo o quello precedente blocca la richiesta.  
  
 Nell'esempio riportato di seguito viene utilizzato il metodo <xref:System.Windows.Input.Keyboard.Focus%2A> per impostare lo stato attivo della tastiera su un oggetto <xref:System.Windows.Controls.Button>.  
  
 [!code-csharp[focussample#FocusSampleSetFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplesetfocus)]
 [!code-vb[focussample#FocusSampleSetFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplesetfocus)]  
  
 La proprietà <xref:System.Windows.UIElement.IsKeyboardFocused%2A> sulle classi degli elementi di base ottiene un valore che indica se l'elemento presenta lo stato attivo della tastiera.  La proprietà <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> sulle classi degli elementi di base ottiene un valore che indica se l'elemento o uno qualsiasi dei relativi elementi figlio visivi presenta lo stato attivo della tastiera.  
  
 Quando si imposta lo stato attivo iniziale all'avvio dell'applicazione, l'elemento che riceverà lo stato attivo deve essere incluso nella struttura ad albero visuale della finestra iniziale caricata dall'applicazione e per tale elemento le proprietà <xref:System.Windows.UIElement.Focusable%2A> e <xref:System.Windows.UIElement.IsVisible%2A> devono essere impostate su `true`.  È consigliabile impostare lo stato attivo iniziale nel gestore eventi <xref:System.Windows.FrameworkElement.Loaded>.  È inoltre possibile utilizzare un callback di <xref:System.Windows.Threading.Dispatcher> chiamando <xref:System.Windows.Threading.Dispatcher.Invoke%2A> o <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A>.  
  
<a name="Logical_Focus"></a>   
## Stato attivo logico  
 Lo stato attivo logico fa riferimento all'oggetto <xref:System.Windows.Input.FocusManager.FocusedElement%2A?displayProperty=fullName> in un ambito di stato attivo.  Per ambito di stato attivo si intende un elemento che tiene traccia di <xref:System.Windows.Input.FocusManager.FocusedElement%2A> all'interno del relativo ambito.  Quando lo stato attivo della tastiera lascia un ambito di stato attivo, l'elemento con lo stato attivo perde lo stato attivo della tastiera, ma mantiene quello logico.  Quando lo stato attivo della tastiera torna nell'ambito di stato attivo, l'elemento con lo stato attivo ottiene nuovamente lo stato attivo della tastiera.  In questo modo, lo stato attivo della tastiera può essere passato tra più ambiti, ma l'elemento con lo stato attivo nell'ambito di stato attivo ottiene nuovamente lo stato attivo della tastiera quando lo stato attivo torna nell'ambito di stato attivo.  
  
 In un'applicazione possono essere presenti più elementi con stato attivo logico, ma in un determinato ambito può esistere un solo elemento con lo stato attivo.  
  
 Un elemento con stato attivo della tastiera presenta lo stato attivo logico per l'ambito a cui appartiene.  
  
 Un elemento può essere modificato in ambito di stato attivo in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] impostando la proprietà associata <xref:System.Windows.Input.FocusManager> <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> su `true`.  Nel codice un elemento può essere convertito in un ambito di stato attivo chiamando <xref:System.Windows.Input.FocusManager.SetIsFocusScope%2A>.  
  
 Nell'esempio riportato di seguito <xref:System.Windows.Controls.StackPanel> viene convertito in un ambito di stato attivo impostando la proprietà associata <xref:System.Windows.Input.FocusManager.IsFocusScope%2A>.  
  
 [!code-xml[MarkupSnippets#MarkupIsFocusScopeXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupisfocusscopexaml)]  
  
 [!code-csharp[FocusSnippets#FocusSetIsFocusScope](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focussetisfocusscope)]
 [!code-vb[FocusSnippets#FocusSetIsFocusScope](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focussetisfocusscope)]  
  
 <xref:System.Windows.Input.FocusManager.GetFocusScope%2A> restituisce l'ambito di stato attivo per l'elemento specificato.  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] le classi che sono ambiti di stato attivo per impostazione predefinita sono <xref:System.Windows.Window>, <xref:System.Windows.Controls.MenuItem>, <xref:System.Windows.Controls.ToolBar> e <xref:System.Windows.Controls.ContextMenu>.  
  
 <xref:System.Windows.Input.FocusManager.GetFocusedElement%2A> ottiene l'elemento con lo stato attivo per l'ambito di stato attivo specificato.  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> imposta invece l'elemento con lo stato attivo nell'ambito di stato attivo specificato.  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> viene in genere utilizzato per impostare l'elemento con lo stato attivo iniziale.  
  
 Nell'esempio riportato di seguito viene illustrato come impostare e ottenere l'elemento con lo stato attivo in un ambito di stato attivo.  
  
 [!code-csharp[FocusSnippets#FocusGetSetFocusedElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focusgetsetfocusedelement)]
 [!code-vb[FocusSnippets#FocusGetSetFocusedElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focusgetsetfocusedelement)]  
  
<a name="Keyboard_Navigation"></a>   
## Navigazione tramite tastiera  
 La classe <xref:System.Windows.Input.KeyboardNavigation> è responsabile dell'implementazione della navigazione dello stato attivo della tastiera predefinita quando viene premuto uno dei tasti di navigazione,  che sono: TAB, MAIUSC\+TAB, CTRL\+TAB, CTRL\+MAIUSC\+TAB, tasti di direzione.  
  
 È possibile modificare il comportamento di navigazione di un contenitore di navigazione impostando le proprietà associate <xref:System.Windows.Input.KeyboardNavigation> <xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A>, <xref:System.Windows.Input.KeyboardNavigation.ControlTabNavigation%2A> e <xref:System.Windows.Input.KeyboardNavigation.DirectionalNavigation%2A>.  Queste proprietà sono di tipo <xref:System.Windows.Input.KeyboardNavigationMode> e i valori possibili sono <xref:System.Windows.Input.KeyboardNavigationMode>, <xref:System.Windows.Input.KeyboardNavigationMode>, <xref:System.Windows.Input.KeyboardNavigationMode>, <xref:System.Windows.Input.KeyboardNavigationMode>, <xref:System.Windows.Input.KeyboardNavigationMode> e <xref:System.Windows.Input.KeyboardNavigationMode>.  Il valore predefinito è <xref:System.Windows.Input.KeyboardNavigationMode>, che indica che l'elemento non è un contenitore di navigazione.  
  
 Nell'esempio riportato di seguito viene creato un controllo <xref:System.Windows.Controls.Menu> con diversi oggetti <xref:System.Windows.Controls.MenuItem>.  La proprietà associata <xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A> viene impostata su <xref:System.Windows.Input.KeyboardNavigationMode> su <xref:System.Windows.Controls.Menu>.  Quando lo stato attivo viene modificato tramite il tasto TAB all'interno di <xref:System.Windows.Controls.Menu>, lo stato attivo viene spostato da un elemento a un altro fino all'ultimo, quindi torna al primo elemento.  
  
 [!code-xml[MarkupSnippets#MarkupKeyboardNavigationTabNavigationXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupkeyboardnavigationtabnavigationxaml)]  
  
 [!code-csharp[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml.cs#markupkeyboardnavigationtabnavigationcode)]
 [!code-vb[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarkupSnippets/visualbasic/window1.xaml.vb#markupkeyboardnavigationtabnavigationcode)]  
  
<a name="Manipulating_Focus_Programmatically"></a>   
## Spostamento dello stato attivo a livello di codice  
 Le [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] che è possibile utilizzare per lo stato attivo sono <xref:System.Windows.UIElement.MoveFocus%2A> e <xref:System.Windows.UIElement.PredictFocus%2A>.  
  
 <xref:System.Windows.FrameworkElement.MoveFocus%2A> sposta lo stato attivo sull'elemento successivo dell'applicazione.  <xref:System.Windows.Input.TraversalRequest> consente di specificare la direzione.  L'oggetto <xref:System.Windows.Input.FocusNavigationDirection> passato a <xref:System.Windows.UIElement.MoveFocus%2A> specifica le direzioni nelle quali è possibile spostare lo stato attivo, ad esempio <xref:System.Windows.Input.FocusNavigationDirection>, <xref:System.Windows.Input.FocusNavigationDirection>, <xref:System.Windows.Input.FocusNavigationDirection> e <xref:System.Windows.Input.FocusNavigationDirection>.  
  
 Nell'esempio riportato di seguito viene utilizzato <xref:System.Windows.FrameworkElement.MoveFocus%2A> per cambiare l'elemento con lo stato attivo.  
  
 [!code-csharp[focussample#FocusSampleMoveFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplemovefocus)]
 [!code-vb[focussample#FocusSampleMoveFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplemovefocus)]  
  
 <xref:System.Windows.FrameworkElement.PredictFocus%2A> restituisce l'oggetto che riceverebbe lo stato attivo qualora questo venisse modificato.  Attualmente, solo <xref:System.Windows.Input.FocusNavigationDirection>, <xref:System.Windows.Input.FocusNavigationDirection>, <xref:System.Windows.Input.FocusNavigationDirection> e <xref:System.Windows.Input.FocusNavigationDirection> sono supportati da <xref:System.Windows.FrameworkElement.PredictFocus%2A>.  
  
<a name="Focus_Events"></a>   
## Eventi di stato attivo  
 Gli eventi correlati allo stato attivo della tastiera sono <xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus>, <xref:System.Windows.Input.Keyboard.GotKeyboardFocus> e <xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocus>, <xref:System.Windows.Input.Keyboard.LostKeyboardFocus>.  Gli eventi sono definiti come eventi associati sulla classe <xref:System.Windows.Input.Keyboard>, ma sono maggiormente accessibili come eventi indirizzati equivalenti sulle classi dell'elemento di base.  Per ulteriori informazioni sugli eventi, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 <xref:System.Windows.Input.Keyboard.GotKeyboardFocus> viene generato quando l'elemento ottiene lo stato attivo della tastiera, mentre  <xref:System.Windows.Input.Keyboard.LostKeyboardFocus> viene generato quando l'elemento perde lo stato attivo della tastiera.  Se l'evento <xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus> o <xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocusEvent> viene gestito e <xref:System.Windows.RoutedEventArgs.Handled%2A> è impostato su `true`, lo stato attivo non cambia.  
  
 Nell'esempio riportato di seguito vengono collegati i gestori eventi <xref:System.Windows.UIElement.GotKeyboardFocus> e <xref:System.Windows.UIElement.LostKeyboardFocus> a un controllo <xref:System.Windows.Controls.TextBox>.  
  
 [!code-xml[keyboardsample#KeyboardSampleXAMLHandlerHookup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml#keyboardsamplexamlhandlerhookup)]  
  
 Quando <xref:System.Windows.Controls.TextBox> ottiene lo stato attivo della tastiera, la proprietà <xref:System.Windows.Controls.Control.Background%2A> di <xref:System.Windows.Controls.TextBox> viene impostata su <xref:System.Windows.Media.Brushes.LightBlue%2A>.  
  
 [!code-csharp[keyboardsample#KeyboardSampleGotFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplegotfocus)]
 [!code-vb[keyboardsample#KeyboardSampleGotFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplegotfocus)]  
  
 Quando <xref:System.Windows.Controls.TextBox> perde lo stato attivo della tastiera, la proprietà <xref:System.Windows.Controls.Control.Background%2A> di <xref:System.Windows.Controls.TextBox> viene nuovamente impostata sul bianco.  
  
 [!code-csharp[keyboardsample#KeyboardSampleLostFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplelostfocus)]
 [!code-vb[keyboardsample#KeyboardSampleLostFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplelostfocus)]  
  
 Gli eventi correlati allo stato attivo logico sono <xref:System.Windows.UIElement.GotFocus> e <xref:System.Windows.UIElement.LostFocus>.  Questi eventi sono definiti su <xref:System.Windows.Input.FocusManager> come eventi associati, ma <xref:System.Windows.Input.FocusManager> non espone wrapper di eventi CLR.  <xref:System.Windows.UIElement> e <xref:System.Windows.ContentElement> espongono questi eventi in modo più appropriato.  
  
## Vedere anche  
 <xref:System.Windows.Input.FocusManager>   
 <xref:System.Windows.UIElement>   
 <xref:System.Windows.ContentElement>   
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [Cenni preliminari sugli elementi di base](../../../../docs/framework/wpf/advanced/base-elements-overview.md)