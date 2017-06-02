---
title: "Risorse XAML | Microsoft Docs"
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
  - "riutilizzo di risorse"
  - "risorse, riutilizzo"
  - "riutilizzo di oggetti comunemente definiti"
  - "XAML, riutilizzo di risorse"
ms.assetid: 91580b89-a0a8-4889-aecb-fddf8e63175f
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 32
---
# Risorse XAML
Una risorsa è un oggetto che può essere riutilizzato in posizioni diverse all'interno dell'applicazione. Sono esempi di risorse di pennelli e stili. In questa panoramica viene descritto come utilizzare le risorse di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. È inoltre possibile creare e accedere alle risorse tramite codice o in modo intercambiabile tra codice e [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]. Per ulteriori informazioni, vedere [risorse e codice](../../../../docs/framework/wpf/advanced/resources-and-code.md).  
  
> [!NOTE]
>  I file di risorse descritta in questo argomento sono diversi da file di risorse descritto in [risorse dell'applicazione WPF, contenuto e i file di dati](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md) e diversi da quelli delle risorse incorporate o collegate descritto in [risorse dell'applicazione di gestione (.NET)](../Topic/Managing%20Application%20Resources%20\(.NET\).md).  
  
   
  
<a name="usingresources"></a>   
## <a name="using-resources-in-xaml"></a>Utilizzo delle risorse in XAML  
 L'esempio seguente definisce una <xref:System.Windows.Media.SolidColorBrush> come risorsa per l'elemento radice di una pagina. Nell'esempio viene quindi fa riferimento alla risorsa e viene utilizzata per impostare le proprietà dei diversi elementi figlio, inclusi un <xref:System.Windows.Shapes.Ellipse>, <xref:System.Windows.Controls.TextBlock>e un <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[FEResourceSH_snip#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xaml)]  
  
 Ogni elemento di livello di framework ( <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>) è un <xref:System.Windows.FrameworkElement.Resources%2A> proprietà, ovvero la proprietà che contiene le risorse (come un <xref:System.Windows.ResourceDictionary>) che definisce una risorsa. È possibile definire le risorse su qualsiasi elemento. Tuttavia, le risorse vengono più spesso definite nell'elemento radice, ovvero <xref:System.Windows.Controls.Page> nell'esempio.  
  
 Ogni risorsa in un dizionario risorse deve essere una chiave univoca. Quando si definiscono le risorse nel markup, si assegna la chiave univoca attraverso il [direttiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md). In genere, la chiave è una stringa. Tuttavia, è possibile anche impostare per altri tipi di oggetto utilizzando le estensioni di markup appropriato. Le chiavi per le risorse vengono utilizzate da alcune aree di funzionalità in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], in particolare per gli stili, risorse del componente e lo stile di dati.  
  
 Dopo aver definito una risorsa, è possibile fare riferimento la risorsa da utilizzare per un valore della proprietà utilizzando una sintassi di estensione di markup di risorse che specifica il nome della chiave, ad esempio:  
  
 [!code-xml[FEResourceSH_snip#KeyNameUsage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#keynameusage)]  
  
 Nell'esempio precedente, quando il [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] caricatore elabora il valore `{StaticResource MyBrush}` per il <xref:System.Windows.Controls.Control.Background%2A> proprietà <xref:System.Windows.Controls.Button>, la logica di ricerca di risorse controlla innanzitutto il dizionario di risorse per la <xref:System.Windows.Controls.Button> elemento. Se <xref:System.Windows.Controls.Button> non dispone di una definizione della chiave di risorsa `MyBrush` (non è presente, ovvero l'insieme di risorse è vuoto), la ricerca controlla quindi l'elemento padre di <xref:System.Windows.Controls.Button>, ovvero <xref:System.Windows.Controls.Page>. Pertanto, quando si definisce una risorsa nella <xref:System.Windows.Controls.Page> elemento radice, tutti gli elementi dell'albero logico di <xref:System.Windows.Controls.Page> possono accedervi ed è possibile riutilizzare la stessa risorsa per l'impostazione del valore di qualsiasi proprietà che accetta il <xref:System.Type> che rappresenta la risorsa. Nell'esempio precedente, lo stesso `MyBrush` due diverse proprietà set di risorse: il <xref:System.Windows.Controls.Control.Background%2A> di un <xref:System.Windows.Controls.Button>e <xref:System.Windows.Shapes.Shape.Fill%2A> di un <xref:System.Windows.Shapes.Rectangle>.  
  
<a name="staticdynamic"></a>   
## <a name="static-and-dynamic-resources"></a>Risorse statiche e dinamiche  
 Una risorsa può fare riferimento come una risorsa statica o una risorsa dinamica. Questa operazione viene eseguita utilizzando il [estensione di Markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) o [estensione di Markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md). Un'estensione di markup è una funzionalità di [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in base al quale è possibile specificare un riferimento all'oggetto con l'estensione di markup elabori la stringa di attributo e restituire l'oggetto a un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] caricatore. Per ulteriori informazioni sul comportamento delle estensioni di markup, vedere [le estensioni di Markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
 Quando si utilizza un'estensione di markup, si forniscono in genere uno o più parametri sotto forma di stringa che vengono elaborati da una particolare estensione di markup, piuttosto che viene valutata nel contesto di proprietà da impostare. Il [estensione di Markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) elabora un tasto cercando il valore per la chiave in tutti i dizionari risorse disponibili. Ciò si verifica durante il caricamento, ovvero il punto nel tempo quando è necessario che il processo di caricamento per assegnare il valore della proprietà che accetta il riferimento a una risorsa statica. Il [estensione di Markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md) invece di elaborare una chiave creando un'espressione che non valutata fino a quando non viene effettivamente eseguita l'applicazione, momento in cui l'espressione viene valutata e fornisce un valore.  
  
 Quando si fa riferimento a una risorsa, possono influenzare le considerazioni seguenti se si utilizza un riferimento a una risorsa statica o un riferimento alla risorsa dinamica:  
  
-   Il principio generale di creazione delle risorse per l'applicazione (per ogni pagina dell'applicazione, in file separati [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], in un assembly di sole risorse).  
  
