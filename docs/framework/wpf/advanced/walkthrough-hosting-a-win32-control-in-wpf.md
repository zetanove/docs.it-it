---
title: "Procedura dettagliata: hosting di un controllo Win32 in WPF | Microsoft Docs"
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
  - "hosting di controlli Win32 in WPF"
  - "codice Win32, interoperabilità WPF"
ms.assetid: a676b1eb-fc55-4355-93ab-df840c41cea0
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Procedura dettagliata: hosting di un controllo Win32 in WPF
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un ambiente dettagliato per la creazione di applicazioni.  Tuttavia, quando si dispone di una grande quantità di codice [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)], può essere opportuno riutilizzare almeno parte di tale codice nell'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] anziché riscriverlo completamente.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] fornisce un meccanismo semplice per l'hosting di una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] in una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 In questo argomento viene illustrata un'applicazione, [Esempio di hosting di un controllo ListBox Win32 in WPF](http://go.microsoft.com/fwlink/?LinkID=159998), che ospita un controllo casella di riepilogo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Questa procedura generale può essere estesa all'hosting di qualsiasi finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
   
  
<a name="requirements"></a>   
## Requisiti  
 Per questo argomento si presuppone una conoscenza di base della programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Guida introduttiva](../../../../docs/framework/wpf/getting-started/index.md).  Per un'introduzione alla programmazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], fare riferimento a uno dei numerosi manuali sull'argomento, in particolare *Programming Windows* di Charles Petzold.  
  
 Poiché l'esempio che accompagna questo argomento è implementato in [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)], vengono utilizzati i [!INCLUDE[TLA#tla_pinvoke](../../../../includes/tlasharptla-pinvoke-md.md)] per accedere all'[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  La conoscenza di [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] è utile ma non essenziale.  
  
> [!NOTE]
>  In questo argomento sono inclusi diversi esempi di codice relativi all'esempio associato.  Tuttavia, per una questione di leggibilità, il codice di esempio completo non è compreso.  È possibile ottenere o visualizzare il codice completo da [Esempio di hosting di un controllo ListBox Win32 in WPF](http://go.microsoft.com/fwlink/?LinkID=159998) \(la pagina potrebbe essere in inglese\).  
  
<a name="basic_procedure"></a>   
## Procedura di base  
 In questa sezione viene illustrata la procedura di base per l'hosting di una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] in una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Nelle sezioni restanti vengono illustrati i dettagli dei vari passaggi.  
  
 La procedura di hosting di base è la seguente:  
  
1.  Implementare una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per ospitare la finestra.  A tal proposito è possibile creare un elemento <xref:System.Windows.Controls.Border> per riservare una sezione della pagina per la finestra di hosting.  
  
2.  Implementare una classe per ospitare il controllo che eredita da <xref:System.Windows.Interop.HwndHost>.  
  
3.  In questa classe, eseguire l'override di <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> del membro della classe <xref:System.Windows.Interop.HwndHost>.  
  
4.  Creare la finestra di hosting come figlio della finestra contenente la pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Benché la programmazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] convenzionale non ne richieda l'uso esplicito, la pagina di hosting è una finestra con un handle \(HWND\).  È possibile ricevere HWND della pagina tramite il parametro `hwndParent` del metodo <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>.  La finestra di hosting deve essere creata come figlio di HWND.  
  
5.  Una volta creata la finestra host, restituire HWND della finestra di hosting.  Per ospitare uno o più controlli [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], si crea in genere una finestra host come figlio di HWND e, successivamente, i controlli vengono impostati come figli di tale finestra host.  Il wrapping dei controlli in una finestra host è una procedura semplice che consente alla pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di ricevere notifiche dai controlli relative ad alcune problematiche [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] particolari circa le notifiche attraverso il limite di HWND.  
  
6.  Gestire i messaggi selezionati inviati alla finestra host, quali ad esempio le notifiche dai controlli figlio.  A questo scopo, è possibile eseguire due operazioni.  
  
    -   Per gestire i messaggi nella classe di hosting, eseguire l'override del metodo <xref:System.Windows.Interop.HwndHost.WndProc%2A> della classe <xref:System.Windows.Interop.HwndHost>.  
  
    -   Per fare in modo che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] gestisca i messaggi, gestire l'evento <xref:System.Windows.Interop.HwndHost.MessageHook> della classe <xref:System.Windows.Interop.HwndHost> nel code\-behind.  Questo evento si verifica per ogni messaggio ricevuto dalla finestra di hosting.  Scegliendo questa opzione, sarà comunque necessario eseguire l'override di <xref:System.Windows.Interop.HwndHost.WndProc%2A>, ma l'implementazione necessaria sarà minima.  
  
