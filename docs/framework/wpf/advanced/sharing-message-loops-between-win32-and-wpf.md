---
title: "Condivisione dei cicli di messaggi tra Win32 e WPF | Microsoft Docs"
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
  - "interoperabilità [WPF], Win32"
  - "cicli di messaggi [WPF]"
  - "condivisione di cicli di messaggi"
  - "codice Win32, condivisione di cicli di messaggi"
ms.assetid: 39ee888c-e5ec-41c8-b11f-7b851a554442
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Condivisione dei cicli di messaggi tra Win32 e WPF
In questo argomento viene illustrato come implementare un ciclo di messaggi per l'interoperabilità con [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], utilizzando l'esposizione del ciclo di messaggi esistente in <xref:System.Windows.Threading.Dispatcher> oppure creando un ciclo di messaggi separato sul lato [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] del codice di interoperabilità.  
  
## ComponentDispatcher e ciclo di messaggi  
 Uno scenario comune di interoperabilità e di supporto degli eventi di tastiera consiste nell'implementazione di <xref:System.Windows.Interop.IKeyboardInputSink> o nella creazione di sottoclassi da classi che già implementano <xref:System.Windows.Interop.IKeyboardInputSink>, ad esempio <xref:System.Windows.Interop.HwndSource> o <xref:System.Windows.Interop.HwndHost>.  Tuttavia, il supporto del sink di tastiera non risponde a tutte le esigenze in termini di ciclo di messaggi che si potrebbero avere quando si inviano e ricevono messaggi attraverso i limiti di interoperabilità.  Per formalizzare un'architettura di cicli di messaggi dell'applicazione, in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] è disponibile la classe <xref:System.Windows.Interop.ComponentDispatcher> che definisce un semplice protocollo che il ciclo di messaggi deve seguire.  
  
 <xref:System.Windows.Interop.ComponentDispatcher> è una classe statica che espone molti membri.  L'ambito di ogni metodo è associato in modo implicito al thread chiamante.  È necessario che un ciclo di messaggi chiami alcune delle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] in momenti critici, come definito nella sezione successiva.  
  
 <xref:System.Windows.Interop.ComponentDispatcher> fornisce eventi per i quali altri componenti \(ad esempio il sink di tastiera\) rimangono in ascolto.  La classe <xref:System.Windows.Threading.Dispatcher> chiama tutti i metodi <xref:System.Windows.Interop.ComponentDispatcher> appropriati in una sequenza appropriata.  Se si implementa un ciclo di messaggi personalizzato, il codice è responsabile della chiamata ai metodi <xref:System.Windows.Interop.ComponentDispatcher> in modo analogo.  
  
 La chiamata ai metodi <xref:System.Windows.Interop.ComponentDispatcher> su un thread comporta la chiamata dei soli gestori eventi registrati su tale thread.  
  
## Scrittura di cicli di messaggi  
 Di seguito viene riportato un elenco di controllo di membri <xref:System.Windows.Interop.ComponentDispatcher> che è necessario utilizzare per scrivere un ciclo di messaggi:  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A>: il ciclo di messaggi deve chiamare questo metodo per indicare che il thread è modale.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A>: il ciclo di messaggi deve chiamare questo metodo per indicare che il thread è stato ripristinato allo stato non modale.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>: il ciclo di messaggi deve chiamare questo metodo per indicare che <xref:System.Windows.Interop.ComponentDispatcher> deve generare l'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>.  <xref:System.Windows.Interop.ComponentDispatcher> non genererà <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> se <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A> è `true`, ma i cicli di messaggi potrebbero chiamare <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A> anche se <xref:System.Windows.Interop.ComponentDispatcher> non è in grado di rispondere se si trova nello stato modale.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A>: il ciclo di messaggi deve chiamare questo metodo per indicare che è disponibile un nuovo messaggio.  Il valore restituito indica se il messaggio è stato gestito da un listener di un evento <xref:System.Windows.Interop.ComponentDispatcher>.  Se il metodo <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A> restituisce `true` \(gestito\), il dispatcher non deve eseguire altre operazioni con il messaggio.  Se il valore restituito è `false`, il dispatcher deve chiamare la funzione [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] `TranslateMessage`, quindi `DispatchMessage`.  
  
