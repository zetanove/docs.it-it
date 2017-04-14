---
title: "Estensioni di markup e XAML WPF | Microsoft Docs"
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
  - "*Extension (classe)"
  - "Binding (estensioni di markup)"
  - "parentesi graffa (carattere)"
  - "caratteri, parentesi graffa"
  - "classi, MarkupExtension"
  - "parentesi graffe (caratteri) ({})"
  - "DynamicResource (estensioni di markup)"
  - "valori letterali parentesi graffe (caratteri) ({})"
  - "estensioni di markup"
  - "MarkupExtension (classe)"
  - "sintassi nelle estensioni annidate"
  - "RelativeSource (estensioni di markup)"
  - "StaticResource (estensioni di markup)"
  - "TemplateBinding (estensioni di markup)"
  - "XAML, estensioni di markup"
ms.assetid: 618dc745-8b14-4886-833f-486d2254bb78
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Estensioni di markup e XAML WPF
In questo argomento viene introdotto il concetto di estensioni di markup per XAML, incluse le regole di sintassi, lo scopo e il modello a oggetti delle classi sottostante.  Le estensioni di markup rappresentano una funzionalità generale del linguaggio XAML e dell'implementazione .NET di servizi XAML.  Questo argomento fornisce informazioni dettagliate sulle estensioni di markup per l'utilizzo in XAML WPF.  
  
 [!INCLUDE[autoOutline](../Token/autoOutline_md.md)]  
  
<a name="XAML_Processors_and_Markup_Extensions"></a>   
## Processori XAML ed estensioni di markup  
 In termini generali, un parser XAML può interpretare un valore dell'attributo come una stringa letterale che può essere convertita in una primitiva oppure convertire il valore in un oggetto tramite diverse modalità.  Una di queste modalità consiste nel fare riferimento a un convertitore di tipi, come illustrato nell'argomento [TypeConverter e XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md).  Tuttavia, vi sono alcuni scenari in cui è necessario un comportamento diverso.  Ad esempio, è possibile indicare a un processore XAML che un valore di un attributo non deve risultare in un oggetto nuovo nell'oggetto grafico.  Al contrario, l'attributo deve risultare in un oggetto grafico che fa riferimento a un oggetto già costruito in un'altra parte del grafico o a un oggetto statico.  Un altro scenario possibile consiste nell'indicare a un processore XAML l'utilizzo di una sintassi che fornisce argomenti non predefiniti al costruttore di un oggetto. Questi sono i tipi di scenario in cui le estensioni di markup possono rappresentare la soluzione.  
  
<a name="Basic_Markup_Extension_Syntax"></a>   
## Sintassi delle estensioni di markup di base  
 È possibile implementare un'estensione di markup per fornire valori per le proprietà nell'utilizzo di un attributo, per le proprietà nell'utilizzo di un elemento proprietà o in entrambi i casi.  
  
 Quando viene utilizzata per fornire un valore di attributo, la sintassi che distingue una sequenza di estensione di markup in un processore XAML è la presenza delle parentesi graffe di apertura e chiusura \({ e }\).  Il tipo di estensione di markup viene quindi identificato tramite il token di stringa immediatamente successivo alla parentesi graffa di apertura.  
  
 Quando viene utilizzata nella sintassi degli elementi proprietà, un'estensione di markup corrisponde visivamente a qualsiasi altro elemento utilizzato per fornire un valore di elemento proprietà, ovvero una dichiarazione di elementi XAML che fa riferimento alla classe dell'estensione di markup come elemento, racchiuso tra parentesi angolari \(\<\>\).  
  
