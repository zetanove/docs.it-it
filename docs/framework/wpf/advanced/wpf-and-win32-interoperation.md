---
title: "Interoperativit&#224; di WPF e Win32 | Microsoft Docs"
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
  - "hosting di contenuto WPF nella finestra Win32"
  - "HWND (interoperabilità) [WPF]"
  - "interoperabilità [WPF], Win32"
  - "codice Win32, interoperabilità WPF"
ms.assetid: 0ffbde0d-701d-45a3-a6fa-dd71f4d9772e
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# Interoperativit&#224; di WPF e Win32
In questo argomento vengono forniti cenni preliminari sull'interoperatività tra codice [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] fornisce un ambiente dettagliato per la creazione di applicazioni.  Tuttavia, in caso di un investimento ingente in codice [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)], può essere più efficiente riutilizzare parte di tale codice.  
  
   
  
<a name="basics"></a>   
## Nozioni fondamentali sull'interoperatività di WPF e Win32  
 Sono disponibili due tecniche di base per l'interoperatività tra codice [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
-   Ospitare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  Con questa tecnica, è possibile utilizzare le funzionalità grafiche avanzate di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] all'interno del framework di una finestra e di un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] standard.  
  
-   Ospitare una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] nel contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Con questa tecnica, è possibile utilizzare un controllo [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] personalizzato esistente nel contesto di altro contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e passare i dati oltre i limiti.  
  
 In questo argomento vengono presentate le due tecniche.  Per informazioni maggiormente orientate al codice sull'hosting di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], vedere [Procedura dettagliata: hosting di contenuto WPF in Win32](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md).  Per informazioni maggiormente orientate al codice sull'hosting di [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], vedere [Procedura dettagliata: hosting di un controllo Win32 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md).  
  
<a name="projects"></a>   
## Progetti di interoperatività WPF  
 Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono costituite da codice gestito, ma la maggior parte dei programmi [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] esistenti è scritta in codice [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] non gestito.  Non è possibile chiamare [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] da un programma non gestito vero e proprio.  Tuttavia, utilizzando l'opzione `/clr` con il compilatore [!INCLUDE[TLA#tla_visualcpp](../../../../includes/tlasharptla-visualcpp-md.md)], è possibile creare un programma misto gestito e non gestito in cui combinare chiamate ad [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] gestite e non gestite senza problemi.  
  
 Una complicazione a livello di progetto è costituita dal fatto che non è possibile compilare file [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] in un progetto [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)].  Per compensare tale problema, sono disponibili diverse tecniche di divisione del progetto.  
  
-   Creare una DLL [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] contenente tutte le pagine [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] come assembly compilato, quindi fare sì che il file eseguibile [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] includa tale [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] come riferimento.  
  