-   La funzionalità dell'applicazione: aggiornamento delle risorse in tempo reale è parte dei requisiti dell'applicazione?  
  
-   Il comportamento di ricerca relativo di tale tipo di riferimento di risorsa.  
  
-   Proprietà specifica o tipo di risorsa e il comportamento di tali tipi nativo.  
  
### <a name="static-resources"></a>Risorse statiche  
 Risorsa statica fa riferimento a lavoro meglio nelle seguenti circostanze:  
  
-   La progettazione dell'applicazione si concentra di tutte le risorse nella pagina o risorsa a livello di applicazione più dizionari. Riferimenti a risorse statiche non vengono rivalutati basato sui comportamenti di runtime, ad esempio il ricaricamento di una pagina e pertanto può essere miglioramento delle prestazioni per evitare un numero elevato di riferimenti a risorse dinamiche quando non sono necessari per la progettazione di applicazioni e risorse.  
  
-   Si imposta il valore di una proprietà che non si trova in un <xref:System.Windows.DependencyObject> o <xref:System.Windows.Freezable>.  
  
-   Si sta creando un dizionario risorse che verrà compilato in una DLL e incluso come parte dell'applicazione o condivisi tra applicazioni.  
  
-   Si sta creando un tema per un controllo personalizzato e si definiscono le risorse utilizzate all'interno dei temi. In questo caso, in genere non si desidera il comportamento di ricerca di riferimento di risorsa dinamica, è invece il comportamento di riferimento di risorsa statica in modo che la ricerca è prevedibile e indipendente per il tema. Con una risorsa dinamica riferimento, anche un riferimento all'interno di un tema viene lasciato non valutato fino alla fase di esecuzione ed è probabile che, quando viene applicato il tema, alcuni elementi locali stabiliscono una chiave che il tema sta tentando di fare riferimento e l'elemento locale precederà il tema nella ricerca. In tal caso, il tema verrà non funzionino nel modo previsto.  
  
