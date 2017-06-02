---
title: "Default XAML Schema Context and WPF XAML Schema Context | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04e06a15-09b3-4210-9bdf-9a64c2eccb83
caps.latest.revision: 7
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 7
---
# Default XAML Schema Context and WPF XAML Schema Context
Un contesto dello schema XAML è un'entità concettuale che determina in che modo una produzione XAML che utilizza un determinato vocabolario XAML interagisce con il comportamento di scrittura dell'oggetto, inclusa la modalità di risoluzione del mapping dei tipi, la modalità di caricamento degli assembly, la modalità di interpretazione di determinate impostazioni di reader e writer.  In questo argomento vengono descritte le caratteristiche dei servizi XAML di .NET Framework e del contesto dello schema XAML predefinito associato, basato sul sistema dei tipi CLR.  Viene inoltre descritto il contesto dello schema XAML utilizzato per WPF.  
  
## Contesto dello schema XAML predefinito  
 I servizi XAML di .NET Framework implementano e utilizzano un contesto dello schema XAML predefinito.  Il comportamento del contesto dello schema XAML predefinito non è sempre completamente visibile nell'API della classe <xref:System.Xaml.XamlSchemaContext>.  Tuttavia, in molti casi il comportamento su cui influisce il contesto dello schema XAML predefinito è osservabile tramite l'aPI comune del sistema dei tipi XAML, ad esempio i membri di <xref:System.Xaml.XamlMember> o di <xref:System.Xaml.XamlType>, oppure tramite API esposte in reader e writer XAML che utilizzano il contesto dello schema XAML predefinito.  
  
 È possibile creare un oggetto <xref:System.Xaml.XamlSchemaContext> che incapsula il comportamento predefinito chiamando il costruttore <xref:System.Xaml.XamlSchemaContext>.  Viene così creato esplicitamente il contesto dello schema XAML predefinito.  Lo stesso contesto dello schema XAML predefinito viene creato in modo implicito, se si inizializza un reader o un writer XAML utilizzando le API che non accettano esplicitamente un parametro di input <xref:System.Xaml.XamlSchemaContext>.  
  
 Il contesto dello schema XAML predefinito si basa sulla reflection CLR per il relativo comportamento di mapping dei tipi.  È inclusa l'analisi dell'oggetto <xref:System.Type> di definizione e l'oggetto <xref:System.Reflection.PropertyInfo> o <xref:System.Reflection.MethodInfo> correlato.  Inoltre, l'attribuzione CLR su tipi o membri viene utilizzata per compilare le specifiche per le informazioni dei tipi o dei membri XAML che utilizzano il tipo di supporto CLR.  Il contesto dello schema XAML predefinito non richiede tecniche di estensione del sistema dei tipi, ad esempio il modello `Invoker`, poiché le informazioni necessarie sono disponibili nel sistema dei tipi CLR.  
  
 Per la logica di caricamento dell'assembly, il contesto dello schema XAML predefinito si basa principalmente su qualsiasi valore di assembly fornito nei mapping dello spazio dei nomi XAML.  È inoltre possibile che la proprietà <xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A> suggerisca un assembly da caricare, per scenari quali il caricamento di tipi interni.  
  