7.  Eseguire l'override dei metodi <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> e <xref:System.Windows.Interop.HwndHost.WndProc%2A> di <xref:System.Windows.Interop.HwndHost>.  È necessario eseguire l'override di questi metodi per soddisfare il contratto <xref:System.Windows.Interop.HwndHost>, ma l'implementazione necessaria potrebbe essere minima.  
  
8.  Nel file code\-behind, creare un'istanza della classe di hosting dei controlli e impostarla come figlio dell'elemento <xref:System.Windows.Controls.Border> nel quale dovrà essere ospitata la finestra.  
  
9. Comunicare con la finestra di hosting inviandole messaggi di [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] e messaggi di gestione dalle finestre figlio, quali ad esempio le notifiche inviate dai controlli.  
  
<a name="page_layout"></a>   
## Implementare il layout della pagina  
 Il layout della pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che ospita il controllo ListBox è composto da due aree.  Il lato sinistro della pagina ospita diversi controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che forniscono un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] tramite la quale è possibile modificare il controllo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Nell'angolo superiore destro della pagina è presente un'area quadrata per il controllo ListBox ospitato.  
  
 Il codice di implementazione di questo layout è piuttosto semplice.  L'elemento radice è un oggetto <xref:System.Windows.Controls.DockPanel> che possiede due elementi figlio.  Il primo è un elemento <xref:System.Windows.Controls.Border> che ospita il controllo ListBox.  Occupa un quadrato 200x200 nell'angolo superiore destro della pagina.  Il secondo è un elemento <xref:System.Windows.Controls.StackPanel> contenente un insieme di controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che consentono di visualizzare informazioni e modificare il controllo ListBox impostando proprietà di interoperatività esposte.  Per ciascuno degli elementi figlio di <xref:System.Windows.Controls.StackPanel>, vedere il materiale di riferimento dei vari elementi utilizzati per i dettagli sulla relativa definizione e l'utilizzo. Questi elementi vengono elencati nel codice di esempio che segue ma non illustrati nel dettaglio. Il modello di interoperatività di base non richiede alcuno di questi elementi, i quali vengono forniti al solo scopo di aggiungere interattività all'esempio.  
  
 [!code-xml[WPFHostingWin32Control#WPFUI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml#wpfui)]  
  
<a name="host_class"></a>   
## Implementare una classe per ospitare il controllo Microsoft Win32  
 L'elemento principale di questo esempio è la classe che ospita realmente il controllo, ControlHost.cs.  Questa classe eredita da <xref:System.Windows.Interop.HwndHost>.  Il costruttore accetta due parametri, altezza e larghezza, corrispondenti all'altezza e alla larghezza dell'elemento <xref:System.Windows.Controls.Border> che ospita il controllo ListBox.  Questi valori verranno utilizzati in un secondo momento per fare in modo che la dimensione del controllo corrisponda all'elemento <xref:System.Windows.Controls.Border>.  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostclass)]
 [!code-vb[WPFHostingWin32Control#ControlHostClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostclass)]  
  
 L'esempio include anche un insieme di costanti,  in gran parte tratte da Winuser.h, che consentono di utilizzare nomi convenzionali per la chiamata alle funzioni [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostConstants](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostconstants)]
 [!code-vb[WPFHostingWin32Control#ControlHostConstants](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostconstants)]  
  
<a name="buildwindowcore"></a>   
### Eseguire l'override di BuildWindowCore per creare la finestra Microsoft Win32  
 Eseguire l'override di questo metodo per creare la finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] che verrà ospitata dalla pagina, quindi creare la connessione tra la finestra e la pagina.  Poiché questo esempio implica l'hosting di un controllo ListBox, vengono create due finestre.  La prima è la finestra realmente ospitata dalla pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Il controllo ListBox viene creato come figlio di tale finestra.  
  
 Questo approccio viene utilizzato per semplificare il processo di ricezione delle notifiche dal controllo.  La classe <xref:System.Windows.Interop.HwndHost> consente di elaborare i messaggi inviati alla finestra di hosting.  Se si ospita direttamente un controllo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], si ricevono i messaggi inviati al ciclo di messaggi interno del controllo.  È possibile visualizzare e inviare messaggi al controllo, ma non si ricevono le notifiche che il controllo invia alla finestra padre.  Ciò significa, tra le altre cose, che non si ha modo di rilevare quando l'utente interagisce con il controllo.  Creare invece una finestra host e impostare il controllo come figlio di tale finestra.  In questo modo sarà possibile elaborare i messaggi per la finestra host, incluse le notifiche inviate dal controllo.  Per comodità, poiché la finestra host è poco più di un semplice wrapper per il controllo, il package verrà definito come controllo ListBox.  
  
<a name="create_the_window_and_listbox"></a>   
#### Creare la finestra host e il controllo ListBox  
 È possibile utilizzare [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] per creare una finestra host per il controllo mediante creazione e registrazione di una classe della finestra e così via.  Tuttavia, un approccio molto più semplice consiste nella creazione di una finestra con la classe "statica" predefinita.  Questo approccio fornisce la routine della finestra necessaria per ricevere le notifiche dal controllo e richiede codice minimo.  
  
 HWND del controllo viene esposto tramite una proprietà di sola lettura, in modo tale che la pagina host possa utilizzarlo per inviare messaggi al controllo.  
  
 [!code-csharp[WPFHostingWin32Control#IntPtrProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#intptrproperty)]
 [!code-vb[WPFHostingWin32Control#IntPtrProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#intptrproperty)]  
  
 Il controllo ListBox viene creato come figlio della finestra host.  L'altezza e la larghezza di entrambe le finestre vengono impostate sui valori passati al costruttore, illustrati in precedenza.  Così facendo le dimensioni della finestra host e del controllo saranno identiche all'area riservata nella pagina.  Una volta create le finestre, nell'esempio viene restituito un oggetto <xref:System.Runtime.InteropServices.HandleRef> contenente HWND della finestra host.  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCore](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcore)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCore](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcore)]  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCoreHelper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcorehelper)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCoreHelper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcorehelper)]  
  
<a name="destroywindow_wndproc"></a>   
### Implementare DestroyWindow e WndProc  
 Oltre a <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>, occorre anche eseguire l'override dei metodi <xref:System.Windows.Interop.HwndHost.WndProc%2A> e <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> di <xref:System.Windows.Interop.HwndHost>.  In questo esempio, i messaggi per il controllo vengono gestiti dal gestore <xref:System.Windows.Interop.HwndHost.MessageHook>, pertanto l'implementazione di <xref:System.Windows.Interop.HwndHost.WndProc%2A> e <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> è minima.  Nel caso di <xref:System.Windows.Interop.HwndHost.WndProc%2A>, impostare `handled` su `false` per indicare che il messaggio non è stato gestito e restituire 0.  Per <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A>, eliminare semplicemente la finestra.  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroy](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroy)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroy](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroy)]  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroyHelper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroyhelper)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroyHelper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroyhelper)]  
  
<a name="host_the_control"></a>   
## Ospitare il controllo nella pagina  
 Per ospitare il controllo nella pagina, creare innanzitutto una nuova istanza della classe `ControlHost`.  Passare l'altezza e la larghezza dell'elemento bordo contenente il controllo \(`ControlHostElement`\) al costruttore `ControlHost`.  Così facendo ListBox avrà le dimensioni corrette.  Ospitare quindi il controllo nella pagina assegnando l'oggetto `ControlHost` alla proprietà <xref:System.Windows.Controls.Decorator.Child%2A> di <xref:System.Windows.Controls.Border> host.  
  
 Nell'esempio viene associato un gestore all'evento <xref:System.Windows.Interop.HwndHost.MessageHook> di `ControlHost` per ricevere messaggi dal controllo.  Questo evento viene generato per ogni messaggio inviato alla finestra di hosting.  In questo caso si tratta dei messaggi inviati alla finestra che esegue il wrapping del controllo ListBox effettivo, incluse le notifiche dal controllo.  Nell'esempio viene chiamato SendMessage per ottenere informazioni dal controllo e modificarne il contenuto.  I dettagli sulla comunicazione tra la pagina e il controllo verranno illustrati nella sezione successiva.  
  
> [!NOTE]
>  Notare che sono presenti due dichiarazioni [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] per SendMessage.  Si tratta di una condizione necessaria in quanto una utilizza il parametro `wParam` per passare una stringa, mentre l'altra lo utilizza per passare un numero intero.  È necessaria una dichiarazione separata per ciascuna firma affinché i dati vengano correttamente sottoposti a marshalling.  
  
 [!code-csharp[WPFHostingWin32Control#HostWindowClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#hostwindowclass)]
 [!code-vb[WPFHostingWin32Control#HostWindowClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#hostwindowclass)]  
  
 [!code-csharp[WPFHostingWin32Control#ControlMsgFilterSendMessage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#controlmsgfiltersendmessage)]
 [!code-vb[WPFHostingWin32Control#ControlMsgFilterSendMessage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#controlmsgfiltersendmessage)]  
  
<a name="communication"></a>   
## Implementare la comunicazione tra il controllo e la pagina  
 Modificare il controllo inviandogli messaggi [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)].  Il controllo avvisa quando l'utente interagisce con esso inviando notifiche alla finestra host.  Nell'[esempio di hosting di un controllo ListBox Win32 in WPF](http://go.microsoft.com/fwlink/?LinkID=159998) è inclusa un'interfaccia utente che fornisce vari esempi di procedure:  
  
-   Aggiungere un elemento all'elenco.  
  
-   Eliminare l'elemento selezionato dall'elenco.  
  
-   Visualizzare il testo dell'elemento attualmente selezionato.  
  
-   Visualizzare il numero di elementi nell'elenco.  
  
 L'utente può anche selezionare un elemento nella casella di riepilogo facendo clic su di esso, esattamente come accade in un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] convenzionale.  I dati visualizzati vengono aggiornati ogni qualvolta l'utente modifica lo stato della casella di riepilogo selezionando o aggiungendo un elemento.  
  
 Per aggiungere elementi, inviare un messaggio LB\_ADDSTRING alla casella di riepilogo.  Per eliminare gli elementi, inviare LB\_GETCURSEL per ottenere l'indice della selezione corrente, quindi LB\_DELETESTRING per eliminare l'elemento.  Nell'esempio viene anche inviato LB\_GETCOUNT e viene utilizzato il valore restituito per aggiornare la visualizzazione del numero di elementi.  Queste istanze di SendMessage utilizzano entrambe una delle dichiarazioni [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] illustrate nella sezione precedente.  
  
 [!code-csharp[WPFHostingWin32Control#AppendDeleteText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#appenddeletetext)]
 [!code-vb[WPFHostingWin32Control#AppendDeleteText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#appenddeletetext)]  
  
 Quando l'utente seleziona un elemento o modifica la selezione, il controllo avvisa la finestra host inviandole un messaggio WM\_COMMAND, il quale genera l'evento <xref:System.Windows.Interop.HwndHost.MessageHook> per la pagina.  Il gestore riceve le stesse informazioni della routine principale della finestra host.  Passa inoltre un riferimento a un valore booleano, `handled`.  Impostare `handled` su `true` per indicare che il messaggio è stato gestito e non necessita di ulteriore elaborazione.  
  
 WM\_COMMAND viene inviato per diverse ragioni, pertanto è necessario esaminare l'identificatore della notifica per determinare se si tratti di un evento che si desidera gestire.  L'identificatore è contenuto nel word alto del parametro `wParam`.  Poiché [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] non possiede una macro HIWORD, nell'esempio vengono utilizzati operatori bit per bit per estrarre l'identificatore.  Se l'utente ha effettuato o modificato la selezione, l'identificatore sarà LBN\_SELCHANGE.  
  
 Quando LBN\_SELCHANGE viene ricevuto, nell'esempio si ottiene l'indice dell'elemento selezionato inviando un messaggio LB\_GETCURSEL al controllo.  Per ottenere il testo, creare innanzitutto un oggetto <xref:System.Text.StringBuilder>.  Inviare quindi un messaggio LB\_GETTEXT al controllo.  Passare l'oggetto <xref:System.Text.StringBuilder> vuoto come parametro `wParam`.  Quando SendMessage viene restituito, <xref:System.Text.StringBuilder> contiene il testo dell'elemento selezionato.  Questo utilizzo di SendMessage richiede un'altra dichiarazione [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)].  
  
 Impostare infine `handled` su `true` per indicare che il messaggio è stato gestito.  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndHost>   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)