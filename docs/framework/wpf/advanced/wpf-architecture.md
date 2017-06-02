---
title: "Architettura WPF | Microsoft Docs"
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
  - "affinità di thread"
  - "architettura"
  - "proprietà associate"
  - "classi, System.Object"
  - "classi, System.Threading.DispatcherObject"
  - "classi, System.Windows.Controls.Control"
  - "classi, System.Windows.DependencyObject"
  - "classi, System.Windows.FrameworkElement"
  - "classi, System.Windows.Media.Visual"
  - "classi, System.Windows.UIElement"
  - "CommandBindings"
  - "componenti, unmanaged"
  - "Control (classe)"
  - "modelli di dati"
  - "DependencyObject (classe)"
  - "DispatcherObject (classe)"
  - "FrameworkElement (classe)"
  - "INotifyPropertyChange (interfaccia)"
  - "interfacce, INotifyPropertyChange"
  - "milcore"
  - "algoritmo del pittore"
  - "proprietà, associate"
  - "Storyboard"
  - "System.Object (classe)"
  - "System.Threading.DispatcherObject (classe)"
  - "System.Windows.Controls.Control (classe)"
  - "System.Windows.DependencyObject (classe)"
  - "System.Windows.FrameworkElement (classe)"
  - "System.Windows.Media.Visual (classe)"
  - "System.Windows.UIElement (classe)"
  - "thread, affinità"
  - "UIElement (classe)"
  - "componenti non gestiti"
  - "Visual (classe)"
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Architettura WPF
In questo argomento viene fornita una presentazione guidata della gerarchia di classi di [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)].  Viene trattata la maggior parte dei sottosistemi principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e ne vengono descritte le modalità di interazione.  Vengono inoltre forniti i dettagli relativi ad alcune scelte effettuate dagli architetti di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
   
  
<a name="System_Object"></a>   
## System.Object  
 Il principale modello di programmazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] viene esposto tramite codice gestito.  Nella fase iniziale della progettazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ci sono stati diversi dibattiti relativi al punto in cui tracciare una linea tra i componenti gestiti del sistema e quelli non gestiti.  [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] fornisce numerose funzionalità che consentono uno sviluppo più produttivo e potente \(incluso la gestione della memoria, la gestione degli errori, Common Type System e così via\) ma che presentano anche alcuni svantaggi.  
  
 Nella figura riportata di seguito vengono illustrati i componenti principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Le sezioni in rosso del diagramma \(PresentationFramework, PresentationCore e milcore\) sono le parti di codice principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Di queste, solo milcore è un componente non gestito.  Milcore è scritto in codice non gestito per consentire una stretta integrazione con [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)].  In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] tutto viene visualizzato tramite il motore [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)], consentendo un rendering efficiente dell'hardware e del software.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] ha richiesto anche un controllo dettagliato sulla memoria e sull'esecuzione.  Il motore di composizione di milcore è estremamente sensibile alle prestazioni e ha richiesto la rinuncia a molti vantaggi di [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] per migliorarne il livello.  
  
 ![Posizione di WPF in .NET Framework](../../../../docs/framework/wpf/advanced/media/wpf-architect1.png "wpf\_architect1")  
  
 La comunicazione tra le parti gestite e quelle non gestite di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] viene discussa più avanti in questo argomento.  Il resto del modello di programmazione gestito viene descritto di seguito.  
  
