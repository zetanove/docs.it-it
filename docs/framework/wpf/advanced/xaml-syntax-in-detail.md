---
title: "Descrizione dettagliata della sintassi XAML | Microsoft Docs"
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
  - "XML, spazi dei nomi"
  - "XAML, analisi degli attributi"
  - "analisi degli attributi"
  - "Estensioni di markup XAML"
  - "proprietà associate"
  - "sintassi dei tag [XAML]"
  - "estensioni di markup"
  - "Sintassi dell'elemento oggetto XAML"
  - "Terminologia della sintassi XAML"
  - "eventi associati"
  - "semantica di ricerca"
  - "XAML, gli eventi associati"
  - "XAML, la sintassi del contenuto"
  - "XAML, la semantica di ricerca"
  - "sintassi di contenuto"
  - "sintassi degli elementi oggetto"
  - "terminologia di sintassi [XAML]"
  - "XAML, le proprietà associate"
  - "attributi [XAML], l'analisi"
  - "XAML, la sintassi di tag"
  - "XAML, la sintassi degli attributi"
  - "sintassi degli elementi di proprietà"
  - "terminologia [XAML]"
  - "spazi dei nomi XML"
  - "sintassi di attributo [XAML]"
  - "XAML, la sintassi degli elementi"
ms.assetid: 67cce290-ca26-4c41-a797-b68aabc45479
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# Descrizione dettagliata della sintassi XAML
In questo argomento definisce le condizioni che vengono utilizzate per descrivere gli elementi della sintassi XAML. Questi termini vengono utilizzati di frequente in tutto il resto di questa documentazione, sia per la documentazione di WPF in modo specifico e per gli altri modelli che utilizzano XAML o i concetti di base XAML abilitati per il supporto del linguaggio XAML a livello di System. Xaml. In questo argomento consente di espandere la terminologia di base presentata nell'argomento [Cenni preliminari su XAML (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).  
  

  
<a name="the_xaml_language_specification"></a>   
## <a name="the-xaml-language-specification"></a>Specifica del linguaggio XAML  
 La terminologia della sintassi XAML definita in questa sezione viene inoltre definita o a cui fa riferimento nella specifica del linguaggio XAML. XAML è un linguaggio basato su XML e segue o si espande sulla regole strutturali XML. Alcuni termini è condiviso da o si basa sulla terminologia comunemente utilizzata per descrivere il linguaggio XML o il modello a oggetti documento XML.  
  
 Per ulteriori informazioni sulla specifica del linguaggio XAML, scaricare [ \[MS-XAML\] ](http://go.microsoft.com/fwlink/?LinkId=114525) dal Microsoft Download Center.  
  
<a name="xaml_and_clr"></a>   
## <a name="xaml-and-clr"></a>XAML e CLR  
 XAML è un linguaggio di markup. Il [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)], come suggerito dal nome, consente di esecuzione. XAML non è da solo uno dei linguaggi comuni utilizzati direttamente dal runtime CLR. Invece, può essere considerato di XAML come il proprio sistema di tipi di supporto. Il sistema di analisi XAML specifico che viene usato da WPF si basa su Common Language Runtime e il sistema di tipi CLR. Tipi XAML vengono mappati ai tipi CLR per creare un'istanza di una rappresentazione di runtime quando viene analizzato il codice XAML per WPF. Per questo motivo, il resto della discussione di sintassi in questo documento includerà i riferimenti al sistema di tipi CLR, anche se non le discussioni sintassi equivalente della specifica del linguaggio XAML. (Per ogni livello di specifica del linguaggio XAML, XAML tipi possono essere mappati a qualsiasi altro sistema di tipi, che non deve essere CLR, ma che richiedono la creazione e utilizzo di un parser XAML.)  
  
#### <a name="members-of-types-and-class-inheritance"></a>Membri di tipi ed ereditarietà delle classi  
 Le proprietà e gli eventi visualizzati come membri XAML di un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] tipo spesso vengono ereditate dai tipi di base. Ad esempio, si consideri l'esempio: `<Button Background="Blue" .../>`. Il <xref:System.Windows.Controls.Control.Background%2A> proprietà non è una proprietà dichiarata immediatamente nel <xref:System.Windows.Controls.Button> classe, se analizzano la definizione della classe, i risultati di reflection o la documentazione. Al contrario, <xref:System.Windows.Controls.Control.Background%2A> viene ereditato dalla base <xref:System.Windows.Controls.Control> (classe).  
  
 Il comportamento dell'ereditarietà di classe [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elementi XAML è un'importante variazione rispetto un'interpretazione del markup XML applicata a livello di schema. Ereditarietà di classe possono diventare complesse, in particolare quando le classi di base intermedie sono astratte o quando sono interessate le interfacce. Questo è il motivo che il set di elementi XAML e dei relativi attributi consentiti è difficile da rappresentare in modo accurato e completo utilizzando i tipi di schema che viene in genere utilizzato per [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] di programmazione, ad esempio formato XSD o DTD. Un altro motivo è che estendibilità e mapping dei tipi di funzionalità del linguaggio XAML stesso precludono completezza di qualsiasi rappresentazione fissa dei tipi consentiti e i membri.  
  
<a name="object_element_syntax"></a>   
## <a name="object-element-syntax"></a>Sintassi degli elementi oggetto  
 *La sintassi degli elementi dell'oggetto* è la sintassi di markup XAML che crea un'istanza di una classe CLR o una struttura dichiarando un elemento XML. Questa sintassi è simile alla sintassi degli elementi di altri linguaggi di markup, ad esempio HTML. La sintassi degli elementi oggetto inizia con una parentesi uncinata aperta (\<), followed immediately by the type name of the class or structure being instantiated. followed="" immediately="" by="" the="" type="" name="" of="" the="" class="" or="" structure="" being="">\</), followed immediately by the type name of the class or structure being instantiated.> Zero o più spazi possono seguire il nome del tipo e zero o più attributi possono anche essere dichiarati nell'elemento oggetto, con uno o più spazi separando ogni nome di attributo = coppia "value". Infine, uno dei seguenti deve essere true:  
  
