---
title: "Interoperativit&#224; di WPF e Windows Form | Microsoft Docs"
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
  - "controllo ibrido [interoperabilità WPF]"
  - "interoperabilità [WPF], Windows Form"
  - "interoperabilità nidificata [WPF]"
  - "Windows Form [WPF], interoperabilità con"
  - "Windows Form, interoperabilità WPF"
ms.assetid: 9e8aa6b6-112c-4579-98d1-c974917df499
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# Interoperativit&#224; di WPF e Windows Form
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] presentano due architetture diverse per la creazione delle interfacce delle applicazioni.  Lo spazio dei nomi <xref:System.Windows.Forms.Integration?displayProperty=fullName> fornisce classi che consentono scenari di interazione comuni.  Le due classi principali che implementano le capacità di interoperatività sono <xref:System.Windows.Forms.Integration.WindowsFormsHost> e <xref:System.Windows.Forms.Integration.ElementHost>.  In questo argomento vengono descritti gli scenari di interazione supportati e non.  
  
> [!NOTE]
>  Una considerazione particolare viene data allo scenario di *controllo ibrido*.  Un controllo ibrido dispone di un controllo di una tecnologia annidato in un controllo di un'altra tecnologia.  Ciò è anche definito *interazione annidata*.  Un *controllo ibrido multilivello* dispone di più di un livello di annidamento dei controlli ibridi.  Un esempio di interazione annidata a più livelli è un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che contiene un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], che contiene un altro controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  I controlli ibridi multilivello non sono supportati:  
  
   
  
<a name="Windows_Presentation_Foundation_Application_Hosting"></a>   
## Hosting di controlli Windows Form in WPF  
 Sono supportati i seguenti scenari di interoperatività quando un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospita un controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]:  
  
-   Il controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] potrebbe ospitare uno o più controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] mediante XAML.  
  
-   Potrebbe ospitare uno o più controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] utilizzando il codice.  
  
