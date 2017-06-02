---
title: "XAML Namespaces for .NET Framework XAML Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4f15f13-c420-4c1e-aeab-9b6f50212047
caps.latest.revision: 3
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 3
---
# XAML Namespaces for .NET Framework XAML Services
Uno spazio dei nomi XAML è un concetto che espande la definizione di uno spazio dei nomi XML.  Come per uno spazio dei nomi XML, è possibile definire uno spazio dei nomi XAML utilizzando un attributo `xmlns` nel markup.  Gli spazi dei nomi XAML sono inoltre rappresentati nel flusso del nodo XAML e in altre API dei servizi XAML.  In questo argomento viene definito il concetto di spazio dei nomi XAML, viene illustrato come è possibile definire gli spazi dei nomi XAML e come vengono utilizzati dai contesti dello schema XAML e vengono spiegati altri aspetti dei servizi XAML di .NET Framework.  
  
## Spazio dei nomi XML e spazio dei nomi XAML  
 Uno spazio dei nomi XAML è uno spazio dei nomi XML specializzato, così come XAML è una forma specializzata di XML e utilizza la forma XML base per il markup.  Nel markup, si dichiara uno spazio dei nomi XAML e il relativo mapping tramite un attributo `xmlns` applicato a un elemento.  È possibile effettuare la dichiarazione `xmlns` nello stesso elemento in cui viene dichiarato lo spazio dei nomi XAML.  Una dichiarazione dello spazio dei nomi XAML effettuata in un elemento è valida per l'elemento, tutti gli attributi dell'elemento e tutti gli elementi figlio dell'elemento.  Un attributo può utilizzare uno spazio dei nomi XAML diverso da quello dell'elemento che lo contiene, purché il nome stesso dell'attributo faccia riferimento al prefisso come parte del nome dell'attributo nel markup.  
  
 La distinzione di uno spazio dei nomi XAML rispetto a uno spazio dei nomi XML è data dal fatto che il secondo potrebbe essere utilizzato per fare riferimento a uno schema o semplicemente per differenziare le entità.  Per XAML, i tipi e i membri utilizzati in XAML devono essere risolti in ultima analisi in tipi di supporto e i concetti dello schema XML non si applicano correttamente a questa funzionalità.  Lo spazio dei nomi XAML contiene informazioni che devono essere disponibile al contesto dello schema XAML per eseguire questo mapping dei tipi.  
  
