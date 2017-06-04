---
title: "Types Migrated from WPF to System.Xaml | Microsoft Docs"
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
  - "WPF XAML [XAML Services], migration to System.Xaml"
  - "XAML [XAML Services], System.Xaml and WPF"
  - "System.Xaml [XAML Services], types migrated from WPF"
ms.assetid: d79dabf5-a2ec-4e8d-a37a-67c4ba8a2b91
caps.latest.revision: 14
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# Types Migrated from WPF to System.Xaml
In [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)] e [!INCLUDE[net_v30_long](../../../includes/net-v30-long-md.md)], sia [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] che [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] disponevano di un'implementazione del linguaggio XAML. Molti dei tipi pubblici che fornivano l'estensibilità per l'implementazione XAML di WPF erano inclusi negli assembly WindowsBase, PresentationCore e PresentationFramework. In modo analogo, i tipi pubblici che fornivano l'estensibilità di XAML per [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] erano inclusi nell'assembly System.Workflow.ComponentModel. In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] è stata eseguita la migrazione di alcuni tipi correlati a XAML nell'assembly System.Xaml. Un'implementazione .NET Framework comune dei servizi del linguaggio XAML apre molti scenari di estensibilità XAML che sono stati definiti in origine dall'implementazione XAML di un framework specifico che ora fanno parte del supporto del linguaggio XAML di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] complessivo. In questo argomento sono elencati i tipi di cui è stata eseguita la migrazione e vengono illustrati i problemi correlati alla migrazione.  
  
<a name="assemblies_and_namespaces"></a>   
## Assembly e spazi dei nomi  
 In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)], i tipi implementati da WPF per il supporto di XAML erano in genere inclusi nello spazio dei nomi <xref:System.Windows.Markup>. La maggior parte di questi tipi era inclusa nell'assembly WindowsBase.  
  
 In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], è stato introdotto un nuovo spazio dei nomi <xref:System.Xaml> e un nuovo assembly System.Xaml. Molti dei tipi implementati in origine per XAML di WPF sono ora forniti come punti di estendibilità o servizi per qualsiasi implementazione di XAML. Nell'ambito della scelta di renderli disponibili per scenari più generali, i tipi sono stati inoltrati dall'assembly WPF originale all'assembly System.Xaml. In questo modo vengono abilitati scenari di estensibilità XAML senza che sia necessario includere assembly di altri Framework \(ad esempio WPF e [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)]\).  
  
 Per quanto riguarda i tipi migrati, la maggior parte rimane nello spazio dei nomi <xref:System.Windows.Markup>. Questa scelta deriva parzialmente dalla necessità di evitare l'interruzione dei mapping dello spazio dei nomi CLR nelle implementazioni esistenti su base file. Di conseguenza, lo spazio dei nomi <xref:System.Windows.Markup> in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] contiene una combinazione di tipi di supporto del linguaggio XAML generali \(dall'assembly System.Xaml\) e i tipi che sono specifici dell'implementazione XAML di WPF \(provenienti da WindowsBase e altri assembly WPF\). Per qualsiasi tipo di cui è stata eseguita la migrazione a System.Xaml e che in precedenza era incluso in un assembly WPF è disponibile il supporto per l'inoltro dei tipi nella versione 4 dell'assembly WPF.  
  
### Tipi di supporto XAML del flusso di lavoro  
 [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] forniva anche tipi di supporto XAML e in molti casi questi tipi avevano nomi brevi identici a un WPF equivalente. Di seguito è riportato un elenco dei tipi di supporto XAML di [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)].  
  
-   <xref:System.Workflow.ComponentModel.Serialization.ContentPropertyAttribute>  
  
-   <xref:System.Workflow.ComponentModel.Serialization.RuntimeNamePropertyAttribute>  
  
-   <xref:System.Workflow.ComponentModel.Serialization.XmlnsPrefixAttribute>  
  
 Questi tipi di supporto sono ancora inclusi negli assembly [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] per [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] e possono essere ancora usati per applicazioni [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] specifiche; tuttavia non è consigliabile non farvi riferimento da applicazioni o framework che non usano [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)].  
  