-   Potrebbe ospitare i controlli contenitore [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che contengono altri controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
-   Potrebbe ospitare un form Master\-Details con un master [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e dettagli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
-   Potrebbe ospitare un form Master\-Details con un master [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e dettagli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Potrebbe ospitare uno o più controlli [!INCLUDE[TLA2#tla_actx](../../../../includes/tla2sharptla-actx-md.md)].  
  
-   Potrebbe ospitare uno o più controlli composti.  
  
-   Potrebbe ospitare controlli ibridi mediante [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)].  
  
-   Potrebbe ospitare controlli ibridi mediante il codice.  
  
### Supporto layout  
 Nell'elenco riportato di seguito vengono descritte le limitazioni note quando l'elemento <xref:System.Windows.Forms.Integration.WindowsFormsHost> tenta di integrare il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato nel sistema di layout [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   In alcuni casi non è possibile ridimensionare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] oppure è possibile ridimensionarli solo in base a dimensioni specifiche.  Ad esempio, un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> supporta una sola altezza definita dalla dimensione del carattere del controllo.  In un layout dinamico di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in cui si suppone che sia possibile estendere gli elementi in verticale, un controllo <xref:System.Windows.Forms.ComboBox> ospitato non verrà esteso nel modo previsto.  
  
-   Non è possibile ruotare o inclinare i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Ad esempio, quando si ruota l'interfaccia utente di 90 gradi, i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitati manterranno la posizione verticale.  
  
-   Nella maggior parte dei casi i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non supportano il ridimensionamento proporzionale.  Anche se le dimensioni complessive del controllo vengono ridimensionate, i controlli figlio e gli elementi componente del controllo non possono essere ridimensionati nel modo previsto.  Questa limitazione dipende dalla modalità in cui ogni controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supporta il ridimensionamento.  
  
-   In un'interfaccia utente di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è possibile modificare l'ordine Z degli elementi per controllare il comportamento di sovrapposizione.  Un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato viene tracciato in un elemento HWND separato, in modo che venga disegnato sempre sopra elementi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supportano il ridimensionamento automatico in base alla dimensione del carattere.  In un'interfaccia utente di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la modifica della dimensione del carattere non causa il ridimensionamento dell'intero layout, benché sia possibile che vengano ridimensionati singoli elementi.  
  
### Proprietà di ambiente  
 Alcune delle proprietà di ambiente dei controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] hanno equivalenti in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  Queste proprietà di ambiente vengono propagate ai controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitati ed esposte come proprietà pubbliche nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> converte ogni proprietà di ambiente [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nell'equivalente [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
 Per ulteriori informazioni, vedere [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md).  
  
### Comportamento  
 Nella tabella riportata di seguito vengono descritti i comportamenti di interazione.  
  
|Comportamento|Supportato|Non supportato|  
|-------------------|----------------|--------------------|  
|Trasparenza|Il rendering del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] supporta la trasparenza.  Lo sfondo del controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] padre può diventare lo sfondo dei controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitati.|Alcuni controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] non supportano la trasparenza.  Ad esempio, i controlli <xref:System.Windows.Forms.TextBox> e <xref:System.Windows.Forms.ComboBox> non saranno trasparenti quando ospitati da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|  
|Tabulazione|L'ordine di tabulazione per i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitati è uguale al caso in cui i controlli vengono ospitati in un'applicazione basata su [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].<br /><br /> La tabulazione da un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] con il tasto TAB e i tasti MAIUSC\+TAB funziona come di consueto.<br /><br /> I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che dispongono di un valore della proprietà <xref:System.Windows.Forms.Control.TabStop%2A> uguale a `false` non ricevono lo stato attivo quando l'utente utilizza il tasto TAB per passare da un controllo all'altro.<br /><br /> -   Ogni controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> dispone di un valore <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A>, che determina il momento in cui il controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> riceverà lo stato attivo.<br />-   I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] contenuti all'interno di un contenitore <xref:System.Windows.Forms.Integration.WindowsFormsHost> seguono l'ordine specificato dalla proprietà <xref:System.Windows.Forms.Control.TabIndex%2A>.  La tabulazione dall'ultimo indice di tabulazione assegna lo stato attivo al controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] successivo, se disponibile.  Se non esistono altri controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivabili, la tabulazione torna al primo controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nell'ordine di tabulazione.<br />-   I valori <xref:System.Windows.Forms.Integration.WindowsFormsHost.TabIndex%2A> per i controlli interni a <xref:System.Windows.Forms.Integration.WindowsFormsHost> sono relativi ai controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] di pari livello contenuti nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.<br />-   La tabulazione rispetta il comportamento specifico dei controlli.  Ad esempio, premendo il tasto TAB in un controllo <xref:System.Windows.Forms.TextBox> che dispone di un valore della proprietà <xref:System.Windows.Forms.TextBoxBase.AcceptsTab%2A> pari a `true` si inserisce una tabulazione nella casella di testo invece di spostare lo stato attivo.|Non applicabile.|  
|Navigazione mediante i tasti di direzione|-   La navigazione con i tasti di direzione nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> è uguale a quello di un controllo contenitore [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] comune, per cui i tasti Freccia SU e Freccia SINISTRA consentono di selezionare il controllo precedente, mentre i tasti Freccia GIÙ e Freccia DESTRA consentono di selezionare il controllo successivo.<br />-   I tasti Freccia SU e Freccia SINISTRA a partire dal primo controllo contenuto nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> consentono di eseguire la stessa azione dei tasti di scelta rapida MAIUSC\+TAB.  Se è disponibile un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivabile, lo stato attivo viene spostato all'esterno del controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Questo comportamento è diverso dal comportamento <xref:System.Windows.Forms.ContainerControl> standard in quando non si verifica alcun ritorno all'ultimo controllo.  Se non è disponibile nessun altro controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivabile, lo stato attivo torna all'ultimo controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nell'ordine di tabulazione.<br />-   I tasti Freccia GIÙ e Freccia DESTRA a partire dall'ultimo controllo contenuto nel controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> consentono di eseguire la stessa azione del tasto TAB.  Se è disponibile un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivabile, lo stato attivo viene spostato all'esterno del controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.  Questo comportamento è diverso dal comportamento <xref:System.Windows.Forms.ContainerControl> standard in quando non si verifica alcun ritorno al primo controllo.  Se non è disponibile nessun altro controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] attivabile, lo stato attivo torna al primo controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nell'ordine di tabulazione.|Non applicabile.|  
|Tasti di scelta rapida|I tasti di scelta rapida funzionano come di consueto, a eccezione di quanto indicato nella colonna "Non supportato".|I tasti di scelta rapida duplicati tra le tecnologie non funzionano come i tasti di scelta rapida duplicati comuni.  Quando un tasto di scelta rapida viene duplicato tra le tecnologie, con almeno un tasto in un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e l'altro in un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] riceve sempre il tasto di scelta rapida.  Lo stato attivo non passa tra i controlli quando viene premuto il tasto di scelta rapida duplicato.|  
|Tasti di scelta rapida|I tasti di scelta rapida funzionano come di consueto, a eccezione di quanto indicato nella colonna "Non supportato".|-   I tasti di scelta rapida di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] gestiti nella fase che precede l'elaborazione hanno sempre la precedenza sui tasti di scelta rapida di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Se ad esempio si dispone di un controllo <xref:System.Windows.Forms.ToolStrip> con i tasti di scelta rapida CTRL\+S definiti ed esiste un comando [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] associato a CTRL\+S, il gestore del controllo <xref:System.Windows.Forms.ToolStrip> viene sempre richiamato per primo, indipendentemente dallo stato attivo.<br />-   I tasti di scelta rapida di [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che sono gestiti dall'evento <xref:System.Windows.Forms.Control.KeyDown> vengono elaborati per ultimi in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  È possibile evitare questo comportamento eseguendo l'override del metodo <xref:System.Windows.Forms.Control.IsInputKey%2A> del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] oppure gestendo l'evento <xref:System.Windows.Forms.Control.PreviewKeyDown>.  Restituire `true` dal metodo <xref:System.Windows.Forms.Control.IsInputKey%2A> o impostare il valore della proprietà <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A?displayProperty=fullName> su `true` nel gestore eventi <xref:System.Windows.Forms.Control.PreviewKeyDown>.|  
|AcceptsReturn, AcceptsTab e altri comportamenti specifici dei controlli|Le proprietà che cambiano il comportamento predefinito della tastiera funzionano come di consueto, supponendo che il controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] esegua l'override del metodo <xref:System.Windows.Forms.Control.IsInputKey%2A> per restituire `true`.|I controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che modificano il comportamento predefinito della tastiera gestendo l'evento <xref:System.Windows.Forms.Control.KeyDown> vengono elaborati per ultimi nel controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] host.  Dato che questi controlli vengono elaborati per ultimi, possono dare un comportamento imprevisto.|  
|Eventi Enter e Leave|Quando lo stato attivo non passa al controllo <xref:System.Windows.Forms.Integration.ElementHost> contenitore, gli eventi Enter e Leave vengono generati come nel caso in cui lo stato attivo cambi in un singolo controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.|Gli eventi Enter e Leave non vengono generati quando si verificano le seguenti modifiche dello stato attivo:<br /><br /> -   Dall'interno all'esterno di un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.<br />-   Dall'esterno all'interno di un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.<br />-   All'esterno di un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.<br />-   Da un controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ospitato in un controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost> a un controllo <xref:System.Windows.Forms.Integration.ElementHost> ospitato all'interno dello stesso controllo <xref:System.Windows.Forms.Integration.WindowsFormsHost>.|  
|Multithreading|Sono supportati tutti i tipi di multithreading.|Entrambe le tecnologie [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] presuppongono un unico modello di concorrenza a thread singolo.  Durante il debug la chiamata agli oggetti framework da altri thread genera un'eccezione per imporre questo requisito.|  
|Sicurezza|Tutti gli scenari di interazione richiedono attendibilità totale.|A nessuno scenario di interazione è consentita un'attendibilità parziale.|  
|Accessibilità|Sono supportati tutti gli scenari di accessibilità.  I prodotti tecnologici di assistenza funzionano correttamente quando utilizzati per applicazioni ibride che contengono sia i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che i controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
|Appunti|Tutte le operazioni relative agli Appunti funzionano come di consueto.  Sono comprese le operazioni di ritaglio e di incollamento tra i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
|Funzionalità di trascinamento della selezione|Tutte le operazioni di trascinamento della selezione funzionano come di consueto.  Sono incluse operazioni tra i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
  