## Componenti dello spazio dei nomi XAML  
 La definizione dello spazio dei nomi XAML ha due componenti: un prefisso e un identificatore.  Ciascuna componente è presente quando uno spazio dei nomi XAML viene dichiarato nel markup o viene definito nel sistema di tipi XAML.  
  
 Il prefisso può essere qualsiasi stringa consentita dalla [specifica degli spazi dei nomi W3C in XML 1.0](http://go.microsoft.com/fwlink/?LinkID=161735).  Per convenzione, i prefissi sono in genere stringhe molto brevi, poiché il prefisso viene ripetuto molte volte in un file di markup tipico.  Determinati spazi dei nomi XAML destinati all'utilizzo in più implementazioni XAML utilizzando prefissi convenzionali particolari.  Ad esempio, lo spazio dei nomi XAML del linguaggio XAML viene in genere mappato utilizzando il prefisso `x`.  È possibile definire uno spazio dei nomi XAML predefinito, in cui il prefisso non è specificato nella definizione ma rappresentato come stringa vuota se definito o richiesto dall'API dei servizi XAML di .NET Framework.  In genere, lo spazio dei nomi XAML predefinito viene scelto deliberatamente allo scopo di promuovere una quantità massimizzata di markup senza prefisso da parte di una tecnologia che implementa XAML e relativi scenari e vocabolari.  
  
 L'identificatore può essere qualsiasi stringa consentita dalla [specifica degli spazi dei nomi W3C in XML 1.0](http://go.microsoft.com/fwlink/?LinkID=161735).  Per convenzione, gli identificatori per gli spazi dei nomi XML o XAML sono spesso specificati in formato URI, di solito come URI assoluto qualificato da protocollo.  Spesso, le informazioni sulla versione che definiscono un determinato vocabolario XAML sono implicite come parte della stringa del percorso.  Gli spazi dei nomi XAML aggiungono una convenzione di identificatore supplementare oltre alla convenzione dell'URI XML.  Per gli spazi dei nomi XAML, l'identificatore comunica le informazioni necessarie a un contesto dello schema XAML per risolvere i tipi specificati come elementi in tale spazio dei nomi XAML o per risolvere gli attributi nei membri.  
  
 Allo scopo di fornire informazioni a un contesto dello schema XAML, l'identificatore per uno spazio dei nomi XAML può ancora essere in formato URI.  Tuttavia, in questo caso l'URI viene anche dichiarato come identificatore corrispondente in un determinato assembly o elenco di assembly.  Questa operazione viene eseguita negli assembly tramite l'assegnazione all'assembly dell'attributo <xref:System.Windows.Markup.XmlnsDefinitionAttribute>.  Questo metodo di identificazione dello spazio dei nomi XAML e di supporto di un comportamento di risoluzione dei tipi basato su CLR nell'assembly con attributo è supportato dal contesto dello schema XAML predefinito nei servizi XAML di .NET Framework.  In termini più generali, è possibile utilizzare questa convenzione per i casi in cui il contesto dello schema XAML incorpori CLR o sia basato sul contesto dello schema XAML predefinito, una condizione necessaria per leggere gli attributi CLR dagli assembly CLR.  
  
 Anche gli spazi dei nomi XAML possono essere identificati da una convenzione che comunica uno spazio dei nomi CLR e un assembly di definizione dei tipi.  Questa convenzione viene utilizzata nei casi in cui non è presente alcuna attribuzione di <xref:System.Windows.Markup.XmlnsDefinitionAttribute> negli assembly che contengono i tipi.  Questa convenzione è potenzialmente più complessa della convenzione dell'URI e può creare ambiguità e duplicati, perché è possibile fare riferimento a un assembly in molti modi.  
  
 Di seguito viene riportata la forma più basilare di identificatore che utilizza lo spazio dei nomi CLR e la convenzione dell'assembly:  
  
 `clr-namespace:` *Nomeclrns* `; assembly=` *NomeBreveassembly*  
  
 `clr-namespace:` e `; assembly=` sono componenti letterali della sintassi.  
  
 *Nomeclrns* è il nome della stringa che identifica uno spazio dei nomi CLR.  Questo nome di stringa include qualsiasi carattere punto \(.\) che fornisce suggerimenti sullo spazio dei nomi CLR e la relativa relazione con altri spazi dei nomi CLR.  
  
 *nomeBreveAssembly* è il nome della stringa di un'assemblea che definisce i tipi utili in XAML.  Si prevede che i tipi a cui accedere tramite lo spazio dei nomi XAML dichiarato siano definiti dall'assembly e dichiarati specificamente nello spazio dei nomi CLR specificato da *Nomeclrns*.  Questo nome di stringa è in genere parallelo alle informazioni riportate da <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=fullName>.  
  
 Di seguito è riportata una definizione più completa dello spazio dei nomi CLR e della convenzione dell'assembly:  
  
 `clr-namespace:` *Nomeclrns* `; assembly=` *nomeAssembly*  
  
 *nomeAssembly* rappresenta qualsiasi stringa valida come input di <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=fullName>.  Questa stringa può includere impostazioni cultura, chiave pubblica o informazioni sulla versione \(le definizioni di questi concetti sono fornite nell'argomento di riferimento per <xref:System.Reflection.Assembly>\).  Il formato e l'evidenza di COFF \(secondo l'utilizzo da parte di altri overload di <xref:System.Reflection.Assembly.Load%2A>\) non sono pertinenti ai fini del caricamento di assembly XAML; tutte le informazioni relative al caricamento devono essere presentate come stringa.  
  
 La specifica di una chiave pubblica per l'assembly è una tecnica utile per la sicurezza XAML o per la rimozione di qualsiasi potenziale ambiguità che può essere presente se gli assembly vengono caricati semplicemente per nome o preesistente in un dominio dell'applicazione o nella cache.  Per ulteriori informazioni, vedere [XAML Security Considerations](../../../docs/framework/xaml-services/xaml-security-considerations.md).  
  
## Dichiarazioni dello spazio dei nomi XAML nelle API dei servizi XAML  
 Nelle API dei servizi XAML una dichiarazione dello spazio dei nomi XAML è rappresentata da un oggetto <xref:System.Xaml.NamespaceDeclaration>.  Per dichiarare uno spazio dei nomi XAML nel codice, chiamare il costruttore <xref:System.Xaml.NamespaceDeclaration.%23ctor%28System.String%2CSystem.String%29>.  I parametri `ns` e `prefix` sono specificati come stringhe e l'input da fornire a tali parametri corrisponde alla definizione dell'identificatore e del prefisso dello spazio dei nomi XAML secondo quanto indicato in precedenza in questo argomento.  
  
 Se si esaminano le informazioni dello spazio dei nomi XAML come parte di un flusso del nodo XAML o tramite un altro accesso al sistema di tipi XAML, <xref:System.Xaml.NamespaceDeclaration.Namespace%2A?displayProperty=fullName> riporta l'identificatore dello spazio dei nomi XAML e <xref:System.Xaml.NamespaceDeclaration.Prefix%2A?displayProperty=fullName> riporta il prefisso dello spazio dei nomi XAML.  
  
 In un flusso del nodo XAML le informazioni sullo spazio dei nomi XAML possono avere l'aspetto di un nodo XAML che precede l'entità a cui si applica.  Sono inclusi i casi in cui le informazioni sullo spazio dei nomi XAML precedono l'oggetto `StartObject` dell'elemento radice XAML.  Per ulteriori informazioni, vedere [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md).  
  
 Per molti scenari che utilizzano l'API dei servizi XAML di .NET Framework, è prevista la presenza di almeno una dichiarazione dello spazio dei nomi XAML che deve contenere o fare riferimento alle informazioni richieste da un contesto dello schema XAML.  Gli spazi dei nomi XAML devono specificare gli assembly da caricare o agevolare la risoluzione dei tipi specifici all'interno degli spazi dei nomi e degli assembly già caricati o noti dal contesto dello schema XAML.  
  
 Per generare un flusso del nodo XAML, le informazioni di tipo XAML devono essere disponibili, tramite il contesto dello schema XAML.  Non è possibile determinare le informazioni di tipo XAML senza prima determinare lo spazio dei nomi XAML pertinente da creare per ogni nodo.  A questo punto non viene ancora creata alcuna istanza di tipi, ma il contesto dello schema XAML può avere l'esigenza di cercare informazioni dall'assembly di definizione e dal tipo di supporto.  Ad esempio, per elaborare il markup `<Party><PartyFavor/></Party>`, è necessario che il contesto dello schema XAML sia in grado di determinare il nome e il tipo di `ContentProperty` di `Party`, nonché conoscere le informazioni sullo spazio dei nomi XAML per `Party` e `PartyFavor`.  Nel caso del contesto dello schema XAML predefinito, la reflection statica contiene molte delle informazioni del sistema di tipi XAML necessarie per generare i nodi di tipo XAML nel flusso del nodo.  
  
 Per generare un oggetto grafico da un flusso del nodo XAML, le dichiarazioni dello spazio dei nomi XAML devono esistere per ogni prefisso XAML utilizzato nel markup originale e registrato nel flusso del nodo XAML.  A questo punto, le istanze vengono create e viene attuato un comportamento di mapping dei tipi effettivo.  
  
 Se è necessario prepopolare le informazioni sullo spazio dei nomi XAML, nei casi in cui lo spazio dei nomi XAML che si intende utilizzare nel contesto dello schema XAML non è definito nel markup, è possibile utilizzare una tecnica che prevede la definizione delle dichiarazioni dello spazio dei nomi XML in <xref:System.Xml.XmlParserContext> per un oggetto <xref:System.Xml.XmlReader>.  Tale <xref:System.Xml.XmlReader> viene quindi utilizzato come input per un costruttore del reader XAML o <xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29?displayProperty=fullName>.  
  
 Altre due API pertinenti per la gestione di spazi dei nomi XAML nei servizi XAML di .NET Framework sono gli attributi <xref:System.Windows.Markup.XmlnsDefinitionAttribute> e <xref:System.Windows.Markup.XmlnsPrefixAttribute>.  Tali attributi si applicano agli assembly.  <xref:System.Windows.Markup.XmlnsDefinitionAttribute> viene utilizzato da un contesto dello schema XAML per interpretare qualsiasi dichiarazione dello spazio dei nomi XAML che includa un URI.  <xref:System.Windows.Markup.XmlnsPrefixAttribute> viene utilizzato dagli strumenti che creano XAML in modo da consentire la serializzazione di un determinato spazio dei nomi XAML con un prefisso prevedibile.  Per ulteriori informazioni, vedere [XAML\-Related CLR Attributes for Custom Types and Libraries](../../../docs/framework/xaml-services/xaml-related-clr-attributes-for-custom-types-and-libraries.md).  
  
## Vedere anche  
 [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md)