<a name="System_Threading_DispatcherObject"></a>   
## System.Threading.DispatcherObject  
 La maggior parte degli oggetti di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] deriva da <xref:System.Windows.Threading.DispatcherObject> che fornisce i costrutti di base per la gestione della concorrenza e del threading.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] si basa su un sistema di messaggistica implementato dal dispatcher.  Funziona in modo molto simile al noto message pump di [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]; infatti, il dispatcher [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] utilizza i messaggi User32 per l'esecuzione di chiamate cross\-thread.  
  
 Quando si discute di concorrenza in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], i due concetti fondamentali da comprendere sono il dispatcher e l'affinità di thread.  
  
 Durante la fase di progettazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], l'obiettivo era di passare a un singolo thread di esecuzione ma con un modello ottimizzato per l'affinità in assenza di altri thread.  L'affinità di thread si verifica quando un componente utilizza l'identità del thread in esecuzione per archiviare un tipo di stato.  Nella forma più comune, per archiviare lo stato viene utilizzata l'archiviazione locale di thread \(TLS\).  L'affinità di thread richiede che ciascun thread di esecuzione logico appartenga a un solo thread fisico del sistema operativo, che può richiedere un elevato consumo di memoria.  Alla fine, il modello di threading di WPF è stato tenuto in sincronia con il modello di threading User32 esistente dell'esecuzione a thread singolo con affinità di thread.  Il motivo principale di questa decisione è stato l'interoperabilità: sistemi quali [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)], Appunti e Internet Explorer richiedono tutti l'esecuzione di affinità di thread singolo \(STA\).  
  
 Disponendo di oggetti con threading STA, è necessaria una modalità di comunicazione tra thread e di conferma di utilizzo del thread corretto.  Qui si colloca il ruolo del dispatcher.  Il dispatcher è un sistema di base di invio di messaggi con più code in ordine di priorità.  Gli esempi di messaggi includono le notifiche di input non elaborato \(spostamenti del mouse\), le funzionalità del framework \(layout\) o i comandi utente \(esecuzione di metodi\).  Derivandolo da <xref:System.Windows.Threading.DispatcherObject>, è possibile creare un oggetto [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], con comportamento STA e dotato di un puntatore verso un dispatcher al momento della creazione.  
  
<a name="System_Windows_DependencyObject"></a>   
## System.Windows.DependencyObject  
 Una delle filosofie di base relative all'architettura utilizzata nella compilazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è stata quella di preferire le proprietà ai metodi o agli eventi.  Le proprietà sono dichiarative e consentono di specificare più facilmente lo scopo anziché l'azione.  In tal modo veniva anche supportato un sistema basato sui modelli o sui dati per la visualizzazione di contenuti interfaccia utente.  Lo scopo di tale approccio era di creare un maggior numero di proprietà con cui stabilire l'associazione per poter controllare meglio il comportamento di un'applicazione.  
  
 Perché una parte maggiore del sistema fosse basata sulle proprietà, era necessario disporre di un sistema di proprietà più ricco di quello fornito da [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Un semplice esempio è rappresentato dalle notifiche di modifica.  Per abilitare l'associazione bidirezionale è necessario che entrambi i lati supportino la notifica di modifica.  Per associare il comportamento a valori di proprietà, è necessario essere notificati quando tale valore viene modificato.  [!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] dispone di un'interfaccia opzionale, **INotifyPropertyChange**, che consente a un oggetto di pubblicare le notifiche di modifica.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce un sistema di proprietà più ricco, derivato dal tipo <xref:System.Windows.DependencyObject>.  Il sistema di proprietà è effettivamente un sistema di proprietà delle "dipendenze" nel senso che tiene traccia delle dipendenze tra espressioni di proprietà e riconvalida automaticamente i valori delle proprietà quando tali dipendenze vengono modificate.  Ad esempio, nel caso di una proprietà che eredita \(come <xref:System.Windows.Controls.Control.FontSize%2A>\), il sistema viene automaticamente aggiornato se la proprietà viene modificata sul padre di un elemento che eredita il valore.  
  
 Il concetto di espressione di proprietà è alla base del sistema di proprietà di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  In questa prima versione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], il sistema delle espressioni di proprietà è chiuso e tutte le espressioni vengono fornite come parte del framework.  Le espressioni rappresentano il motivo per cui il sistema di proprietà non dispone di associazione dati, stili o ereditarietà hardcoded forniti invece dai livelli successivi all'interno del framework.  
  
 Il sistema di proprietà, inoltre, presenta possibilità limitate di archiviazione per i valori di proprietà.  Poiché gli oggetti hanno decine, se non centinaia, di proprietà e la maggior parte dei valori si trova nel relativo stato predefinito \(ereditato, impostato per stile e così via\), non tutte le istanze di un oggetto devono avere il peso di ciascuna proprietà in esso definita.  
  
 La nuova funzionalità finale del sistema di proprietà è la nozione di [proprietà associate](GTMT).  Gli elementi [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] sono basati sul principio di composizione e riutilizzo del componente.  Spesso avviene che qualche elemento contenitore \(ad esempio, un elemento di layout <xref:System.Windows.Controls.Grid>\) abbia bisogno di dati aggiuntivi sugli elementi figlio per controllarne il comportamento \(ad esempio, le informazioni relative a righe e colonne\).  Anziché associare tutte queste proprietà a ciascun elemento, un oggetto può fornire le definizioni delle proprietà per qualsiasi altro oggetto,  come avviene per le funzionalità "expando" di JavaScript.  
  