-   L'elemento e il tag deve essere chiuso da una barra (/) seguita immediatamente da una parentesi uncinata chiusa (>).  
  
-   Il tag di apertura deve essere completato da una parentesi uncinata chiusa (>). Altri elementi oggetto, proprietà o testo interno, è possibile seguire il tag di apertura. Il contenuto esatto che è possibile in questo caso è generalmente vincolato dal modello a oggetti dell'elemento. L'equivalente di tag di chiusura per l'elemento oggetto deve inoltre esistere nella nidificazione appropriata e bilanciato con altre coppie di tag di apertura e chiusura.  
  
 XAML come implementato dalla .NET dispone di un set di regole di mapping degli elementi oggetto in tipi, attributi di proprietà o eventi e spazi dei nomi XAML per gli spazi dei nomi CLR e assembly. Per WPF e .NET Framework, gli elementi oggetto XAML eseguire il mapping a [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] fare riferimento ai tipi come definito nell'assembly e gli attributi vengono associati ai membri di tali tipi. Quando si fa riferimento a un tipo CLR in XAML, è possibile accedere ai membri ereditati di tale tipo.  
  
 Ad esempio, nell'esempio seguente è la sintassi degli elementi oggetto che crea una nuova istanza di <xref:System.Windows.Controls.Button> e inoltre specifica un <xref:System.Windows.FrameworkElement.Name%2A> attributo e un valore per l'attributo:  
  
 [!code-xml[XAMLOvwSupport#SyntaxOE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxoe)]  
  
 Nell'esempio seguente è la sintassi degli elementi oggetto che include anche la sintassi di proprietà di contenuto XAML. Il testo interno contenuto verrà utilizzato per impostare il <xref:System.Windows.Controls.TextBox> proprietà di contenuto XAML, <xref:System.Windows.Controls.TextBox.Text%2A>.  
  
 [!code-xml[XAMLOvwSupport#ThisIsATextBox](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#thisisatextbox)]  
  
### <a name="content-models"></a>Modelli di contenuto  
 Una classe potrebbe supportare un utilizzo come un elemento oggetto XAML in termini di sintassi, ma tale elemento funzionerà correttamente in un'applicazione o pagina solo quando viene posizionato in una posizione prevista di un albero del modello o un elemento contenuto globale. Ad esempio, un <xref:System.Windows.Controls.MenuItem> devono in genere essere inserite solo come figlio di un <xref:System.Windows.Controls.Primitives.MenuBase> classe derivata, ad esempio <xref:System.Windows.Controls.Menu>. Modelli per elementi specifici sono documentati come parte delle note nelle pagine delle classi per i controlli e altri contenuti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] classi che possono essere utilizzate come elementi XAML.  
  
<a name="properties_of_object_elements"></a>   
## <a name="properties-of-object-elements"></a>Proprietà degli elementi oggetto  
 Proprietà in XAML vengono impostate da una varietà di sintassi possibili. Sintassi può essere utilizzata per una particolare proprietà varia in base alle caratteristiche di sistema tipo sottostante della proprietà da impostare.  
  
 Impostando i valori delle proprietà, aggiungere funzionalità o caratteristiche agli oggetti in cui si trovano nell'oggetto grafico fase di esecuzione. Lo stato iniziale dell'oggetto creato da un elemento oggetto si basa il comportamento del costruttore predefinito. In genere, l'applicazione utilizzerà un valore diverso da un'istanza completamente predefinita di un qualsiasi oggetto specificato.  
  
<a name="attribute_syntax_properties"></a>   
## <a name="attribute-syntax-properties"></a>Sintassi degli attributi (proprietà)  
 La sintassi degli attributi è la sintassi di markup XAML che imposta un valore per una proprietà dichiarando un attributo di un elemento oggetto esistente. Il nome dell'attributo deve corrispondere al nome di membro CLR della proprietà della classe che supporta l'elemento oggetto pertinente. Il nome dell'attributo è seguito da un operatore di assegnazione (=). Il valore dell'attributo deve essere una stringa racchiusa tra virgolette.  
  
> [!NOTE]
>  È possibile utilizzare le virgolette alterne per inserire un segno di virgolette letterale all'interno di un attributo. Ad esempio è possibile utilizzare le virgolette singole come mezzo per dichiarare una stringa che contiene un carattere di virgolette doppie all'interno di esso. Se si utilizzano virgolette singole o doppie, è necessario utilizzare una coppia corrispondente per l'apertura e chiusura di stringa del valore di attributo. Sono disponibili anche le sequenze di escape o altre tecniche per risolvere restrizioni dei caratteri imposto da una particolare sintassi XAML. Vedere [entità carattere XML e XAML](../../../../docs/framework/xaml-services/xml-character-entities-and-xaml.md).  
  
 Per poter essere impostato tramite la sintassi degli attributi, una proprietà deve essere pubblica e deve essere scrivibile. Il valore della proprietà nel sistema di tipi di backup deve essere un tipo di valore o deve essere un tipo di riferimento che può essere creata un'istanza o a cui fa riferimento un processore XAML durante l'accesso del tipo di backup.  
  
 Per gli eventi XAML WPF, l'evento che viene fatto riferimento come il nome dell'attributo deve essere pubblici e dispone di un delegato pubblico.  
  
 La proprietà o evento deve essere un membro della classe o struttura che viene creata un'istanza per l'elemento oggetto contenitore.  
  
### <a name="processing-of-attribute-values"></a>Elaborazione dei valori di attributo  
 Il valore stringa contenuto all'interno delle parentesi e virgolette di chiusura viene elaborato da un processore XAML. Per le proprietà, il comportamento di elaborazione predefinito è determinato dal tipo di proprietà CLR sottostante.  
  
 Il valore dell'attributo viene inserito uno dei seguenti, utilizzando questo ordine di elaborazione:  
  
1.  Se il processore XAML rileva una parentesi graffa o un elemento oggetto che deriva da <xref:System.Windows.Markup.MarkupExtension>, quindi l'estensione di markup di cui viene fatto riferimento viene valutata per prima anziché il valore sotto forma di stringa di elaborazione e l'oggetto restituito dall'estensione di markup viene utilizzato come valore. In molti casi l'oggetto restituito da un'estensione di markup è un riferimento a un oggetto esistente o un'espressione che rinvia la valutazione in fase di esecuzione, non è un oggetto appena creata un'istanza.  
  
2.  Se viene dichiarata la proprietà con un oggetto con attributi <xref:System.ComponentModel.TypeConverter>, o il tipo di valore di tale proprietà viene dichiarato con un oggetto con attributi <xref:System.ComponentModel.TypeConverter>, il valore di stringa dell'attributo viene inviato al convertitore di tipi come input una conversione e il convertitore restituirà una nuova istanza dell'oggetto.  
  
3.  Se è presente alcun <xref:System.ComponentModel.TypeConverter>, viene tentata una conversione diretta per il tipo di proprietà. Questo livello finale è una conversione diretta dal valore di codice nativo del parser tra tipi primitivi del linguaggio XAML o una ricerca per i nomi di costanti denominate in un'enumerazione (il parser accede quindi i valori corrispondenti).  
  
#### <a name="enumeration-attribute-values"></a>Valori di attributo (enumerazione)  
 Enumerazioni in XAML vengono elaborate intrinsecamente dai parser XAML e i membri di un'enumerazione devono essere specificati, specificando il nome della stringa di una delle costanti dell'enumerazione.  
  
 Per valori di enumerazione nonflag, il comportamento nativo è per elaborare la stringa del valore di attributo e risolverla in uno dei valori di enumerazione. Non si specifica l'enumerazione nel formato *enumerazione*.*Valore*, come avviene nel codice. È invece necessario specificare solo *valore*, e *enumerazione* viene dedotto dal tipo di proprietà sta impostando. Se si specifica un attributo di *enumerazione*.*Valore* , non verrà risolto correttamente.  
  
 Per le enumerazioni, il comportamento dipende il <xref:System.Enum.Parse%2A?displayProperty=fullName> metodo. È possibile specificare più valori per un'enumerazione basata su flag separando ciascun valore con una virgola. Tuttavia, non è possibile combinare i valori di enumerazione non basati su flag. Ad esempio, è possibile utilizzare la sintassi della virgola per tentare di creare un <xref:System.Windows.Trigger> che agisce su più condizioni di un'enumerazione:  
  
```  
<!--This will not compile, because Visibility is not a flagwise enumeration.-->  
...  
<Trigger Property="Visibility" Value="Collapsed,Hidden">  
  <Setter ... />  
</Trigger>  
...  
```  
  
 Le enumerazioni che supportano gli attributi che possono essere impostati in XAML sono rare in WPF. Tuttavia, è un'enumerazione di questo tipo è <xref:System.Windows.Media.StyleSimulations>. È possibile, ad esempio, utilizzare la sintassi di delimitato da virgole di attributi basata su flag per modificare l'esempio fornito nella sezione Osservazioni per la <xref:System.Windows.Documents.Glyphs> classe; `StyleSimulations = "BoldSimulation"` potrebbe diventare `StyleSimulations = "BoldSimulation,ItalicSimulation"`. <xref:System.Windows.Input.KeyBinding.Modifiers%2A?displayProperty=fullName> è un'altra proprietà in cui può essere specificato più di un valore di enumerazione. Tuttavia, questa proprietà risulta essere un caso speciale, poiché il <xref:System.Windows.Input.ModifierKeys> enumerazione supporta un convertitore. Il convertitore di tipi per i modificatori utilizza un segno più (+) come delimitatore, anziché una virgola (,). Questa conversione supporta la sintassi più tradizionale per rappresentare le combinazioni di tasti nella programmazione di Microsoft Windows, ad esempio "Ctrl + Alt".  
  
### <a name="properties-and-event-member-name-references"></a>Le proprietà e i riferimenti ai nomi di membro di evento  
 Quando si specifica un attributo, è possibile fare riferimento a qualsiasi proprietà o evento esistente come membro del tipo CLR che è creata un'istanza dell'elemento oggetto contenitore.  
  
 In alternativa, è possibile fare riferimento a una proprietà associata o evento associato, indipendente dell'elemento oggetto contenitore. (In una sezione successiva vengono illustrate le proprietà associate).  
  
 È inoltre possibile assegnare un nome qualsiasi evento di qualsiasi oggetto che è accessibile tramite lo spazio dei nomi predefinito mediante un *typeName*.*evento* nome parziale, questa sintassi supporta l'associazione di gestori per gli eventi indirizzati in cui il gestore è progettato per gestire l'evento indirizzato da elementi figlio, ma l'elemento padre non tale evento è presente nella relativa tabella dei membri. Questa sintassi è simile alla sintassi di un evento associato, ma in questo caso l'evento non è un evento associato effettivo. Al contrario, si fa riferimento a un evento con un nome completo. Per ulteriori informazioni, vedere [Cenni preliminari sugli eventi indirizzati](../../../../docs/framework/wpf/advanced/routed-events-overview.md).  
  
 In alcuni scenari, i nomi delle proprietà sono a volte disponibili come valore di un attributo, anziché il nome dell'attributo. Nome di tale proprietà può includere anche qualificatori, ad esempio la proprietà specificata nel formato *TipoProprietario*.*dependencyPropertyName*. Questo scenario è comune quando si scrivono stili o modelli in XAML. Le regole di elaborazione per i nomi di proprietà forniti come valore di attributo sono diverse e dipendono dal tipo di impostazione della proprietà o i comportamenti di particolari sottosistemi WPF. Per informazioni dettagliate, vedere [di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md).  
  
 Un altro utilizzo di nomi di proprietà è quando un valore di attributo descrive una relazione proprietà-proprietà. Questa funzionalità viene utilizzata per l'associazione dati e per le destinazioni di storyboard ed è abilitata per il <xref:System.Windows.PropertyPath> classe e il convertitore. Per una descrizione più completa della semantica di ricerca, vedere [sintassi XAML di PropertyPath](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md).  
  
<a name="property_element_syntax"></a>   
## <a name="property-element-syntax"></a>La sintassi degli elementi  
 *La sintassi degli elementi* certi versi dalle regole di sintassi XML base per gli elementi. In XML, il valore di un attributo è una stringa standard de facto, con la sola possibile variazione viene utilizzato il formato di codifica di stringa. In XAML, è possibile assegnare altri elementi oggetto come valore di una proprietà. Questa funzionalità è abilitata per la sintassi. Anziché la proprietà viene specificata come un attributo all'interno del tag di elemento, la proprietà viene specificata utilizzando un elemento di apertura di tag in *nomeTipoElemento*.*propertyName* form, il valore della proprietà viene specificato all'interno e quindi viene chiuso l'elemento di proprietà.  
  
 In particolare, la sintassi inizia con una parentesi uncinata aperta (\<), followed immediately by the type name of the class or structure that the property element syntax is contained within. followed="" immediately="" by="" the="" type="" name="" of="" the="" class="" or="" structure="" that="" the="" property="" element="" syntax="" is="" contained="">\</), followed immediately by the type name of the class or structure that the property element syntax is contained within.> Questo è immediatamente seguito da un punto singolo (.), quindi dal nome di una proprietà, quindi da una parentesi uncinata chiusa (>). Come con la sintassi degli attributi, tale proprietà deve esistere all'interno i membri pubblici dichiarati nel tipo specificato. Il valore da assegnare alla proprietà è contenuto all'interno dell'elemento di proprietà. In genere, il valore viene assegnato come uno o più elementi oggetto, perché gli oggetti come valori è lo scenario che la sintassi degli elementi è destinato all'indirizzo. Infine, un tag di chiusura equivalente che specifica la stessa *nomeTipoElemento*.*propertyName* combinazione deve essere specificata, in opportunamente annidato e bilanciato con gli altri tag di elemento.  
  
 Ad esempio, ecco la sintassi degli elementi di proprietà per il <xref:System.Windows.FrameworkElement.ContextMenu%2A> proprietà di un <xref:System.Windows.Controls.Button>.  
  
 [!code-xml[XAMLOvwSupport#ContextMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#contextmenu)]  
  
 Il valore all'interno di un elemento di proprietà può anche essere fornito come testo interno, nei casi in cui il tipo della proprietà specificato è un tipo di valore primitivo, ad esempio <xref:System.String>, o un'enumerazione in cui viene specificato un nome. Questi due utilizzi sono molto comuni, perché ognuno di questi casi anche possibile utilizzare una semplice sintassi di attributo. Uno scenario per riempire un elemento di proprietà con una stringa per le proprietà che non sono proprietà di contenuto XAML, ma vengono ancora utilizzate per la rappresentazione testo dell'interfaccia utente, e determinati elementi di spazio, ad esempio caratteri di avanzamento riga sono necessarie da inserire nel testo dell'interfaccia utente. La sintassi degli attributi non consente di mantenere gli avanzamenti riga, ma la sintassi degli elementi possono, purché il mantenimento degli spazi vuoti significativi sia attivo (per informazioni dettagliate, vedere [Whitespace Processing in XAML](../../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)). È un altro scenario in modo che [direttiva X:UID](../../../../docs/framework/xaml-services/x-uid-directive.md) può essere applicato all'elemento property e contrassegnare quindi il valore all'interno di un valore che deve essere localizzato in WPF output BAML o da altre tecniche.  
  
 Nell'albero logico WPF non è rappresentato un elemento di proprietà. Un elemento della proprietà è semplicemente una sintassi particolare per l'impostazione di una proprietà e non è un elemento che dispone di un'istanza o un oggetto il backup. (Per informazioni dettagliate sul concetto di albero logico, vedere [Trees in WPF](../../../../docs/framework/wpf/advanced/trees-in-wpf.md).)  
  
 Per le proprietà in cui sono supportati sia l'attributo sia proprietà sintassi degli elementi, la due sintassi in genere hanno lo stesso risultato, anche se possono variare leggermente sfumature, ad esempio gestione degli spazi vuoti tra i tipi di sintassi.  
  
<a name="collection_syntax"></a>   
## <a name="collection-syntax"></a>Sintassi della raccolta  
 La specifica XAML richiede che le implementazioni del processore XAML per identificare le proprietà in cui il tipo di valore è una raccolta. Implementazione del processore XAML generale in .NET è basato sul codice gestito e il CLR e identifica i tipi di raccolta tramite uno dei seguenti:  
  
-   Il tipo implementa <xref:System.Collections.IList>.  
  
-   Il tipo implementa <xref:System.Collections.IDictionary>.  
  
-   Tipo deriva da <xref:System.Array> (per ulteriori informazioni sulle matrici in XAML, vedere [estensione di Markup X:Array](../../../../docs/framework/xaml-services/x-array-markup-extension.md).)  
  
 Se il tipo di una proprietà è una raccolta, il tipo di insieme dedotto è necessario specificare nel markup come elemento oggetto. Gli elementi che devono essere gli elementi nella raccolta vengono invece specificati come uno o più elementi figlio dell'elemento di proprietà. Ognuno di questi elementi viene valutata a un oggetto durante il caricamento e aggiunto alla raccolta chiamando il `Add` dell'insieme implicito. Ad esempio, il <xref:System.Windows.Style.Triggers%2A> proprietà di <xref:System.Windows.Style> accetta il tipo di insieme specializzato <xref:System.Windows.TriggerCollection>, che implementa l'interfaccia <xref:System.Collections.IList>. Non è necessario creare un'istanza di un <xref:System.Windows.TriggerCollection> elemento oggetto nel markup. È invece necessario specificare uno o più <xref:System.Windows.Trigger> elementi come elementi all'interno di `Style.Triggers` elemento proprietà, in cui <xref:System.Windows.Trigger> (o una classe derivata) è il tipo previsto come tipo di elemento fortemente tipizzato e implicito <xref:System.Windows.TriggerCollection>.  
  
 [!code-xml[XAMLOvwSupport#SyntaxPECollection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxpecollection)]  
  
 Una proprietà può essere sia un tipo di raccolta e la proprietà di contenuto XAML per il tipo e tipi derivati, come descritto nella sezione successiva di questo argomento.  
  
 Un elemento insieme implicito crea un membro nella rappresentazione dell'albero logico, anche se non viene visualizzato nel markup come elemento. In genere il costruttore del tipo padre esegue la creazione di istanze per la raccolta che è una delle relative proprietà e l'insieme inizialmente vuoto diventa parte dell'albero di oggetti.  
  
> [!NOTE]
>  L'elenco e il dizionario di interfacce generiche (<xref:System.Collections.Generic.IList%601> e <xref:System.Collections.Generic.IDictionary%602>) non sono supportate per il rilevamento della raccolta.\</TKey, TValue> Tuttavia, è possibile utilizzare il <xref:System.Collections.Generic.List%601> classe come classe base, poiché implementa <xref:System.Collections.IList> , direttamente o <xref:System.Collections.Generic.Dictionary%602> come classe base, poiché implementa <xref:System.Collections.IDictionary> direttamente.\</TKey, TValue>  
  
 Nelle pagine di riferimento di .NET per i tipi di raccolta, questa sintassi con l'omissione intenzionale dell'elemento oggetto per una raccolta si nota occasionalmente nelle sezioni di sintassi XAML come sintassi per insiemi implicita.  
  
 Fatta eccezione per l'elemento radice, ogni elemento oggetto in un file XAML nidificati come elemento figlio di un altro elemento rappresenta in realtà uno o entrambi i casi seguenti: un membro di una proprietà di raccolta implicita del relativo elemento padre o un elemento che specifica il valore della proprietà di contenuto XAML per l'elemento padre (XAML contenuto verranno descritte le proprietà di una sezione successiva). In altre parole, la relazione tra gli elementi padre e figlio in una pagina di markup è realmente un singolo oggetto nella directory principale e ogni elemento oggetto sotto la radice rappresenta una singola istanza che fornisce un valore della proprietà dell'elemento padre, o uno degli elementi all'interno di una raccolta che è anche un valore di proprietà di tipo di raccolta dell'elemento padre. Questo concetto di radice singola è comune in XML e viene spesso rafforzato il comportamento delle API che caricano XAML, ad esempio <xref:System.Windows.Markup.XamlReader.Load%2A>.  
  
 Nell'esempio seguente viene illustrata una sintassi con l'elemento oggetto per una raccolta (<xref:System.Windows.Media.GradientStopCollection>) specificato in modo esplicito.  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <GradientStopCollection>  
      <GradientStop Offset="0.0" Color="Red" />  
      <GradientStop Offset="1.0" Color="Blue" />  
    </GradientStopCollection>  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
 Si noti che non sempre è possibile dichiarare in modo esplicito la raccolta. Ad esempio, tenta di dichiarare <xref:System.Windows.TriggerCollection> in modo esplicito illustrato in precedenza <xref:System.Windows.Style.Triggers%2A> esempio avrà esito negativo. Dichiarare in modo esplicito la raccolta richiede che la classe di raccolta deve supportare un costruttore predefinito, e <xref:System.Windows.TriggerCollection> non dispone di un costruttore predefinito.  
  
<a name="xaml_content_properties"></a>   
## <a name="xaml-content-properties"></a>Proprietà di contenuto XAML  
 Sintassi del contenuto XAML è una sintassi che è disponibile solo nelle classi che specificano il <xref:System.Windows.Markup.ContentPropertyAttribute> come parte della relativa dichiarazione di classe. Il <xref:System.Windows.Markup.ContentPropertyAttribute> fa riferimento il nome della proprietà che è la proprietà di contenuto per quel tipo di elemento (incluse le classi derivate). Quando vengono elaborati da un processore XAML, tutti gli elementi figlio o testo interno rilevato tra i tag di apertura e chiusura dell'elemento oggetto verrà assegnato il valore della proprietà di contenuto XAML per l'oggetto. È consentito specificare elementi di proprietà esplicita per la proprietà di contenuto, ma questo utilizzo non è in genere illustrato nelle sezioni sintassi XAML di riferimento di .NET. La tecnica esplicita/dettagliata ha un valore occasionale per maggiore chiarezza del codice o lo stile del markup, ma in genere l'intento di una proprietà di contenuto è semplificare il codice in modo che gli elementi correlati intuitivamente come padre-figlio possono essere annidati direttamente. Tag di elemento di proprietà per le altre proprietà su un elemento non viene assegnato come "contenuto" per una definizione di linguaggio XAML strict. essi vengono elaborati in precedenza nell'ordine di elaborazione del parser XAML e non sono considerati "contenuto".  
  
### <a name="xaml-content-property-values-must-be-contiguous"></a>Valori di proprietà di contenuto XAML devono essere contigui  
 Il valore di una proprietà di contenuto XAML deve essere fornito completamente prima o completamente dopo qualsiasi altro elemento di proprietà in quell'elemento oggetto. Ciò è vero se il valore di una proprietà di contenuto XAML è specificato come una stringa o come uno o più oggetti. Ad esempio, non analizza il markup seguente:  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 Questa situazione non è consentita perché se questa sintassi fosse resa esplicita tramite la sintassi degli elementi per la proprietà di contenuto, quindi la proprietà di contenuto viene impostata due volte:  
  
```  
<Button>  
  <Button.Content>I am a </Button.Content>  
  <Button.Background>Blue</Button.Background>  
  <Button.Content> blue button</Button.Content>  
</Button>  
```  
  
 Un esempio è se la proprietà di contenuto è una raccolta, e gli elementi figlio sono frammisto a elementi di proprietà:  
  
```  
<StackPanel>  
  <Button>This example</Button>  
  <StackPanel.Resources>  
    <SolidColorBrush x:Key="BlueBrush" Color="Blue"/>  
  </StackPanel.Resources>  
  <Button>... is illegal XAML</Button>  
</StackPanel>  
```  
  
<a name="content_properties_and_collection_syntax_combined"></a>   
## <a name="content-properties-and-collection-syntax-combined"></a>Proprietà di contenuto e la sintassi di raccolta combinati  
 Per accettare più di un singolo elemento oggetto come contenuto, il tipo della proprietà di contenuto deve essere specificamente un tipo di raccolta. Simile alla sintassi degli elementi di proprietà per i tipi di raccolta, un processore XAML necessario identificare i tipi che sono tipi di raccolta. Se un elemento è una proprietà di contenuto XAML e il tipo della proprietà di contenuto XAML è una raccolta, il tipo di raccolta implicito non è necessario specificare nel markup come elemento oggetto e proprietà di contenuto XAML non è necessario essere specificato come un elemento di proprietà. Pertanto il modello di contenuto apparente nel markup può ora includere più di un elemento figlio assegnato come contenuto. Di seguito è riportata la sintassi del contenuto per un <xref:System.Windows.Controls.Panel> classe derivata. Tutti <xref:System.Windows.Controls.Panel> classi derivate stabiliscono le proprietà di contenuto XAML per essere <xref:System.Windows.Controls.Panel.Children%2A>, che richiede un valore di tipo <xref:System.Windows.Controls.UIElementCollection>.  
  
 [!code-xml[XAMLOvwSupport#SyntaxContent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page5.xaml#syntaxcontent)]  
  
 Si noti che né l'elemento di proprietà per <xref:System.Windows.Controls.Panel.Children%2A> né l'elemento per il <xref:System.Windows.Controls.UIElementCollection> necessario nel markup. Questa è una funzionalità di progettazione di XAML in modo che i contenuti in modo ricorsivo gli elementi che definiscono un [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] sono rappresentate in modo più intuitivo come una struttura ad albero di elementi annidati con relazioni padre-figlio immediate, senza tag di elemento proprietà o oggetti della raccolta. In effetti, <xref:System.Windows.Controls.UIElementCollection> non può essere specificato in modo esplicito nel markup come elemento oggetto in base alla progettazione. Poiché il solo utilizzo previsto è come raccolta implicita, <xref:System.Windows.Controls.UIElementCollection> non espone un costruttore predefinito pubblico e pertanto non può essere un'istanza come elemento oggetto.  
  
### <a name="mixing-property-elements-and-object-elements-in-an-object-with-a-content-property"></a>La combinazione di elementi di proprietà e gli elementi oggetto in un oggetto con una proprietà di contenuto  
 La specifica XAML dichiara che un processore XAML possa imporre che gli elementi oggetto utilizzati per compilare la proprietà di contenuto XAML all'interno di un elemento oggetto devono essere contigui e non devono essere combinati. Questa restrizione che limita la combinazione di elementi di proprietà e il contenuto viene applicata dal [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] processori XAML.  
  
 È possibile configurare un elemento oggetto figlio come primo markup all'interno di un elemento oggetto. È possibile introdurre elementi di proprietà. In alternativa, è possibile specificare uno o più elementi di proprietà, quindi e altri elementi di proprietà. Ma una volta che un elemento proprietà dopo il contenuto, è possibile inserire qualsiasi altro contenuto, è possibile aggiungere solo gli elementi di proprietà.  
  
 Questo contenuto / proprietà elemento ordine requisito non si applica al testo interno utilizzato come contenuto. Tuttavia, è ancora uno stile consigliabile mantenere il testo interno contigue, perché gli spazi vuoti significativi sarà difficili da rilevare visivamente nel markup se gli elementi di proprietà vengono intercalati con testo interno.  
  
<a name="xaml_namespaces"></a>   
## <a name="xaml-namespaces"></a>Spazi dei nomi XAML  
 Nessuno degli esempi di sintassi precedente specificato uno spazio dei nomi XAML diverso da spazio dei nomi XAML predefinito. Nelle tipiche [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] applicazioni, il valore predefinito dello spazio dei nomi XAML specificato è il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] dello spazio dei nomi. È possibile specificare spazi dei nomi XAML diverso da spazio dei nomi XAML predefinito e continuare a utilizzare la sintassi seguente. Quindi, in qualsiasi punto in cui viene denominata una classe che non è accessibile all'interno dello spazio dei nomi XAML predefinito, il nome della classe deve essere preceduto il prefisso dello spazio dei nomi XAML mappato allo spazio dei nomi CLR corrispondente. Ad esempio, `<custom:Example/>` è la sintassi degli elementi oggetto per creare un'istanza del `Example` (classe), in cui lo spazio dei nomi CLR che contiene tale classe (ed eventualmente le informazioni sull'assembly esterno che contiene i tipi di supporto) è stato precedentemente mappato al `custom` prefisso.  
  
 Per ulteriori informazioni sugli spazi dei nomi XAML, vedere [spazi dei nomi XAML e Namespace Mapping for WPF XAML](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md).  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>Estensioni di markup  
 XAML definisce un'estensione di markup di entità che costituisce un'alternativa la normale gestione processore XAML di valori di stringa degli attributi o elementi oggetto e rinvia l'elaborazione di una classe di supporto di programmazione. Il carattere che identifica un'estensione di markup in un processore XAML quando si utilizza la sintassi degli attributi è la parentesi graffa di apertura ({), seguita da qualsiasi carattere diverso da una parentesi graffa di chiusura (}). La prima stringa segue la parentesi graffa deve fare riferimento alla classe che fornisce il comportamento dell'estensione particolare, il riferimento in cui è possibile omettere la sottostringa "Estensione" se tale sottostringa fa parte del nome effettivo della classe. Successivamente, può risultare uno spazio, e quindi ogni carattere successivo viene utilizzato come input dall'implementazione dell'estensione, fino a quando viene rilevata la parentesi graffa di chiusura.  
  
 L'implementazione di XAML di .NET utilizza il <xref:System.Windows.Markup.MarkupExtension> classe astratta come base per tutte le estensioni di markup supportate da [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] nonché altri framework o tecnologie. Le estensioni di markup che [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] implementa specificatamente è spesso destinate a fornire un mezzo per fare riferimento ad altri oggetti esistenti o per rinviare riferimenti a oggetti che verranno valutati in fase di esecuzione. Ad esempio, una semplice associazione dati WPF viene eseguita specificando il `{Binding}` estensione di markup al posto del valore che in genere richiederebbe una particolare proprietà. Molte delle estensioni di markup WPF consentono una sintassi degli attributi per le proprietà in cui una sintassi degli attributi non sarebbe possibile. Ad esempio, un <xref:System.Windows.Style> oggetto è un tipo relativamente complesso che contiene una serie di oggetti e proprietà annidata. In WPF vengono in genere definiti come una risorsa in un <xref:System.Windows.ResourceDictionary>, quindi farvi riferimento tramite una delle due estensioni di markup WPF che richiedono una risorsa. L'estensione di markup posticipa la valutazione del valore della proprietà di ricerca di risorse e consente di specificare il valore di <xref:System.Windows.FrameworkElement.Style%2A> proprietà, che accetta il tipo <xref:System.Windows.Style>, nell'attributo sintassi come illustrato nell'esempio seguente:  
  
 `<Button Style="{StaticResource MyStyle}">My button</Button>`  
  
 In questo caso, `StaticResource` identifica il <xref:System.Windows.StaticResourceExtension> classe che fornisce l'implementazione dell'estensione di markup. La stringa successiva `MyStyle` viene utilizzato come input per il valore non predefinito <xref:System.Windows.StaticResourceExtension> costruttore, in cui il parametro accettato dalla stringa di estensione dichiara l'oggetto richiesto <xref:System.Windows.ResourceKey>. `MyStyle`è previsto che il [X:Key](../../../../docs/framework/xaml-services/x-key-directive.md) valore di un <xref:System.Windows.Style> definito come risorsa. Il [estensione di Markup StaticResource](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md) utilizzo richiede che la risorsa venga utilizzata per fornire la <xref:System.Windows.Style> valore della proprietà tramite la logica di ricerca di risorse statiche in fase di caricamento.  
  
 Per ulteriori informazioni sulle estensioni di markup, vedere [le estensioni di Markup e XAML WPF](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md). Per un riferimento di estensioni di markup e altre funzionalità abilitate nell'implementazione XAML di .NET generale di programmazione XAML, vedere [XAML Namespace (x) Funzionalità del linguaggio](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md). Per le estensioni di markup specifiche di WPF, vedere [estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md).  
  
<a name="attached_properties"></a>   
## <a name="attached-properties"></a>Proprietà associate  
 Le proprietà associate sono un concetto di programmazione introdotto in XAML, in base al quale le proprietà possono essere di proprietà e definite da un determinato tipo, ma come attributi o elementi di proprietà impostate su qualsiasi elemento. Lo scenario principale che sono destinate le proprietà associate consiste nell'abilitare gli elementi figlio in una struttura di markup di fornire informazioni a un elemento padre senza la necessità di un modello a oggetti ampiamente condiviso tra tutti gli elementi. Viceversa, le proprietà associate possono essere utilizzate dagli elementi padre per registrare le informazioni per gli elementi figlio. Per ulteriori informazioni sullo scopo delle proprietà associate e come crearne di proprie proprietà associate, vedere [Attached Properties Overview](../../../../docs/framework/wpf/advanced/attached-properties-overview.md).  
  
 Le proprietà associate utilizzano una sintassi che assomiglia per certi versi alla sintassi degli elementi di proprietà, in quanto è anche possibile specificare un *typeName*.*propertyName* combinazione. Vi sono due differenze importanti:  
  
-   È possibile utilizzare il *typeName*.*propertyName* anche quando si imposta una proprietà associata tramite la sintassi degli attributi. Le proprietà associate sono che l'unico caso in cui la qualifica il nome della proprietà è un requisito di una sintassi degli attributi.  
  
-   È anche possibile utilizzare la sintassi degli elementi per le proprietà associate. Tuttavia, per la sintassi degli elementi di proprietà tipica, il *typeName* si specifica l'elemento oggetto che contiene l'elemento di proprietà. Se si fa riferimento a una proprietà associata, il *typeName* è la classe che definisce la proprietà associata, non l'elemento oggetto contenitore.  
  
<a name="attached_events"></a>   
## <a name="attached-events"></a>Eventi associati  
 Gli eventi associati sono un altro concetto di programmazione introdotto in XAML in cui gli eventi possono essere definiti da un tipo specifico, ma è possibile associare i gestori a qualsiasi elemento oggetto. Nell'implementazione di WPF, spesso il tipo che definisce un evento associato è un tipo statico che definisce un servizio e in alcuni casi gli eventi associati sono esposti dall'alias di un evento indirizzato in tipi che espongono il servizio. I gestori per gli eventi associati vengono specificati tramite la sintassi degli attributi. Come gli eventi associati, la sintassi degli attributi viene espansa per gli eventi associati consentire un *typeName*.*eventName* utilizzo, in cui *typeName* è la classe che fornisce `Add` e `Remove` funzioni di accesso del gestore eventi per l'infrastruttura degli eventi associati e *eventName* è il nome dell'evento.  
  
<a name="anatomy_of_a_xaml_page_root_element"></a>   
## <a name="anatomy-of-a-xaml-root-element"></a>Anatomia di un elemento radice XAML  
 Nella tabella seguente viene illustrato un tipico elemento radice XAML frammentato, che mostra gli attributi specifici di un elemento radice:  
  
|||  
|-|-|  
|`<Page`|Apertura dell'elemento oggetto dell'elemento radice|  
|`xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`|Il valore predefinito ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]) dello spazio dei nomi XAML|  
|`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`|Lo spazio dei nomi XAML del linguaggio XAML|  
|`x:Class="ExampleNamespace.ExampleCode"`|Dichiarazione di classe parziale che connette il markup per un qualsiasi code-behind definito per la classe parziale|  
|`>`|Fine dell'elemento oggetto per la radice. Oggetto non è ancora chiuso perché l'elemento contiene elementi figlio|  
  
<a name="optional_and_nonrecommended_xaml_usages"></a>   
## <a name="optional-and-nonrecommended-xaml-usages"></a>Utilizzi di XAML non consigliati e facoltativi  
 Nelle sezioni seguenti vengono descritti gli utilizzi XAML tecnicamente supportate dai processori XAML, ma che generano il livello di dettaglio o altri problemi estetici che interferiscono con i file XAML leggibili quando di sviluppare applicazioni che contengono origini XAML.  
  
### <a name="optional-property-element-usages"></a>Utilizzi degli elementi di proprietà facoltativa  
 Gli utilizzi degli elementi di proprietà facoltativa includere la scrittura in modo esplicito le proprietà del contenuto di elemento che considerate implicite dal processore XAML. Ad esempio, quando si dichiara il contenuto di un <xref:System.Windows.Controls.Menu>, è possibile scegliere di dichiarare in modo esplicito il <xref:System.Windows.Controls.ItemsControl.Items%2A> raccolta del <xref:System.Windows.Controls.Menu> come un `<Menu.Items>` tag di elemento di proprietà e inserire ciascun <xref:System.Windows.Controls.MenuItem> all'interno di `<Menu.Items>`, anziché utilizzare il comportamento del processore XAML implicito che tutti gli elementi figlio di un <xref:System.Windows.Controls.Menu> deve essere un <xref:System.Windows.Controls.MenuItem> e collocati nel <xref:System.Windows.Controls.ItemsControl.Items%2A> insieme. Talvolta gli utilizzi facoltativi possono aiutare a chiarire visivamente la struttura dell'oggetto come indicato nel markup. In altri casi utilizzo di un elemento di proprietà esplicite possa evitare markup tecnicamente funzionale ma visivamente confuso, ad esempio estensioni di markup annidato all'interno di un valore di attributo.  
  
### <a name="full-typenamemembername-qualified-attributes"></a>Attributi qualificati nomeTipo. nomemembro completi  
 The *typeName*.*memberName* modulo per un attributo in effetti funziona in maniera più diretta rispetto indirizzato. Ma in altre situazioni tale formato è superfluo ed è necessario evitare, se solo per motivi di stile di markup e di migliorare la leggibilità. Nell'esempio seguente, ognuno dei tre riferimenti al <xref:System.Windows.Controls.Control.Background%2A> attributo sono completamente equivalenti:  
  
 [!code-xml[XAMLOvwSupport#TypeNameProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenameprop)]  
  
 `Button.Background`Poiché la ricerca qualificata per tale proprietà su <xref:System.Windows.Controls.Button> ha esito positivo (<xref:System.Windows.Controls.Control.Background%2A> ereditato dal controllo) e <xref:System.Windows.Controls.Button> è la classe dell'elemento oggetto o una classe di base. `Control.Background`Poiché il <xref:System.Windows.Controls.Control> classe definisce effettivamente <xref:System.Windows.Controls.Control.Background%2A> e <xref:System.Windows.Controls.Control> è un <xref:System.Windows.Controls.Button> classe di base.  
  
 Tuttavia, le operazioni seguenti *typeName*.*memberName* esempio di form non funziona e in cui sono visualizzato i commento:  
  
 [!code-xml[XAMLOvwSupport#TypeNameBadProp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenamebadprop)]  
  
 <xref:System.Windows.Controls.Label> è un'altra classe derivata di <xref:System.Windows.Controls.Control>, e se è stato specificato `Label.Background` all'interno di un <xref:System.Windows.Controls.Label> elemento oggetto, questo utilizzo avrebbe avuto esito positivo. Tuttavia, poiché <xref:System.Windows.Controls.Label> è la classe o una classe di base di <xref:System.Windows.Controls.Button>, il comportamento del processore XAML specificato consiste nell'elaborazione `Label.Background` come una proprietà associata. `Label.Background`non è una proprietà associata disponibile, e questo utilizzo ha esito negativo.  
  
### <a name="basetypenamemembername-property-elements"></a>Elementi di proprietà nomeTipoBase. nomemembro  
 In modo analogo a come il *typeName*.*memberName* formato funziona per la sintassi di attributo, un *baseTypeName*.* memberName* funziona per la sintassi degli elementi di sintassi. Ad esempio, la sintassi seguente funziona:  
  
 [!code-xml[XAMLOvwSupport#GoofyPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofype)]  
  
 In questo caso, l'elemento di proprietà viene fornito come `Control.Background` anche se la proprietà era contenuto in `Button`.  
  
 Ma come *typeName*.*memberName* form per gli attributi, *baseTypeName*.* memberName* non rappresenta uno stile nel markup ed è opportuno evitare.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica su XAML (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [XAML Namespace (x) Funzionalità del linguaggio](../../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md)   
 [Estensioni XAML WPF](../../../../docs/framework/wpf/advanced/wpf-xaml-extensions.md)   
 [Cenni preliminari sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [TypeConverter e XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md)   
 [Classi XAML e personalizzate per WPF](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)