-   Creare un eseguibile [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] per il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e impostarlo affinché faccia riferimento a una [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] contenente il contenuto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
-   Utilizzare <xref:System.Windows.Markup.XamlReader.Load%2A> per caricare [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in fase di esecuzione, anziché compilare [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] personalizzato.  
  
-   Non utilizzare affatto [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e scrivere tutti gli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nel codice, costruendo la struttura ad albero dell'elemento da <xref:System.Windows.Application>.  
  
 Utilizzare l'approccio più funzionale per lo scenario in questione.  
  
> [!NOTE]
>  Se si utilizza [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] prima, è possibile che si notino alcune nuove parole chiave come `gcnew` e `nullptr` negli esempi di codice di interoperabilità. Queste parole chiave sostituiscono la sintassi con doppio carattere di sottolineatura \(`__gc`\) e forniscono una sintassi più naturale per il codice gestito in [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)].  Per ulteriori informazioni sulle funzionalità gestite di [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)], vedere [Estensioni componenti per le piattaforme runtime](../Topic/Component%20Extensions%20for%20Runtime%20Platforms.md) e [Hello, C\+\+\/CLI](http://go.microsoft.com/fwlink/?LinkId=98739) \(la pagina potrebbe essere in inglese\).  
  
<a name="hwnds"></a>   
## Utilizzo di Hwnds in WPF  
 Per la maggior parte delle operazioni di interoperatività HWND di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario comprendere la modalità di utilizzo di HWND in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Per qualsiasi HWND, non è possibile combinare rendering [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] con rendering [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] o [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] \/ [!INCLUDE[TLA2#tla_gdiplus](../../../../includes/tla2sharptla-gdiplus-md.md)],  condizione che ha varie implicazioni.  Principalmente, per combinare questi modelli di rendering, è necessario creare una soluzione di interoperatività e utilizzare segmenti designati di interoperatività per ogni modello di rendering che si decide di utilizzare.  Inoltre, il comportamento di rendering crea una restrizione di "spazio aereo" per i risultati della soluzione di interoperatività.  Il concetto di "spazio aereo" è illustrato più dettagliatamente nell'argomento [Cenni preliminari sulle aree di tecnologia](../../../../docs/framework/wpf/advanced/technology-regions-overview.md).  
  
 Tutti gli elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nella schermata sono supportati da HWND.  Quando si crea un oggetto <xref:System.Windows.Window> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene creato HWND di primo livello e viene utilizzato un oggetto <xref:System.Windows.Interop.HwndSource> per inserire <xref:System.Windows.Window> e il relativo contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in HWND.  Il resto del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nell'applicazione condivide tale HWND.  Un'eccezione è costituita da menu, caselle combinate a discesa e altri popup.  Poiché questi elementi creano una propria finestra di primo livello, è possibile che un menu [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] superi potenzialmente il bordo dell'elemento HWND finestra che lo contiene.  Quando si utilizza <xref:System.Windows.Interop.HwndHost> per inserire un elemento HWND in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] segnala a [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] come posizionare il nuovo elemento HWND figlio relativo all'elemento HWND <xref:System.Windows.Window> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Un concetto correlato a HWND è la trasparenza in ogni elemento HWND e tra ogni elemento HWND  Questo concetto viene illustrato nell'argomento [Cenni preliminari sulle aree di tecnologia](../../../../docs/framework/wpf/advanced/technology-regions-overview.md).  
  
<a name="hosting_a_wpf_page"></a>   
## Hosting di contenuto WPF in una finestra Microsoft Win32  
 La chiave dell'hosting di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] è la classe <xref:System.Windows.Interop.HwndSource>.  Questa classe esegue il wrapping del contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], consentendo di incorporare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nell'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] come finestra figlio.  Nell'approccio illustrato di seguito [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono combinati in un'unica applicazione.  
  
1.  Implementare il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(elemento radice di contenuto\) come classe gestita.  In genere, la classe eredita da una delle classi che può contenere più elementi figlio e\/o utilizzata come elemento radice, ad esempio <xref:System.Windows.Controls.DockPanel> o <xref:System.Windows.Controls.Page>.  Nei passaggi successivi, questa classe è indicata come classe contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e le istanze di tale classe come oggetti contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
2.  Implementare un'applicazione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] con [!INCLUDE[TLA2#tla_cppcli](../../../../includes/tla2sharptla-cppcli-md.md)].  Se si parte da un'applicazione [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] non gestita esistente, è in genere possibile consentire la chiamata a codice gestito modificando le impostazioni del progetto in modo da includere il flag del compilatore `/clr` \(l'ambito completo degli elementi necessari per supportare la compilazione `/clr` non viene illustrato in questo argomento\).  
  
3.  Impostare il modello di threading su apartment a thread singolo \(STA\).  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza questo modello di threading.  
  
4.  Gestire la notifica WM\_CREATE nella procedura della finestra.  
  
5.  All'interno del gestore \(o di una funzione chiamata dal gestore\), eseguire le operazioni seguenti:  
  
    1.  Creare un nuovo oggetto <xref:System.Windows.Interop.HwndSource> con l'elemento HWND finestra padre come parametro `parent`.  
  
    2.  Creare un'istanza della classe di contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
    3.  Assegnare alla proprietà <xref:System.Windows.Interop.HwndSource.RootVisual%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource> un riferimento all'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
    4.  La proprietà <xref:System.Windows.Interop.HwndSource.Handle%2A> dell'oggetto <xref:System.Windows.Interop.HwndSource> contiene l'handle di finestra \(HWND\).  Per ottenere HWND utilizzabile nella parte non gestita dell'applicazione, eseguire il cast di `Handle.ToPointer()` a HWND.  
  
6.  Implementare una classe gestita che contiene un campo statico contenente un riferimento all'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Questa classe consente di ottenere un riferimento all'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dal codice [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] ma, dato più importante, impedisce di sottoporre inavvertitamente <xref:System.Windows.Interop.HwndSource> a procedure di Garbage Collection.  
  
7.  Ricevere notifiche dall'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] associando un gestore a uno o più eventi dell'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
8.  Comunicare con l'oggetto contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizzando il riferimento archiviato nel campo statico per impostare proprietà, chiamare metodi, e così via.  
  
> [!NOTE]
>  È possibile eseguire parzialmente o completamente la definizione della classe contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] per punto in uno [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] utilizzando la classe parziale predefinita della classe contenuto, se si genera un assembly separato a cui si fa riferimento. Sebbene in genere includere un oggetto <xref:System.Windows.Application> come parte della compilazione [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in un assembly, non vengono generati utilizzano tale <xref:System.Windows.Application> come parte dell'interoperabilità, appena si utilizza una o più classi principali per i file [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] definiti dall'applicazione e si fa riferimento alle classi parziali.  Il resto della procedura è essenzialmente analogo a quanto illustrato in precedenza.  
>   
>  Ciascuno di questi passaggi viene illustrato tramite codice nell'argomento [Procedura dettagliata: hosting di contenuto WPF in Win32](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md).  
  
<a name="hosting_an_hwnd"></a>   
## Hosting di una finestra Microsoft Win32 in WPF  
 La chiave per l'hosting di una finestra [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] all'interno di altro contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è la classe <xref:System.Windows.Interop.HwndHost>.  Questa classe esegue il wrapping della finestra in un elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] che può essere aggiunto a una struttura ad albero di elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  <xref:System.Windows.Interop.HwndHost> supporta anche le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] che consentono di eseguire tali attività come messaggi del processo per la finestra di hosting.  La procedura di base è la seguente:  
  
1.  Creare una struttura ad albero dell'elemento per un'applicazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(tramite codice o markup\).  Trovare un punto adatto e consentito nella struttura ad albero dell'elemento in cui sia possibile aggiungere l'implementazione di <xref:System.Windows.Interop.HwndHost> come elemento figlio.  Nei restanti passaggi, viene fatto riferimento a questo elemento come elemento di riserva.  
  
2.  Creare un oggetto contenente il contenuto [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] derivando da <xref:System.Windows.Interop.HwndHost>.  
  
3.  Nella classe host, eseguire l'override del metodo <xref:System.Windows.Interop.HwndHost> <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>.  Restituire l'elemento HWND della finestra di hosting.  Può essere necessario eseguire il wrapping dei controlli effettivi come finestra figlio della finestra restituita. Questa operazione offre un modo semplice per fare sì che il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] riceva notifiche dai controlli.  Questa tecnica consente di correggere alcuni problemi [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] relativi alla gestione dei messaggi sul limite del controllo ospitato.  
  