-   Si utilizzano risorse per impostare un numero elevato di proprietà di dipendenza. Le proprietà di dipendenza sono la memorizzazione nella cache il valore effettivo attivata dal sistema di proprietà, pertanto se si specifica un valore per una proprietà di dipendenza che può essere valutata in fase di caricamento, la proprietà di dipendenza non è necessario verificare la presenza di un'espressione rivalutata e può restituire l'ultimo valore effettivo. Questa tecnica può essere un miglioramento delle prestazioni.  
  
-   Si desidera modificare la risorsa sottostante per tutti i consumer o si desidera mantenere istanze scrivibili separate per ogni consumer mediante la [x: Shared Attribute](../../../../docs/framework/xaml-services/x-shared-attribute.md).  
  
#### <a name="static-resource-lookup-behavior"></a>Comportamento di ricerca di risorse statiche  
  
1.  La chiave richiesta all'interno del dizionario risorse definito dall'elemento che imposta la proprietà controlla il processo di ricerca.  
  
2.  Il processo di ricerca attraversa quindi verso l'alto, l'albero logico per l'elemento padre e il dizionario risorse. Il processo continua fino a raggiunta l'elemento radice.  
  
3.  Successivamente, vengono controllate le risorse dell'applicazione. Si tratta delle risorse all'interno del dizionario risorse definito dall'applicazione di <xref:System.Windows.Application> dell'oggetto per il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dell'applicazione.  
  
 Riferimenti a risorse statiche all'interno di un dizionario risorse devono fare riferimento a una risorsa che è già stata definita lessicalmente prima il riferimento a una risorsa. Riferimenti in avanti non è possibile risolvere un riferimento a una risorsa statica. Per questo motivo, se si utilizzano i riferimenti a risorse statiche, è necessario progettare la struttura del dizionario risorse in modo che le risorse destinate all'utilizzo per risorsa sono definite in o verso l'inizio di ogni dizionario risorse corrispondente.  
  
 Ricerca delle risorse statiche può estendersi, temi o alle risorse di sistema, ma questa funzionalità è supportata solo perché il [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] caricatore rinvia la richiesta. Proroga è necessaria affinché il tema di runtime al momento che del caricamento della pagina in modo corretto all'applicazione. Tuttavia, riferimenti alle risorse statiche alle chiavi che sicuramente esistono solo in temi o come sistema di risorse non sono consigliate. Questo avviene perché tali riferimenti non vengono valutate nuovamente se il tema è stato modificato dall'utente in tempo reale. Un riferimento alla risorsa dinamica è più affidabile quando si richiede il tema o risorse di sistema. L'eccezione è quando un elemento tema stesso richiede un'altra risorsa. Questi riferimenti devono essere riferimenti a risorse statiche, per i motivi descritti in precedenza.  
  
 Il comportamento di eccezione se non viene trovato un riferimento a una risorsa statica varia. Se la risorsa è stata rinviata, viene generata l'eccezione in fase di esecuzione. Se la risorsa non è stata posticipata, l'eccezione si verifica in fase di caricamento.  
  
### <a name="dynamic-resources"></a>Risorse dinamiche  
 Risorse dinamiche funzionano meglio nelle seguenti circostanze:  
  
-   Il valore della risorsa dipende dalle condizioni che non sono noti fino al runtime. Ciò include le risorse di sistema o risorse che sono impostabile dall'utente in caso contrario. Ad esempio, è possibile creare valori setter che fanno riferimento alle proprietà di sistema, come esposto da <xref:System.Windows.SystemColors>, <xref:System.Windows.SystemFonts>, o <xref:System.Windows.SystemParameters>. Questi valori sono effettivamente dinamici perché in definitiva derivano dall'ambiente di runtime dell'utente e sistema operativo. Potrebbe inoltre essere temi a livello di applicazione che possono essere modificati, in cui l'accesso alle risorse a livello di pagina deve inoltre acquisire la modifica.  
  
