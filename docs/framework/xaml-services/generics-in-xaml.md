---
title: "Generics in XAML | Microsoft Docs"
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
  - "generics [XAML Services]"
ms.assetid: 835bfed7-585c-4216-ae67-b674edab8b92
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# Generics in XAML
I servizi XAML di .NET Framework implementati in System.Xaml forniscono il supporto per l'utilizzo di tipi CLR generici.  Questo supporto include la specifica dei vincoli dei generics come argomento di tipo e l'applicazione dei vincoli mediante chiamata al metodo `Add` appropriato per i casi di raccolte generiche.  In questo argomento vengono descritti vari aspetti dell'utilizzo e del riferimento a tipi generici in XAML.  
  
## x:TypeArguments  
 `x:TypeArguments` è una direttiva definita dal linguaggio XAML.  Se utilizzata come membro di un tipo XAML supportato da un tipo generico, `x:TypeArguments` passa argomenti di tipo vincolanti del tipo generico al costruttore di supporto.  Per la sintassi di riferimento relativa agli utilizzi di `x:TypeArguments` da parte dei servizi XAML di .NET Framework, inclusi alcuni esempi di sintassi, vedere [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md).  
  
 Poiché `x:TypeArguments` accetta una stringa ed è supportato da un convertitore di tipi, viene in genere dichiarato come attributo nell'utilizzo in XAML.  
  
 Nel flusso del nodo XAML, le informazioni dichiarate da `x:TypeArguments` possono essere ottenute da <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=fullName> in corrispondenza di una posizione `StartObject` nel flusso del nodo.  Il valore restituito di <xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=fullName> è un elenco di valori <xref:System.Xaml.XamlType>.  Per stabilire se un tipo XAML rappresenti un tipo generico, è possibile chiamare <xref:System.Xaml.XamlType.IsGeneric%2A?displayProperty=fullName>.  
  
## Regole e convenzioni di sintassi per i generics in XAML  
 In XAML, un tipo generico deve sempre essere rappresentato come generico vincolato; un generico non vincolato non viene mai utilizzato nel sistema di tipi XAML o in un flusso del nodo XAML e non può essere rappresentato nel markup XAML.  Un generico può essere oggetto di riferimento nella sintassi degli attributi XAML nei casi in cui rappresenta un vincolo di tipo annidato di un generico a cui fa riferimento `x:TypeArguments` o nei casi in cui `x:Type` fornisce un riferimento del tipo CLR per un tipo generico.  Questa possibilità è supportata tramite la classe <xref:System.Xaml.Schema.XamlTypeTypeConverter> definita dai servizi XAML di .NET Framework.  
  
 La forma di sintassi degli attributi XAML abilitata da <xref:System.Xaml.Schema.XamlTypeTypeConverter> modifica la convenzione della sintassi MSIL \/ CLR tipica che utilizza parentesi uncinate per tipi e vincoli di generics sostituendo le parentesi per il contenitore dei vincoli.  Per un esempio, vedere [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md).  
  
## Generics e funzionalità di XAML 2009  
 Se si utilizza XAML 2009, anziché eseguire il mapping dei tipi di base CLR per ottenere tipi XAML per le primitive di linguaggio comuni, è possibile utilizzare i [tipi incorporati di XAML 2009](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md) come elementi informazione in `x:TypeArguments`.  Ad esempio, è possibile dichiarare quanto segue \(mapping dei prefissi non indicati, ma `x` è lo spazio dei nomi XAML del linguaggio XAML per XAML 2009\):  
  
```  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
## Supporto dei generics in WPF e altri framework v3.5  
 Per l'utilizzo in XAML 2006 con destinazione specifica WPF, [x:Class](../../../docs/framework/xaml-services/x-class-directive.md) deve inoltre essere fornito nello stesso elemento di `x:TypeArguments`, che deve essere l'elemento radice in un documento XAML.  L'elemento radice deve eseguire il mapping a un tipo generico con almeno un argomento di tipo.  <xref:System.Windows.Navigation.PageFunction%601> è un esempio.  
  
 Le possibili soluzioni alternative per supportare gli utilizzi dei generics includono la definizione di un'estensione di markup personalizzata in grado di restituire tipi generici o la specificazione di una definizione di classe di wrapping che deriva da un tipo generico ma appiattisce il vincolo generico nella propria definizione di classe.  
  
 In WPF e in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] di destinazione è possibile utilizzare le funzionalità di XAML 2009 insieme a `x:TypeArguments`, soltanto però per codice XAML separato e non per codice compilato dal markup.  Il codice XAML compilato dal markup per WPF e il modulo BAML di XAML non supportano attualmente le parole chiave e le funzionalità di XAML 2009.  
  
 I flussi di lavoro personalizzati in [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] per [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] non supportano l'utilizzo di XAML generico.  
  
## Vedere anche  
 [x:TypeArguments Directive](../../../docs/framework/xaml-services/x-typearguments-directive.md)   
 [x:Class Directive](../../../docs/framework/xaml-services/x-class-directive.md)   
 [Built\-in Types for Common XAML Language Primitives](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)