4.  Eseguire l'override dei metodi  <xref:System.Windows.Interop.HwndHost> <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> e <xref:System.Windows.Interop.HwndHost.WndProc%2A>.  Lo scopo è quello di eseguire la pulitura e rimuovere riferimenti al contenuto ospitato, in particolare se sono stati creati riferimenti a oggetti non gestiti.  
  
5.  Nel file code\-behind, creare un'istanza della classe di hosting del controllo e renderla l'elemento figlio dell'elemento di riserva.  In genere si utilizza un gestore eventi quale <xref:System.Windows.FrameworkElement.Loaded> oppure il costruttore di classe parziale.  È tuttavia anche possibile aggiungere il contenuto di interoperatività tramite un comportamento in fase di esecuzione.  
  
6.  Elaborare i messaggi finestra selezionati, ad esempio le notifiche dei controlli.  Sono disponibili due approcci  che forniscono entrambi un identico accesso al flusso di messaggi, pertanto la scelta dipende essenzialmente dalle esigenze di programmazione.  
  
    -   Implementare l'elaborazione per tutti i messaggi \(non solo quelli di arresto\) nell'override del metodo <xref:System.Windows.Interop.HwndHost> <xref:System.Windows.Interop.HwndHost.WndProc%2A>.  
  
    -   Fare sì che l'elemento [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di hosting elabori i messaggi gestendo l'evento <xref:System.Windows.Interop.HwndHost.MessageHook>.  Questo evento viene generato per ogni messaggio inviato alla routine della finestra principale della finestra ospitata.  
  
    -   Non è possibile elaborare messaggi da finestre esterne al processo utilizzando <xref:System.Windows.Interop.HwndHost.WndProc%2A>.  
  