## Utilizzo di ComponentDispatcher e gestione del messaggio esistente  
 Di seguito viene riportato un elenco di controllo di membri <xref:System.Windows.Interop.ComponentDispatcher> che è necessario utilizzare con il ciclo di messaggi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] inerente:  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A>: indica se l'applicazione si trova nello stato modale, ad esempio se è stato inserito un ciclo di messaggi modale.  <xref:System.Windows.Interop.ComponentDispatcher> può tenere traccia di questo stato perché la classe gestisce un conteggio di chiamate <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A> e <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A> dal ciclo di messaggi.  
  
-   Gli eventi <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> e <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> seguono le regole standard per le chiamate a delegati.  I delegati vengono chiamati in un ordine non specificato e vengono chiamati tutti, anche se il primo contrassegna il messaggio come gestito.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>: indica un'ora appropriata per l'elaborazione in periodi di inattività \(nessun messaggio in sospeso per il thread\).  L'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> non viene generato se il thread si trova nello stato modale.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>: generato per tutti i messaggi elaborati dal message pump.  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>: generato per tutti i messaggi che non sono stati gestiti durante l'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>.  
  
 Un messaggio viene considerato gestito se dopo l'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> o <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>, il parametro `handled` passato per riferimento nei dati di evento è `true`.  I gestori eventi dovrebbero ignorare il messaggio se `handled` è `true`, perché ciò significa che il messaggio è stato gestito prima dall'altro handler.  È possibile che il messaggio venga modificato dai gestori eventi di entrambi gli eventi.  Il dispatcher deve inviare il messaggio modificato, non quello originale.  <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> viene recapitato a tutti i listener, ma in base all'architettura solo la finestra di livello principale contenente l'HWND a cui i messaggi sono destinati deve richiamare il codice in risposta al messaggio.  
  
## Gestione di eventi ComponentDispatcher da parte di HwndSource  
 Se l'oggetto <xref:System.Windows.Interop.HwndSource> è una finestra di livello principale \(nessun HWND padre\), la registrazione viene eseguita con <xref:System.Windows.Interop.ComponentDispatcher>.  Se viene generato l'evento <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> e il messaggio è destinato all'oggetto <xref:System.Windows.Interop.HwndSource> o alle finestre figlio, <xref:System.Windows.Interop.HwndSource> chiama la sequenza del sink di tastiera <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TranslateAccelerator%2A>, <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A>, <xref:System.Windows.Interop.IKeyboardInputSink.OnMnemonic%2A>.  
  
 Se <xref:System.Windows.Interop.HwndSource> non è una finestra di livello principale \(presenta un HWND padre\), non viene eseguita alcuna operazione di gestione.  Si prevede che la gestione venga eseguita unicamente dalla finestra di livello principale e si prevede che si tratti di una finestra di livello superiore con supporto del sink di tastiera in un qualsiasi scenario di interoperabilità.  
  
 Se il metodo <xref:System.Windows.Interop.HwndHost.WndProc%2A> su un oggetto <xref:System.Windows.Interop.HwndSource> viene chiamato senza che sia stato chiamato un metodo del sink di tastiera appropriato, l'applicazione riceverà gli eventi di tastiera di livello più elevato, ad esempio <xref:System.Windows.UIElement.KeyDown>.  Non verrà tuttavia chiamato alcun metodo del sink di tastiera, situazione che elude funzionalità auspicabili del modello di input della tastiera, ad esempio il supporto dei tasti di scelta.  Questo problema può verificarsi perché il ciclo di messaggi non ha notificato correttamente il thread pertinente su <xref:System.Windows.Interop.ComponentDispatcher> o perché l'HWND padre non ha richiamato le risposte del sink di tastiera corrette.  
  
 È possibile che un messaggio diretto al sink di tastiera non venga inviato all'HWND se sono stati aggiunti hook per tale messaggio tramite il metodo <xref:System.Windows.Interop.HwndSource.AddHook%2A>.  È possibile che il messaggio sia stato gestito al livello del message pump e non inviato alla funzione `DispatchMessage`.  
  
## Vedere anche  
 <xref:System.Windows.Interop.ComponentDispatcher>   
 <xref:System.Windows.Interop.IKeyboardInputSink>   
 [Interoperatività di WPF e Win32](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [Modello di threading](../../../../docs/framework/wpf/advanced/threading-model.md)   
 [Cenni preliminari sull’input](../../../../docs/framework/wpf/advanced/input-overview.md)