---
title: "Markup Extensions for XAML Overview | Microsoft Docs"
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
  - "markup extensions [XAML Services], custom"
  - "XAML [XAML Services], markup extensions"
ms.assetid: 261b2b11-2dc0-462f-8c66-55b8c9c6e436
caps.latest.revision: 14
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 14
---
# Markup Extensions for XAML Overview
Le estensioni di markup sono una tecnica XAML per ottenere un valore che non è una primitiva né un tipo XAML specifico. Per utilizzo dell'attributo, le estensioni di markup usano la sequenza di caratteri nota costituita da una parentesi graffa aperta `{` per l'immissione dell'ambito dell'estensione di markup e da una parentesi graffa chiusa `}`. Quando si usano i servizi XAML di .NET Framework, si possono usare alcune delle estensioni di markup predefinite del linguaggio XAML contenute nell'assembly System.Xaml.  inoltre possibile creare una sottoclasse dalla classe <xref:System.Windows.Markup.MarkupExtension>, definita in System.Xaml, e definire estensioni di markup personalizzate. In alternativa, è possibile usare le estensioni di markup definite da un particolare framework se già si fa riferimento a tale framework.  
  
 Quando viene eseguito l'accesso a un utilizzo dell'estensione di markup, il writer di oggetti XAML può fornire servizi a una classe <xref:System.Windows.Markup.MarkupExtension> personalizzata tramite un punto di connessione del servizio nell'override del metodo <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A?displayProperty=fullName>. I servizi possono essere usati per ottenere il contesto relativo all'utilizzo, funzionalità specifiche del writer di oggetti, il contesto dello schema XAML e così via.  
  
<a name="XAML_Defined_Markup_Extensions"></a>   
## Estensioni di markup definite da XAML  
 Diverse estensioni di markup vengono implementate dai servizi XAML di .NET Framework per il supporto del linguaggio XAML. Le estensioni di markup corrispondono a parti della specifica di XAML come linguaggio. In genere, queste estensioni sono identificabili dal prefisso `x:` nella sintassi come illustrato nell'utilizzo comune. Le implementazioni dei servizi XAML di .NET Framework per questi elementi del linguaggio XAML derivano tutte dalla classe base <xref:System.Windows.Markup.MarkupExtension>.  
  
> [!NOTE]
>  Il prefisso `x:` viene usato per il mapping dello spazio dei nomi XAML tipico dello spazio dei nomi del linguaggio XAML, nell'elemento radice di una produzione XAML. Ad esempio, nei modelli di progetto e pagina di [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] per diversi framework specifici, avviare un file XAML usando il mapping `x:`. Nel mapping dello spazio dei nomi XAML personalizzato è possibile scegliere un token di prefisso diverso. Tuttavia, per identificare le entità che rappresentano una parte definita dello spazio dei nomi XAML del linguaggio XAML, in questa documentazione viene usato il mapping `x:` predefinito anziché lo spazio dei nomi XAML predefinito di un framework specifico o altri spazi dei nomi CLR o XML arbitrari.  
  
### x:Type  
 `x:Type` fornisce l'oggetto <xref:System.Type> per il tipo denominato. Questa funzionalità viene il più delle volte usata nei meccanismi di rinvio che usano il tipo CLR sottostante e la derivazione del tipo come moniker o identificatore di raggruppamento. Gli stili e i modelli WPF, nonché il loro utilizzo delle proprietà `TargetType`, sono un esempio specifico. Per altre informazioni, vedere [x:Type Markup Extension](../../../docs/framework/xaml-services/x-type-markup-extension.md).  
  
### x:Static  
 `x:Static` produce valori statici da entità di codice di tipo di valore che non sono direttamente il tipo del valore di una proprietà, ma possono essere valutate in base a tale tipo. Questo è utile per specificare valori già esistenti come costanti note in una definizione del tipo. Per altre informazioni, vedere [x:Static Markup Extension](../../../docs/framework/xaml-services/x-static-markup-extension.md).  
  
### x:Null  
 `x:Null` specifica `null` come valore per un membro XAML. In base alla progettazione di tipi specifici o a concetti di framework più ampi, non sempre `null` è un valore predefinito di una proprietà o il valore implicito dell'attributo di una stringa vuota. Per altre informazioni, vedere [x:Null Markup Extension](../../../docs/framework/xaml-services/x-null-markup-extension.md).  
  
