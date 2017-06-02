---
title: "Linee guida per la progettazione di controlli a cui &#232; possibile applicare degli stili | Microsoft Docs"
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
  - "controlli, progettazione dello stile"
  - "progettazione dello stile per i controlli"
ms.assetid: c52dde45-a311-4531-af4c-853371c4d5f4
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Linee guida per la progettazione di controlli a cui &#232; possibile applicare degli stili
In questo documento viene riepilogata una serie di procedure ottimali da tenere in considerazione per la progettazione di un controllo a cui siano facilmente applicabili stili e modelli.  Tali procedure sono il risultato di numerosi tentativi ed errori durante l'elaborazione degli stili dei controlli dei temi per il set di controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] incorporato.  Una corretta applicazione degli stili non dipende solo da un modello a oggetti ben progettato ma anche dallo stile stesso.  Questo documento è destinato in primo luogo agli autori dei controlli, non agli autori degli stili.  
  
   
  
<a name="Terminology"></a>   
## Terminologia  
 Per "applicazione di stili e modelli" si intende l'insieme di tecnologie che consente a un autore di controlli di rinviare gli aspetti visivi del controllo allo stile e al modello del controllo.  In questo insieme di tecnologie sono inclusi:  
  
-   Stili \(compresi i metodi per l'impostazione delle proprietà, i trigger e gli storyboard\).  
  
-   Risorse.  
  
-   Modelli di controllo.  
  
-   Modelli di dati.  
  
 Per un'introduzione all'applicazione di stili e modelli, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
<a name="Before_You_Start__Understanding_Your_Control"></a>   
## Prima di iniziare: conoscenza del controllo  
 Prima di passare alla lettura di queste linee guida, è importante aver compreso e definito l'utilizzo comune del controllo.  L'applicazione degli stili offre spesso una serie di possibilità che non rispondono a regole costanti.  Il problema dei controlli creati per un ampio utilizzo \(in un gran numero di applicazioni, da parte di molti sviluppatori\) è relativo al fatto che l'applicazione degli stili può essere utilizzata per apportare modifiche di vasta portata all'aspetto visivo del controllo,  per cui, il controllo a cui è stato applicato uno stile potrebbe non corrispondere al progetto dell'autore.  Poiché la flessibilità offerta dall'applicazione degli stili è essenzialmente illimitata, un'idea dell'utilizzo comune consentirà di definire un ambito per le proprie decisioni.  
  
 Per comprendere l'utilizzo comune del controllo, è utile riflettere sulla proposta di valore del controllo,  considerando le possibilità offerte da un determinato controllo rispetto ad altri.  L'utilizzo comune non è legato a un particolare aspetto visivo, ma piuttosto alla filosofia del controllo e a una serie di ragionevoli aspettative relative all'utilizzo del controllo stesso.  Questa considerazione consente di formulare alcune ipotesi relative al modello di composizione e ai comportamenti standard del controllo definiti dallo stile.  Nel caso di <xref:System.Windows.Controls.ComboBox>, ad esempio, la comprensione dell'utilizzo comune non sarà di nessun aiuto nel sapere se un determinato oggetto <xref:System.Windows.Controls.ComboBox> avrà gli angoli arrotondati, ma consentirà di prevedere che quell'oggetto <xref:System.Windows.Controls.ComboBox> richiede probabilmente una finestra popup e una modalità di attivazione e disattivazione nel caso in cui venga aperta.  
  
<a name="General_Guidelines"></a>   
## Indicazioni generali  
  
-   **Non applicare in maniera rigida i contratti dei modelli.** Il contratto del modello di un controllo può includere elementi, comandi, associazioni, trigger o anche impostazioni di proprietà richieste o previste per il corretto funzionamento del controllo.  
  
    -   Ridurre al minimo i contratti per quanto possibile.  
  
    -   Lavorare alla progettazione con la consapevolezza che in questa fase \(ovvero quando si utilizza uno strumento di progettazione\) è normale che il modello del controllo si trovi in uno stato incompleto.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non offre un'infrastruttura di stato della composizione; pertanto la compilazione dei controlli dovrà essere eseguita nella prospettiva che tale stato possa essere valido.  
  
    -   Non generare eccezioni quando un aspetto qualsiasi di un contratto del modello non viene rispettato.  Secondo queste linee guida, i pannelli non devono generare eccezioni se contengono un numero troppo elevato o troppo esiguo di elementi figlio.  
  
-   **Scomporre le funzionalità secondarie in elementi di supporto del modello.** Ogni controllo deve essere incentrato sulla funzionalità di base e sull'effettiva proposta di valore e definito in base all'utilizzo comune.  A tal fine, utilizzare elementi di composizione e di supporto all'interno del modello per abilitare comportamenti e visualizzazioni secondari, ovvero quei comportamenti e quelle visualizzazioni che non contribuiscono alla funzionalità di base del controllo.  Gli elementi di supporto sono suddivisi in tre categorie:  
  
    -   I tipi di supporto **autonomi** sono controlli o primitive pubblici e riutilizzabili che vengono utilizzati "in modo anonimo" all'interno di un modello, vale a dire che l'elemento di supporto non è in grado di rilevare il controllo al quale è stato applicato lo stile e viceversa.  Da un punto di vista tecnico, qualsiasi elemento può essere di tipo anonimo, ma in questo contesto il termine descrive i tipi che incapsulano funzionalità specializzate per abilitare scenari di destinazione.  
  
    -   Gli elementi di supporto **basati su tipi** sono tipi nuovi che incapsulano funzionalità specializzate.  Tali elementi vengono progettati in genere con una gamma di funzionalità più limitata rispetto ai controlli o alle primitive comuni.  A differenza degli elementi di supporto autonomi, quelli basati su tipi sono in grado di rilevare il contesto in cui vengono utilizzati e in genere devono condividere i dati con il controllo del relativo modello di appartenenza.  
  
    -   Gli elementi di supporto **con nome** sono i controlli e le primitive comuni di cui è prevista l'identificazione in base al nome da parte di un controllo all'interno del relativo modello. A tali elementi viene assegnato un nome noto all'interno del modello, consentendo pertanto a un controllo di individuare l'elemento e di interagire con esso a livello di codice.  In ciascun modello può esistere un solo elemento con un determinato nome.  
  
     Nella tabella seguente vengono riportati gli elementi di supporto attualmente utilizzati dagli stili del controllo \(l'elenco non è completo\):  
  
    |Elemento|Type|Utilizzato da|  
    |--------------|----------|-------------------|  
    |<xref:System.Windows.Controls.ContentPresenter>|Basato su tipi|<xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.CheckBox>, <xref:System.Windows.Controls.RadioButton>, <xref:System.Windows.Controls.Frame> e così via \(tutti i tipi <xref:System.Windows.Controls.ContentControl>\)|  
    |<xref:System.Windows.Controls.ItemsPresenter>|Basato su tipi|<xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.Menu> e così via \(tutti i tipi <xref:System.Windows.Controls.ItemsControl>\)|  
    |<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|Con nome|<xref:System.Windows.Controls.ToolBar>|  
    |<xref:System.Windows.Controls.Primitives.Popup>|Autonomo|<xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.ToolBar>, <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.ToolTip> e così via|  
    |<xref:System.Windows.Controls.Primitives.RepeatButton>|Con nome|<xref:System.Windows.Controls.Slider>, <xref:System.Windows.Controls.Primitives.ScrollBar> e così via|  
    |<xref:System.Windows.Controls.Primitives.ScrollBar>|Con nome|<xref:System.Windows.Controls.ScrollViewer>|  
    |<xref:System.Windows.Controls.ScrollViewer>|Autonomo|<xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.Menu>, <xref:System.Windows.Controls.Frame> e così via|  
    |<xref:System.Windows.Controls.Primitives.TabPanel>|Autonomo|<xref:System.Windows.Controls.TabControl>|  
    |<xref:System.Windows.Controls.TextBox>|Con nome|<xref:System.Windows.Controls.ComboBox>|  
    |<xref:System.Windows.Controls.Primitives.TickBar>|Basato su tipi|<xref:System.Windows.Controls.Slider>|  
  
-   **Ridurre al minimo le associazioni o le impostazioni di proprietà richieste specificate dall'utente per gli elementi di supporto**.  Di regola, un elemento di supporto richiede determinate associazioni o impostazioni di proprietà per un corretto funzionamento all'interno del modello di controllo.  Tali impostazioni dovrebbero essere specificate, per quanto possibile, dall'elemento di supporto e dal controllo basato su modelli.  Al momento dell'impostazione delle proprietà o della definizione delle associazioni, è necessario prestare attenzione a non eseguire l'override dei valori impostati dall'utente.  Di seguito vengono indicate le procedure consigliate:  
  
    -   Gli elementi di supporto con nome devono essere identificati dall'elemento padre, che deve stabilire le impostazioni richieste nell'elemento di supporto.  
  
    -   Le impostazioni richieste per gli elementi di supporto basati su tipi devono essere stabilite direttamente negli elementi.  Tale operazione talvolta richiede, da parte dell'elemento di supporto, l'esecuzione di una query sul contesto delle informazioni nel quale viene utilizzato, incluso l'oggetto `TemplatedParent` \(il tipo di controllo del modello in cui viene utilizzato\).  <xref:System.Windows.Controls.ContentPresenter>, ad esempio, associa automaticamente la proprietà `Content` del relativo oggetto `TemplatedParent` alla proprietà <xref:System.Windows.Controls.ContentPresenter.Content%2A>, se utilizzato in un tipo derivato <xref:System.Windows.Controls.ContentControl>.  
  
    -   Non è possibile ottimizzare allo stesso modo gli elementi di supporto autonomi, perché, per definizione, l'elemento di supporto e l'elemento padre non sono in grado di rilevarsi a vicenda.  
  
-   **Utilizzare la proprietà Name per impostare i flag degli elementi all'interno di un modello**.  Per individuare un elemento dello stile e accedere a tale elemento a livello di codice, un controllo dovrà utilizzare la proprietà `Name` e il paradigma `FindName`.  Se l'elemento non viene trovato, il controllo non dovrà generare un'eccezione ma piuttosto disabilitare in modo regolare e senza visualizzare alcun messaggio la funzionalità in cui tale elemento era richiesto.  
  
-   **Utilizzare le procedure consigliate per esprimere lo stato e il comportamento del controllo all'interno di uno stile.** Di seguito viene riportato un elenco ordinato delle procedure consigliate per indicare le modifiche e il comportamento dello stato del controllo all'interno di uno stile.  È opportuno utilizzare il primo elemento dell'elenco per abilitare lo scenario.  
  
    1.  Associazione di proprietà.  Esempio: associazione tra <xref:System.Windows.Controls.ComboBox.IsDropDownOpen%2A?displayProperty=fullName> e <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A?displayProperty=fullName>.  
  
    2.  Modifiche delle proprietà attivate o animazioni delle proprietà.  Esempio: stato di un oggetto <xref:System.Windows.Controls.Button> al passaggio del mouse.  
  
    3.  Comando.  Esempio: <xref:System.Windows.Controls.Primitives.ScrollBar.LineUpCommand> \/ <xref:System.Windows.Controls.Primitives.ScrollBar.LineDownCommand> in <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
    4.  Elementi di supporto autonomi.  Esempio: <xref:System.Windows.Controls.Primitives.TabPanel> in <xref:System.Windows.Controls.TabControl>.  
  
    5.  Tipi di supporto basati su tipi.  Esempio: <xref:System.Windows.Controls.ContentPresenter> in <xref:System.Windows.Controls.Button>, <xref:System.Windows.Controls.Primitives.TickBar> in <xref:System.Windows.Controls.Slider>.  
  
    6.  Elementi di supporto con nome.  Esempio: <xref:System.Windows.Controls.TextBox> in <xref:System.Windows.Controls.ComboBox>.  
  
    7.  Eventi propagati da tipi di supporto con nome.  Se si è in ascolto di eventi propagati da un elemento dello stile, è opportuno richiedere che l'elemento che ha generato l'evento possa essere identificato in modo univoco.  Esempio: <xref:System.Windows.Controls.Primitives.Thumb> in <xref:System.Windows.Controls.ToolBar>.  
  
    8.  Comportamento `OnRender` personalizzato.  Esempio: <xref:Microsoft.Windows.Themes.ButtonChrome> in <xref:System.Windows.Controls.Button>.  
  
-   **Utilizzare i trigger degli stili \(anziché i trigger dei modelli\) in modo sporadico**.  I trigger che hanno effetto sulle proprietà degli elementi del modello devono essere dichiarati nel modello.  I trigger che hanno effetto sulle proprietà del controllo \(escluso `TargetName`\) possono essere dichiarati nello stile, a meno che la modifica del modello non comporti l'eliminazione del trigger.  
  
-   **Essere coerenti con i modelli di applicazione dello stile esistenti.** Spesso esistono diversi modi per risolvere un problema.  È fondamentale conoscere e, se possibile, essere coerenti con i modelli di applicazione dello stile del controllo esistenti.  Tale accorgimento è particolarmente importante per i controlli che derivano dallo stesso tipo di base \(ad esempio, <xref:System.Windows.Controls.ContentControl>, <xref:System.Windows.Controls.ItemsControl>, <xref:System.Windows.Controls.Primitives.RangeBase> e così via\).  
  
-   **Esporre le proprietà per abilitare scenari di personalizzazione comuni senza applicare nuovamente i modelli**.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] non supporta parti personalizzabili o collegabili. Di conseguenza, l'utente di un controllo avrà a disposizione soltanto due metodi per la personalizzazione: l'impostazione diretta delle proprietà o l'impostazione delle proprietà tramite gli stili.  Pertanto, sarà opportuno limitare il numero di proprietà destinate a scenari di personalizzazione molto comuni, ad alta priorità, che richiederebbero altrimenti una nuova applicazione dei modelli.  Di seguito sono riportate le procedure consigliate per stabilire il momento e il metodo adatti per abilitare gli scenari di personalizzazione:  
  
    -   Le personalizzazioni molto comuni devono essere esposte come proprietà nel controllo e utilizzate dal modello.  
  
    -   Le personalizzazioni meno comuni \(benché non rare\) devono essere esposte come proprietà associate e utilizzate dal modello.  
  
    -   È accettabile che le personalizzazioni note ma poco comuni richiedano una nuova applicazione di modelli.  
  
<a name="Theme_Considerations"></a>   
## Considerazioni sui temi  
  
-   **Gli stili dei temi dovrebbero presentare una semantica delle proprietà coerente in tutti i temi, tuttavia non offrono alcuna garanzia in proposito**.  Come parte della documentazione, il controllo dovrebbe includere un documento con la descrizione della semantica delle proprietà del controllo, vale a dire del "significato" di una proprietà per un controllo.  Il controllo <xref:System.Windows.Controls.ComboBox>, ad esempio, dovrebbe definire il significato della proprietà <xref:System.Windows.Controls.Control.Background%2A> all'interno di <xref:System.Windows.Controls.ComboBox>.  Gli stili predefiniti per il controllo dovrebbero, per quanto possibile, attenersi alla semantica definita in tale documento per tutti i temi.  Gli utenti del controllo, d'altra parte, dovrebbero essere consapevoli del fatto che la semantica delle proprietà può variare da tema a tema.  In alcuni casi, potrebbe non essere possibile esprimere una determinata proprietà a causa dei vincoli visivi richiesti da un particolare tema.  Ad esempio, per molti controlli nel tema Classico non è disponibile un singolo bordo a cui applicare `Thickness`.  
  
-   **Gli stili dei temi non devono necessariamente presentare una semantica dei trigger coerente in tutti i temi**.  Il comportamento esposto da uno stile del controllo tramite trigger o animazioni può variare da tema a tema.  Gli utenti del controllo dovrebbero essere consapevoli del fatto che un controllo non impiega necessariamente lo stesso meccanismo in tutti i temi per ottenere un determinato comportamento.  È possibile, ad esempio, che un tema utilizzi un'animazione per indicare un comportamento al passaggio del mouse, laddove un altro tema utilizza un trigger.  Pertanto, nei controlli personalizzati è possibile che si verifichino delle incoerenze nella conservazione di un comportamento.  La modifica della proprietà dello sfondo, ad esempio, potrebbe non avere effetto sullo stato del controllo al passaggio del mouse, se tale stato viene espresso tramite un trigger.  Tuttavia, se lo stato al passaggio del mouse viene implementato mediante un'animazione, la modifica dello sfondo potrebbe interrompere l'animazione e di conseguenza la transizione di stato.  
  
-   **Gli stili dei temi non devono necessariamente presentare una semantica di "layout" coerente in tutti i temi**.  L'utilizzo dello stile predefinito, ad esempio, non deve garantire che un controllo conservi le stesse dimensioni in tutti i temi o che il relativo contenuto abbia gli stessi margini o la stessa spaziatura interna in tutti i temi.  
  
## Vedere anche  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)