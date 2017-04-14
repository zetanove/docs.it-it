---
title: "Propriet&#224; Dependency personalizzate | Microsoft Docs"
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
  - "proprietà Dependency personalizzate"
  - "proprietà di dipendenza, personalizzati"
  - "implementazione, wrapper"
  - "metadati, per le proprietà"
  - "proprietà, metadati"
  - "proprietà, registrazione"
  - "registrazione di proprietà"
  - "wrapper, implementazione"
ms.assetid: e6bfcfac-b10d-4f58-9f77-a864c2a2938f
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# Propriet&#224; Dependency personalizzate
In questo argomento vengono descritte le ragioni per cui sviluppatori di applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e autori di componenti potrebbero decidere di creare una [proprietà di dipendenza](GTMT) personalizzata e vengono illustrati i passaggi dell'implementazione nonché alcune opzioni di implementazione in grado di migliorare le prestazioni, l'usabilità o la versatilità della proprietà.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="prerequisites"></a>   
## Prerequisiti  
 In questo argomento si presuppone la conoscenza delle proprietà di dipendenza dal punto di vista di un consumer di proprietà di dipendenza esistenti nelle classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], nonché la lettura dell'argomento [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  Per seguire gli esempi di questo argomento, è necessaria inoltre la comprensione di [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] oltre che la conoscenza della modalità di scrittura delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="whatis"></a>   
## Definizione della proprietà di dipendenza  
 È possibile consentire a una proprietà che in caso contrario sarebbe una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] il supporto dell'aggiunta di stili, dell'associazione dati, dell'ereditarietà, delle animazioni e di valori predefiniti mediante l'implementazione della proprietà stessa come [proprietà di dipendenza](GTMT).  Le proprietà di dipendenza sono proprietà registrate con il sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] chiamando il metodo <xref:System.Windows.DependencyProperty.Register%2A> \(o <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A>\) e che sono supportate da un campo di identificazione <xref:System.Windows.DependencyProperty>.  Le proprietà di dipendenza possono essere utilizzate solo dai tipi <xref:System.Windows.DependencyObject>; tuttavia, dal momento che <xref:System.Windows.DependencyObject> è piuttosto elevato nella gerarchia di classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], la maggior parte delle classi disponibili in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] è in grado di supportare questo tipo di proprietà.  Per ulteriori informazioni sulle proprietà di dipendenza e per la terminologia e le convenzioni utilizzate per descriverle in questo [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)], vedere [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md).  
  
<a name="example_dp"></a>   
## Esempi di proprietà di dipendenza  
 Tra gli esempi di proprietà di dipendenza implementati nelle classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono incluse le proprietà <xref:System.Windows.Controls.Control.Background%2A>, <xref:System.Windows.FrameworkElement.Width%2A> e <xref:System.Windows.Controls.TextBox.Text%2A>.  Ogni proprietà di dipendenza esposta da una classe dispone di un campo statico pubblico corrispondente del tipo <xref:System.Windows.DependencyProperty> esposto in quella stessa classe. Si tratta dell'identificatore per la proprietà di dipendenza.  L'identificatore viene denominato mediante la seguente convenzione: nome della [proprietà di dipendenza](GTMT) seguito dalla stringa `Property`.  Ad esempio, il campo di identificazione <xref:System.Windows.DependencyProperty> corrispondente per la proprietà <xref:System.Windows.Controls.Control.Background%2A> è <xref:System.Windows.Controls.Control.BackgroundProperty>.  L'identificatore archivia le informazioni sulla [proprietà di dipendenza](GTMT) al momento della registrazione della proprietà e viene utilizzato in seguito per altre operazioni che coinvolgono la [proprietà di dipendenza](GTMT), ad esempio la chiamata di <xref:System.Windows.DependencyObject.SetValue%2A>.  
  
 Come indicato in [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md), tutte le proprietà di dipendenza di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] \(eccetto la maggior parte delle [proprietà associate](GTMT)\) sono inoltre proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] a causa dell'implementazione del "wrapper".  Pertanto, mediante il codice è possibile ottenere o impostare proprietà di dipendenza chiamando funzioni di accesso [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] che definiscono i wrapper in modo identico alle altre proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  I consumer di proprietà di dipendenza stabilite in genere non utilizzano i metodi <xref:System.Windows.DependencyObject><xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>, che sono il punto di connessione al sistema di proprietà sottostante.  Piuttosto, l'implementazione esistente delle proprietà [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] avrà già chiamato <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A> all'interno delle implementazioni dei wrapper `get` e `set` della proprietà, utilizzando in modo appropriato il campo dell'identificatore.  Se l'implementazione di una proprietà di dipendenza personalizzata viene eseguita in modo autonomo, il wrapper verrà definito in modo simile.  
  