### x:Array  
 `x:Array` supporta la creazione di matrici generali nella sintassi XAML nei casi in cui si sceglie intenzionalmente di non usare il supporto delle raccolte fornito dagli elementi di base e dai modelli di controllo. Per altre informazioni, vedere [x:Array Markup Extension](../../../docs/framework/xaml-services/x-array-markup-extension.md). Nel caso specifico di XAML 2009, l'accesso alle matrici avviene come primitive di linguaggio anziché come un'estensione. Per altre informazioni, vedere [XAML 2009 Language Features](../../../docs/framework/xaml-services/xaml-2009-language-features.md).  
  
### x:Reference  
 `x:Reference` fa parte di XAML 2009, un'estensione del set del linguaggio originale \(2006\).`x:Reference` rappresenta un riferimento a un altro oggetto esistente in un oggetto grafico. Questo oggetto viene definito dal relativo attributo `x:Name`. Per altre informazioni, vedere [x:Reference Markup Extension](../../../docs/framework/xaml-services/x-reference-markup-extension.md).  
  
### Altri costrutti x:  
 Esistono altri costrutti `x:` che supportano le funzionalità del linguaggio XAML, che però non sono implementati come estensioni di markup. Per altre informazioni, vedere [XAML Namespace \(x:\) Language Features](../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md).  
  
<a name="the_markupextension_base_class"></a>   
## Classe base MarkupExtension  
 Per definire un'estensione di markup personalizzata che possa interagire con le implementazioni predefinite di reader XAML e writer XAML in System.Xaml, è possibile derivare una classe dalla classe <xref:System.Windows.Markup.MarkupExtension> astratta. Questa classe ha di un unico metodo di cui eseguire l'override, ovvero <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>. Potrebbe anche essere necessario definire costruttori aggiuntivi per il supporto di argomenti dell'utilizzo dell'estensione di markup, nonché le proprietà impostabili.  
  
 Tramite <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>, un'estensione di markup personalizzata dispone di accesso a un contesto del servizio che segnala l'ambiente in cui l'estensione di markup viene effettivamente richiamata da un processore XAML. Nel percorso di caricamento si tratta in genere di un oggetto <xref:System.Xaml.XamlObjectWriter>. Nel percorso di salvataggio si tratta in genere di un oggetto <xref:System.Xaml.XamlXmlWriter>. Il contesto del servizio viene segnalato come classe di contesto del provider di servizi XAML interna che implementa un modello del provider di servizi. Per altre informazioni sui servizi disponibili e su ciò che rappresentano, vedere [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md).  
  
 La classe dell'estensione di markup deve usare un livello di accesso pubblico. I processori XAML devono essere sempre in grado di creare un'istanza della classe di supporto dell'estensione di markup in modo da usare i relativi servizi.  
  
<a name="naming_the_support_type"></a>   
## Definizione del tipo di supporto per un'estensione di markup personalizzata  
 Quando si usano i servizi XAML di .NET Framework o framework basati sui servizi XAML di .NET Framework, esistono due possibilità per denominare il tipo di supporto dell'estensione di markup. Il nome del tipo è rilevante per la modalità con cui i writer dell'oggetto XAML tentano di accedere e richiamare un tipo di supporto dell'estensione di markup quando rilevano un utilizzo dell'estensione di markup in XAML. Usare una delle strategie di denominazione seguenti:  
  
-   Denominare il tipo in modo che corrisponda esattamente al token di utilizzo del markup XAML.  Ad esempio, per supportare l'utilizzo di un'estensione `{Collate ...}`, denominare il tipo di supporto `Collate`.  
  
-   Denominare il tipo in modo che corrisponda al token della stringa dell'utilizzo seguito dal suffisso `Extension`.  Ad esempio, per supportare l'utilizzo di un'estensione `{Collate ...}`, denominare il tipo di supporto `CollateExtension`.  
  
 L'ordine di ricerca prevede che venga cercato per primo il nome della classe con il suffisso `Extension`, quindi il nome della classe senza il suffisso `Extension`.  
  
 Dal punto di vista dell'utilizzo del markup, l'inclusione del suffisso `Extension` come parte dell'utilizzo è una procedura valida. Tuttavia, `Extension` viene considerato a tutti gli effetti parte del nome della classe, per cui i writer di oggetti XAML non riuscirebbero a risolvere una classe di supporto dell'estensione di markup per quell'utilizzo se la stessa classe non avesse il suffisso `Extension`.  
  