<a name="System_Windows_Media_Visual"></a>   
## System.Windows.Media.Visual  
 Dopo avere definito un sistema, il passaggio successivo è di ottenere pixel disegnati sullo schermo.  La classe <xref:System.Windows.Media.Visual> fornisce una struttura ad albero di oggetti visivi per la compilazione. Ciascun oggetto contiene facoltativamente le istruzioni per il disegno e i metadati su come eseguire il rendering di tali istruzioni \(area di visualizzazione, trasformazione e così via\).  <xref:System.Windows.Media.Visual> è progettato per essere estremamente leggero e flessibile, in modo che la maggior parte delle funzionalità non abbia esposizione [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] pubblica e si basi in modo rilevante sulle funzioni di callback protette.  
  
 <xref:System.Windows.Media.Visual> è effettivamente il punto di ingresso del sistema di composizione [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  <xref:System.Windows.Media.Visual> rappresenta il punto di connessione tra questi due sottosistemi, le [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] gestite e milcore non gestito.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] visualizza i dati spostandosi all'interno di strutture di dati non gestiti gestite da milcore.  Queste strutture, denominate nodi di composizione, rappresentano una struttura di visualizzazione gerarchica ad albero con istruzioni di rendering in ciascun nodo.  La struttura ad albero, illustrata a destra nella figura riportata di seguito, è accessibile solo mediante un protocollo di messaggistica.  
  
 Durante la programmazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], vengono creati elementi <xref:System.Windows.Media.Visual> e tipi derivati che comunicano internamente con la struttura ad albero della composizione mediante questo protocollo di messaggistica.  Ogni <xref:System.Windows.Media.Visual> in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] può creare uno, nessuno o numerosi nodi di composizione.  
  
 ![Struttura ad albero visuale di Windows Presentation Foundation](../../../../docs/framework/wpf/advanced/media/wpf-architecture2.png "wpf\_architecture2")  
  
 In questo caso va notato un dettaglio molto importante relativo all'architettura: l'intera struttura ad albero degli elementi visivi e delle istruzioni di disegno è memorizzata nella cache.  In termini di grafica, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] utilizza un sistema di rendering memorizzato.  Ciò fornisce al sistema elevate frequenze di aggiornamento senza che il sistema di composizione si blocchi sui callback al codice utente  e consente di impedire la visualizzazione di applicazioni che non rispondono.  
  
 Un altro dettaglio importante, non facilmente individuabile nel diagramma, è il modo in cui il sistema esegue effettivamente la composizione.  
  
 In User32 e [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)], il sistema funziona in base a un sistema di ritaglio in modalità immediata.  Quando è necessario eseguire il rendering di un componente, il sistema stabilisce un limite di ritaglio al di fuori del quale il componente non può toccare i pixel; poi viene chiesto al componente di disegnare i pixel in tale casella.  Questo sistema funziona molto bene nei sistemi con memoria limitata poiché quando vengono apportate modifiche basta intervenire solo sul componente interessato. Non sono mai richiesti due componenti per il colore di un singolo pixel.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] utilizza un modello di disegno denominato "algoritmo del pittore".  Ciò significa che anziché ritagliare ogni componente, viene richiesto il rendering di ciascun componente dallo sfondo al primo piano della visualizzazione.  In tal modo ciascun componente viene disegnato sulla visualizzazione del componente precedente.  Il vantaggio di questo modello è la possibilità di avere forme complesse, parzialmente trasparenti.  L'hardware grafico moderno rende questo modello relativamente veloce, a differenza di quando sono stati creati User32 e [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)].  
  
 Come accennato in precedenza, uno degli scopi principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è di passare a un modello di programmazione più dichiarativo, basato sulle proprietà.  Nel sistema visuale, ciò è evidente in un paio di punti interessanti.  
  
 Primo, se si pensa al sistema grafico in modalità memorizzata, c'è un deciso allontanamento da un modello imperativo di tipo DrawLine\/DrawLine verso un modello orientato ai dati di tipo new Line\(\)\/new Line\(\).  Questo spostamento verso il rendering basato sui dati consente operazioni complesse sulle istruzioni di disegno da esprimere utilizzando le proprietà.  I tipi derivanti da <xref:System.Windows.Media.Drawing> sono effettivamente il modello a oggetti per eseguire il rendering.  
  
 Secondo, se si esamina il sistema di animazione appare evidente che è quasi completamente dichiarativo.  Anziché richiedere a uno sviluppatore di calcolare la posizione o il colore successivo, è possibile esprimere le animazioni come una serie di proprietà su un oggetto di animazione.  Le animazioni possono quindi esprimere l'intenzione dello sviluppatore o del progettista \(spostare questo pulsante da questa a quella posizione in 5 secondi\) e il sistema può stabilire il modo più efficace per raggiungere tale scopo.  
  