7.  Comunicare con la finestra ospitata utilizzando platform invoke per chiamare la funzione `SendMessage` non gestita.  
  
 Tramite questi passaggi viene creata un'applicazione che funziona con input del mouse.  È possibile aggiungere il supporto della tabulazione per la finestra ospitata implementando l'interfaccia <xref:System.Windows.Interop.IKeyboardInputSink>.  
  
 Ognuno di questi passaggi viene illustrato tramite codice nell'argomento [Procedura dettagliata: hosting di un controllo Win32 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md).  
  
### HWND in WPF  
 L'oggetto <xref:System.Windows.Interop.HwndHost> può essere considerato come un controllo speciale.  Tecnicamente, <xref:System.Windows.Interop.HwndHost> è una classe <xref:System.Windows.FrameworkElement> derivata, non una classe <xref:System.Windows.Controls.Control> derivata, ma può essere considerato un controllo ai fini dell'interoperatività. <xref:System.Windows.Interop.HwndHost> estrae la natura [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] sottostante del contenuto ospitato in modo tale che il resto di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consideri il contenuto ospitato come un altro oggetto simile a un controllo, che deve eseguire il rendering e l'elaborazione dell'input.  <xref:System.Windows.Interop.HwndHost> in genere ha un comportamento analogo a qualsiasi altro [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.FrameworkElement>, anche se vi sono alcune differenze importanti relative all'output \(disegno e grafica\) e all'input \(mouse e tastiera\) in base alle limitazioni del supporto degli elementi HWND sottostanti.  
  
#### Differenze rilevanti nel comportamento di output  
  
-   <xref:System.Windows.FrameworkElement> che costituisce la classe di base <xref:System.Windows.Interop.HwndHost> ha alcune proprietà che implicano modifiche nell'interfaccia utente.  Tra queste sono incluse proprietà quali <xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=fullName> che modifica il layout degli elementi all'interno dell'elemento come padre.  Tuttavia, la maggior parte di queste proprietà non sono mappate a possibili equivalenti [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], anche se tali equivalenti possono essere presenti.  Poiché un numero troppo elevato di queste proprietà e dei relativi significati è troppo specifico della tecnologia di rendering, il mapping non è una soluzione pratica.  Pertanto, l'impostazione di proprietà come <xref:System.Windows.FrameworkElement.FlowDirection%2A> su <xref:System.Windows.Interop.HwndHost> non ha effetto.  
  
-   Non è possibile ruotare, ridimensionare, inclinare, né applicare altri tipi di trasformazioni a <xref:System.Windows.Interop.HwndHost>.  
  
-   <xref:System.Windows.Interop.HwndHost> non supporta la proprietà <xref:System.Windows.UIElement.Opacity%2A> \(alpha blending\).  Se il contenuto all'interno dell'oggetto <xref:System.Windows.Interop.HwndHost> esegue operazioni <xref:System.Drawing> che includono informazioni alpha, ciò non costituisce una violazione, ma l'oggetto <xref:System.Windows.Interop.HwndHost> nel suo insieme supporta solo un valore di opacità pari a 1.0 \(100%\).  
  
-   <xref:System.Windows.Interop.HwndHost> verrà visualizzato sopra gli altri elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nella stessa finestra di livello principale.  Tuttavia, un menu generato da <xref:System.Windows.Controls.ToolTip> o <xref:System.Windows.Controls.ContextMenu> è una finestra di primo livello separata e pertanto avrà un comportamento corretto con <xref:System.Windows.Interop.HwndHost>.  
  
-   <xref:System.Windows.Interop.HwndHost> non rispetta l'area di visualizzazione dell'oggetto <xref:System.Windows.UIElement> padre.  Questa situazione costituisce un potenziale problema se si tenta di inserire una classe <xref:System.Windows.Interop.HwndHost> all'interno di un'area di scorrimento o <xref:System.Windows.Controls.Canvas>.  
  
#### Differenze rilevanti nel comportamento di input  
  
-   In genere, mentre l'ambito dei dispositivi di input è all'interno dell'area [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] ospitata da <xref:System.Windows.Interop.HwndHost>, gli eventi di input vanno direttamente in [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  
  
-   Mentre il mouse si trova su <xref:System.Windows.Interop.HwndHost>, l'applicazione non riceve gli eventi del mouse [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e il valore della proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sarà `false`.  
  
-   Mentre <xref:System.Windows.Interop.HwndHost> ha lo stato attivo, l'applicazione non riceve gli eventi di tastiera [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e il valore della proprietà <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sarà `false`.  
  
-   Quando lo stato attivo è all'interno di <xref:System.Windows.Interop.HwndHost> e passa a un altro controllo all'interno di <xref:System.Windows.Interop.HwndHost>, l'applicazione non riceve gli eventi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.UIElement.GotFocus> o <xref:System.Windows.UIElement.LostFocus>.  
  
-   Proprietà ed eventi di stilo correlati sono analoghi e non comunicano informazioni mentre lo stilo si trova su <xref:System.Windows.Interop.HwndHost>.  
  
<a name="tabbing_mnemonics_accelerators"></a>   
## Tabulazioni, tasti di scelta e tasti di scelta rapida  
 Le interfacce <xref:System.Windows.Interop.IKeyboardInputSink> e <xref:System.Windows.Interop.IKeyboardInputSite> consentono l'utilizzo della tastiera senza problemi in applicazioni miste [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]:  
  
-   Tabulazione tra componenti [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]  
  
-   I tasti di scelta e i tasti di scelta rapida funzionano sia quando lo stato attivo è all'interno di un componente Win32 sia quando è all'interno di un componente WPF.  
  
 Le classi <xref:System.Windows.Interop.HwndHost> e <xref:System.Windows.Interop.HwndSource> forniscono entrambe implementazioni di <xref:System.Windows.Interop.IKeyboardInputSink>, ma potrebbero non essere in grado di gestire tutti i messaggi di input necessari in scenari più avanzati.  Eseguire l'override dei metodi appropriati per ottenere il comportamento di tastiera desiderato.  
  
 Le interfacce offrono supporto solo per le operazioni eseguite nella transizione tra le aree [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)].  All'interno dell'area [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)], il comportamento di tabulazione è completamente controllato dalla logica implementata da [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] per la tabulazione, se presente.  
  
## Vedere anche  
 <xref:System.Windows.Interop.HwndHost>   
 <xref:System.Windows.Interop.HwndSource>   
 <xref:System.Windows.Interop>   
 [Procedura dettagliata: hosting di un controllo Win32 in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md)   
 [Procedura dettagliata: hosting di contenuto WPF in Win32](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md)