### Costruttore predefinito  
 Per tutti i tipi di supporto dell'estensione di markup è necessario esporre un costruttore pubblico predefinito. È necessario un costruttore predefinito per qualsiasi caso in cui un writer dell'oggetto XAML crei un'istanza dell'estensione di markup dall'utilizzo di un elemento oggetto. L'utilizzo dell'elemento oggetto di supporto è un'aspettativa legittima per un'estensione di markup, specialmente per la serializzazione. Si può tuttavia possibile implementare un'estensione di markup senza un costruttore pubblico quando si intende supportare solo gli utilizzi degli attributi dell'estensione di markup.  
  
 Se l'utilizzo dell'estensione di markup non dispone di argomenti, il costruttore predefinito sarà necessario per supportare l'utilizzo.  
  
<a name="constructor_patterns_and_positional_arguments_for_a_custom_markup_extension"></a>   
## Modelli di costruttore e argomenti posizionali per un'estensione di markup personalizzata  
 Per un'estensione di markup con utilizzo degli argomenti previsto, i costruttori pubblici devono corrispondere alle modalità dell'utilizzo previsto. In altri termini, se l'estensione di markup viene progettata per richiedere un argomento posizionale come utilizzo valido, è necessario supportare un costruttore pubblico con un parametro di input che accetti l'argomento posizionale.  
  
 Si supponga ad esempio che sia previsto che l'estensione di markup `Collate` supporti solo una modalità in cui è presente un argomento posizionale che rappresenta la relativa modalità, specificato come costante di enumerazione `CollationMode`. In questo caso, è necessario che sia presente un costruttore nel formato seguente:  
  
```  
public Collate(CollationMode collationMode) {...}  
```  
  
 A un livello di base, gli argomenti passati a un'estensione di markup sono costituiti da una stringa in quanto vengono inoltrati dai valori dell'attributo del markup. È possibile rendere stringhe tutti gli argomenti e utilizzare l'input a tale livello. Si dispone tuttavia dell'accesso a determinate attività di elaborazione che vengono eseguite prima del passaggio degli argomenti dell'estensione di markup alla classe di supporto.  
  
 L'elaborazione viene eseguita a livello concettuale come se l'estensione di markup fosse un oggetto da creare, quindi vengono impostati i valori di membro. Ogni proprietà specificata da impostare viene valutata nello stesso modo in cui un membro specificato può essere impostato su un oggetto creato durante l'analisi del codice XAML. Vi sono due differenze importanti:  
  
-   Come osservato in precedenza, non è necessario che un'estensione di markup disponga di un costruttore predefinito perché sia possibile crearne un'istanza in XAML. La costruzione di oggetti viene rinviata fino a quando gli argomenti possibili corrispondenti nella sintassi del testo non vengono convertiti in formato token e valutati come argomenti posizionali o denominati e il costruttore appropriato non viene a quel punto chiamato.  
  
-   Gli utilizzi delle estensioni di markup possono essere annidati. L'estensione di markup più interna viene valutata per prima. È dunque possibile presupporre tale utilizzo e dichiarare uno dei parametri della costruzione come tipo che richiede un convertitore di valori, ad esempio un'estensione di markup, da produrre.  
  
 Nell'esempio precedente viene illustrato l'affidamento su tale elaborazione. Il writer di oggetti XAML dei servizi XAML di .NET Framework elabora i nomi delle costanti di enumerazione in valori enumerati a livello nativo.  
  
 L'elaborazione della sintassi del testo di un parametro posizionale dell'estensione di markup può anche basarsi su un convertitore di tipi associato al tipo nell'argomento della costruzione.  
  
 Gli argomenti sono detti argomenti posizionali perché l'ordine in base al quale vengono rilevati i token nell'utilizzo corrisponde all'ordine posizionale del parametro del costruttore a cui sono assegnati. Si consideri ad esempio la firma del costruttore seguente:  
  
```  
public Collate(CollationMode collationMode, object collateThis) {...}  
```  
  
 Un processore XAML prevede la presenza di due argomenti posizionali per questa estensione di markup. Per un utilizzo `{Collate AlphaUp,{x:Reference circularFile}}`, il token `AlphaUp` viene inviato al primo parametro e quindi valutato come costante denominata dell'enumerazione `CollationMode`. Il risultato dell'argomento `x:Reference` interno viene inviato al secondo parametro e valutato come oggetto.  
  
 Nelle regole specificate per XAML per la sintassi e l'elaborazione dell'estensione di markup, la virgola è il delimitatore degli argomenti, sia posizionali che denominati.  
  
