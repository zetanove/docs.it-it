---
title: "x:Name Directive | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "x:Name"
  - "xName"
  - "Name"
helpviewer_keywords: 
  - "x:Name attribute [XAML Services]"
  - "XAML [XAML Services], x:Name attribute"
  - "Name attribute in XAML [XAML Services]"
ms.assetid: b7e61222-e8cf-48d2-acd0-6df3b7685d48
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 27
---
# x:Name Directive
Identifica in modo univoco gli elementi XAML nell'ambito dei nomi XAML.  I namescope XAML e i rispettivi modelli di univocità possono essere applicati agli oggetti di cui è stata creata un'istanza, quando i framework forniscono API o implementano i comportamenti che accedono all'oggetto grafico creato da XAML in fase di esecuzione.  
  
## Utilizzo della sintassi XAML per gli attributi  
  
```  
<object x:Name="XAMLNameValue".../>  
```  
  
## Valori XAML  
  
|||  
|-|-|  
|`XAMLNameValue`|Stringa conforme alle limitazioni dell'oggetto [Grammatica XamlName](../../../docs/framework/xaml-services/xamlname-grammar.md).|  
  
## Note  
 Una volta applicato `x:Name` a un modello di programmazione di supporto del framework, il nome è uguale alla variabile che contiene un riferimento a un oggetto o un'istanza come restituito da un costruttore.  
  
 Il valore di un utilizzo della direttiva `x:Name` deve essere univoco all'interno di un ambito dei nomi XAML.  Per impostazione predefinita, quando viene utilizzata dall'API dei servizi XAML di .NET Framework, i principali namescope XAML sono definiti nell'elemento radice XAML di una singola produzione di XAML e includono gli elementi contenuti nella produzione di XAML.  Altri namescope XAML discreti che potrebbero verificarsi all'interno di una singola produzione XAML possono essere definiti dai framework per indirizzare scenari specifici.  Ad esempio, in WPF, i nuovi ambiti dei nomi XAML vengono definiti e creati da un modello definito nella produzione XAML.  Per ulteriori informazioni sui NameScope di XAML \(scritti per WPF ma attinenti per molti concetti di NameScope di XAML\), vedere [NameScope XAML WPF](../../../ocs/framework/wpf/advanced/wpf-xaml-namescopes.md).  
  
 In generale, `x:Name` non deve essere applicata in situazioni che utilizzano anche `x:Key`.  Le implementazioni XAML da framework specifici esistenti hanno introdotto i concetti di sostituzione tra `x:Key` e `x:Name`, ma non si tratta di una procedura consigliata.  I servizi XAML di .NET Framework non supportano tali concetti di sostituzione in caso di gestione di informazioni di tipo nome\/chiave come <xref:System.Windows.Markup.INameScope> o <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>.  
  
 Le regole dell'autorizzazione di `x:Name` e dell'imposizione di univocità del nome sono definite potenzialmente dai framework di implementazione specifici.  Tuttavia, per essere utilizzabili con i Servizi XAML di .NET Framework, le definizioni di framework dell'univocità dell'ambito dei nomi XAML devono essere coerenti con la definizione delle informazioni <xref:System.Windows.Markup.INameScope> in questa documentazione e devono utilizzare le stesse regole relative al contesto in cui sono applicate le informazioni.  Ad esempio, l'implementazione [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] divide vari elementi di markup in intervalli <xref:System.Windows.NameScope> separati, come ad esempio dizionari risorse, l'albero logico creato da XAML a livello di pagina, modelli e altri contenuti posticipati, e successivamente attiva l'univocità del nome XAML in ciascun spazio dei nomi XAML.  
  
 Per tipi personalizzati che utilizzano i writer degli oggetti XAML dei servizi XAML di .NET Framework, una proprietà che esegue il mapping a `x:Name` su un tipo può essere stabilita o può essere modificata.  È possibile definire questo comportamento facendo riferimento al nome della proprietà per eseguire il mapping con <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> nel codice della definizione del tipo.  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> è un attributo a livello di tipo.  
  
 Utilizzando i servizi Using.NET Framework XAML, la logica di supporto per il supporto di NameScope di XAML può essere definito in modo framework\-neutro implementando l'interfaccia <xref:System.Windows.Markup.INameScope>.  
  
