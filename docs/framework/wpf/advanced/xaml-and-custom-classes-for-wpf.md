---
title: "Classi XAML e personalizzate per WPF | Microsoft Docs"
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
  - "classi, classi personalizzate in XAML"
  - "classi personalizzate in XAML"
  - "XAML, classi personalizzate"
ms.assetid: e7313137-581e-4a64-8453-d44e15a6164a
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# Classi XAML e personalizzate per WPF
XAML implementato in [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] i framework supporta la possibilità di definire una classe o una struttura personalizzata in qualsiasi  [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] linguaggio e quindi accesso a tale classe utilizzando il markup XAML.  È possibile utilizzare una combinazione di tipi definiti da [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] e di tipi personalizzati all'interno dello stesso file di markup, in genere mediante l'esecuzione del mapping dei tipi personalizzati a un prefisso degli spazi dei nomi XAML.  In questo argomento vengono descritti i requisiti che una classe personalizzata deve soddisfare per essere utilizzata come elemento XAML.  
  
   
  
<a name="Custom_Classes_in_Applications_vs__in_Assemblies"></a>   
## Classi personalizzate in applicazioni o assembly  
 Le classi personalizzate utilizzate in XAML possono essere definite in due modi distinti: all'interno del code\-behind o di un altro codice che genera il principale [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] applicazione, oppure come classe in un assembly separato, come un file eseguibile o una DLL utilizzato come libreria di classi.  Ognuno di questi approcci presenta vantaggi e svantaggi particolari.  
  
-   Il vantaggio della creazione di una libreria di classi consiste nella possibilità di condividere una qualsiasi di queste classi personalizzate tra un gran numero di applicazioni diverse.  Una libreria separata rende inoltre dei problemi di controllo delle versioni delle applicazioni più facili controllare e semplifica la creazione di una classe in cui l'utilizzo previsto della classe è come elemento radice in una pagina XAML.  
  
-   Il vantaggio della definizione di classi personalizzate nell'applicazione consiste nel fatto che si tratta di una tecnica relativamente semplice, che riduce al minimo i problemi di distribuzione e di test che si riscontrano quando si introducono assembly separati oltre al file eseguibile dell'applicazione principale.  
  
-   Se definite nello stesso assembly o in un assembly diverso, le classi personalizzate è necessario eseguire il mapping tra lo spazio dei nomi CLR e lo spazio dei nomi XML per essere utilizzata in XAML come elementi.  Vedere [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
<a name="Requirements_for_a_Custom_Class_as_a_XAML_Element"></a>   
## Requisiti per una classe personalizzata come elemento XAML  
 Affinché sia possibile crearne un'istanza come elemento oggetto, la classe deve soddisfare i seguenti requisiti:  
  
-   La classe personalizzata deve essere pubblica e deve supportare un costruttore pubblico predefinito \(senza parametri\).  Per le note riguardanti le strutture, vedere la sezione seguente.  
  
-   La classe personalizzata non deve essere una classe annidata.  Le classi annidate e il punto presente nella relativa sintassi di utilizzo generale di CLR interferiscono con altre funzionalità di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e\/o XAML, ad esempio le proprietà collegate.  
  
 Oltre ad abilitare la sintassi degli elementi oggetto, la definizione dell'oggetto abilita la sintassi degli elementi proprietà per tutte le altre proprietà pubbliche che accettano tale oggetto come tipo di valore.  Ciò è dovuto al fatto che non è possibile creare un'istanza dell'oggetto come elemento oggetto e quindi inserire il valore di elemento proprietà di tale proprietà.  
  
### Strutture  
 Le strutture definite come tipi personalizzati possono sempre essere costruite in XAML in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] . Ciò è dovuto  [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] i compilatori creano in modo implicito un costruttore predefinito per una struttura che inizializza tutti i valori delle proprietà alle impostazioni predefinite.  In alcuni casi, il comportamento predefinito della costruzione e\/o utilizzo dell'elemento oggetto per una struttura non è appropriato.  Il motivo può essere che la struttura è prevista per inserire valori e funzioni concettualmente come unione i cui valori potrebbero disporre di interpretazioni che si escludono reciprocamente, pertanto nessuna delle proprietà è impostabile.  Un esempio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] di tale struttura è <xref:System.Windows.GridLength>.  Tali strutture devono in genere implementare un convertitore di tipi in modo che sia possibile esprimere i valori in forma di attributo, utilizzando convenzioni di stringa che creano interpretazioni o modalità diverse dei valori della struttura.  La struttura deve inoltre esporre un comportamento simile per la costruzione del codice tramite un costruttore non predefinito.  
  