<a name="System_Windows_UIElement"></a>   
## System.Windows.UIElement  
 <xref:System.Windows.UIElement> definisce i sottosistemi principali incluso Layout, Input ed Eventi.  
  
 Layout è un concetto fondamentale di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  In molti sistemi è presente un set fisso di modelli di layout \(HTML supporta tre modelli di layout: flusso, assoluto e tabelle\) oppure non è presente alcun modello di layout \(User32 supporta effettivamente solo il posizionamento assoluto\).  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è nato dal presupposto che gli sviluppatori e i progettisti avessero bisogno di un modello di layout flessibile ed estendibile da basare sui valori di proprietà piuttosto che sulla logica imperativa.  Il contratto di base per il layout viene introdotto al livello <xref:System.Windows.UIElement>: un modello a due fasi con i passaggi <xref:System.Windows.UIElement.Measure%2A> e <xref:System.Windows.UIElement.Arrange%2A>.  
  
 <xref:System.Windows.UIElement.Measure%2A> consente a un componente di stabilire le dimensioni richieste.  Si tratta di una fase diversa da <xref:System.Windows.UIElement.Arrange%2A> poiché esistono molte situazioni in cui un elemento padre chiede a un elemento figlio di eseguire la misurazione più volte per stabilire la posizione e le dimensioni ottimali.  Il fatto che gli elementi padre chiedano agli elementi figlio di eseguire le misurazioni consente di dimostrare un altro concetto chiave di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]: il ridimensionamento del contenuto.  Tutti i controlli di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] supportano la capacità di adattare il contenuto alle relative dimensioni standard.  Tutto ciò semplifica il processo di localizzazione e consente il layout dinamico degli elementi quando gli oggetti vengono ridimensionati.  La fase <xref:System.Windows.UIElement.Arrange%2A> consente a un elemento padre di posizionare e stabilire le dimensioni finali di ciascun figlio.  
  
 Si parla spesso del lato output di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]: <xref:System.Windows.Media.Visual> e relativi oggetti.  Tuttavia, esiste una straordinaria quantità di innovazione anche sul lato input.  Probabilmente, la modifica più importante al modello di input per [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è rappresentata dal modello coerente in base al quale gli eventi di input vengono indirizzati attraverso il sistema.  
  
 L'input come segnale proviene da un driver di dispositivo in modalità kernel e viene indirizzato verso il processo e il thread corretti mediante un complicato processo che interessa il kernel di Windows e User32.  Dopo essere stato indirizzato verso [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], il messaggio User32 corrispondente all'input viene convertito in un messaggio di input non elaborato [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e viene inviato al dispatcher.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente la conversione degli eventi di input non elaborati in più eventi effettivi, abilitando l'implementazione di funzioni quali "MouseEnter" a un livello basso del sistema con recapito garantito.  
  
 Ciascun evento di input viene convertito in almeno due eventi: un evento in "anteprima" e l'evento effettivo.  Tutti gli eventi di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] dispongono di una nozione di indirizzamento mediante la struttura ad albero dell'elemento.  Si parla di "eventi di bubbling" se passano da una destinazione nella parte superiore della struttura ad albero alla relativa radice e di "eventi di tunneling" se partono dalla radice per raggiungere la destinazione.  Gli eventi di input in anteprima effettuano il tunneling consentendo a qualsiasi elemento della struttura ad albero di filtrare o svolgere un'azione sull'evento.  Gli eventi regolari \(non in anteprima\) vengono propagati dalla destinazione fino alla radice.  
  
 Questa suddivisione tra fase di tunneling e fase di bubbling consente di implementare funzionalità, quali i tasti di scelta rapida, in modo coerente in un contesto composito.  In User32, i tasti di scelta rapida vengono implementati con una sola tabella globale che contiene tutti i tasti da supportare \(mapping di Ctrl\+N su "Nuovo"\).  Nel dispatcher dell'applicazione viene chiamato **TranslateAccelerator** che rileva la presenza dei messaggi di input in User32 e stabilisce se esiste una corrispondenza con un tasto di scelta rapida registrato.  Questa procedura non funziona in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] perché il sistema è totalmente "componibile": qualsiasi elemento può gestire e utilizzare qualsiasi tasto di scelta rapida.  Questo modello a due fasi per l'input consente ai componenti di implementare il proprio "TranslateAccelerator".  
  
 <xref:System.Windows.UIElement> introduce inoltre la nozione di CommandBindings.  Il sistema di comandi di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] consente agli sviluppatori di definire la funzionalità in termini di endpoint di un comando e cioè qualcosa che implementi <xref:System.Windows.Input.ICommand>.  Le associazioni di comandi consentono a un elemento di definire un mapping tra un movimento di input \(Ctrl\+N\) e un comando \(Nuovo\).  I movimenti di input e le definizioni dei comandi sono estendibili e possono essere collegati al momento dell'utilizzo.  In tal modo, ad esempio, è possibile consentire a un utente finale di personalizzare le combinazioni di tasti da utilizzare in un'applicazione.  
  
 Fino a questo punto sono state trattate le funzionalità principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e cioè quelle implementate nell'assembly PresentationCore.  In fase di compilazione di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], si desiderava ottenere una netta separazione tra le parti fondamentali \(ad esempio, il contratto per il layout con **Measure** e **Arrange**\) e le parti del framework \(ad esempio, l'implementazione di un layout specifico come <xref:System.Windows.Controls.Grid>\).  Lo scopo era quello di fornire un punto di estendibilità basso nello stack per consentire agli sviluppatori esterni di creare dei propri framework, se necessario.  
  