<a name="markupextension"></a>   
## MarkupExtension  
 In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] la classe <xref:System.Windows.Markup.MarkupExtension> per WPF era inclusa nell'assembly WindowsBase. Una classe parallela per [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)], <xref:System.Workflow.ComponentModel.Serialization.MarkupExtension>, era presente nell'assembly System.Workflow.ComponentModel. In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], viene eseguita la migrazione della classe <xref:System.Windows.Markup.MarkupExtension> all'assembly System.Xaml. In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], <xref:System.Windows.Markup.MarkupExtension> è destinato a qualsiasi scenario di estensibilità XAML in cui sono usati i servizi XAML di .NET Framework, non solo per quelli basati su framework specifici. Quando possibile, framework specifici o codice utente nel framework deve essere basati anche sulla classe <xref:System.Windows.Markup.MarkupExtension> per l'estensione XAML.  
  
<a name="markupextension_supporting_service_classes"></a>   
## MarkupExtension con supporto di classi del servizio  
 In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] per WPF venivano offerti diversi servizi disponibili agli implementatori di <xref:System.Windows.Markup.MarkupExtension> e alle implementazioni <xref:System.ComponentModel.TypeConverter> per supportare l'utilizzo di tipi\/proprietà in XAML. Questi servizi sono i seguenti:  
  
-   <xref:System.Windows.Markup.IProvideValueTarget>  
  
-   <xref:System.Windows.Markup.IUriContext>  
  
-   <xref:System.Windows.Markup.IXamlTypeResolver>  
  
> [!NOTE]
>  Un altro servizio di [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] correlato alle estensioni di markup è l'interfaccia <xref:System.Windows.Markup.IReceiveMarkupExtension>. Non è stata eseguita la migrazione di <xref:System.Windows.Markup.IReceiveMarkupExtension> ed è contrassegnato con `[Obsolete]` per [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Negli scenari in precedenza veniva usato <xref:System.Windows.Markup.IReceiveMarkupExtension>, ora invece è necessario usare callback con attributi <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute>. Anche <xref:System.Windows.Markup.AcceptedMarkupExtensionExpressionTypeAttribute> è contrassegnato come `[Obsolete]`.  
  
<a name="xaml_language_features"></a>   
## Funzionalità del linguaggio XAML  
 Diversi componenti e funzionalità del linguaggio XAML per WPF erano in precedenza inclusi nell'assembly PresentationFramework. Questi venivano implementati come una sottoclasse <xref:System.Windows.Markup.MarkupExtension> per esporre gli utilizzi delle estensioni di markup nel markup XAML. In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] questi componenti e funzionalità sono presenti nell'assembly System.Xaml in modo che i progetti che non includono assembly WPF possono usare tali funzionalità a livello di linguaggio XAML. In WPF vengono usate queste stesse implementazioni per le applicazioni [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Come per gli altri casi elencati in questo argomento, i tipi di supporto continuano a esistere nello spazio dei nomi <xref:System.Windows.Markup> per evitare l'interruzione di riferimenti precedenti.  
  
 Nella tabella seguente è riportato un elenco delle classi di supporto delle funzionalità del linguaggio XAML definite in System.Xaml:  
  
|Funzionalità del linguaggio XAML|Utilizzo|  
|--------------------------------------|--------------|  
|<xref:System.Windows.Markup.ArrayExtension>|`<x:Array ...>`|  
|<xref:System.Windows.Markup.NullExtension>|`{x:Null}`|  
|<xref:System.Windows.Markup.StaticExtension>|`{x:Static ...}`|  
|<xref:System.Windows.Markup.TypeExtension>|`{x:Type ...}`|  
  
 Sebbene in System.Xaml possano non essere presenti classi di supporto specifiche, la logica generale per l'elaborazione delle funzionalità del linguaggio per XAML si trova ora in System.Xaml e nei relativi reader XAML e writer XAML implementati.  Ad esempio, `x:TypeArguments` è un attributo elaborato da reader XAML e writer XAML delle implementazioni di System.Xaml. Può essere indicato nel flusso del nodo XAML, viene gestito nel contesto dello schema XAML predefinito \(basato su CLR\), dispone di una rappresentazione del sistema di tipi di XAML e così via. Di conseguenza, la documentazione di riferimento per tutte le funzionalità a livello di linguaggio XAML è inclusa come argomento secondario per [XAML Services](../../../docs/framework/xaml-services/index.md) e per l'area generale specifica del set di documentazione .NET Framework, anziché far parte del set di documentazione WPF come argomento secondario di [Avanzate \(WPF\)](../../../ml/index.xml), come accade ancora nei set di documentazione 3.5.  
  
<a name="valueserializer_and_supporting_classes"></a>   
## ValueSerializer e classi di supporto  
 La classe <xref:System.Windows.Markup.ValueSerializer> supporta la conversione di tipi in una stringa, in particolare per i casi di serializzazione di XAML in cui per la serializzazione possono essere necessarie più modalità o nodi nell'output. In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] la classe <xref:System.Windows.Markup.ValueSerializer> per WPF era inclusa nell'assembly WindowsBase. In [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] la classe <xref:System.Windows.Markup.ValueSerializer> è in System.Xaml ed è usata per qualsiasi scenario di estensibilità XAML, non solo per quelli basati su WPF. Viene inoltre eseguita la migrazione degli oggetti <xref:System.Windows.Markup.IValueSerializerContext> \(servizio di supporto\) e <xref:System.Windows.Markup.DateTimeValueSerializer> \(sottoclasse specifica\) a System.Xaml.  
  
<a name="xamlrelated_attributes"></a>   
## Attributi correlati a XAML  
 In XAML per WPF erano inclusi vari attributi che potevano essere applicati a tipi CLR per fornire indicazioni sul relativo comportamento XAML. Di seguito viene fornito un elenco degli attributi presenti negli assembly WPF in [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)]. Questi attributi vengono migrati a System.Xaml in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  
  