## Contesto dello schema XAML WPF  
 In questo argomento viene descritto il contesto dello schema XAML WPF poiché l'implementazione WPF offre un'interessante illustrazione dei tipi di funzionalità che è possibile introdurre con l'implementazione di un contesto dello schema XAML non predefinito.  Inoltre, il concetto del contesto dello schema XAML non viene approfondito nella documentazione WPF dedicata al linguaggio XAML WPF; il comportamento consentito dal contesto dello schema XAML può essere compreso pienamente solo se integrato con una discussione relativa alla modalità di funzionamento del contesto dello schema XAML predefinito.  Il contesto dello schema XAML WPF implementa il comportamento seguente.  
  
 **Override delle ricerche:** WPF include alcuni modelli di contenuto per XAML in cui sono presenti proprietà del contenuto XAML che funzionano senza avere l'attributo <xref:System.Windows.Markup.ContentPropertyAttribute>.  <xref:System.Xaml.XamlType.LookupContentProperty%2A> esegue l'override affinché WPF implementi questo comportamento.  
  
 **Rinvio per espressioni WPF:** WPF include diverse classi di espressione tramite cui un valore viene rinviato finché non è disponibile un contesto di runtime.  Inoltre, l'espansione del modello è un comportamento di runtime basato su tecniche di rinvio.  
  
 **Ottimizzazioni delle ricerche nel sistema dei tipi:** WPF include un vocabolario XAML completo e un modello a oggetti, che comprende definizioni dei membri della classe base da cui ereditano centinaia di classi definite da WPF.  WPF stesso, inoltre, è suddiviso tra diversi assembly.  In WPF la ricerca dei tipi è ottimizzata utilizzando tabelle di ricerca e altre tecniche.  Ciò garantisce miglioramenti delle prestazioni sul contesto dello schema XAML predefinito e la relativa ricerca dei tipi basata su CLR.  Nei casi in cui in una tabella di ricerca non esistono tipi, vengono utilizzate le tecniche di contesto dello schema XAML simili al contesto dello schema XAML predefinito.  
  
 **Estensione di XamlType e XamlMember:** in WPF vengono estesi i concetti di proprietà con le proprietà di dipendenza e i concetti di evento con gli eventi indirizzati.  Per dare maggiore visibilità a questi concetti per le operazioni di elaborazione XAML, in WPF vengono estesi <xref:System.Xaml.XamlType> e <xref:System.Xaml.XamlMember> e vengono aggiunte proprietà interne con caratteristiche delle proprietà indipendenti e degli eventi indirizzati.  
  
### Accesso al contesto dello schema XAML WPF  
 Se si utilizzano tecniche XAML basate su <xref:System.Windows.Markup.XamlReader?displayProperty=fullName> o <xref:System.Windows.Markup.XamlWriter?displayProperty=fullName> WPF, il contesto dello schema XAML WPF è già in uso nelle implementazioni del reader e del writer XAML.  
  
 Se si utilizzano altre implementazioni di reader o writer XAML che non vengono inizializzate con il contesto dello schema XAML WPF, è possibile ottenere un contesto dello schema XAML WPF di lavoro dal metodo <xref:System.Windows.Markup.XamlReader.GetWpfSchemaContext%2A?displayProperty=fullName>.  È quindi possibile utilizzare questo valore come inizializzazione per altre API che utilizzano <xref:System.Xaml.XamlSchemaContext>.  Ad esempio, è possibile chiamare <xref:System.Xaml.XamlXmlReader.%23ctor%2A> per l'inizializzazione e passare il contesto dello schema XAML WPF.  In alternativa, è possibile utilizzare il contesto dello schema XAML WPF per le operazioni del sistema dei tipi XAML.  Potrebbe essere inclusa l'inizializzazione della costruzione di un oggetto <xref:System.Xaml.XamlType> o <xref:System.Xaml.XamlMember> o la chiamata a <xref:System.Xaml.XamlSchemaContext.GetXamlType%2A?displayProperty=fullName>.  
  
 Si noti che se si accede a determinati aspetti di XAML WPD da una prospettiva puramente basata sul flusso del nodo XAML, alcune funzionalità del framework WPF potrebbero non avere ancora eseguito azioni.  Ad esempio, i modelli WPF per i controlli non sono ancora stati applicati.  Pertanto, se si accede a una proprietà che potrebbe essere popolata con una struttura ad albero visuale completa in fase di esecuzione, è possibile che sia visibile solo un valore di proprietà che fa riferimento a un modello.  Anche il contesto di servizio fornito per le estensioni di markup WPF potrebbe non essere accurato se fornito da una situazione non di runtime e potrebbe generare eccezioni quando si tenta di scrivere un oggetto grafico.  
  