<a name="Requirements_for_Properties_of_a_Custom_Class_as_XAML"></a>   
## Requisiti per proprietà di una classe personalizzata come attributi XAML  
 Le proprietà devono fare riferimento a un tipo per valore \(ad esempio una primitiva\) oppure utilizzare una classe per il tipo che sia un costruttore predefinito o un convertitore di tipi al quale può accedere un processore XAML.  Nell'implementazione XAML di CLR i processori XAML individuano tali convertitori tramite il supporto nativo per le primitive di linguaggio o tramite applicazione di <xref:System.ComponentModel.TypeConverterAttribute> a un tipo o un membro nelle definizioni del tipo di supporto.  
  
 In alternativa, la proprietà può fare riferimento a un tipo di classe astratta oppure a un'interfaccia.  Per le classi astratte o le interfacce, l'aspettativa per l'analisi XAML è che il valore della proprietà sia compilato con istanze della classe pratica che implementano l'interfaccia oppure con istanze di tipi che derivano dalla classe astratta.  
  
 Le proprietà possono essere dichiarate su una classe astratta, ma possono essere impostate solo su classi pratiche che derivano dalla classe astratta.  Questo perché la creazione dell'elemento oggetto per la classe richiede sempre un costruttore predefinito pubblico sulla classe.  
  