-   Si sta creando o riferimento a stili del tema per un controllo personalizzato.  
  
-   Si prevede di modificare il contenuto di un <xref:System.Windows.ResourceDictionary> durante un ciclo di vita dell'applicazione.  
  
-   Si dispone di una struttura risorse complicata con interdipendenze, in cui potrebbe essere necessario un riferimento in avanti. Riferimenti a risorse statiche non supportano i riferimenti in avanti, ma riferimenti a risorse dinamiche li supportano perché la risorsa non deve essere valutata fino alla fase di esecuzione e i riferimenti in avanti non sono pertanto un concetto rilevante.  
  
-   Si fa riferimento a una risorsa di dimensioni particolarmente grande dalla prospettiva di una compilazione o un set di lavoro e la risorsa non è possibile utilizzare immediatamente al caricamento della pagina. Riferimenti a risorse statiche sempre caricate da [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] quando la pagina viene caricata; tuttavia, un riferimento alla risorsa dinamica non viene caricato finché non viene effettivamente utilizzato.  
  
-   Si sta creando uno stile in cui i valori di setter potrebbero provenire da altri valori che sono influenzate da temi o altre impostazioni utente.  
  
-   Si applicano le risorse per gli elementi che potrebbe essere ricollegati nell'albero logico nel corso della durata dell'applicazione. L'elemento padre anche potenzialmente Modifica ambito di ricerca, quindi, se si desidera la risorsa per un elemento nuovo padre sia rivalutata in base all'ambito di nuovo, utilizzare sempre un riferimento alla risorsa dinamica.  
  
#### <a name="dynamic-resource-lookup-behavior"></a>Comportamento di ricerca di risorse dinamiche  
 Comportamento di ricerca di risorse per un riferimento alla risorsa dinamica parallelo al comportamento di ricerca nel codice se si chiama <xref:System.Windows.FrameworkElement.FindResource%2A> o <xref:System.Windows.FrameworkElement.SetResourceReference%2A>.  
  
1.  La chiave richiesta all'interno del dizionario risorse definito dall'elemento che imposta la proprietà controlla il processo di ricerca.  
  
    -   Se l'elemento definisce un <xref:System.Windows.FrameworkElement.Style%2A> proprietà, il <xref:System.Windows.Style.Resources%2A> dizionario interno la <xref:System.Windows.Style> sia selezionata.  
  
    -   Se l'elemento definisce un <xref:System.Windows.Controls.Control.Template%2A> proprietà, il <xref:System.Windows.FrameworkTemplate.Resources%2A> dizionario interno la <xref:System.Windows.FrameworkTemplate> sia selezionata.  
  
2.  Il processo di ricerca attraversa quindi verso l'alto, l'albero logico per l'elemento padre e il dizionario risorse. Il processo continua fino a raggiunta l'elemento radice.  
  
3.  Successivamente, vengono controllate le risorse dell'applicazione. Si tratta delle risorse all'interno del dizionario risorse definito dall'applicazione di <xref:System.Windows.Application> dell'oggetto per il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dell'applicazione.  
  
4.  Dizionario è selezionata, per il tema attualmente attivo. Se il tema verrà modificato in fase di esecuzione, il valore viene rivalutato.  
  
5.  Risorse di sistema vengono controllate.  
  
 Comportamento delle eccezioni (se presente) varia:  
  
-   Se è stata richiesta una risorsa da un <xref:System.Windows.FrameworkElement.FindResource%2A> chiamare e non viene trovata, viene generata un'eccezione.  
  
-   Se è stata richiesta una risorsa da un <xref:System.Windows.FrameworkElement.TryFindResource%2A> chiamare e non è stato trovato, viene generata alcuna eccezione, ma il valore restituito è `null`. Se la proprietà viene impostata non accetta `null`, è comunque possibile che venga generata un'eccezione più profonda (ciò dipende dalla singola proprietà impostata).  
  