<a name="Windows_Forms_Application_Hosting_Windows"></a>   
## Hosting di controlli WPF in Windows Form  
 Sono supportati i seguenti scenari di interoperatività quando un controllo [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)] ospita un controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
-   Hosting di uno o più controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] mediante il codice.  
  
-   Associazione di una finestra delle proprietà a uno o più controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitati.  
  
-   Hosting di una o più pagine [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in un form.  
  
-   Avvio di una finestra [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Hosting di un form Master\-Details con un master [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e dettagli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
-   Hosting di un form Master\-Details con un master [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e dettagli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].  
  
-   Hosting di controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] personalizzati.  
  
-   Hosting di controlli ibridi.  
  
### Proprietà di ambiente  
 Alcune proprietà di ambiente dei controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] hanno equivalenti in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Queste proprietà di ambiente vengono propagate ai controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitati ed esposte come proprietà pubbliche nel controllo <xref:System.Windows.Forms.Integration.ElementHost>.  Il controllo <xref:System.Windows.Forms.Integration.ElementHost> converte ogni proprietà di ambiente [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] nell'equivalente [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Per ulteriori informazioni, vedere [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md).  
  
### Comportamento  
 Nella tabella riportata di seguito vengono descritti i comportamenti di interazione.  
  
|Comportamento|Supportato|Non supportato|  
|-------------------|----------------|--------------------|  
|Trasparenza|Il rendering del controllo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] supporta la trasparenza.  Lo sfondo del controllo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] padre può diventare lo sfondo dei controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ospitati.|Non applicabile.|  
|Multithreading|Sono supportati tutti i tipi di multithreading.|Entrambe le tecnologie [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] presuppongono un unico modello di concorrenza a thread singolo.  Durante il debug la chiamata agli oggetti framework da altri thread genera un'eccezione per imporre questo requisito.|  
|Sicurezza|Tutti gli scenari di interazione richiedono attendibilità totale.|A nessuno scenario di interazione è consentita un'attendibilità parziale.|  
|Accessibilità|Sono supportati tutti gli scenari di accessibilità.  I prodotti tecnologici di assistenza funzionano correttamente quando utilizzati per applicazioni ibride che contengono sia i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] che i controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
|Appunti|Tutte le operazioni relative agli Appunti funzionano come di consueto.  Sono comprese le operazioni di ritaglio e di incollamento tra i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
|Funzionalità di trascinamento della selezione|Tutte le operazioni di trascinamento della selezione funzionano come di consueto.  Sono incluse operazioni tra i controlli [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].|Non applicabile.|  
  
## Vedere anche  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [Procedura dettagliata: hosting di controlli Windows Form in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli Windows Form compositi in WPF](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Procedura dettagliata: hosting di controlli compositi di WPF in Windows Form](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [Mapping di proprietà di Windows Form e WPF](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)