### Sintassi per attributi abilitata per TypeConverter  
 Se si fornisce un convertitore dei tipi dedicato con attribuiti a livello di classe, la conversione dei tipi applicata abilita la sintassi per attributi per qualsiasi proprietà per la quale è necessario creare un'istanza di quel tipo.  Un convertitore dei tipi non consente l'utilizzo dell'elemento oggetto del tipo; solo la presenza di un costruttore predefinito per quel tipo consente l'utilizzo dell'elemento oggetto.  Pertanto, le proprietà che sono abilitate dal convertitore dei tipi in genere non possono essere utilizzate nella sintassi per proprietà, a meno che il tipo stesso non supporti anche la sintassi per elementi oggetto.  L'eccezione è costituita dalla possibilità di specificare una sintassi per elementi proprietà, ma dalla necessità che l'elemento proprietà contenga una stringa.  Tale utilizzo in realtà è essenzialmente equivalente all'utilizzo di una sintassi per attributi e non è comune a meno che non sia necessaria una gestione degli spazi vuoti più affidabile del valore dell'attributo.  L'utilizzo dell'elemento proprietà riportato di seguito, ad esempio, accetta una stringa e l'equivalente dell'utilizzo dell'attributo:  
  
 [!code-xml[XamlOvwSupport#GoofyTCPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe)]  
  
 [!code-xml[XamlOvwSupport#GoofyTCPE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe2)]  
  
 Esempi di proprietà in cui la sintassi degli attributi ma non è consentita la sintassi per elementi proprietà che contiene un elemento oggetto viene impedito a XAML sono diverse proprietà che accettano <xref:System.Windows.Input.Cursor> tipo.  La classe <xref:System.Windows.Input.Cursor> contiene un convertitore dei tipi dedicato <xref:System.Windows.Input.CursorConverter>, ma non espone un costruttore predefinito, pertanto la proprietà <xref:System.Windows.FrameworkElement.Cursor%2A> può essere impostata solo tramite la sintassi per attributi anche se il tipo <xref:System.Windows.Input.Cursor> effettivo è un tipo di riferimento.  
  
### Convertitori dei tipi per proprietà  
 In alternativa, la proprietà stessa può dichiarare un convertitore dei tipi a livello della proprietà.  In tal modo viene abilitato un "minilinguaggio" che crea un'istanza di oggetti del tipo della proprietà inline, elaborando i valori di stringa in ingresso dell'attributo come input per un'operazione <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> basata sul tipo appropriato.  In genere questa operazione viene eseguita per fornire una funzione di accesso pratica e non implementa solo per consentire l'impostazione di una proprietà in XAML.  Tuttavia, è anche possibile utilizzare convertitori dei tipi per gli attributi nei quali si desidera utilizzare tipi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] esistenti che non forniscono un costruttore predefinito o un convertitore dei tipi con attributi.  Esempi da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] L'API è determinate proprietà che accettano  <xref:System.Globalization.CultureInfo> tipo.  in questo caso, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza l'esistenza [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] <xref:System.Globalization.CultureInfo> tipo per aggiornare gli scenari di compatibilità e migrazione di indirizzi utilizzati nelle versioni precedenti dei framework, ma  <xref:System.Globalization.CultureInfo> il tipo non supportava i costruttori necessari o della conversione di tipi a livello di tipo per poter essere utilizzato come valore della proprietà XAML.  
  
 Ogni volta che si espone una proprietà che presenta un utilizzo XAML, in particolare se si è un autore di controlli, è necessario considerare l'eventualità di supportare tale proprietà con una proprietà di dipendenza.  Questo è particolarmente vero se si utilizza l'esistenza [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] implementazione del processore XAML, perché è possibile migliorare le prestazioni utilizzando  <xref:System.Windows.DependencyProperty> supporto.  Una proprietà di dipendenza esporrà funzionalità del sistema di proprietà per la proprietà prevista dagli utenti come proprietà accessibile XAML.  Tale proprietà include funzionalità quali l'animazione, l'associazione dati e il supporto degli stili.  Per ulteriori informazioni, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) e [Caricamento XAML e proprietà di dipendenza](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md).  
  
### Scrittura e associazione di attributi a un convertitore dei tipi  
 Talvolta può essere necessario scrivere una classe derivata <xref:System.ComponentModel.TypeConverter> personalizzata per fornire la conversione di tipi per il tipo della proprietà utilizzato.  Per istruzioni sulle modalità di derivazione e di creazione di un convertitore dei tipi in grado di supportare gli utilizzi XAML e sulle modalità di applicazione di <xref:System.ComponentModel.TypeConverterAttribute>, vedere [TypeConverter e XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md).  
  
<a name="Requirements_for_Events_of_a_Custom_Class_as_XAML"></a>   
## Requisiti per la sintassi per attributi del gestore eventi XAML negli eventi di una classe personalizzata  
 Per poter essere utilizzato come evento [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], l'evento deve essere esposto come evento pubblico in una classe che supporta un costruttore predefinito oppure in una classe astratta in cui è possibile accedere all'evento nelle classi derivate.  Per essere utilizzato in modo appropriato come [evento indirizzato](GTMT), l'evento [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] deve implementare i metodi espliciti `add` e `remove`, che aggiungono e rimuovono gestori per la firma dell'evento [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e inoltrare quei gestori ai metodi <xref:System.Windows.UIElement.AddHandler%2A> e <xref:System.Windows.UIElement.RemoveHandler%2A>.  Questi metodi aggiungono o rimuovono i gestori per l'archivio del gestore eventi indirizzati nell'istanza alla quale è associato l'evento.  
  
> [!NOTE]
>  È possibile registrare direttamente i gestori per gli eventi indirizzati utilizzando <xref:System.Windows.UIElement.AddHandler%2A> e non definire intenzionalmente un evento [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] che espone l'evento indirizzato [](GTMT).  Questa operazione non è in genere consigliabile poiché l'evento non abiliterà la sintassi degli attributi XAML per collegare i gestori e la classe risultante offrirà una visualizzazione XAML meno trasparente delle funzionalità di tale tipo.  
  
<a name="Collection_Properties"></a>   
## Scrittura di proprietà di raccolta  
 Le proprietà che accettano un tipo di raccolta presentano una sintassi XAML che consente di specificare gli oggetti che vengono aggiunti alla raccolta.  Questa sintassi presenta due funzionalità rilevanti.  
  
-   L'oggetto che rappresenta l'oggetto raccolta non deve essere specificato nella sintassi per elementi oggetto.  La presenza di quel tipo di raccolta è implicita ogni volta che in XAML si specifica una proprietà che accetta un tipo di raccolta.  
  
-   Gli elementi figlio della proprietà della raccolta nel markup vengono elaborati per diventare membri della raccolta.  L'accesso del codice ai membri di una raccolta viene di norma eseguito tramite metodi di elenco\/dizionario, ad esempio `Add` oppure tramite un indicizzatore.  Ma la sintassi XAML non supporta i metodi o indicizzatori \(eccezione: XAML 2009 supporti i metodi, ma utilizzo di XAML 2009 limita gli utilizzi possibili di WPF; vedere [Funzionalità del linguaggio XAML 2009](../../../../docs/framework/xaml-services/xaml-2009-language-features.md)\).  Dal momento che le raccolte sono un requisito molto comune per la compilazione di una struttura ad albero di elementi, sono necessari alcuni modi per popolarli nella sintassi XAML dichiarativa.  Pertanto, gli elementi figlio di una proprietà della raccolta vengono elaborati aggiungendoli alla raccolta che rappresenta il valore del tipo di proprietà della raccolta.  
  
 Servizi XAML di.NET Framework l'implementazione e il processore XAML WPF utilizzano la definizione seguente relativamente agli elementi che costituiscono una proprietà collection.  Il tipo di proprietà della proprietà deve implementare uno dei seguenti elementi:  
  
-   Implementa <xref:System.Collections.IList>.  
  
-   Implementa <xref:System.Collections.IDictionary> o l'equivalente generico \(<xref:System.Collections.Generic.IDictionary%602>\).  
  
-   deriva da <xref:System.Array> \(per ulteriori informazioni sulle matrici in XAML, vedere  [Estensione del markup x:Array](../../../../docs/framework/xaml-services/x-array-markup-extension.md)\).  
  
-   Implementa <xref:System.Windows.Markup.IAddChild> \(un'interfaccia definita da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]\).  
  
 Ognuno di questi tipi in CLR dispone `Add` metodo, utilizzato dal processore XAML per aggiungere elementi alla raccolta sottostante durante la creazione dell'oggetto grafico.  
  
> [!NOTE]
>  L'oggetto generico `List` e  `Dictionary` interfacce \(<xref:System.Collections.Generic.IList%601> e  <xref:System.Collections.Generic.IDictionary%602>\) non essere supportato per il rilevamento della raccolta da  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Processore XAML.  Tuttavia, è possibile utilizzare la classe <xref:System.Collections.Generic.List%601> come classe di base, poiché implementa direttamente <xref:System.Collections.IList> oppure <xref:System.Collections.Generic.Dictionary%602> come classe di base, poiché implementa direttamente <xref:System.Collections.IDictionary>.  
  
 Quando si dichiara una proprietà che accetta una raccolta, prestare attenzione alle modalità con cui quel valore di proprietà viene inizializzato nelle nuove istanze del tipo.  Se non si sta implementando la proprietà come proprietà di dipendenza, è opportuno fare in modo che la proprietà utilizzi un campo di backup che chiama il costruttore del tipo di raccolta.  Se la proprietà è una proprietà di dipendenza, potrebbe essere necessario inizializzare proprietà della raccolta come parte del costruttore del tipo predefinito.  Questo dipende dal fatto che una proprietà di dipendenza accetta il relativo valore predefinito dai metadati e in genere non si desidera che il valore iniziale di una proprietà della raccolta sia una raccolta statica condivisa.  È necessario che esista un'istanza di raccolta per ogni istanza del tipo contenitore.  Per ulteriori informazioni, vedere [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md).  
  
 È possibile implementare un tipo di raccolta personalizzato per la proprietà della raccolta.  A causa della gestione della proprietà della raccolta implicita, il tipo di raccolta personalizzata non deve necessariamente fornire un costruttore predefinito per essere utilizzato implicitamente in XAML .  Tuttavia, se si desidera, è possibile fornire un costruttore predefinito per il tipo di raccolta.  Questa operazione può risultare utile.  A meno che se non si fornisca un costruttore predefinito, non è possibile dichiarare in modo esplicito la raccolta come elemento oggetto.  È possibile che alcuni autori di markup preferiscano considerare la raccolta esplicita una questione di stile del markup.  Inoltre, un costruttore predefinito può semplificare i requisiti dell'inizializzazione quando si creano nuovi oggetti che utilizzano il tipo di raccolta come valore della proprietà.  
  
<a name="XAMLCONtent"></a>   
## Dichiarazione delle proprietà di contenuto XAML  
 Il linguaggio XAML definisce il concetto di un oggetto [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] proprietà di contenuto.  Ogni classe che è possibile utilizzare nella sintassi per oggetti può disporre esattamente di una proprietà di contenuto XAML.  Per dichiarare una proprietà in modo che sia la proprietà di contenuto XAML per la classe, applicare l'oggetto <xref:System.Windows.Markup.ContentPropertyAttribute> come parte della definizione della classe.  Specificare il nome della proprietà di contenuto XAML desiderata come <xref:System.Windows.Markup.ContentPropertyAttribute.Name%2A> nell'attributo.  La proprietà viene specificata come stringa per nome, non come costrutto di reflection come<xref:System.Reflection.PropertyInfo>.  
  
 È possibile specificare una proprietà della raccolta in modo che sia la proprietà di contenuto XAML.  Tale operazione genera un utilizzo di quella proprietà in base al quale l'elemento oggetto può disporre di uno o più elementi figlio senza che si frappongano elementi oggetto di raccolta o tag di elementi proprietà.  Questi elementi vengono quindi trattati come valore per la proprietà di contenuto XAML e aggiunti all'istanza della raccolta di supporto.  
  
 Alcune proprietà di contenuto esistenti XAML utilizzando il tipo di proprietà `oggetto`.  In questo modo viene abilitata una proprietà di contenuto XAML in grado di accettare valori primitivi, quali un oggetto <xref:System.String>, nonché di accettare un valore di oggetto con riferimento singolo.  Se si segue questo modello, il tipo utilizzato è responsabile della determinazione del tipo oltre che della gestione dei tipi possibili.  Lo scopo più comune per un tipo di contenuto <xref:System.Object> è quella di supportare sia un'aggiunta semplice di contenuto oggetto come stringa \(che riceve un trattamento di presentazione predefinito\), sia un'aggiunta di contenuto oggetto avanzata, che specifica una presentazione non predefinita o dati aggiuntivi.  
  
<a name="Serializing"></a>   
## Serializzazione di XAML  
 Per determinati scenari, ad esempio se si è un autore di controlli, è possibile che si desideri assicurare che qualsiasi rappresentazione dell'oggetto che è possibile creare un'istanza in XAML possa essere serializzata nel markup XAML equivalente.  I requisiti della serializzazione non sono descritti in questo argomento.  Vedere le proprietà [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md) e [Struttura ad albero e serializzazione degli elementi](../../../../docs/framework/wpf/advanced/element-tree-and-serialization.md).  
  
## Vedere anche  
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Proprietà Dependency personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [Cenni preliminari sugli elementi di base](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [Caricamento XAML e proprietà di dipendenza](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)