<a name="System_Windows_FrameworkElement"></a>   
## System.Windows.FrameworkElement  
 <xref:System.Windows.FrameworkElement> può essere esaminato in due modi diversi:  da un lato presenta una serie di criteri e personalizzazioni dei sottosistemi introdotti nei livelli inferiori di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] e dall'altro una serie di nuovi sottosistemi.  
  
 I criteri principali introdotti da <xref:System.Windows.FrameworkElement> sono quelli relativi al layout dell'applicazione.  <xref:System.Windows.FrameworkElement> si basa sul contratto di base del layout introdotto da <xref:System.Windows.UIElement> e aggiunge la nozione di "slot" di layout che consente agli autori di layout di ottenere più facilmente una semantica coerente basata sulle proprietà.  Le proprietà come <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>, <xref:System.Windows.FrameworkElement.MinWidth%2A> e <xref:System.Windows.FrameworkElement.Margin%2A> \(solo per citarne alcune\) assegnano a tutti i componenti derivati da <xref:System.Windows.FrameworkElement> un comportamento coerente all'interno dei contenitori di layout.  
  
 <xref:System.Windows.FrameworkElement> fornisce anche un'esposizione [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] semplificata a molte funzionalità che si trovano nei livelli principali di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Ad esempio, <xref:System.Windows.FrameworkElement> fornisce un accesso diretto all'animazione mediante il metodo <xref:System.Windows.FrameworkElement.BeginStoryboard%2A>.  <xref:System.Windows.Media.Animation.Storyboard> fornisce un modo per eseguire lo script di più animazioni rispetto a una serie di proprietà.  
  
 I due elementi più critici introdotti da <xref:System.Windows.FrameworkElement> sono l'associazione dati e gli stili.  
  
 Chiunque abbia utilizzato [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] o [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] per creare un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] per un'applicazione, dovrebbe avere una certa familiarità con il sottosistema di associazione dati in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  In ciascuno di questi sistemi, è possibile effettuare in modo semplice l'associazione di una o più proprietà di un dato elemento a un blocco di dati.  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] fornisce supporto completo per l'associazione di proprietà, la trasformazione e l'associazione di elenco.  
  
 Una delle funzionalità più interessanti dell'associazione dati in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è l'introduzione dei modelli di dati  che consentono di specificare in modo dichiarativo come deve essere visualizzato un blocco di dati.  Anziché creare un'interfaccia utente personalizzata che può essere associata ai dati, è possibile aggirare il problema e fare in modo che siano i dati a stabilire il tipo di visualizzazione da creare.  
  
 L'applicazione degli stili è effettivamente un tipo di associazione dati semplice  e il suo utilizzo consente di associare una serie di proprietà di una definizione condivisa a una o più istanze di un elemento.  Gli stili vengono applicati per riferimento esplicito \(impostando la proprietà <xref:System.Windows.FrameworkElement.Style%2A>\) oppure implicitamente associando uno stile al tipo [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] dell'elemento.  
  