### Grado duplicato di argomenti posizionali  
 Se un writer di oggetti XAML rileva un utilizzo dell'estensione di markup con argomenti posizionali e sono presenti più argomenti del costruttore che accettano il numero di argomenti specificato \(un grado duplicato\), non si tratta necessariamente di un errore. Il comportamento dipende da un'impostazione del contesto dello schema XAML personalizzabile, <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A>. Se <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A> è `true`, un writer di oggetti XAML non genera un'eccezione solo per motivi di grado duplicato. Il comportamento oltre tale punto non è definito con precisione. Il presupposto di base per la progettazione è che il contesto dello schema disponga di informazioni sul tipo disponibili per i parametri specifici e possa tentare cast espliciti corrispondenti ai candidati duplicati per individuare la firma che potenzialmente costituisce la corrispondenza ottimale. È comunque possibile che venga generata un'eccezione se nessuna delle firme supera i test imposti da tale particolare contesto dello schema in esecuzione in un writer di oggetti XAML.  
  
 Per impostazione predefinita, <xref:System.Xaml.XamlSchemaContextSettings.SupportMarkupExtensionsWithDuplicateArity%2A> è `false` nell'oggetto <xref:System.Xaml.XamlSchemaContext> basato su CLR per i servizi XAML di .NET Framework. L'oggetto <xref:System.Xaml.XamlObjectWriter> predefinito, pertanto, genera eccezioni se rileva un utilizzo dell'estensione di markup con grado duplicato nei costruttori del tipo sottostante.  
  
<a name="named_arguments_for_a_custom_markup_extension"></a>   
## Argomenti denominati per un'estensione di markup personalizzata  
 Le estensioni di markup specificate da XAML possono anche usare argomenti denominati per l'utilizzo. Al primo livello di tokenizzazione, la sintassi del testo è divisa in argomenti. La presenza di un segno di uguale \(\=\) all'interno di qualsiasi argomento lo identifica come argomento denominato.  L'argomento viene inoltre convertito in formato token in una coppia nome\/valore. Il nome in questo caso denomina una proprietà impostabile pubblica del tipo di supporto dell'estensione di markup. Se si intende supportare l'utilizzo di argomenti denominati, sarà necessario fornire queste proprietà impostabili pubbliche. Le proprietà possono essere proprietà ereditate, fino a quando rimangono pubbliche.  
  
<a name="accessing_service_provider_context_from_a_markup_extension_implementation"></a>   
## Accesso al contesto del provider di servizi da un'implementazione dell'estensione di markup  
 I servizi disponibili sono gli stessi per qualsiasi convertitore di valori. L'unica differenza risiede nel modo in cui ogni convertitore di valori riceve il contesto del servizio.  L'accesso ai servizi e i servizi disponibili sono illustrati nell'argomento [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md).  
  
<a name="property_element_usage_of_a_markup_extension"></a>   
## Utilizzo dell'elemento proprietà di un'estensione di markup  
 Gli scenari per gli utilizzi di estensioni di markup sono spesso progettati attorno all'uso dell'estensione di markup nell'utilizzo dell'attributo. Tuttavia, si può anche definire la classe sottostante in modo che supporti l'utilizzo dell'elemento proprietà.  
  
 Per supportare l'utilizzo dell'elemento proprietà dell'estensione di markup, definire un costruttore predefinito pubblico. Deve trattarsi di un costruttore di istanza, non di un costruttore statico. Questo è necessario perché un processore XAML deve in genere richiamare il costruttore predefinito in qualsiasi elemento oggetto elaborato dal markup, incluse le classi dell'estensione di markup come elementi oggetto. Per gli scenari avanzati, è possibile definire percorsi di costruzione non predefiniti per le classi. Per altre informazioni, vedere [x:FactoryMethod Directive](../../../docs/framework/xaml-services/x-factorymethod-directive.md). Tuttavia, non si devono usare questi modelli per scopi di estensione di markup poiché questo rende molto più difficile l'individuazione del modello di utilizzo tanto per i progettisti quanto per gli utenti di markup non elaborato.  
  
<a name="attributing_for_a_custom_markup_extension"></a>   
## Associazione di attributi per un'estensione di markup personalizzata  
 Per supportare sia gli ambienti di progettazione sia determinati scenari dei writer di oggetti XAML, è necessario associare al tipo di supporto dell'estensione di markup diversi attributi CLR. Questi attributi indicano l'utilizzo dell'estensione di markup desiderato.  
  
 <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute> specifica le informazioni <xref:System.Type> per il tipo di oggetto restituito da <xref:System.Windows.Markup.ArrayExtension.ProvideValue%2A>. In base alla semplice firma, <xref:System.Windows.Markup.ArrayExtension.ProvideValue%2A> restituisce <xref:System.Object>. Diversi consumer potrebbero però richiedere informazioni più precise sul tipo restituito, vale a dire:  
  