-   Se è stata richiesta una risorsa da un riferimento alla risorsa dinamica in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]e non è stato trovato, quindi il comportamento dipende dal sistema di proprietà generale, ma il comportamento generale come se nessuna operazione di impostazione della proprietà effettuata al livello in cui esiste la risorsa. Ad esempio, se si tenta di impostare lo sfondo in un elemento singolo pulsante utilizzando una risorsa che non può essere valutata, quindi impostato alcun valore risultati, ma il valore effettivo ancora può provenire da altri partecipanti in precedenza della proprietà di sistema e il valore. Ad esempio, il valore di background ancora potrebbe provenire da uno stile di pulsante definito localmente o dallo stile del tema. Per le proprietà che non sono definite mediante gli stili del tema, il valore effettivo dopo la valutazione di una risorsa non riuscita potrebbe derivare il valore predefinito nei metadati della proprietà.  
  
#### <a name="restrictions"></a>Restrizioni  
 Riferimenti a risorse dinamiche hanno alcune restrizioni rilevanti. Almeno uno dei seguenti deve essere true:  
  
-   Impostazione della proprietà deve essere una proprietà di un <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>. Tale proprietà deve essere supportata da un <xref:System.Windows.DependencyProperty>.  
  
-   Il riferimento è un valore all'interno di un <xref:System.Windows.Style><xref:System.Windows.Setter>.  
  
-   Impostazione della proprietà deve essere una proprietà di un <xref:System.Windows.Freezable> che viene fornito come un valore di un <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> , proprietà o un <xref:System.Windows.Setter> valore.  
  
 Poiché la proprietà viene impostata deve essere un <xref:System.Windows.DependencyProperty> o <xref:System.Windows.Freezable> proprietà, la maggior parte delle modifiche alle proprietà propagarsi all'interfaccia utente perché la modifica di una proprietà (il valore di risorsa dinamica modificato) viene riconosciuta dal sistema di proprietà. La maggior parte dei controlli comprende una logica che impone un altro layout di un controllo, se un <xref:System.Windows.DependencyProperty> modifiche e proprietà potrebbero influire sul layout. Tuttavia, non tutte le proprietà che hanno un [estensione di Markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md) come i relativi valori sono garantiti per fornire il valore in modo l'aggiornamento in tempo reale nell'interfaccia utente. Comunque, tale funzionalità può variare a seconda della proprietà, nonché a seconda del tipo che possiede la proprietà, o anche la struttura logica dell'applicazione.  
  