<a name="backing_with_dp"></a>   
## Quando implementare una proprietà di dipendenza  
 Quando si implementa una proprietà in una classe, se la classe deriva da <xref:System.Windows.DependencyObject>, è possibile supportare la proprietà con un identificatore <xref:System.Windows.DependencyProperty>, rendendola pertanto una proprietà di dipendenza.  Trasformare una proprietà in una proprietà di dipendenza non sempre è necessario o appropriato e dipende dalle esigenze dello scenario.  Talvolta è opportuno utilizzare la tecnica normale che consiste nel supportare la proprietà con un campo privato.  Tuttavia, se si desidera che la proprietà supporti una o più delle seguenti funzionalità [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è necessario implementarla come [proprietà di dipendenza](GTMT):  
  
-   Si desidera che la proprietà possa essere impostata in uno stile.  Per ulteriori informazioni, vedere [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
-   Si desidera che la proprietà supporti l'associazione dati.  Per le ulteriori informazioni sulle proprietà di dipendenza con associazione dati, vedere [Eseguire l'associazione delle proprietà di due controlli](../../../../docs/framework/wpf/data/how-to-bind-the-properties-of-two-controls.md).  
  
-   Si desidera che la proprietà possa essere impostata con un riferimento di risorsa dinamica.  Per ulteriori informazioni, vedere [Risorse XAML](../../../../docs/framework/wpf/advanced/xaml-resources.md).  
  
-   Si desidera ereditare un valore di proprietà automaticamente da un elemento padre nella struttura ad albero dell'elemento.  In questo caso, effettuare la registrazione con il metodo <xref:System.Windows.DependencyProperty.RegisterAttached%2A>, persino nel caso in cui si crei anche un wrapper della proprietà per l'accesso [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Per ulteriori informazioni, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
-   Si desidera che la proprietà sia animata.  Per ulteriori informazioni, vedere [Cenni preliminari sull'animazione](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md).  
  
-   Si desidera che il sistema di proprietà segnali quando il valore precedente della proprietà è stato modificato da azioni intraprese dal sistema di proprietà, dall'ambiente o dall'utente oppure tramite la lettura e l'utilizzo degli stili.  Se si utilizzano i metadati della proprietà, la proprietà può specificare un metodo di callback che verrà richiamato ogni volta il sistema di proprietà determina che il valore della proprietà è stato modificato definitivamente.  Un concetto correlato è la coercizione del valore di proprietà.  Per ulteriori informazioni, vedere [Callback e convalida delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md).  
  
-   Si desidera utilizzare convenzioni di metadati definite che sono utilizzate anche dai processi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ad esempio la segnalazione dell'eventualità che la modifica di un valore di proprietà richieda che il sistema di layout ricomponga gli elementi visivi di un elemento.  Oppure si desidera utilizzare override di metadati in modo che le classi derivate possano modificare caratteristiche basate sui metadati quali il valore predefinito.  
  
-   Si desidera che le proprietà di un controllo personalizzato ricevano supporto [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)], ad esempio la modifica della finestra **Proprietà**.  Per ulteriori informazioni, vedere [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
 Quando si esaminano questi scenari, è necessario considerare inoltre se è possibile realizzare lo scenario eseguendo l'override dei metadati di una [proprietà di dipendenza](GTMT) esistente, piuttosto che implementando una proprietà completamente nuova.  La validità dell'utilizzo di un override di metadati dipende dallo scenario e dalla vicinanza di quello scenario, in termini di somiglianza, all'implementazione nelle proprietà di dipendenza [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] esistenti e nelle classi.  Per ulteriori informazioni sull'override dei metadati nelle proprietà esistenti, vedere [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="checklist"></a>   
## Elenco di controllo per la definizione di una proprietà di dipendenza  
 La definizione di una proprietà di dipendenza include quattro concetti distinti.  Tali concetti non rappresentano necessariamente passaggi rigidi di una procedura, in quanto alcuni di questi finiscono per essere combinati come singole righe di codice nell'implementazione:  
  
-   \(Facoltativo\) Creare metadati di proprietà per la proprietà di dipendenza.  
  
-   Registrare il nome della proprietà con il sistema di proprietà, specificando un tipo di proprietario e il tipo del valore di proprietà.  Se utilizzati, specificare anche i metadati della proprietà.  
  
-   Definire un identificatore <xref:System.Windows.DependencyProperty> come campo `static` `public` `readonly` per il tipo di proprietario.  
  
-   Definire una proprietà "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] il cui nome corrisponda al nome della proprietà di dipendenza.  Implementare le funzioni di accesso `get` e `set` della proprietà "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] da connettere alla proprietà di dipendenza che la supporta.  
  
<a name="registering"></a>   
### Registrazione della proprietà con il sistema di proprietà.  
 Affinché la proprietà sia una [proprietà di dipendenza](GTMT), è necessario registrarla in una tabella gestita dal sistema di proprietà e fornirle un identificatore univoco utilizzato come qualificatore per le successive operazioni del sistema di proprietà.  Tali operazioni potrebbero essere operazioni interne oppure le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] del sistema di proprietà di chiamata del codice.  Per registrare la proprietà, chiamare il metodo <xref:System.Windows.DependencyProperty.Register%2A> all'interno del corpo della classe \(all'interno della classe, ma all'esterno di qualsiasi definizione del membro\).  Il campo dell'identificatore viene inoltre fornito dalla chiamata al metodo <xref:System.Windows.DependencyProperty.Register%2A>, come valore restituito.  La ragione per la quale la chiamata a <xref:System.Windows.DependencyProperty.Register%2A> viene effettuata all'esterno delle definizioni degli altri membri è che questo valore restituito viene utilizzato per assegnare e creare un campo `static` `public` `readonly` di tipo <xref:System.Windows.DependencyProperty> come parte della classe.  Questo campo diventa l'identificatore per la proprietà di dipendenza.  
  
 [!code-csharp[WPFAquariumSln#RegisterAG](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerag)]
 [!code-vb[WPFAquariumSln#RegisterAG](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerag)]  
  
<a name="nameconventions"></a>   
### Convenzioni di denominazione delle proprietà di dipendenza  
 Esistono convenzioni di denominazione definite relative alle proprietà di dipendenza che è necessario seguire in tutte le circostanze tranne in casi eccezionali.  
  
 La proprietà di dipendenza stessa avrà un nome di base, "AquariumGraphic" come in questo esempio, fornito come primo parametro di <xref:System.Windows.DependencyProperty.Register%2A>.  Tale nome deve essere univoco all'interno di ogni tipo di registrazione.  Le proprietà di dipendenza ereditate tramite tipi di base sono considerate già parte del tipo di registrazione; i nomi delle proprietà ereditate non possono essere registrati nuovamente.  Tuttavia, esiste una tecnica per aggiungere una classe come proprietario di una proprietà di dipendenza persino quando quella proprietà di dipendenza non è ereditata; per informazioni dettagliate, vedere [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
 Quando si crea il campo dell'identificatore, denominare questo campo con il nome della proprietà registrata, più il suffisso `Property`.  Questo campo rappresenta l'identificatore per la proprietà di dipendenza e sarà utilizzato in seguito come un input per le chiamate a <xref:System.Windows.DependencyObject.SetValue%2A> e a <xref:System.Windows.DependencyObject.GetValue%2A> nei wrapper, da parte di qualsiasi altro accesso di codice alla proprietà, dal codice personale, da qualsiasi accesso di codice esterno consentito, dal sistema di proprietà e potenzialmente dai processori [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
> [!NOTE]
>  La definizione della proprietà di dipendenza nel corpo della classe costituisce l'implementazione tipica, tuttavia è anche possibile definire una proprietà di dipendenza nel costruttore statico della classe.  Questo approccio potrebbe essere utile nel caso in cui siano necessarie più righe di codice per inizializzare la proprietà di dipendenza.  
  
<a name="wrapper1"></a>   
### Implementazione del "wrapper"  
 L'implementazione del wrapper deve chiamare <xref:System.Windows.DependencyObject.GetValue%2A> nell'implementazione `get` e <xref:System.Windows.DependencyObject.SetValue%2A> nell'implementazione `set` \(la chiamata di registrazione originale e il campo sono mostrati anche in questo caso per chiarezza\).  
  
 In tutte le circostanze tranne in casi eccezionali, le implementazioni del wrapper devono eseguire solo le azioni <xref:System.Windows.DependencyObject.GetValue%2A> e <xref:System.Windows.DependencyObject.SetValue%2A>, rispettivamente.  La ragione è discussa nell'argomento [Caricamento XAML e proprietà di dipendenza](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md).  
  
 Tutte le proprietà di dipendenza pubbliche esistenti fornite nelle classi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizzano questo semplice modello di implementazione del wrapper; la maggior parte della complessità della modalità di funzionamento delle proprietà di dipendenza è dovuta a un comportamento intrinseco del sistema di proprietà oppure è implementata tramite altri concetti quali la coercizione o i callback di modifica della proprietà mediante i metadati della proprietà.  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
 Anche in questo caso, per convenzione, il nome della proprietà del wrapper deve corrispondere esattamente al nome scelto e fornito come primo parametro della chiamata <xref:System.Windows.DependencyProperty.Register%2A> che ha registrato la proprietà.  Se la proprietà non segue la convenzione, non necessariamente vengono disabilitati tutti i possibili utilizzi, ma si incontreranno molti problemi rilevanti:  
  
-   Determinati aspetti di stili e modelli non funzioneranno.  
  
-   La maggior parte degli strumenti e delle finestre di progettazione devono basarsi sulle convenzioni di denominazione per serializzare correttamente [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] o per fornire assistenza relativamente all'ambiente della finestra di progettazione a livello di singola proprietà.  
  
-   L'implementazione corrente del caricatore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ignora completamente i wrapper e si basa sulla convenzione di denominazione al momento dell'elaborazione dei valori dell'attributo.  Per ulteriori informazioni, vedere [Caricamento XAML e proprietà di dipendenza](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md).  
  
<a name="metadata"></a>   
### Metadati della proprietà per una nuova proprietà di dipendenza.  
 Quando si registra una proprietà di dipendenza, la registrazione tramite il sistema di proprietà crea un oggetto dei metadati che archivia le caratteristiche della proprietà.  Molte di queste caratteristiche dispongono di impostazioni predefinite che vengono impostate se la proprietà viene registrata con le semplici firme di <xref:System.Windows.DependencyProperty.Register%2A>.  Le altre firme di <xref:System.Windows.DependencyProperty.Register%2A> consentono di specificare i metadati desiderati quando si registra la proprietà.  I metadati più comuni per le proprietà di dipendenza consistono nel fornire a tali proprietà un valore predefinito che viene applicato alle nuove istanze che utilizzano la proprietà.  
  
 Se si crea una proprietà di dipendenza che esiste in una classe derivata di <xref:System.Windows.FrameworkElement>, è possibile utilizzare la classe dei metadati <xref:System.Windows.FrameworkPropertyMetadata> più specializzata piuttosto che la classe <xref:System.Windows.PropertyMetadata> di base.  Il costruttore per la classe <xref:System.Windows.FrameworkPropertyMetadata> dispone di molte firme nelle quali è possibile specificare una combinazione delle varie caratteristiche dei metadati.  Se si desidera specificare solo il valore predefinito, utilizzare la firma che accetta un singolo parametro di tipo <xref:System.Object>.  Passare quel parametro di oggetto come valore predefinito specifico del tipo per la proprietà \(il valore predefinito fornito deve essere il tipo fornito come parametro `propertyType` nella chiamata a <xref:System.Windows.DependencyProperty.Register%2A>\).  
  
 Per <xref:System.Windows.FrameworkPropertyMetadata>, è inoltre possibile specificare i flag di opzione dei metadati per la proprietà.  Tali flag vengono convertiti in proprietà discrete nei metadati della proprietà dopo la registrazione e utilizzati per comunicare determinate istruzioni condizionali agli altri processi quali il motore di layout.  
  
#### Impostazione di flag di metadati appropriati  
  
-   Se la proprietà \(o le modifiche nel relativo valore\) influisce sull'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] e in particolare sul modo in cui il sistema di layout deve ridimensionare o eseguire il rendering dell'elemento in una pagina, impostare uno o più flag tra quelli indicati di seguito: <xref:System.Windows.FrameworkPropertyMetadataOptions>, <xref:System.Windows.FrameworkPropertyMetadataOptions>, <xref:System.Windows.FrameworkPropertyMetadataOptions>.  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> indica che una modifica a questa proprietà richiede una modifica al rendering dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] nella quale l'oggetto contenitore potrebbe richiedere uno spazio maggiore o minore all'interno dell'elemento padre.  Ad esempio, è necessario impostare questo flag in una proprietà "Width".  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> indica che una modifica a questa proprietà richiede una modifica al rendering dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] che in genere non rende necessaria una modifica nello spazio dedicato, ma che tuttavia indica che il posizionamento all'interno dello spazio è stato modificato.  Ad esempio, è necessario impostare questo flag in una proprietà "Alignment".  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> indica che si è verificata un'altra modifica che non influirà sul layout e sulla misurazione ma che richiede un altro rendering.  Un esempio potrebbe essere una proprietà che modifica un colore di un elemento esistente, ad esempio "Background".  
  
    -   Questi flag spesso sono utilizzati come protocollo nei metadati per le implementazioni di override del sistema di proprietà o per i callback del layout.  È possibile, ad esempio, che si disponga di un callback di <xref:System.Windows.DependencyObject.OnPropertyChanged%2A> che esegue la chiamata a <xref:System.Windows.UIElement.InvalidateArrange%2A> se una qualsiasi proprietà dell'istanza segnala una modifica del valore e presenta un valore `true` per <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> nei relativi metadati.  
  
-   Alcune proprietà possono influire sulle caratteristiche di rendering dell'elemento padre contenitore, in modo maggiore rispetto alle modifiche nelle dimensioni necessarie indicate in precedenza.  Un esempio è la proprietà <xref:System.Windows.Documents.Paragraph.MinOrphanLines%2A> utilizzata nel modello del documento dinamico, nel quale le modifiche a quella proprietà possono modificare il rendering globale del documento dinamico che contiene il paragrafo.  Utilizzare <xref:System.Windows.FrameworkPropertyMetadataOptions> o <xref:System.Windows.FrameworkPropertyMetadataOptions> per identificare casi simili nelle proprietà utilizzate.  
  
-   Per impostazione predefinita, le proprietà di dipendenza supportano l'associazione dati.  È possibile disabilitare intenzionalmente l'associazione dati per i casi in cui non esiste uno scenario realistico per l'associazione dati o nei quali le prestazioni dell'associazione dati per un oggetto di grandi dimensioni viene considerata un problema.  
  
-   Per impostazione predefinita, l'associazione dati <xref:System.Windows.Data.Binding.Mode%2A> per le proprietà di dipendenza utilizza <xref:System.Windows.Data.BindingMode> come valore predefinito.  È sempre possibile modificare l'associazione in modo che diventi <xref:System.Windows.Data.BindingMode> per istanza di associazione; per i dettagli, vedere [Specificare la direzione dell'associazione](../../../../docs/framework/wpf/data/how-to-specify-the-direction-of-the-binding.md).  Tuttavia, in qualità di autore della proprietà di dipendenza, è possibile scegliere di fare in modo che la proprietà utilizzi la modalità di associazione <xref:System.Windows.Data.BindingMode> per impostazione predefinita.  Un esempio di una proprietà di dipendenza esistente è <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A?displayProperty=fullName>; lo scenario per questa proprietà consiste nel fatto che la logica di impostazione <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> e la composizione di <xref:System.Windows.Controls.MenuItem> interagiscono con lo stile del tema predefinito.  La logica della proprietà <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> utilizza l'associazione dati a livello nativo per gestire lo stato della proprietà in conformità alle altre proprietà di stato e alle chiamate ai metodi.  Un altro esempio di proprietà che esegue l'associazione di <xref:System.Windows.Data.BindingMode> per impostazione predefinita è <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName>.  
  
-   È anche possibile abilitare l'ereditarietà della proprietà in una proprietà di dipendenza personalizzata impostando il flag <xref:System.Windows.FrameworkPropertyMetadataOptions>.  L'ereditarietà della proprietà è utile per uno scenario nel quale elementi padre ed elementi figlio dispongono di una proprietà in comune ed è inoltre utile che quel particolare valore degli elementi figlio sia impostato sullo stesso valore impostato dall'elemento padre.  Una proprietà ereditabile di esempio è <xref:System.Windows.FrameworkElement.DataContext%2A>, utilizzata per fare in modo che le operazioni di associazione attivino l'importante scenario Master\-Details per la presentazione dei dati.  Se si rende ereditabile la proprietà <xref:System.Windows.FrameworkElement.DataContext%2A>, tutti gli elementi figlio ereditano anche quel contesto dati.  A causa dell'ereditarietà del valore della proprietà, è possibile specificare un contesto dati alla radice della pagina o dell'applicazione e non è necessario specificarlo di nuovo per le associazioni in tutti i possibili elementi figlio.  <xref:System.Windows.FrameworkElement.DataContext%2A> rappresenta un ottimo esempio di come l'ereditarietà ignori il valore predefinito ma è sempre possibile impostarlo localmente su qualsiasi elemento figlio; per informazioni dettagliate, vedere [Utilizzare il modello Master\-Details con dati gerarchici](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md).  L'ereditarietà del valore della proprietà può incidere negativamente sulle prestazioni e pertanto deve essere utilizzata sporadicamente; per informazioni dettagliate, vedere [Ereditarietà del valore della proprietà](../../../../docs/framework/wpf/advanced/property-value-inheritance.md).  
  
-   Impostare il flag <xref:System.Windows.FrameworkPropertyMetadataOptions> per indicare se la proprietà di dipendenza deve essere rilevata o utilizzata dai servizi di journaling di navigazione.  Un esempio è rappresentato dalla proprietà <xref:System.Windows.Controls.Primitives.Selector.SelectedIndex%2A>; qualsiasi elemento selezionato in un controllo di selezione deve essere conservato quando si esplora la cronologia del journaling.  
  
<a name="RODP"></a>   
## Proprietà di dipendenza di sola lettura  
 È possibile definire una proprietà di dipendenza di sola lettura.  Tuttavia, gli scenari in base ai quali è possibile definire la proprietà come proprietà di sola lettura sono piuttosto diversi, allo stesso modo della procedura per registrare queste proprietà con il sistema di proprietà e di quella per esporre l'identificatore.  Per ulteriori informazioni, vedere [Proprietà di dipendenza di sola lettura](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md).  
  
<a name="CTDP"></a>   
## Proprietà di dipendenza di tipo raccolta  
 Le proprietà di dipendenza di tipo di raccolta presentano alcuni problemi di implementazione aggiuntivi che è opportuno considerare.  Per informazioni dettagliate, vedere [Proprietà di dipendenza di tipo raccolta](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md).  
  
<a name="SecurityC"></a>   
## Considerazioni sulla sicurezza della proprietà di dipendenza  
 Le proprietà di dipendenza devono essere dichiarate come proprietà pubbliche.  I campi dell'identificatore delle proprietà di dipendenza devono essere dichiarati come campi statici pubblici.  Anche se si tenta di dichiarare altri livelli di accesso \(ad esempio protetto\), è sempre possibile accedere a una proprietà di dipendenza tramite l'identificatore in combinazione con le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] del sistema di proprietà .  In teoria, è possibile persino accedere a un campo dell'identificatore protetto grazie alla segnalazione dei metadati o alle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] per la determinazione del valore che fanno parte del sistema di proprietà, ad esempio <xref:System.Windows.LocalValueEnumerator>.  Per ulteriori informazioni, vedere [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md).  
  
<a name="DPCtor"></a>   
## Proprietà di dipendenza e costruttori di classi  
 Esiste un principio generale nella programmazione del codice gestito \(spesso applicato mediante strumenti di analisi del codice quale FxCop\) in base al quale i costruttori di classi non devono chiamare metodi virtuali.  Il motivo sta nel fatto che i costruttori possono essere chiamati come inizializzazione di base di un costruttore di classe derivato, pertanto l'utilizzo del metodo virtuale tramite il costruttore potrebbe avvenire a uno stato incompleto dell'inizializzazione dell'istanza di oggetto in corso di creazione.  Quando si deriva da una qualsiasi classe che deriva già da <xref:System.Windows.DependencyObject>, è necessario essere consapevoli che il sistema di proprietà stesso chiama ed espone internamente metodi virtuali.  Tali metodi virtuali sono parte dei servizi del sistema di proprietà [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  L'esecuzione dell'override dei metodi consente alle classi derivate di partecipare alla determinazione del valore.  Per evitare eventuali problemi con l'inizializzazione del runtime non è necessario impostare valori della proprietà di dipendenza all'interno dei costruttori di classi, a meno che non si esegua un modello del costruttore molto specifico.  Per informazioni dettagliate, vedere [Modelli di costruttore sicuri per DependencyObject](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md).  
  
## Vedere anche  
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [Metadati della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [Proprietà di dipendenza di tipo raccolta](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)   
 [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md)   
 [Caricamento XAML e proprietà di dipendenza](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)   
 [Modelli di costruttore sicuri per DependencyObject](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)