## XAML e caricamento di assembly  
 Il caricamento di assembly per XAML e servizi XAML di .NET Framework è integrato con il concetto definito da CLR di <xref:System.AppDomain>.  Un contesto dello schema XAML interpreta la modalità di caricamento degli assembly o di ricerca dei tipi in fase di esecuzione o di progettazione, in base all'utilizzo di <xref:System.AppDomain> e altri fattori.  La logica è leggermente differente a seconda che XAML sia separato per un reader XAML, sia compilato in una DLL da `XamlBuildTask` o sia BAML generato da `PresentationBuildTask` di WPF.  
  
 Il contesto dello schema XAML per WPF è integrato al modello dell'applicazione WPF, in cui si utilizza <xref:System.AppDomain> ed altri fattori che sono dettagli dell'implementazione WPF.  
  
#### Input del reader XAML \(XAML separato\)  
  
1.  Il contesto dello schema XAML viene ripetuto nell'oggetto <xref:System.AppDomain> dell'applicazione, alla ricerca di un assembly già caricato che corrisponde a tutti gli aspetti del nome, a partire dall'assembly caricato più recentemente.  Se viene individuata una corrispondenza, l'assembly viene utilizzato per la risoluzione.  
  
2.  In caso contrario, viene utilizzata una delle tecniche seguenti basate sull'API <xref:System.Reflection.Assembly> CLR per caricare un assembly:  
  
    -   Se il nome è completo nel mapping, chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName> sul nome completo.  
  
    -   Se il passaggio precedente ha esito negativo, utilizzare il nome breve \(e il token di chiave pubblica se presente\) per chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  
  
    -   Se il nome non è completo nel mapping, chiamare <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>.  
  
#### XamlBuildTask  
 `XamlBuildTask` viene utilizzato per [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)] e [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)].  
  
 Si noti che i riferimenti all'assembly tramite `XamlBuildTask` sono sempre completi.  
  
1.  Chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName> sul nome completo.  
  
2.  Se il passaggio precedente ha esito negativo, utilizzare il nome breve \(e il token di chiave pubblica se presente\) per chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  
  
#### BAML \(PresentationBuildTask\)  
 Occorre considerare due aspetti relativi al caricamento di assembly per BAML: il caricamento dell'assembly iniziale che contiene BAML come componente e il caricamento degli assembly di supporto dei tipi per qualsiasi tipo cui fa riferimento la produzione BAML.  
  
##### Caricamento dell'assembly per il markup iniziale:  
 Il riferimento all'assembly da cui caricare il markup è sempre non qualificato.  
  
1.  Il contesto dello schema XAML WPF viene ripetuto nell'oggetto <xref:System.AppDomain> dell'applicazione WPF, alla ricerca di un assembly già caricato che corrisponde a tutti gli aspetti del nome, a partire dall'assembly caricato più recentemente.  Se viene individuata una corrispondenza, l'assembly viene utilizzato per la risoluzione.  
  
2.  Se il passaggio precedente ha esito negativo, utilizzare il nome breve \(e il token di chiave pubblica se presente\) per chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  
  
##### Riferimenti all'assembly dai tipi BAML:  
 I riferimenti all'assembly per i tipi utilizzati nella produzione BAML sono sempre completi, come un output dell'attività di compilazione.  
  
1.  Il contesto dello schema XAML WPF viene ripetuto nell'oggetto <xref:System.AppDomain> dell'applicazione WPF, alla ricerca di un assembly già caricato che corrisponde a tutti gli aspetti del nome, a partire dall'assembly caricato più recentemente.  Se viene individuata una corrispondenza, l'assembly viene utilizzato per la risoluzione.  
  
2.  In caso contrario, viene utilizzata una delle tecniche seguenti per caricare un assembly:  
  
    -   Chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName> sul nome completo.  
  
    -   Se una combinazione di nome breve e token di chiave pubblica corrisponde all'assembly da cui è stato caricato il codice BAML, utilizzare tale assembly.  
  
    -   Utilizzare nome breve e token di chiave pubblica per chiamare <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  
  
## Vedere anche  
 [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)