-   Finestre di progettazione e IDE, potenzialmente in grado di fornire supporto dipendente dal tipo per gli utilizzi delle estensioni di markup.  
  
-   Implementazioni avanzate di gestori `SetMarkupExtension` in classi di destinazione, che possono basarsi sulla reflection per determinare il tipo restituito di un'estensione di markup anziché creare un ramo in implementazioni di <xref:System.Windows.Markup.MarkupExtension> specifiche note in base al nome.  
  
<a name="serialization_of_markup_extension_usages"></a>   
## Serializzazione degli utilizzi di estensioni di markup  
 Quando un writer di oggetti XAML elabora un utilizzo dell'estensione di markup e chiama <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>, il contesto del metodo che è stato precedentemente un utilizzo dell'estensione di markup viene reso persistente nel flusso del nodo XAML, ma non nell'oggetto grafico. Nell'oggetto grafico viene mantenuto solo il valore. In presenza di scenari di progettazione o altri motivi che determinano la necessità di rendere persistente l'utilizzo dell'estensione di markup originale nell'output serializzato, sarà necessario progettare un'infrastruttura personalizzata per la verifica degli utilizzi delle estensioni di markup dal flusso del nodo XAML del percorso di caricamento. Si può implementare il comportamento per ricreare gli elementi del flusso del nodo dal percorso di caricamento e riprodurli per i writer XAML per la serializzazione nel percorso di salvataggio, sostituendo il valore nella posizione appropriata del flusso del nodo.  
  
<a name="markup_extensions_in_the_xaml_node_stream"></a>   
## Estensioni di markup nel flusso di nodi XAML  
 Se si usa un flusso del nodo XAML nel percorso di caricamento, un utilizzo dell'estensione di markup viene visualizzato come oggetto nel flusso del nodo.  
  
 Se l'utilizzo dell'estensione di markup usa argomenti posizionali, viene rappresentato come oggetto iniziale con un valore di inizializzazione. Come rappresentazione di testo approssimativa, il flusso del nodo sarà simile a quanto segue:  
  
 `StartObject` \(<xref:System.Xaml.XamlType> è il tipo di definizione dell'estensione di markup, non il tipo restituito\)  
  
 `StartMember` \(il nome di <xref:System.Xaml.XamlMember> è `_InitializationText`\)  
  
 `Value` \(rappresenta gli argomenti posizionali sotto forma di stringa, inclusi i delimitatori frapposti\)  
  
 `EndMember`  
  
 `EndObject`  
  
 Un utilizzo dell'estensione di markup con argomenti denominati viene rappresentato come oggetto con membri dei nomi pertinenti, ognuno impostato con valori della stringa di testo.  
  
 In realtà, il richiamo dell'implementazione di `ProvideValue` di un'estensione di markup necessita del contesto dello schema XAML, poiché questo richiede il mapping dei tipi e la creazione di un'istanza del tipo di supporto dell'estensione di markup. Questo è uno dei motivi per cui gli utilizzi dell'estensione di markup sono conservati in questo modo nei flussi del nodo dei servizi XAML di .NET Framework predefiniti. La parte del reader di un percorso di caricamento spesso non ha a disposizione il contesto dello schema XAML necessario.  
  
 Se si utilizza un flusso del nodo XAML nel percorso di salvataggio, in genere la rappresentazione dell'oggetto grafico non contiene alcun elemento che possa indicare che l'oggetto da serializzare fosse originariamente fornito da un utilizzo dell'estensione di markup e un risultato `ProvideValue`. Negli scenari che richiedono il salvataggio permanente degli utilizzi dell'estensione di markup per le sequenze di andata e ritorno e al contempo l'acquisizione di altre modifiche nell'oggetto grafico, è necessario ideare tecniche personalizzate per preservare la conoscenza di un utilizzo dell'estensione di markup dall'input XAML originale. Ad esempio, per ripristinare gli utilizzi dell'estensione di markup, può essere necessario usare il flusso del nodo nel percorso di salvataggio oppure eseguire una sorta di unione tra XAML originale e XAML sottoposto a sequenza di andata e ritorno. Alcuni framework che implementano XAML, ad esempio WPF, usano tipi intermedi \(espressioni\) per rappresentare i casi in cui gli utilizzi dell'estensione di markup hanno fornito i valori.  
  
## Vedere anche  
 <xref:System.Windows.Markup.MarkupExtension>   
 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)   
 [Estensioni di markup e XAML WPF](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)