<a name="System_Windows_Controls_Control"></a>   
## System.Windows.Controls.Control  
 La funzionalità più significativa dei controlli è l'applicazione di modelli.  Considerando il sistema di composizione di WPF come un sistema di rendering in modalità memorizzata, l'applicazione di modelli consente a un controllo di descriverne il rendering in modo dichiarativo e con parametri.  <xref:System.Windows.Controls.ControlTemplate> è semplicemente uno script che consente di creare una serie di elementi figlio con associazioni alle proprietà offerte dal controllo.  
  
 <xref:System.Windows.Controls.Control> fornisce una serie di proprietà predefinite, <xref:System.Windows.Controls.Control.Foreground%2A>, <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.Controls.Control.Padding%2A>, solo per citarne alcune, che possono essere utilizzate dagli autori di modelli per personalizzare la visualizzazione di un controllo.  L'implementazione di un controllo fornisce un modello dati e un modello di interazione.  Il modello di interazione definisce una serie di comandi \(ad esempio, Chiudi per una finestra\) e di associazioni a movimenti di input \(ad esempio, fare clic sulla X rossa nell'angolo superiore della finestra\).  Il modello dati fornisce una serie di proprietà per la personalizzazione del modello di interazione o della visualizzazione \(stabilita dal modello\).  
  
 Questa suddivisione tra modello dati \(proprietà\), modello di interazione \(comandi ed eventi\) e modello di visualizzazione \(modelli\) consente una personalizzazione completa dell'aspetto e del comportamento di un controllo.  
  
 Una caratteristica comune del modello dati dei controlli è il modello di contenuto.  Esaminando un controllo come <xref:System.Windows.Controls.Button>, si può notare che dispone di una proprietà denominata "Content" di tipo <xref:System.Object>.  In [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] e [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)], questa proprietà è in genere una stringa; tuttavia questo limita il tipo di contenuto che può essere inserito in un pulsante.  Il contenuto di un pulsante può essere una stringa semplice, un oggetto dati complesso o l'intera struttura ad albero di un elemento.  Nel caso di un oggetto dati, il modello dati viene utilizzato per costruire una visualizzazione.  
  
<a name="Summary"></a>   
## Riepilogo  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è progettato per consentire la creazione di sistemi di presentazione dinamici, basati sui dati.  Ogni parte del sistema è progettata per la creazione di oggetti utilizzando insiemi di proprietà che ne definiscono il comportamento.  L'associazione dati è una parte fondamentale del sistema ed è integrata a ogni livello.  
  
 Le applicazioni tradizionali creano una visualizzazione e poi associano i dati.  In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], tutti gli elementi del controllo e ogni aspetto della visualizzazione sono generati da un tipo di associazione dati.  Il testo che si trova nei pulsanti viene visualizzato creando un controllo composto all'interno del pulsante e associando la relativa visualizzazione alla proprietà del contenuto del pulsante.  
  
 Lo sviluppo di applicazioni basate su [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] dovrebbe risultare molto familiare per gli utenti.  È possibile impostare proprietà, utilizzare oggetti e associare dati in modo molto simile a quanto avviene in [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] o [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)].  Un'indagine più approfondita dell'architettura di [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] evidenzierà la possibilità di creare applicazioni molto più ricche in cui i dati vengono considerati gli elementi principali dell'applicazione.  
  
## Vedere anche  
 <xref:System.Windows.Media.Visual>   
 <xref:System.Windows.UIElement>   
 <xref:System.Windows.Input.ICommand>   
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.Threading.DispatcherObject>   
 <xref:System.Windows.Input.CommandBinding>   
 <xref:System.Windows.Controls.Control>   
 [Cenni preliminari sull'associazione dati](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [Layout](../../../../docs/framework/wpf/advanced/layout.md)   
 [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)