<a name="XAML_Defined_Markup_Extensions"></a>   
## Estensioni di markup definite da XAML  
 Esistono varie estensioni di markup che non sono specifiche dell'implementazione WPF di XAML, ma che sono invece implementazioni di intrinseci o funzionalità di XAML come linguaggio.  Queste estensioni di markup vengono implementante nell'assembly System.Xaml come parte dei servizi XAML di .NET Framework generali e che rientrano nello spazio dei nomi XAML del linguaggio XAML.  Nell'utilizzo di markup comune, queste estensioni sono in genere identificabili dall'uso del prefisso `x:`.  La classe di base <xref:System.Windows.Markup.MarkupExtension>, definita anche in System.Xaml, fornisce il modello che tutte le estensioni di markup devono utilizzare per il supporto nei lettori XAML e nei writer XAML, XAML WPF incluso.  
  
-   `x:Type` fornisce l'oggetto <xref:System.Type> per il tipo denominato.  Questa funzionalità viene utilizzata più frequentemente in stili e modelli.  Per informazioni dettagliate, vedere [Estensione del markup x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md).  
  
-   `x:Static` produce valori statici.  Questi valori provengono da entità di codice di tipo di valore che non sono direttamente il tipo del valore di una proprietà di destinazione, ma possono essere valutate in base a tale tipo.  Per informazioni dettagliate, vedere [Estensione del markup x:Static](../../../../docs/framework/xaml-services/x-static-markup-extension.md).  
  
-   `x:Null` specifica `null` come valore per una proprietà e può essere utilizzato per gli attributi o per i valori dell'elemento proprietà.  Per informazioni dettagliate, vedere [Estensione del markup x:Null](../../../../docs/framework/xaml-services/x-null-markup-extension.md).  
  
-   `x:Array` offre supporto per la creazione di matrici generali nella sintassi XAML, per i casi in cui si sceglie intenzionalmente di non utilizzare il supporto delle raccolte fornito dagli elementi di base e dai modelli di controllo WPF.  Per informazioni dettagliate, vedere [Estensione del markup x:Array](../../../../docs/framework/xaml-services/x-array-markup-extension.md).  
  
> [!NOTE]
>  Il prefisso `x:` viene utilizzato per il mapping dello spazio dei nomi degli intrinseci del linguaggio XAML, nell'elemento radice di un file o produzione XAML.  Ad esempio nei modelli di [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] per le applicazioni WPF, un file XAML viene avviato tramite il mapping `x:`.  Nel mapping dello spazio dei nomi XAML personalizzato è possibile scegliere un token di prefisso diverso. Tuttavia per identificare le entità che rappresentano una parte definita dello spazio dei nomi XAML per il linguaggio XAML, in questa documentazione viene utilizzato il mapping `x:` predefinito anziché lo spazio dei nomi predefinito WPF o altri spazi dei nomi XAML non correlati a un framework specifico.  
  
<a name="WPF_Specific_Markup_Extensions"></a>   
## Estensioni di markup specifiche di WPF  
 Le estensioni di markup più comuni utilizzate nella programmazione WPF sono quelle che supportano riferimenti alle risorse \(`StaticResource` e `DynamicResource`\) e quelle che supportano l'associazione dati \(`Binding`\).  
  
-   `StaticResource` fornisce un valore per una proprietà sostituendo il valore di una risorsa già definita.  Una valutazione `StaticResource` viene effettuata al momento del caricamento di XAML e non dispone di accesso all'oggetto grafico in fase di esecuzione. Per informazioni dettagliate, vedere [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md).  
  
-   `DynamicResource` fornisce un valore per una proprietà rinviando tale valore come riferimento in fase di esecuzione a una risorsa.  Un riferimento di risorsa dinamica forza una nuova ricerca ogni volta che viene eseguito l'accesso a tale risorsa e che questa ha accesso all'oggetto grafico in fase di esecuzione.  Per ottenere l'accesso, il concetto `DynamicResource` è supportato da proprietà di dipendenza nel sistema di proprietà WPF e dalle espressioni valutate.  Di conseguenza è possibile utilizzare solo `DynamicResource` per una destinazione della proprietà di dipendenza.  Per informazioni dettagliate, vedere [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md).  
  
