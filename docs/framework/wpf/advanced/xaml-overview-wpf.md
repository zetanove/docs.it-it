---
title: "Cenni preliminari su XAML (WPF) | Microsoft Docs"
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
  - "sintassi di attributo [XAML]"
  - "classi di base [XAML]"
  - "classi [XAML]"
  - "code-behind (file) [WPF], XAML"
  - "proprietà di raccolte [XAML]"
  - "modelli di contenuto [XAML]"
  - "eventi [XAML]"
  - "Extensible Application Markup Language (vedere XAML)"
  - "proprietà (elemento) [XAML]"
  - "radice (elemento) [XAML]"
  - "eventi indirizzati"
  - "interfacce utente [XAML]"
  - "XAML [WPF], informazioni su XAML"
ms.assetid: a80db4cd-dd0f-479f-a45f-3740017c22e4
caps.latest.revision: 57
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 50
---
# Cenni preliminari su XAML (WPF)
In questo argomento vengono descritte le funzionalità del linguaggio XAML e viene illustrato come utilizzare XAML per la scrittura di applicazioni [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  In particolare, viene descritto il linguaggio XAML implementato in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Il linguaggio XAML in quanto tale, tuttavia, rappresenta un concetto di linguaggio più ampio rispetto a quello implementato in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
   
  
<a name="what_is_xaml"></a>   
## Definizione di XAML  
 XAML è un linguaggio di markup dichiarativo  Applicato al modello di programmazione [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)], XAML semplifica la creazione di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] per un'applicazione [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)].  È possibile creare elementi di [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] visibili nel markup XAML dichiarativo, quindi separare la definizione di [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] dalla logica di runtime utilizzando file code\-behind, uniti al markup tramite definizioni di classe parziali.  XAML rappresenta in modo diretto la creazione di istanze di oggetti in un set specifico di tipi di supporto definiti in assembly. In ciò si differenzia dalla maggior parte degli altri linguaggi di markup, che sono in genere linguaggi interpretati senza un legame diretto con il sistema di tipi di supporto.  XAML consente un flusso di lavoro in cui parti distinte possono operare nell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] e nella logica di un'applicazione, utilizzando strumenti potenzialmente diversi.  
  
 Se rappresentati come testo, i file XAML sono file XML in genere con estensione `.xaml`.  I file possono essere codificati tramite qualsiasi codifica XML, tuttavia la codifica tipica è UTF\-8.  
  
 Nell'esempio seguente viene illustrato come creare un pulsante come parte di un'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  L'esempio non deve essere ritenuto esaustivo e ha il semplice scopo di fornire un'idea molto generale del modo in cui XAML rappresenta metafore di programmazione dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] comuni.  
  
 [!code-xml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
<a name="xaml_syntax_in_brief"></a>   
## Cenni sulla sintassi XAML  
 Nelle sezioni seguenti vengono descritte le forme di base della sintassi XAML e viene fornito un breve esempio di markup.  L'obiettivo di queste sezioni non consiste nel fornire informazioni complete su ogni forma di sintassi, ad esempio sulla modalità di rappresentazione di queste sintassi nel sistema di tipi di supporto.  Per ulteriori informazioni sulle specifiche della sintassi XAML per ognuna delle forme di sintassi introdotte in questo argomento, vedere [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 Se si ha familiarità con il linguaggio XML, la maggior parte del materiale incluso in alcune delle sezioni successive risulterà di facile comprensione.  Ciò è dovuto a uno dei principi di base della progettazione XAML.  Il linguaggio XAML definisce concetti propri, tuttavia questi concetti funzionano nel linguaggio XML e nel formato del markup.  
  
### Elementi oggetto di XAML  
 In genere, un elemento oggetto dichiara un'istanza di un tipo.  Il tipo è definito negli assembly che forniscono i tipi di supporto per una tecnologia che utilizza XAML come linguaggio.  
  
 La sintassi degli elementi oggetto inizia sempre con una parentesi angolare di apertura \(\<\),  seguita dal nome del tipo in cui si desidera creare un'istanza.  Il nome può includere un prefisso. Questo concetto verrà illustrato in seguito. Se lo si desidera, è quindi possibile dichiarare attributi nell'elemento oggetto.  Per completare il tag dell'elemento oggetto, terminare con una parentesi angolare di chiusura \(\>\).  In alternativa, è possibile utilizzare una forma di chiusura automatica senza contenuto, completando il tag con una barra e una parentesi angolare di chiusura in successione \(\/\>\).  Osservare nuovamente il frammento di markup illustrato in precedenza:  
  
 [!code-xml[XAMLOvwSupport#DirtSimple](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]  
  
 Vengono specificati due elementi oggetto: `<StackPanel>` \(con contenuto e un tag di chiusura successivo\) e `<Button .../>` \(forma di chiusura automatica, con diversi attributi\).  Gli elementi oggetto `StackPanel` e `Button` vengono mappati ciascuno al nome di una classe definita da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e che fa parte degli assembly [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Quando si specifica il tag di un elemento oggetto, si crea un'istruzione per la creazione di una nuova istanza da parte dell'elaborazione XAML.  Ogni istanza viene creata chiamando il costruttore predefinito del tipo sottostante durante l'analisi e il caricamento del markup XAML.  
  
### Sintassi per attributi \(proprietà\)  
 Spesso le proprietà di un oggetto possono essere espresse come attributi dell'elemento oggetto.  Una sintassi per attributi definisce un nome per la proprietà impostata nella sintassi, seguito dall'operatore di assegnazione \(\=\).  Il valore di un attributo viene sempre specificato come stringa inclusa tra virgolette.  
  
 La sintassi per attributi è la sintassi per l'impostazione di proprietà più semplice, nonché la più intuitiva per gli sviluppatori che hanno già utilizzato linguaggi di markup in passato.  Nel markup seguente ad esempio, viene creato un pulsante che presenta un testo rosso e uno sfondo blu oltre a un testo visualizzato specificato come `Content`.  
  
 [!code-xml[XAMLOvwSupport#BlueRedButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbutton)]  
  
### Sintassi per gli elementi proprietà  
 Per alcune proprietà di un elemento oggetto, la sintassi per attributi non può essere utilizzata in quanto non è possibile esprimere l'oggetto o le informazioni necessarie per fornire il valore di proprietà in modo adeguato tra virgolette e nel rispetto delle limitazioni della stringa della sintassi di attributo.  In questi casi, è possibile utilizzare una sintassi diversa, nota come sintassi per elementi proprietà,  
  
 La sintassi per il tag di inizio dell'elemento proprietà è `<`*nomeTipo*`.`*nomeProprietà*`>`.  Il contenuto di tale tag è in genere un elemento oggetto del tipo accettato come valore dalla proprietà.  Dopo avere specificato il contenuto, è necessario chiudere l'elemento proprietà con un tag di fine.  La sintassi per il tag di fine è `</`*nomeTipo*`.`*nomeProprietà*`>`.  
  
 Se supportata, la sintassi per attributi è in genere più efficace e consente un markup più compatto. Si tratta tuttavia di una questione di stile e non di un limite tecnico.  Nell'esempio seguente vengono mostrate le stesse proprietà impostate nell'esempio di sintassi per attributi precedente, tuttavia questa volta viene utilizzata la sintassi per elementi proprietà per tutte le proprietà dell'oggetto `Button`.  
  
 [!code-xml[XAMLOvwSupport#BlueRedButtonPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbuttonpe)]  
  
### Sintassi per raccolte  
 Il linguaggio XAML include alcune ottimizzazioni che producono un markup più leggibile per l'utente.  Una di queste ottimizzazioni prevede che se una proprietà specifica accetta un tipo di raccolta, gli elementi dichiarati nel markup come elementi figlio in quel valore della proprietà diventano di conseguenza parte della raccolta.  In questo caso, una raccolta di elementi oggetto figlio corrisponde al valore impostato nella proprietà della raccolta.  
  
 Nell'esempio seguente viene illustrata la sintassi per raccolte per l'impostazione dei valori della proprietà <xref:System.Windows.Media.GradientBrush.GradientStops%2A>:  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <!-- no explicit new GradientStopCollection, parser knows how to find or create -->  
    <GradientStop Offset="0.0" Color="Red" />  
    <GradientStop Offset="1.0" Color="Blue" />  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
### Proprietà di contenuto XAML  
 XAML specifica una funzionalità del linguaggio tramite cui una classe può designare esattamente una delle relative proprietà come proprietà di contenuto XAML.  Gli elementi figlio dell'elemento oggetto vengono utilizzati per impostare il valore di questa proprietà di contenuto.  In altre parole, solo per la proprietà di contenuto, è possibile omettere un elemento proprietà quando si imposta tale proprietà nel markup XAML ed è possibile produrre una metafora padre\/figlio più visibile nel markup.  
  
 Ad esempio, <xref:System.Windows.Controls.Border> specifica una proprietà di contenuto di <xref:System.Windows.Controls.Decorator.Child%2A>.  I due elementi <xref:System.Windows.Controls.Border> seguenti vengono gestiti in modo identico.  Il primo sfrutta la sintassi della proprietà di contenuto e omette l'elemento proprietà `Border.Child`.  Il secondo specifica `Border.Child` in modo esplicito.  
  
```xaml  
<Border>  
  <TextBox Width="300"/>  
</Border>  
<!--explicit equivalent-->  
<Border>  
  <Border.Child>  
    <TextBox Width="300"/>  
  </Border.Child>  
</Border>  
```  
  
 Secondo le regole del linguaggio XAML, il valore di una proprietà di contenuto XAML deve essere specificato completamente prima o completamente dopo qualsiasi altro elemento proprietà nell'elemento oggetto.  Ad esempio, il markup seguente non viene compilato:  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 Per ulteriori informazioni su questa restrizione nelle proprietà di contenuto XAML, vedere la sezione "Proprietà di contenuto XAML" di [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
### Contenuto di testo  
 Un numero ridotto di elementi XAML può elaborare il testo direttamente come contenuto.  A tale scopo, deve verificarsi uno dei casi seguenti:  
  
-   La classe deve dichiarare una proprietà di contenuto e tale proprietà di contenuto deve essere di un tipo assegnabile a una stringa \(il tipo può essere <xref:System.Object>\).  Qualsiasi oggetto <xref:System.Windows.Controls.ContentControl>, ad esempio, utilizza <xref:System.Windows.Controls.ContentControl.Content%2A> come proprietà di contenuto ed è di tipo <xref:System.Object>, che supporta il seguente utilizzo in un oggetto <xref:System.Windows.Controls.ContentControl> pratico, ad esempio <xref:System.Windows.Controls.Button>: `<Button>Hello</Button>`.  
  
-   Il tipo deve dichiarare un convertitore di tipi e, in tal caso, il contenuto di testo viene utilizzato come testo di inizializzazione per il convertitore di tipi.  Ad esempio, `<Brush>Blue</Brush>`.  Nella pratica questo caso è meno comune.  
  
-   Il tipo deve essere un tipo primitivo noto del linguaggio XAML.  
  
### Combinazione di proprietà di contenuto e sintassi per raccolte  
 Si consideri l'esempio seguente:  
  
```xaml  
<StackPanel>  
  <Button>First Button</Button>  
  <Button>Second Button</Button>  
</StackPanel>  
```  
  
 Nell'esempio ogni elemento <xref:System.Windows.Controls.Button> è un elemento figlio di <xref:System.Windows.Controls.StackPanel>.  Si tratta di un markup semplice e intuitivo nel quale vengono omessi due tag per due ragioni diverse.  
  
-   **Elemento proprietà StackPanel.Children omesso:**  <xref:System.Windows.Controls.StackPanel> deriva da <xref:System.Windows.Controls.Panel>.  <xref:System.Windows.Controls.Panel> definisce <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=fullName> come proprietà di contenuto XAML.  
  
-   **Elemento oggetto UIElementCollection omesso:** la proprietà <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=fullName> accetta il tipo <xref:System.Windows.Controls.UIElementCollection>, che implementa <xref:System.Collections.IList>.  In base alle regole XAML per l'elaborazione di raccolte come <xref:System.Collections.IList>, è possibile omettere il tag dell'elemento della raccolta.  In questo caso, non è effettivamente possibile creare un'istanza di <xref:System.Windows.Controls.UIElementCollection>, in quanto non espone un costruttore predefinito e per questo motivo l'elemento oggetto <xref:System.Windows.Controls.UIElementCollection> risulta impostato come commento.  
  
```xaml  
<StackPanel>  
  <StackPanel.Children>  
    <!--<UIElementCollection>-->  
    <Button>First Button</Button>  
    <Button>Second Button</Button>  
    <!--</UIElementCollection>-->  
  </StackPanel.Children>  
</StackPanel>  
```  
  
### Sintassi per attributi \(eventi\)  
 È possibile utilizzare la sintassi per attributi anche per membri che sono eventi anziché proprietà.  In questo caso il nome dell'attributo corrisponde al nome dell'evento.  Nell'implementazione WPF di eventi per XAML, il valore dell'attributo corrisponde al nome di un gestore che implementa il delegato dell'evento.  Nel markup seguente, ad esempio, viene assegnato un gestore per l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> a un controllo <xref:System.Windows.Controls.Button> creato nel markup:  
  
 [!code-xml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 La correlazione tra eventi e XAML in WPF è molto più complessa di questo semplice esempio di sintassi per attributi.  Ci si potrebbe chiedere ad esempio, cosa rappresenti `ClickHandler` a cui viene fatto riferimento e come questo venga definito.  Questi aspetti verranno illustrati nella sezione  più avanti in questo argomento.  
  
<a name="case_and_whitespace_in_xaml"></a>   
## Maiuscolo e minuscolo e spazi vuoti in XAML  
 In genere, XAML effettua la distinzione tra maiuscole e minuscole.  Per la risoluzione di tipi di supporto, XAML WPF effettua la distinzione tra maiuscole e minuscole in base alle stesse regole applicate da CLR relativamente a tale distinzione.  Gli elementi oggetto, gli elementi proprietà e i nomi di attributo devono essere specificati tutti utilizzando correttamente le maiuscole e le minuscole quando si esegue il confronto del nome con il nome del tipo sottostante nell'assembly o con il nome di un membro di un tipo.  La distinzione tra maiuscole e minuscole viene effettuata anche per le parole chiave e le primitive del linguaggio XLAM.  Per i valori la distinzione tra maiuscole e minuscole non viene sempre effettuata.  Tale distinzione per i valori dipenderà dal comportamento del convertitore dei tipi associato alla proprietà che accetta il valore o al tipo di valore della proprietà.  Ad esempio, le proprietà che accettano il tipo <xref:System.Boolean> possono accettare `true` o `True` come valori equivalenti, ma solo perché la conversione in <xref:System.Boolean> dei tipi nativi del parser XAML WPF per la stringa consente già tali valori come equivalenti.  
  
 I processori e i serializzatori XAML WPF ignoreranno o rimuoveranno tutti gli spazi vuoti non significativi e normalizzeranno gli spazi vuoti significativi.  Ciò è coerente con i requisiti di comportamento degli spazi vuoti predefiniti della specifica XAML.  Questo comportamento è generalmente significativo solo quando si specificano stringhe all'interno di proprietà di contenuto XAML.  In termini più semplici, in XAML i caratteri di spazio, avanzamento riga e tabulazione vengono convertiti in spazi e viene conservato solo l'eventuale spazio rilevato a una delle estremità di una stringa contigua.  La spiegazione completa della gestione degli spazi vuoti in XAML non è oggetto di trattazione in questo argomento.  Per informazioni dettagliate, vedere [Elaborazione degli spazi vuoti in XAML](../../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
<a name="markup_extensions"></a>   
## Estensioni di markup  
 Le estensioni di markup sono un concetto del linguaggio XAML.  Se utilizzate per specificare il valore di una sintassi per attributi, le parentesi graffe \(`{` e `}`\) indicano l'utilizzo di un'estensione di markup.  Questo utilizzo indica all'elaborazione XAML che, diversamente dal solito, i valori degli attributi non devono essere considerati valori di stringa letterale o valori convertibili in stringa.  
  
 Le estensioni di markup maggiormente utilizzate nella programmazione di applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sono [Binding](../../../../docs/framework/wpf/advanced/binding-markup-extension.md), utilizzata per le espressioni di associazione dati e i riferimenti alle risorse [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) e [DynamicResource](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md).  Le estensioni di markup consentono di utilizzare la sintassi per attributi per specificare valori per le proprietà anche quando le proprietà non supportano in generale una sintassi per attributi.  Spesso, le estensioni di markup vengono utilizzate con tipi di espressione intermedi per abilitare funzionalità quali il posticipo di valori o il riferimento ad altri oggetti presenti solo in fase di esecuzione.  
  
 Nel markup seguente, ad esempio, viene impostato il valore della proprietà <xref:System.Windows.FrameworkElement.Style%2A> utilizzando la sintassi per attributi.  La proprietà <xref:System.Windows.FrameworkElement.Style%2A> accetta un'istanza della classe <xref:System.Windows.Style>, di cui per impostazione predefinita non è stato possibile creare un'istanza tramite una stringa di sintassi per attributi.  Tuttavia, in questo caso l'attributo fa riferimento a una particolare estensione di markup, [StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md).  Quando quell'estensione di markup viene elaborata, restituisce un riferimento a uno stile del quale in precedenza è stata creata un'istanza come risorsa con chiave in un dizionario di risorse.  
  
<!-- TODO: review snippet reference  [!CODE [FEResourceSH#XAMLOvwShortResources](FEResourceSH#XAMLOvwShortResources)]  -->  
<!-- TODO: review snippet reference [!CODE [FEResourceSH#XAMLOvwShortResources2](FEResourceSH#XAMLOvwShortResources2)]  -->  
<!-- TODO: review snippet reference [!CODE [FEResourceSH#XAMLOvwShortResources3](FEResourceSH#XAMLOvwShortResources3)]  -->  
  
 Per un elenco di riferimento di tutte le estensioni di markup per il linguaggio XAML implementato specificamente in WPF, vedere [Estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md).  Per un elenco di riferimento delle estensioni di markup definite da System.Xaml e più ampiamente disponibili per implementazioni XAML .NET Framework, vedere [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md).  Per ulteriori informazioni sui concetti correlati alle estensioni di markup, vedere [Estensioni di markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md).  
  
<a name="type_converters"></a>   
## Convertitori di tipi  
 Nella sezione  è stato affermato che il valore dell'attributo deve poter essere impostato tramite una stringa.  La gestione nativa di base della conversione delle stringhe in altri tipi di oggetto o valori primitivi si basa sul tipo <xref:System.String> stesso, nonché su un'elaborazione nativa per determinati tipi, ad esempio <xref:System.DateTime> o <xref:System.Uri>.  Molti tipi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] o membri di tali tipi, tuttavia, estendono il comportamento di elaborazione degli attributi stringa di base in modo che le istanze di tipi di oggetto più complessi possano essere specificate come stringhe e attributi.  
  
 La struttura <xref:System.Windows.Thickness> è un esempio di un tipo associato a una conversione di tipi abilitata per gli utilizzi di XAML.  <xref:System.Windows.Thickness> indica misure all'interno di un rettangolo annidato e viene utilizzata come valore per proprietà quali <xref:System.Windows.FrameworkElement.Margin%2A>.  Inserendo un convertitore di tipi in <xref:System.Windows.Thickness>, tutte le proprietà che utilizzano una struttura <xref:System.Windows.Thickness> risultano più facili da specificare in XAML, in quanto possono essere specificate come attributi.  Nell'esempio seguente vengono utilizzate una conversione di tipi e la sintassi per attributi per specificare un valore per una proprietà <xref:System.Windows.FrameworkElement.Margin%2A>:  
  
 [!code-xml[XAMLOvwSupport#MarginTCE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#margintce)]  
  
 L'esempio precedente di sintassi per attributi è equivalente all'esempio di sintassi più dettagliato riportato di seguito, in cui <xref:System.Windows.FrameworkElement.Margin%2A> è impostato invece tramite la sintassi per elementi proprietà contenente un elemento oggetto <xref:System.Windows.Thickness>.  Le quattro proprietà chiave di <xref:System.Windows.Thickness> sono impostate come attributi nella nuova istanza:  
  
 [!code-xml[XAMLOvwSupport#MarginVerbose](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#marginverbose)]  
  
> [!NOTE]
>  Esiste inoltre un numero limitato di oggetti in cui la conversione dei tipi rappresenta l'unico modo pubblico per impostare una proprietà su quel tipo senza coinvolgere una sottoclasse, poiché il tipo stesso non dispone di un costruttore predefinito.  <xref:System.Windows.Input.Cursor> è un esempio.  
  
 Per ulteriori informazioni sul supporto della conversione dei tipi e del relativo utilizzo per la sintassi per attributi, vedere [TypeConverter e XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md).  
  
<a name="xaml_root_elements_and_xaml_namespaces"></a>   
## Elementi radice XAML e spazi dei nomi XAML  
 Per essere sia un file [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] ben formato sia un file XAML valido, un file XAML deve includere solo un elemento radice.  Per scenari WPF tipici, è possibile utilizzare un elemento radice dotato di un significato prominente nel modello applicativo WPF, ad esempio <xref:System.Windows.Window> o <xref:System.Windows.Controls.Page> per una pagina, <xref:System.Windows.ResourceDictionary> per un dizionario esterno oppure <xref:System.Windows.Application> per la definizione dell'applicazione.  Nell'esempio seguente viene illustrato l'elemento radice di un tipico file XAML per una pagina [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], con l'elemento radice di <xref:System.Windows.Controls.Page>.  
  
 [!code-xml[XAMLOvwSupport#RootOnly](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly)]  
[!code-xml[XAMLOvwSupport#RootOnly2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly2)]  
  
 L'elemento radice inoltre contiene gli attributi `xmlns` e `xmlns:x`,  che indicano a un processore XAML gli spazi dei nomi XAML che contengono le definizioni dei tipi per i tipi di supporto a cui il markup farà riferimento come elementi.  L'attributo `xmlns` indica in modo specifico lo spazio dei nomi XAML predefinito.  All'interno dello spazio dei nomi XAML predefinito gli elementi oggetto nel markup possono essere specificati senza prefisso.  Per la maggior parte degli scenari con applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e per quasi tutti gli esempi forniti nelle sezioni di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nell'[!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)], lo spazio dei nomi XAML predefinito viene mappato allo spazio dei nomi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)].  L'attributo `xmlns:x` indica uno spazio dei nomi XAML aggiuntivo, che viene mappato allo spazio dei nomi del linguaggio XAML [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)].  
  
 Tale utilizzo di `xmlns` per definire un ambito per l'utilizzo e il mapping di un NameScope è coerente con la specifica XML 1.0.  I NameScope XAML sono diversi dai NameScope XML solo in quanto nei primi vengono indicati anche alcuni aspetti correlati al supporto degli elementi del NameScope da parte dei tipi riguardo a risoluzione dei tipi e analisi di XAML.  
  
 Si noti che gli attributi `xmlns` sono strettamente necessari solo per l'elemento radice di ogni file XAML.  Le definizioni `xmlns` si applicheranno a tutti gli elementi discendenti dell'elemento radice, un comportamento coerente con la specifica XML 1.0 per `xmlns`. Gli attributi `xmlns` sono inoltre consentiti in altri elementi sottostanti la radice e si applicherebbero a qualsiasi elemento discendente dell'elemento di definizione.  Tuttavia, la definizione o ridefinizione frequente degli spazi dei nomi XAML può provocare uno stile di markup XAML di difficile lettura.  
  
 L'implementazione [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] del relativo processore XAML include un'infrastruttura che rileva gli assembly principali WPF.  Gli assembly principali [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] contengono notoriamente i tipi che supportano i mapping [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] allo spazio dei nomi XAML predefinito.  Ciò è consentito tramite la configurazione inclusa nel file di compilazione del progetto e nei sistemi di compilazione e del progetto WPF.  La dichiarazione dello spazio dei nomi XAML predefinito come `xmlns` predefinito, pertanto, è l'unica operazione necessaria per fare riferimento a elementi XAML provenienti da assembly [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
### Prefisso x:  
 Nell'esempio di elemento radice precedente è stato utilizzato il prefisso `x:` per eseguire il mapping dello spazio dei nomi XAML [!INCLUDE[TLA#tla_xamlxmlnsv1](../../../../includes/tlasharptla-xamlxmlnsv1-md.md)], che è lo spazio dei nomi XAML dedicato che supporta costrutti di linguaggio XAML.  Il prefisso `x:` viene utilizzato per il mapping di questo spazio dei nomi XAML nei modelli per i progetti, negli esempi e nella documentazione in tutto l'[!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)].  Lo spazio dei nomi XAML per il linguaggio XAML contiene diversi costrutti di programmazione che verranno utilizzati molto frequentemente in XAML.  Di seguito viene fornito un elenco dei più comuni costrutti di programmazione del prefisso `x:` che verranno utilizzati:  
  
-   [x:Key](../../../../docs/framework/xaml-services/x-key-directive.md): imposta una chiave univoca per ogni risorsa in un oggetto <xref:System.Windows.ResourceDictionary> o concetti di dizionario simili di altri framework.  `x:Key` sarà coinvolto probabilmente nel 90% degli utilizzi di `x:` osservati nel markup di un'applicazione WPF tipica.  
  
-   [x:Class](../../../../docs/framework/xaml-services/x-class-directive.md): specifica lo spazio dei nomi [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] e il nome della classe che fornisce il code\-behind per una pagina XAML.  È necessario che tale classe supporti il code\-behind per ciascun modello di programmazione WPF ed è per questa ragione che quasi sempre viene eseguito il mapping di `x:`, anche se non sono presenti delle risorse.  
  
-   [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md): specifica il nome di un oggetto di runtime per l'istanza presente nel codice di esecuzione dopo l'elaborazione di un elemento oggetto.  In genere, si utilizzerà spesso una proprietà equivalente definita in WPF per [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md).  Tali proprietà eseguono specificamente il mapping a una proprietà di supporto CLR e risultano pertanto più utili per la programmazione di applicazioni, in cui spesso viene utilizzato codice di runtime per individuare gli elementi denominati da XAML inizializzato.  Tra queste proprietà la più comune è <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=fullName>.  È ancora possibile utilizzare [x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) nei casi in cui la proprietà <xref:System.Windows.FrameworkElement.Name%2A> equivalente a [livello di framework WPF](GTMT) non sia supportata in un tipo particolare.  Tale situazione si verifica in determinati scenari di animazione.  
  
-   [x:Static](../../../../docs/framework/xaml-services/x-static-markup-extension.md): abilita il riferimento che restituisce un valore statico che non costituisce in altro modo una proprietà compatibile con XAML.  
  
-   [x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md): crea un riferimento <xref:System.Type> basato sul nome di un tipo.  È utilizzato per specificare attributi che accettano <xref:System.Type>, ad esempio <xref:System.Windows.Style.TargetType%2A?displayProperty=fullName>, sebbene spesso la proprietà disponga di una conversione nativa da stringa a <xref:System.Type> che rende facoltativo l'utilizzo dell'estensione di markup [x:Type](../../../../docs/framework/xaml-services/x-type-markup-extension.md).  
  
 Nel prefisso `x:` o nello spazio dei nomi XAML sono presenti altri costrutti di programmazione non altrettanto comuni.  Per informazioni dettagliate, vedere [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md).  
  
<a name="custom_prefixes_and_custom_types_in_xaml"></a>   
## Prefissi personalizzati e tipi personalizzati in XAML  
 Per gli assembly personalizzati o per gli assembly esterni agli elementi principali WPF di PresentationCore, PresentationFramework e WindowsBase, è possibile specificare l'assembly come parte di un mapping `xmlns` personalizzato.  È quindi possibile fare riferimento ai tipi dell'assembly in XAML, purché tale tipo sia stato implementato correttamente per supportare gli utilizzi di XAML desiderati.  
  
 Di seguito viene fornito un esempio molto semplice del funzionamento dei prefissi personalizzati nel markup XAML.  Il prefisso `custom` è definito nel tag dell'elemento radice e viene mappato a un assembly specifico compresso e disponibile con l'applicazione.  Questo assembly contiene un tipo `NumericUpDown` implementato per supportare l'utilizzo generale di XAML, nonché l'utilizzo di un'ereditarietà delle classi che ne consenta l'inserimento in questo punto specifico in un modello di contenuto XAML WPF.  Un'istanza di questo controllo `NumericUpDown` viene dichiarata come elemento oggetto, utilizzando il prefisso in modo tale che un parser XAML sia in grado di riconoscere lo spazio dei nomi XAML contenente il tipo e pertanto la posizione dell'assembly di supporto che contiene la definizione del tipo.  
  
```  
<Page  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"   
    xmlns:custom="clr-namespace:NumericUpDownCustomControl;assembly=CustomLibrary"  
    >  
  <StackPanel Name="LayoutRoot">  
    <custom:NumericUpDown Name="numericCtrl1" Width="100" Height="60"/>  
...  
  </StackPanel>  
</Page>  
```  
  
 Per ulteriori informazioni sui tipi personalizzati in XAML, vedere [Classi XAML e personalizzate per WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md).  
  
 Per ulteriori informazioni sulla modalità di correlazione tra gli spazi dei nomi XML e gli spazi dei nomi del codice di supporto negli assembly, vedere [Spazi dei nomi XAML e mapping dello spazio dei nomi per XAML WPF](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
<a name="events_and_xaml_codebehind"></a>   
## Eventi e code\-behind XAML  
 La maggior parte delle applicazioni [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] include sia markup che code\-behind XAML.  All'interno di un progetto, XAML viene scritto come file `.xaml` e per scrivere un file code\-behind viene utilizzato un linguaggio [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], ad esempio [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] o [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)].  Durante la compilazione dal markup di un file XAML come parte dei modelli di applicazione e di programmazione WPF, il percorso del file code\-behind XAML per un file XAML viene identificato specificando uno spazio dei nomi e una classe come attributo `x:Class` dell'elemento radice della pagina XAML.  
  
 Negli esempi riportati fino a questo momento sono stati illustrati molti pulsanti, nessuno dei questi era associato a un comportamento logico.  Il meccanismo primario a livello di applicazione per l'aggiunta di un comportamento per un elemento oggetto consiste nell'utilizzo di un evento esistente della classe dell'elemento e nella scrittura di un gestore specifico per quell'evento che viene richiamato nel momento in cui l'evento viene generato in fase di esecuzione.  Il nome dell'evento e il nome del gestore da utilizzare sono specificati nel markup, mentre il codice che implementa il gestore è definito nel code\-behind.  
  
 [!code-xml[XAMLOvwSupport#ButtonWithCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]  
  
 [!code-csharp[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml.cs#buttonwithcodebehindhandler)]
 [!code-vb[XAMLOvwSupport#ButtonWithCodeBehindHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#buttonwithcodebehindhandler)]  
  
 Notare che il file code\-behind utilizza lo spazio dei nomi CLR `ExampleNamespace` e dichiara `ExamplePage` come classe parziale all'interno di tale spazio dei nomi.  Questo è parallelo al valore dell'attributo `x:Class` di `ExampleNamespace`.`ExamplePage` fornito nella radice del markup.  Il compilatore del markup WPF creerà una classe parziale per ogni file XAML compilato derivando una classe dal tipo di elemento radice.  Quando si fornisce code\-behind che definisce anche la stessa classe parziale, il codice risultante viene combinato all'interno dello stesso spazio dei nomi e della stessa classe dell'applicazione compilata.  
  
 Per ulteriori informazioni sui requisiti per la programmazione di code\-behind in WPF, vedere la sezione di [Code\-behind e XAML in WPF](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md) relativa a code\-behind, gestore eventi e requisiti delle classi parziali.  
  
 Se non si desidera creare un file code\-behind distinto, è anche possibile incorporare il codice in un file XAML.  Tuttavia, il codice inline è una tecnica meno versatile che presenta limitazioni sostanziali.  Per informazioni dettagliate, vedere [Code\-behind e XAML in WPF](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md).  
  
### Eventi indirizzati  
 Un [evento indirizzato](GTMT) è una particolare funzionalità evento fondamentale per [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  Gli eventi indirizzati consentono a un elemento di gestire un evento generato da un elemento diverso, purché gli elementi siano connessi tramite una relazione di struttura ad albero.  Quando si specifica la gestione dell'evento con un attributo XAML, l'evento indirizzato può essere ascoltato e gestito in qualsiasi elemento, inclusi quelli che non elencano l'evento specifico nella tabella dei membri della classe.  Ciò è possibile qualificando l'attributo del nome evento con il nome della classe di appartenenza.  Ad esempio, l'elemento padre `StackPanel` nell'esempio `StackPanel` \/ `Button` potrebbe registrare un gestore per l'evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> del pulsante dell'elemento figlio specificando l'attributo `Button.Click` nell'elemento oggetto `StackPanel`, con il nome del gestore come valore dell'attributo.  Per ulteriori informazioni sul funzionamento degli eventi indirizzati, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
<a name="x_name_and_xaml_named_elements"></a>   
## Elementi denominati XALM  
 Per impostazione predefinita, l'istanza di oggetto creata in un oggetto grafico mediante l'elaborazione di un elemento oggetto XAML non possiede un identificatore univoco o un riferimento a un oggetto.  Al contrario, se si chiama un costruttore nel codice, quasi sempre il risultato del costruttore viene utilizzato per impostare una variabile sull'istanza creata, in modo che sia possibile fare riferimento all'istanza nel codice in un secondo momento.  Per fornire accesso standard agli oggetti creati tramite una definizione del markup, in XAML viene definito l'[attributo x:Name](../../../../docs/framework/xaml-services/x-name-directive.md).  È possibile impostare il valore dell'attributo `x:Name` in qualsiasi elemento oggetto.  All'interno del code\-behind, l'identificatore scelto è equivalente a una variabile dell'istanza che fa riferimento all'istanza costruita.  Gli elementi denominati funzionano sotto ogni aspetto come istanze dell'oggetto \(il nome fa riferimento a tale istanza\) e il code\-behind può fare riferimento agli elementi denominati per gestire le interazioni di runtime all'interno dell'applicazione.  Questa connessione tra istanze e variabili viene effettuata tramite il compilatore di markup XAML WPF e più specificatamente coinvolge funzionalità e modelli non approfonditi in questo argomento, ad esempio <xref:System.Windows.Markup.IComponentConnector.InitializeComponent%2A>.  
  
 Gli elementi XAML [a livello di framework WPF](GTMT) ereditano una proprietà <xref:System.Windows.FrameworkElement.Name%2A>, che equivale all'attributo `x:Name` definito in XAML.  Altre classi forniscono equivalenti a livello di proprietà per `x:Name`, che in genere viene definito anche come proprietà `Name`.  In generale se non è possibile individuare una proprietà `Name` nella tabella dei membri dell'elemento o del tipo scelto, utilizzare `x:Name` in alternativa.  I valori `x:Name` forniranno a un elemento XAML un identificatore che può essere utilizzato in fase di esecuzione dai sottosistemi specifici o dai metodi di utilità, ad esempio <xref:System.Windows.FrameworkElement.FindName%2A>.  
  
 Nell'esempio seguente, viene impostata la proprietà <xref:System.Windows.FrameworkElement.Name%2A> per un elemento <xref:System.Windows.Controls.StackPanel>.  Quindi un gestore di un <xref:System.Windows.Controls.Button> all'interno di <xref:System.Windows.Controls.StackPanel> fa riferimento a <xref:System.Windows.Controls.StackPanel> tramite il relativo riferimento all'istanza `buttonContainer` impostato da <xref:System.Windows.FrameworkElement.Name%2A>.  
  
 [!code-xml[XAMLOvwSupport#NamedE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede)]  
[!code-xml[XAMLOvwSupport#NamedE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede2)]  
  
 [!code-csharp[XAMLOvwSupport#NameCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml.cs#namecode)]
 [!code-vb[XAMLOvwSupport#NameCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#namecode)]  
  
 Come accade per una variabile, il nome XAML di un'istanza è governato da un concetto di ambito, per cui è possibile attivare nomi che siano univoci all'interno di un determinato ambito prevedibile.  Il markup primario che definisce una pagina denota un NameScope XAML univoco, il cui limite è costituito dall'elemento radice della pagina.  Altre origini di markup, tuttavia, possono interagire con una pagina in fase di esecuzione, ad esempio gli stili o i modelli all'interno degli stili, e tali origini di markup spesso dispongono di NameScope XAML propri non necessariamente connessi al NameScope XAML della pagina.  Per ulteriori informazioni su `x:Name` e i NameScope XAML, vedere <xref:System.Windows.FrameworkElement.Name%2A>, [Direttiva x:Name](../../../../docs/framework/xaml-services/x-name-directive.md) o [NameScope XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md).  
  
<a name="attached_properties_and_attached_events"></a>   
## Proprietà ed eventi associati  
 XAML specifica una funzionalità del linguaggio che consente di specificare determinati eventi o proprietà in qualsiasi elemento, indipendentemente dalla presenza della proprietà o dell'evento all'interno delle definizioni del tipo per l'elemento per cui è impostato l'evento o la proprietà.  La versione delle proprietà di questa funzionalità è denominata [proprietà associata](GTMT), la versione degli eventi è denominata [evento associato](GTMT).  Concettualmente, è possibile pensare alle proprietà associate e agli eventi associati come a membri globali che possono essere impostati in qualsiasi elemento o istanza di oggetto XAML.  Tuttavia, tale elemento, classe o infrastruttura più ampia dovrà supportare un archivio delle proprietà di supporto per i valori associati.  
  
 Le proprietà associate in XAML vengono in genere utilizzate tramite la sintassi per attributi.  Per specificare una proprietà associata in questa sintassi, è necessario utilizzare la forma *tipoProprietario*.*nomeProprietà*.  
  
 In apparenza, assomiglia all'utilizzo di un elemento proprietà, tuttavia in questo caso il *tipoProprietario* che si specifica è sempre un tipo diverso rispetto all'elemento oggetto nel quale è impostata la proprietà associata.  *tipoProprietario* è il tipo che fornisce i metodi della funzione di accesso richiesti da un processore XAML per ottenere o impostare il valore della proprietà associata.  
  
 Lo scenario più comune per le proprietà associate consiste nel consentire agli elementi figlio di segnalare un valore di proprietà al relativo elemento padre.  
  
 Nell'esempio seguente viene illustrata la proprietà associata <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>.  La classe <xref:System.Windows.Controls.DockPanel> definisce le funzioni di accesso per <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> e pertanto possiede la proprietà associata.  La classe <xref:System.Windows.Controls.DockPanel> include inoltre la logica che scorre i relativi elementi figlio e verifica in modo specifico in ogni elemento la presenza di un valore impostato di <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>.  Se individuato, quel valore viene utilizzato durante il layout per posizionare gli elementi figlio.  L'utilizzo della proprietà associata <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> e questa funzionalità di posizionamento rappresentano infatti lo scenario opportuno per la classe <xref:System.Windows.Controls.DockPanel>.  
  
 [!code-xml[XAMLOvwSupport#DockAP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#dockap)]  
  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] la maggior parte o tutte le proprietà associate sono implementate anche come [proprietà di dipendenza](GTMT).  Per informazioni dettagliate, vedere [Cenni preliminari sulle proprietà associate](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
 Gli eventi associati utilizzano una forma di sintassi per attributi *tipoProprietario*.*nomeEvento* simile.  Come per gli eventi non associati, il valore dell'attributo per un evento associato in XAML specifica il nome del metodo di gestione richiamato quando l'evento viene gestito nell'elemento.  Gli utilizzi di eventi associati in XAML WPF sono meno comuni.  Per ulteriori informazioni, vedere [Cenni preliminari sugli eventi associati](../../../../docs/framework/wpf/advanced/attached-events-overview.md).  
  
<a name="base_classes_and_xaml"></a>   
## Tipi di base e XAML  
 Il markup XAML WPF sottostante e il relativo spazio dei nomi XAML sono una raccolta di tipi corrispondenti a oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], nonché a elementi di markup da utilizzare in XAML.  Tuttavia non è possibile eseguire il mapping di tutte le classi agli elementi.  Classi astratte come <xref:System.Windows.Controls.Primitives.ButtonBase> e alcune classi di base non astratte vengono utilizzate per l'ereditarietà nel modello a oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)].  Le classi di base, incluse quelle astratte, continuano a essere importanti per lo sviluppo di XAML, in quanto ciascuno degli elementi XAML concreti eredita i membri da una classe di base nella relativa gerarchia.  Spesso tali membri includono proprietà che possono essere impostate come attributi nell'elemento oppure eventi che possono essere gestiti.  <xref:System.Windows.FrameworkElement> è la classe di base concreta dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a [livello di framework WPF](GTMT).  Durante la progettazione dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], si utilizzano diverse classi Shape, Panel, Decorator oppure Control, che derivano tutte da <xref:System.Windows.FrameworkElement>.  Una classe di base correlata, <xref:System.Windows.FrameworkContentElement>, supporta elementi orientati al documento utili per una presentazione del layout di flusso, mediante le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] che eseguono il mirroring delle [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] in <xref:System.Windows.FrameworkElement>.  La combinazione di attributi a livello di elemento e di un modello a oggetti [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] fornisce un set di proprietà comuni che è possibile impostare nella maggior parte degli elementi XAML concreti, indipendentemente dall'elemento XAML specifico e dal relativo tipo sottostante.  
  
<a name="xaml_security"></a>   
## Sicurezza XAML  
 XAML è un linguaggio di markup che rappresenta direttamente la creazione di istanze di oggetti e la relativa esecuzione.  Gli elementi creati in XAML, pertanto, hanno la stessa capacità di interagire con risorse di sistema \(quali accesso di rete e IO file system\) del codice generato equivalente.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] supporta la [!INCLUDE[TLA#tla_cas](../../../../includes/tlasharptla-cas-md.md)] del framework di sicurezza [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].  Di conseguenza, il contenuto [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] in esecuzione nell'area Internet dispone di autorizzazioni di esecuzione ridotte.    In questa area Internet vengono in genere eseguiti il codice "XAML separato", ovvero pagine di XAML non compilato interpretato in fase di caricamento da parte di un visualizzatore XAML, e l'[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)], che utilizzano lo stesso set di autorizzazioni.  Il codice XAML caricato in un'applicazione completamente attendibile, tuttavia, dispone dello stesso accesso alle risorse di sistema dell'applicazione host.  Per ulteriori informazioni, vedere [Sicurezza con attendibilità parziale in WPF](../../../../docs/framework/wpf/wpf-partial-trust-security.md).  
  
<a name="loading_xaml_from_code"></a>   
## Caricamento di XAML dal codice  
 Sebbene sia possibile utilizzare XAML per definire un'interfaccia utente completa, è talvolta opportuno definire solo una parte dell'interfaccia utente tramite XAML.  Questa funzionalità può risultare utile per consentire una personalizzazione parziale, l'archiviazione locale di informazioni, l'utilizzo di XAML per fornire un oggetto business o per molti altri scenari possibili.  La chiave per questi scenari è la classe <xref:System.Windows.Markup.XamlReader> e il relativo metodo <xref:System.Windows.Markup.XamlReader.Load%2A>.  L'input è un file XAML, mentre l'output è un oggetto che rappresenta l'intera struttura ad albero di oggetti di runtime creata dal markup.  È possibile quindi inserire l'oggetto in modo che sia una proprietà di un altro oggetto già esistente nell'applicazione.  Se la proprietà è una proprietà appropriata nel modello di contenuto che dispone di funzionalità di visualizzazione e che notifica al motore di esecuzione che è stato aggiunto nuovo contenuto nell'applicazione, è possibile modificare in modo piuttosto semplice il contenuto di un'applicazione in esecuzione tramite il caricamento in XAML.  Notare che questa funzionalità in genere è disponibile solo nelle applicazioni con attendibiiltà completa, a causa delle ovvie implicazioni di sicurezza del caricamento di file all'interno delle applicazioni in esecuzione.  
  
<a name="whats_next"></a>   
## Argomenti successivi  
 In questo argomento viene fornita un'introduzione di base ai concetti e alla terminologia correlati alla sintassi XAML come applicata in WPF.  Per ulteriori informazioni sui termini utilizzati in questo argomento, vedere [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md).  
  
 Nel caso in cui non sia ancora stato fatto, è possibile svolgere i passaggi dell'esercitazione [Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md).  Durante la creazione dell'applicazione basata sul markup descritta nell'esercitazione, l'esercizio consentirà di approfondire molti dei concetti trattati in questo argomento.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] utilizza un particolare modello dell'applicazione basato sulla classe <xref:System.Windows.Application>.  Per informazioni dettagliate, vedere [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
 In [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md) vengono forniti maggiori dettagli su come compilare applicazioni che includono XAML utilizzando la riga di comando e [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)].  
  
 In [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md) vengono fornite ulteriori informazioni sulla versatilità delle proprietà in [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e viene introdotto il concetto di [proprietà di dipendenza](GTMT).  
  
## Vedere anche  
 [Descrizione dettagliata della sintassi XAML](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)   
 [Classi XAML e personalizzate per WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)   
 [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [Estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [Cenni preliminari sugli elementi di base](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [Strutture ad albero in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)