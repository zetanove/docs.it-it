---
title: "Architettura di input per l&#39;interoperabilit&#224; tra Windows Form e WPF | Microsoft Docs"
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
  - "ElementHost (tastiera e messaggi)"
  - "architettura di input [interoperabilità WPF]"
  - "interoperabilità [WPF], Windows Form"
  - "interoperabilità da tastiera [WPF]"
  - "messaggi [WPF]"
  - "finestre di dialogo non modali [WPF]"
  - "form non modali"
  - "Windows Form [WPF], interoperabilità con"
  - "Windows Form, interoperabilità WPF"
  - "WindowsFormsHost (tastiera e messaggi)"
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Architettura di input per l&#39;interoperabilit&#224; tra Windows Form e WPF
L'interoperabilità tra [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] richiede che entrambe le tecnologie dispongano dell'elaborazione dell'input della tastiera appropriata.  In questo argomento viene illustrato come queste tecnologie implementano l'elaborazione dell'input della tastiera e dei messaggi per consentire l'interoperabilità nelle applicazioni ibride.  
  
 In questo argomento sono contenute le seguenti sottosezioni:  
  
-   Finestre di dialogo e form non modali  
  
-   Tastiera WindowsFormsHost ed elaborazione dei messaggi  
  
-   Tastiera ElementHost ed elaborazione dei messaggi  
  
## Finestre di dialogo e form non modali  
 Chiamare il metodo <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> sull'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> per aprire una finestra di dialogo o un form non modale da un'applicazione basata su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Chiamare il metodo <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> sul controllo <xref:System.Windows.Forms.Integration.ElementHost> per aprire una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non modale in un'applicazione basata su [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
## Tastiera WindowsFormsHost ed elaborazione dei messaggi  
 Se ospitata in un'applicazione basata su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], l'elaborazione dei messaggi e dell'input della tastiera [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] è data dalle operazioni elencate di seguito:  
  
-   La classe <xref:System.Windows.Forms.Integration.WindowsFormsHost> acquisisce i messaggi dal ciclo di messaggi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], implementato dalla classe <xref:System.Windows.Interop.ComponentDispatcher>.  
  
-   La classe <xref:System.Windows.Forms.Integration.WindowsFormsHost> crea un ciclo di messaggi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] surrogato per garantire l'esecuzione dell'elaborazione dell'input della tastiera [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ordinaria.  
  
-   La classe <xref:System.Windows.Forms.Integration.WindowsFormsHost> implementa l'interfaccia <xref:System.Windows.Interop.IKeyboardInputSink> per coordinare la gestione dello stato attivo con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   I controlli <xref:System.Windows.Forms.Integration.WindowsFormsHost> eseguono la registrazione e avviano i relativi cicli di messaggi.  
  
 Nelle sezioni riportate di seguito vengono illustrate in dettaglio queste parti del processo.  
  