## Note sull'utilizzo di WPF  
 Con la configurazione di compilazione standard per un progetto di applicazione [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] che utilizza XAML, classi parziali e code\-behind, l'oggetto `x:Name` specificato diviene il nome di un campo creato nel codice sottostante quando [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] viene elaborato da un'attività di compilazione con markup e tale campo contiene un riferimento all'oggetto. Per impostazione predefinita, il campo creato è interno.  È possibile modificare l'accesso al campo specificando l'attributo [x:FieldModifier](../../../docs/framework/xaml-services/x-fieldmodifier-directive.md).  In WPF e Silverlight, la sequenza è impostata in modo che la compilazione del markup definisce e nomina il campo in una classe parziale, ma il valore è inizialmente vuoto.  Quindi, un metodo generato denominato `InitializeComponent` viene chiamato dall'interno del costruttore della classe.  `InitializeComponent` è costituito dalle chiamate a `FindName` utilizzando ognuno dei valori `x:Name` che si trovano nella parte definita in XAML della classe parziale come stringhe di input.  I valori restituiti vengono quindi assegnati al riferimento di campo omonimo in modo da riempire i valori di campo con oggetti creati dall'analisi XAML.  L'esecuzione di `InitializeComponent` consente di fare riferimento direttamente all'oggetto grafico in fase di esecuzione mediante `x:Name`\/nome campo, anziché dovendo chiamare `FindName` in modo esplicito quando si necessita di un riferimento a un oggetto definito in XAML.  
  
 In caso di un'applicazione WPF che utilizza le destinazioni di [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] e include i file XAML con un'azione di compilazione `Page` viene creata una proprietà di riferimento separata durante la compilazione, che aggiunge la parola chiave `WithEvents` a tutti gli elementi che dispongono di un attributo `x:Name`, per supportare la sintassi `Handles` per i delegati del gestore eventi.  Questa proprietà è sempre pubblica.  Per ulteriori informazioni, vedere [Visual Basic e la gestione degli eventi WPF](../../../ocs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md).  
  
 `x:Name` viene utilizzato dal processore XAML WPF per registrare un nome in un namescope XAML al momento del carico, persino nei casi in cui la pagina non viene compilata in markup da azioni di compilazione \(ad esempio, quando XAML è separato da un dizionario della risorsa\).  Questo comportamento si verifica perché l'attributo `x:Name` può essere necessario per l'associazione <xref:System.Windows.Data.Binding.ElementName%2A>.  Per informazioni dettagliate, vedere [Cenni preliminari sull'associazione dati](../../../ocs/framework/wpf/data/data-binding-overview.md).  
  
 Come menzionato precedentemente, `x:Name` \(o `Name`\) non devono essere applicati in situazioni che utilizzano anche `x:Key`.  [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.ResourceDictionary> segue un comportamento speciale, autodefinendosi come namescope XAML ma restituendo Not Implemented o valori null per le API <xref:System.Windows.Markup.INameScope> in maniera tale da imporre il comportamento stesso.  Se il parser XAML WPF rileva `Name` o `x:Name` in <xref:System.Windows.ResourceDictionary>definito in XAML, il nome non viene aggiunto ad alcun namescope XAML.  Se si tenta di trovare tale nome dai namescope XAML e i metodi `FindName` non vengono restituiti risultati validi.  
  
### Nome e x:Name  
 Diversi scenari di applicazioni WPF possono non utilizzare l'attributo `x:Name` perché la proprietà di dipendenza `Name` specificata all'interno dello spazio dei nomi XAML per molte delle classi base importanti, come ad esempio <xref:System.Windows.FrameworkElement> e <xref:System.Windows.FrameworkContentElement> soddisfa questo stesso scopo.  Esistono ancora alcuni scenari XAML e WPF comuni in cui l'accesso di codice a un elemento senza alcuna proprietà `Name` a livello di framework è importante.  Ad esempio, determinate classi di supporto di animazioni e storyboard non supportano una proprietà `Name`, ma è necessario farvi riferimento nel codice per comandare l'animazione.  È necessario specificare `x:Name` come attributo nelle sequenze temporali e nelle trasformazioni create in XAML, se si intende utilizzarle come riferimento dal codice.  
  
 Se l'oggetto <xref:System.Windows.FrameworkElement.Name%2A> è disponibile come proprietà nella classe, gli oggetti <xref:System.Windows.FrameworkElement.Name%2A> e `x:Name` possono essere utilizzati in modo intercambiabile come attributi, tuttavia, un'eccezione di analisi risulterà se entrambi vengono specificati nello stesso elemento.  Se nel XAML è stata eseguita la compilazione di markup, si verificherà l'eccezione sulla compilazione di markup, in caso contrario si verificherà nel caricamento.  
  
 <xref:System.Windows.FrameworkElement.Name%2A> può essere impostato utilizzando la sintassi per gli attributi XAML, e nel codice mediante <xref:System.Windows.DependencyObject.SetValue%2A>; notare, tuttavia, che in alcune circostanze l'impostazione della proprietà <xref:System.Windows.FrameworkElement.Name%2A> nel codice non crea il riferimento rappresentativo del campo all'interno del namescope dove XAML è già caricato.  Anziché tentare di impostare <xref:System.Windows.FrameworkElement.Name%2A> nel codice, utilizzare i metodi <xref:System.Windows.NameScope> dal codice sul namescope corretto.  
  
 È possibile inoltre impostare <xref:System.Windows.FrameworkElement.Name%2A> utilizzando la sintassi per gli elementi delle proprietà con testo interno, ma è una procedura non comune.  Al contrario, `x:Name` non può essere impostato nella sintassi dell'elemento della proprietà XAML o nel codice usando <xref:System.Windows.DependencyObject.SetValue%2A>; tale impostazione può essere effettuata solo utilizzando la sintassi per gli attributi sugli oggetti perché è una direttiva.  
  
## Note sull'utilizzo di Silverlight.  
 `x:Name` per Silverlight è documentato separatamente.  Per ulteriori informazioni, vedere [Funzionalità del linguaggio dello spazio dei nomi XAML \(x:\)](http://msdn.microsoft.com/it-it/library/cc188995\(vs.95\).aspx).  
  
## Vedere anche  
 <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=fullName>   
 <xref:System.Windows.FrameworkContentElement.Name%2A?displayProperty=fullName>   
 [Strutture ad albero in WPF](../../../ocs/framework/wpf/advanced/trees-in-wpf.md)