<a name="stylesimplicitkeys"></a>   
## <a name="styles-datatemplates-and-implicit-keys"></a>Gli stili, DataTemplate e chiavi implicite  
 In precedenza, è stato dichiarato che tutti gli elementi un <xref:System.Windows.ResourceDictionary> deve avere una chiave. Tuttavia, ciò significa che tutte le risorse devono avere esplicita `x:Key`. Diversi tipi di oggetto supportano una chiave implicita quando viene definito come una risorsa, in cui è associato il valore della chiave per il valore di un'altra proprietà. Ciò è noto come chiave implicita, mentre un `x:Key` attributo è una chiave esplicita. È possibile sovrascrivere qualsiasi chiave implicita specificando una chiave esplicita.  
  
 Uno scenario molto importante per le risorse è quando si definisce un <xref:System.Windows.Style>. In realtà, un <xref:System.Windows.Style> è quasi sempre definito come una voce in un dizionario risorse, perché gli stili sono implicitamente destinati al riutilizzo. Per ulteriori informazioni sugli stili, vedere [di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
 Possono essere sia creati con gli stili dei controlli e si fa riferimento con una chiave implicita. Gli stili del tema che definiscono l'aspetto predefinito di un controllo si basano su questa chiave implicita. La chiave implicita dal punto di vista della richiesta è il <xref:System.Type> del controllo stesso. La chiave implicita dal punto di vista della definizione della risorsa è il <xref:System.Windows.Style.TargetType%2A> dello stile. Pertanto, se si siano creando i temi per i controlli personalizzati, la creazione di stili che interagiscono con gli stili del tema esistente, non devi specificare un [direttiva X:Key](../../../../docs/framework/xaml-services/x-key-directive.md) che <xref:System.Windows.Style>. E se si desidera utilizzare gli stili dei temi, non è necessario specificare uno stile affatto. Ad esempio, la definizione di stile seguente funziona anche se il <xref:System.Windows.Style> risorse sembrano non avere una chiave:  
  
 [!code-xml[FEResourceSH_snip#ImplicitStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#implicitstyle)]  
  
 Tale stile dispone effettivamente di una chiave: la chiave implicita `typeof(` <xref:System.Windows.Controls.Button>`)`. Nel markup, è possibile specificare un <xref:System.Windows.Style.TargetType%2A> direttamente come tipo di nome (o è possibile utilizzare facoltativamente [{x: Type...}](../../../../docs/framework/xaml-services/x-type-markup-extension.md) per restituire un <xref:System.Type>.  
  
 Attraverso i meccanismi di stile del tema predefinito utilizzati da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], che viene applicato lo stile come stile di runtime di un <xref:System.Windows.Controls.Button> nella pagina anche se il <xref:System.Windows.Controls.Button> stesso non tenta di specificare il relativo <xref:System.Windows.FrameworkElement.Style%2A> proprietà o un riferimento a una risorsa specifica lo stile. Lo stile definito nella pagina viene trovato in precedenza lo stile del dizionario tema, utilizzando la stessa chiave che lo stile del dizionario tema ha in precedenza nella sequenza di ricerca. È possibile specificare solo `<Button>Hello</Button>` in qualsiasi parte della pagina e lo stile è definita con <xref:System.Windows.Style.TargetType%2A> di `Button` si applicherebbe a tale pulsante. Se si desidera, è possibile chiave in modo esplicito lo stile con lo stesso valore di tipo come <xref:System.Windows.Style.TargetType%2A>per maggiore chiarezza nel markup, ma che è facoltativo.  
  
 Le chiavi implicite per gli stili non si applicano in un controllo se <xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> è `true` (si noti inoltre che <xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> potrebbe essere impostato come parte del comportamento nativo per la classe del controllo, anziché in modo esplicito in un'istanza del controllo). Inoltre, per supportare le chiavi implicite per gli scenari di classe derivata, il controllo deve eseguire l'override <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> (tutti i controlli esistenti forniti come parte di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] eseguire questa operazione). Per ulteriori informazioni sulla progettazione dei controlli, temi e stili, vedere [linee guida per la progettazione di controlli di stile](../../../../docs/framework/wpf/controls/guidelines-for-designing-stylable-controls.md).  
  
 <xref:System.Windows.DataTemplate> dispone anche di una chiave implicita. La chiave implicita di un <xref:System.Windows.DataTemplate> è il <xref:System.Windows.DataTemplate.DataType%2A> valore della proprietà.                  <xref:System.Windows.DataTemplate.DataType%2A> può anche essere specificato come il nome del tipo anziché in modo esplicito utilizzando [{x: Type...} ](../../../../docs/framework/xaml-services/x-type-markup-extension.md). Per informazioni dettagliate, vedere [Cenni preliminari sui modelli di dati](../../../../docs/framework/wpf/data/data-templating-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.ResourceDictionary>   
 [Risorse dell'applicazione](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Risorse e codice](../../../../docs/framework/wpf/advanced/resources-and-code.md)   
 [Definire e fare riferimento a una risorsa](../../../../docs/framework/wpf/advanced/how-to-define-and-reference-a-resource.md)   
 [Panoramica di gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md)   
 [Estensione di Markup X:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [Estensione del Markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [Estensione del Markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)