### Acquisizione di messaggi dal ciclo di messaggi WPF  
 La classe <xref:System.Windows.Interop.ComponentDispatcher> implementa la gestione del ciclo di messaggi per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  La classe <xref:System.Windows.Interop.ComponentDispatcher> fornisce hook per consentire ai client esterni di filtrare i messaggi prima che vengano elaborati da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 L'implementazione dell'interoperabilità gestisce l'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> che consente ai controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] di elaborare i messaggi prima dei controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Ciclo di messaggi Windows Form surrogato  
 Per impostazione predefinita, la classe <xref:System.Windows.Forms.Application?displayProperty=fullName> contiene il ciclo di messaggi primario per le applicazioni [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Durante l'interoperabilità, il ciclo di messaggi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non elabora i messaggi.  Questa logica deve pertanto essere riprodotta.  Tramite il gestore dell'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> vengono eseguiti i passaggi riportati di seguito:  
  
1.  Filtro del messaggio tramite l'interfaccia <xref:System.Windows.Forms.IMessageFilter>.  
  
2.  Chiamata al metodo <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=fullName>.  
  
3.  Conversione e invio del messaggio, se necessario.  
  
4.  Passaggio del messaggio al controllo di hosting, se nessuno altro controllo elabora il messaggio.  
  
### Implementazione IKeyboardInputSink  
 Il ciclo di messaggi surrogato gestisce la gestione della tastiera.  Il metodo <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=fullName> è pertanto l'unico membro <xref:System.Windows.Interop.IKeyboardInputSink> che richiede un'implementazione nella classe <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  
  
 Per impostazione predefinita, la classe <xref:System.Windows.Interop.HwndHost> restituisce `false` per l'implementazione di <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> relativa.  In questo modo, si evita di dover passare da un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
 L'implementazione <xref:System.Windows.Forms.Integration.WindowsFormsHost> del metodo <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=fullName> prevede l'esecuzione dei passaggi riportati di seguito:  
  
1.  Ricerca del primo o dell'ultimo controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] contenuto nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> e che può ricevere lo stato attivo.  La scelta del controllo dipende dalle informazioni dell'attraversamento.  
  
2.  Impostazione dello stato attivo del controllo e restituzione di `true`.  
  
3.  Se nessun controllo può ricevere lo stato attivo, viene restituito `false`.  
  
### Registrazione di WindowsFormsHost  
 Quando viene creato l'handle della finestra a un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>, il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> chiama un metodo statico interno che registra la propria presenza per il ciclo di messaggi.  
  
 Durante la registrazione, il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> esamina il ciclo di messaggi.  Se il ciclo di messaggi non è stato avviato, viene creato il gestore dell'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName>.  Il ciclo di messaggi viene considerato in esecuzione se il gestore dell'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> è collegato.  
  
 Quando l'handle della finestra viene eliminato, il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> viene rimosso dalla registrazione.  
  
## Tastiera ElementHost ed elaborazione dei messaggi  
 Se ospitata in un'applicazione [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], l'elaborazione dei messaggi e dell'input della tastiera [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è data dalle operazioni indicate di seguito:  
  
-   Implementazioni delle interfacce <xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.IKeyboardInputSink> e <xref:System.Windows.Interop.IKeyboardInputSite>.  
  
-   Tabulazione e tasti di direzione.  
  
-   Tasti di comando e di finestre di dialogo.  
  
-   Elaborazione dei tasti di scelta rapida [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
 Nelle sezioni riportate di seguito vengono illustrate in dettaglio queste parti.  
  
### Implementazioni di interfacce  
 In [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] i messaggi della tastiera vengono indirizzati all'handle della finestra del controllo che presenta lo stato attivo.  Nel controllo <xref:System.Windows.Forms.Integration.ElementHost>, questi messaggi sono indirizzati all'elemento ospitato.  A tale scopo, il controllo <xref:System.Windows.Forms.Integration.ElementHost> fornisce un'istanza dell'oggetto <xref:System.Windows.Interop.HwndSource>.  Se il controllo <xref:System.Windows.Forms.Integration.ElementHost> presenta lo stato attivo, l'istanza dell'oggetto <xref:System.Windows.Interop.HwndSource> indirizza la maggior parte dell'input della tastiera affinché possa essere elaborato dalla classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Input.InputManager>.  
  
 La classe <xref:System.Windows.Interop.HwndSource> implementa le interfacce <xref:System.Windows.Interop.IKeyboardInputSink> e <xref:System.Windows.Interop.IKeyboardInputSite>.  
  
 L'interoperabilità della tastiera è basata sull'implementazione del metodo <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> per gestire l'input del tasto TAB e dei tasti di direzione che rimuovono lo stato attivo dagli elementi ospitati.  
  
### Tabulazione e tasti di direzione  
 La logica di selezione di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene mappata ai metodi <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> e <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> per implementare la navigazione tramite tasto TAB e tasti di direzione.  L'override del metodo <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> consente l'esecuzione di questo mapping.  
  
### Tasti di comando e di finestre di dialogo  
 Per dare a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la prima opportunità di elaborare tasti di comando e di finestre di dialogo, la pre\-elaborazione dei comandi [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] viene connessa al metodo <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A>.  L'override del metodo <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=fullName> consente la connessione delle due tecnologie.  
  
 Con il metodo <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A>, gli elementi ospitati possono gestire qualsiasi messaggio di tasti, ad esempio WM\_KEYDOWN, WM\_KEYUP, WM\_SYSKEYDOWN o WM\_SYSKEYUP, inclusi tasti di comando quali TAB, Invio, ESC e tasti di direzione.  Se il messaggio di un tasto non viene gestito, viene spostato a un livello superiore della gerarchia dei predecessori di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] per la gestione.  
  
### Elaborazione dei tasti di scelta rapida  
 Affinché venga eseguita in modo corretto, l'elaborazione dei tasti di scelta rapida di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] deve essere connessa alla classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager>.  Tutti i messaggi WM\_CHAR devono inoltre essere indirizzati correttamente agli elementi ospitati.  
  
 Perché l'implementazione di <xref:System.Windows.Interop.HwndSource> predefinita del metodo <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> restituisce `false`, i messaggi WM\_CHAR vengono elaborati utilizzando la logica riportata di seguito:  
  
-   L'override del metodo <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=fullName> viene eseguito per garantire che tutti i messaggi WM\_CHAR vengano inoltrati agli elementi ospitati.  
  
-   Se si preme ALT, il messaggio è WM\_SYSCHAR.  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non elabora questo messaggio tramite il metodo <xref:System.Windows.Forms.Control.IsInputChar%2A>.  Viene pertanto eseguito l'override del metodo <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> per consentire l'esecuzione di una query dell'oggetto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Input.AccessKeyManager> per un tasto di scelta rapida registrato.  Se viene trovato un tasto di scelta rapida registrato, viene elaborato dall'oggetto <xref:System.Windows.Input.AccessKeyManager>.  
  
-   Se il tasto ALT non viene premuto, la classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> elabora l'input non gestito.  Se l'input è dato da un tasto di scelta rapida, viene elaborato dall'oggetto <xref:System.Windows.Input.AccessKeyManager>.  L'evento <xref:System.Windows.Input.InputManager.PostProcessInput> viene gestito per i messaggi WM\_CHAR che non sono stati elaborati.  
  
 Quando viene premuto il tasto ALT, i segnali visivi del tasto di scelta rapida sono visibili nel form intero.  A supporto di questo comportamento, tutti i controlli <xref:System.Windows.Forms.Integration.ElementHost> nel form attivo ricevono messaggi WM\_SYSKEYDOWN, a prescindere dal controllo che presenta lo stato attivo.  
  
 I messaggi vengono inviati solo ai controlli <xref:System.Windows.Forms.Integration.ElementHost> nel form attivo.  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>   
 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>   
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)