-   <xref:System.Windows.Markup.AmbientAttribute>  
  
-   <xref:System.Windows.Markup.ContentPropertyAttribute>  
  
-   <xref:System.Windows.Markup.ContentWrapperAttribute>  
  
-   <xref:System.Windows.Markup.DependsOnAttribute>  
  
-   <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>  
  
-   <xref:System.Windows.Markup.NameScopePropertyAttribute>  
  
-   <xref:System.Windows.Markup.RootNamespaceAttribute>  
  
-   <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>  
  
-   <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>  
  
-   <xref:System.Windows.Markup.ValueSerializerAttribute>  
  
-   <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>  
  
-   <xref:System.Windows.Markup.XmlLangPropertyAttribute>  
  
-   <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>  
  
-   <xref:System.Windows.Markup.XmlnsDefinitionAttribute>  
  
-   <xref:System.Windows.Markup.XmlnsPrefixAttribute>  
  
<a name="miscellaneous_classes"></a>   
## Classi di vario tipo  
 L'interfaccia <xref:System.Windows.Markup.IComponentConnector> era inclusa in WindowsBase in [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)], ma è presente in System.Xaml in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. L'interfaccia <xref:System.Windows.Markup.IComponentConnector> è principalmente destinata al supporto per gli strumenti di supporto e compilatori di markup XAML.  
  
 L'interfaccia <xref:System.Windows.Markup.INameScope> era inclusa in WindowsBase in [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)], ma è presente in System.Xaml in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. <xref:System.Windows.Markup.INameScope> definisce le operazioni di base per un NameScope XAML.  
  
<a name="xamlrelated_classes_with_shared_names_that_exist_in_wpf_and_systemxaml"></a>   
## Classi correlate a XAML con nomi condivisi incluse in WPF e System.Xaml  
 Le classi seguenti sono incluse negli assembly WPF e nell'assembly System.Xaml in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]:  
  
 `XamlReader`  
  
 `XamlWriter`  
  
 `XamlParseException`  
  
 L'implementazione WPF si trova nello spazio dei nomi <xref:System.Windows.Markup> e nell'assembly PresentationFramework. L'implementazione di System.Xaml si trova nello spazio dei nomi <xref:System.Xaml>. Se si usano tipi WPF o si deriva da tipi WPF, è in genere necessario usare le implementazioni WPF di <xref:System.Windows.Markup.XamlReader> e <xref:System.Windows.Markup.XamlWriter> anziché le implementazioni di System.Xaml. Per altre informazioni, vedere la sezione Osservazioni in <xref:System.Windows.Markup.XamlReader?displayProperty=fullName> e <xref:System.Windows.Markup.XamlWriter?displayProperty=fullName>.  
  
 Se si includono riferimenti agli assembly WPF a System.Xaml e si usano anche istruzioni `include` per gli spazi dei nomi <xref:System.Windows.Markup> e <xref:System.Xaml>, potrebbe essere necessario qualificare completamente le chiamate a queste API per risolvere i tipi senza ambiguità.  
  
## Vedere anche  
 [XAML Services](../../../docs/framework/xaml-services/index.md)