-   `Binding` fornisce un valore associato a dati per una proprietà, utilizzando il contesto dati che si applica all'oggetto padre in fase di esecuzione.  Questa estensione di markup è relativamente complessa, poiché abilita una sintassi inline sostanziale per la specifica di un'associazione dati.  Per informazioni dettagliate, vedere [Associazione dell'estensione di markup](../../../../docs/framework/wpf/advanced/binding-markup-extension.md).  
  
-   `RelativeSource` fornisce informazioni di origine per un oggetto <xref:System.Windows.Data.Binding> che può passare tra diverse relazioni possibili nella struttura ad albero di oggetti in fase di esecuzione.  Vengono in tal modo fornite origini specializzate per le associazioni create nei modelli multiuso o nel codice senza una conoscenza approfondita della struttura ad albero di oggetti circostante.  Per informazioni dettagliate, vedere [Estensione del markup RelativeSource](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md).  
  
-   Con `TemplateBinding`, un modello di controllo può utilizzare valori per proprietà basate su modelli che provengono da proprietà definite sul modello a oggetti della classe che utilizzerà il modello.  In altri termini, la proprietà all'interno della definizione del modello può accedere a un contesto che esiste solo una volta il modello applicato.  Per informazioni dettagliate, vedere [Estensione del markup TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md).  Per ulteriori informazioni sull'utilizzo pratico di `TemplateBinding`, vedere [Esempio di applicazione di stili con ControlTemplate](http://go.microsoft.com/fwlink/?LinkID=160041) \(la pagina potrebbe essere in inglese\).  
  
-   `ColorConvertedBitmap` supporta uno scenario di gestione immagini relativamente avanzato.  Per informazioni dettagliate, vedere [Estensione del markup ColorConvertedBitmap](../../../../docs/framework/wpf/advanced/colorconvertedbitmap-markup-extension.md).  
  
-   `ComponentResourceKey` e `ThemeDictionary` supportano aspetti di ricerca delle risorse, in particolare per risorse e temi inclusi con i controlli personalizzati.  Per ulteriori informazioni, vedere [Estensione del markup ComponentResourceKey](../../../../docs/framework/wpf/advanced/componentresourcekey-markup-extension.md), [Estensione del markup ThemeDictionary](../../../../docs/framework/wpf/advanced/themedictionary-markup-extension.md) o [Cenni preliminari sulla modifica di controlli](../../../../docs/framework/wpf/controls/control-authoring-overview.md).  
  
<a name="StarExtension"></a>   
## \*Classi di estensione  
 Sia per le estensioni del linguaggio XAML generale che per le estensioni di markup specifiche di WPF, il comportamento di ogni estensione di markup viene identificato in un processore XAML tramite una classe `*Extension` che deriva da <xref:System.Windows.Markup.MarkupExtension> e che fornisce un'implementazione del metodo <xref:System.Windows.Markup.StaticExtension.ProvideValue%2A>.  Questo metodo fornisce su ogni estensione l'oggetto che viene restituito quando viene valutata l'estensione di markup.  In genere, viene l'oggetto viene valutato in base ai vari token di stringa passati all'estensione di markup.  
  
 Ad esempio, la classe <xref:System.Windows.StaticResourceExtension> fornisce l'implementazione di superficie della ricerca effettiva di risorse in modo che l'implementazione <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> restituisca l'oggetto richiesto, con l'input di tale implementazione costituito da una stringa utilizzata per cercare la risorsa in base al proprio `x:Key`.  Molti dettagli di questa implementazione non sono importanti se si utilizza un'estensione di markup esistente.  
  
 Alcune estensioni di markup non utilizzano argomenti del token di stringa.  Ciò è dovuto al fatto che restituiscono un valore statico o coerente o che il contesto per il valore da restituire è disponibile tramite uno dei servizi passati tramite il parametro `serviceProvider`.  
  
 Il modello di denominazione `*Extension` viene utilizzato per praticità e coerenza.  Non è necessario affinché un processore XAML identifichi quella classe come supporto per un'estensione di markup.  Se il codebase include System.Xaml e utilizza le implementazioni dei servizi XAML di .NET Framework, ai fini del riconoscimento come estensione di markup XAML sono necessari solo la derivazione da <xref:System.Windows.Markup.MarkupExtension> e il supporto di una sintassi di costruzione.  WPF definisce classi che consentono l'estensione di markup e che non seguono il modello di denominazione `*Extension`, ad esempio <xref:System.Windows.Data.Binding>.  In genere il motivo di questo consiste nel fatto che la classe supporta scenari oltre il puro supporto di estensioni di markup.  Nel caso di <xref:System.Windows.Data.Binding>, tale classe supporta l'accesso in fase di esecuzione ai metodi e alle proprietà dell'oggetto per gli scenari che hanno nulla a che fare con XAML.  
  
### Interpretazione di testo di inizializzazione nelle classi di estensione  
 I token di stringa che seguono il nome dell'estensione di markup e si trovano all'interno delle parentesi graffe sono interpretati da un processore XAML in uno dei modi seguenti:  
  
-   Una virgola rappresenta sempre il separatore o il delimitatore di token singoli.  
  
-   Se i singoli token separati non contengono segni di uguale, ogni token viene trattato come un argomento del costruttore.  Ogni parametro del costruttore deve essere fornito come il tipo previsto dalla firma e nell'ordine corretto previsto dalla firma.  
  
    > [!NOTE]
    >  Un processore XAML deve chiamare il costruttore che corrisponde al conteggio di argomenti del numero di coppie.  Per questo motivo, se si implementa un'estensione di markup personalizzata, non fornire più parametri con lo stesso conteggio di argomenti.  Il comportamento di un processore XALM per i casi in cui sono presenti più percorsi di costruttori dell'estensione di markup con lo stesso conteggio di parametri non è definito ma è opportuno prevedere che un processore XAML può generare un'eccezione sull'utilizzo se questa situazione è presente nelle definizioni del tipo di estensione di markup.  
  
-   Se i singoli token separati contengono segni di uguale, un processore XAML chiama innanzitutto il costruttore predefinito per l'estensione di markup.  Quindi, ogni coppia nome\=valore viene interpretata come nome di proprietà presente nell'estensione di markup e come valore da assegnare a tale proprietà.  
  
-   Se in un'estensione di markup è presente un risultato parallelo tra il comportamento del costruttore e il comportamento dell'impostazione delle proprietà, il comportamento utilizzato è ininfluente.  È più comune utilizzare coppie *proprietà*`=`*valore* per estensioni di markup che presentano più proprietà impostabili, anche perché con questa soluzione il markup è più intenzionale ed è meno probabile che si traspongano accidentalmente parametri del costruttore.  Quando si specificano coppie proprietà\=valore, tali proprietà possono essere in qualsiasi ordine. Inoltre, non vi è garanzia che un'estensione di markup fornisca un parametro del costruttore che imposti ciascuna delle proprietà impostabili.  Ad esempio, <xref:System.Windows.Data.Binding> è un'estensione di markup, con molte proprietà impostabili tramite l'estensione nel formato *proprietà*`=`*valore*, ma <xref:System.Windows.Data.Binding> supporta solo due costruttori: un costruttore predefinito e uno che imposta un percorso iniziale.  
  
-   Non è possibile passare una virgola letterale a un'estensione di markup senza sequenza di escape.  
  
<a name="EscapeSequences"></a>   
## Sequenza di escape ed estensioni di markup  
 Nella gestione degli attributi in un processore XAML vengono utilizzate le parentesi graffe come indicatori di una sequenza di estensione del markup.  Se necessario, è anche possibile produrre un valore di attributo letterale per i caratteri di parentesi graffe, immettendo una sequenza di escape tramite una coppia di parentesi graffe vuota seguita dalla parentesi graffa letterale.  Vedere [Sequenza di escape\/Estensione di markup {}](../../../../docs/framework/xaml-services/escape-sequence-markup-extension.md).  
  
<a name="Nesting"></a>   
## Annidamento di estensioni di markup nell'utilizzo di XAML  
 L'annidamento di più estensioni di markup è supportato. Ogni estensione di markup viene innanzitutto valutata al livello più profondo.  Si consideri ad esempio il seguente utilizzo:  
  
```  
<Setter Property="Background"  
  Value="{DynamicResource {x:Static SystemColors.ControlBrushKey}}" />  
  
```  
  
 In questo utilizzo, l'istruzione `x:Static` viene valutata per prima e restituisce una stringa.  Tale stringa viene quindi utilizzata come argomento per `DynamicResource`.  
  
## Estensioni di markup e sintassi degli elementi delle proprietà  
 Se una classe di estensione di markup viene utilizzata come elemento oggetto che riempie il valore di un elemento proprietà, non è possibile distinguerla a livello visivo da un elemento oggetto comune supportato dal tipo che può essere utilizzato in XAML.  La differenza pratica tra un elemento oggetto comune e un'estensione di markup è che l'estensione di markup viene valutata a un valore tipizzato o viene rinviata come espressione.  Di conseguenza i meccanismi per tutti gli errori di tipo possibili dei valori di proprietà per l'estensione di markup saranno diversi, analogamente a come una proprietà ad associazione tardiva viene trattata in altri modelli di programmazione.  Un elemento oggetto comune verrà valutato per il tipo rispetto alla proprietà di destinazione che imposta quando il codice XAML viene analizzato.  
  
 La maggior parte delle estensioni di markup, se utilizzate nella sintassi di elementi oggetto per riempire un elemento proprietà, non avrà contenuto o altra sintassi degli elementi proprietà all'interno.  Ciò consente di chiudere il tag dell'elemento oggetto senza fornire elementi figlio.  Ogni volta che viene rilevato un elemento oggetto da un processore XAML, il costruttore per tale classe viene chiamato, creando un'istanza dell'oggetto creato dall'elemento analizzato.  Una classe di estensione di markup non è diversa: se si desidera che l'estensione di markup sia utilizzabile nella sintassi degli elementi oggetto, è necessario fornire un costruttore predefinito.  Alcune estensioni di markup esistenti hanno almeno un valore di proprietà obbligatorio che è necessario specificare per un'inizializzazione efficace.  In tal caso, il valore di tale proprietà viene generalmente fornito come attributo di proprietà sull'elemento oggetto.  Nelle pagine di riferimento su [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md) e [Estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md) sono indicate le estensioni di markup che presentano proprietà obbligatorie, con i nomi di tali proprietà.  Nelle pagine di riferimento viene inoltre indicato se la sintassi degli elementi oggetto o la sintassi degli attributi non è consentita per determinate estensioni di markup.  Un caso da tenere presente è [Estensione del markup x:Array](../../../../docs/framework/xaml-services/x-array-markup-extension.md), che non può supportare la sintassi degli attributi poiché è necessario specificare il contenuto di tale matrice all'interno della codifica come contenuto.  Il contenuto delle matrici è gestito come oggetto generico, pertanto non è possibile applicare alcun convertitore di tipi predefinito per l'attributo.  Inoltre, [Estensione del markup x:Array](../../../../docs/framework/xaml-services/x-array-markup-extension.md) richiede un parametro `type`.  
  
## Vedere anche  
 [Cenni preliminari su XAML \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [Estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [Estensione del markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)   
 [Associazione dell'estensione di markup](../../../../docs/framework/wpf/advanced/binding-markup-extension.md)   
 [Estensione del markup DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)   
 [Estensione del markup x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md)