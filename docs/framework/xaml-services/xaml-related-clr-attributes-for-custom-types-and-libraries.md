---
title: "XAML-Related CLR Attributes for Custom Types and Libraries | Microsoft Docs"
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
  - "CLR attributes for custom types [XAML Services]"
ms.assetid: 5dfb299a-b6e2-41b8-8694-e6ac987547f1
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# XAML-Related CLR Attributes for Custom Types and Libraries
In questo argomento vengono descritti gli attributi di Common Language Runtime \(CLR\) definiti dai servizi XAML di .NET Framework.  Vengono inoltre descritti altri attributi CLR definiti in .NET Framework con uno scenario correlato a XAML per l'applicazione ad assembly o tipi.  L'applicazione di questi attributi CLR ad assembly, tipi o membri fornisce informazioni sul sistema di tipi XAML correlate ai tipi.  Le informazioni vengono fornite a tutti i consumer XAML che utilizzano i servizi XAML di .NET Framework per elaborare il flusso del nodo XAML direttamente o tramite i reader XAML e i writer XAML dedicati.  
  
## Attributi CLR correlati a XAML per tipi e membri personalizzati  
 L'utilizzo degli attributi CLR implica l'utilizzo di CLR nel suo complesso per definire i tipi, altrimenti tali attributi non sono disponibili.  Se si utilizza CLR per definire il supporto dei tipi, il contesto dello schema XAML predefinito utilizzato dai writer XAML dei servizi XAML di .NET Framework sarà in grado di leggere l'attribuzione CLR tramite reflection rispetto agli assembly di supporto.  
  
 Nelle sezioni che seguono vengono descritti gli attributi correlati a XAML che è possibile applicare a tipi o membri personalizzati.  Ogni attributo CLR comunica informazioni relative a un sistema di tipi XAML.  Nel percorso di caricamento, le informazioni degli attributi consentono al reader XAML di formare un flusso del nodo XAML valido o al writer XAML di produrre un oggetto grafico valido.  Nel percorso di salvataggio, le informazioni con attributi consentono al reader XAML di creare un flusso del nodo XAML valido che ricostituisce le informazioni sul sistema dei tipi XAML oppure dichiarano suggerimenti o requisiti di serializzazione per il writer XAML o altri consumer XAML.  
  
### AmbientAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.AmbientAttribute>  
  
 **Si applica a:** membri di classe, proprietà o funzione di accesso `get` che supportano le proprietà associabili.  
  
 **Argomenti:** nessuno.  
  
 <xref:System.Windows.Markup.AmbientAttribute> indica che è necessario interpretare la proprietà o tutte le proprietà che accettano il tipo con attributi in base al concetto della proprietà di ambiente in XAML.  Il concetto di ambiente si riferisce al modo in cui i processori XAML determinano i proprietari dei tipi dei membri.  Una proprietà di ambiente è una proprietà in cui il valore deve essere disponibile nel contesto del parser durante la creazione di un oggetto grafico, ma la ricerca tipica di tipi o membri viene sospesa ai fini della creazione immediata del set di nodi XAML.  
  
 Il concetto di ambiente può essere applicato ai membri associabili, i quali non vengono rappresentati come proprietà relativamente al modo in cui l'attribuzione CLR definisce <xref:System.AttributeTargets>.  L'utilizzo dell'attribuzione del metodo deve essere applicato solo nel caso di una funzione di accesso `get` che supporta l'utilizzo associabile per XAML.  
  
### ConstructorArgumentAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.ConstructorArgumentAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** una stringa che specifica il nome della proprietà corrispondente a un unico argomento del costruttore.  
  
 <xref:System.Windows.Markup.ConstructorArgumentAttribute> specifica che un oggetto può essere inizializzato tramite una sintassi del costruttore non predefinita e che una proprietà con il nome specificato fornisce informazioni sulla costruzione.  Queste informazioni sono utili principalmente per la serializzazione XAML.  Per ulteriori informazioni, vedere <xref:System.Windows.Markup.ConstructorArgumentAttribute>.  
  
### ContentPropertyAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.ContentPropertyAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** stringa che specifica il nome di un membro del tipo con attributo.  
  
 <xref:System.Windows.Markup.ContentPropertyAttribute> indica che la proprietà denominata dall'argomento deve fungere da proprietà di contenuto XAML per il tipo in questione.  La definizione della proprietà di contenuto XAML eredita in tutti i tipi derivati assegnabili al tipo di definizione.  È possibile eseguire l'override della definizione in un tipo derivato specifico applicando <xref:System.Windows.Markup.ContentPropertyAttribute> nel tipo in questione.  
  
 Per la proprietà che funge da proprietà di contenuto XAML, nell'utilizzo di XAML è possibile omettere la codifica degli elementi della proprietà.  In genere si definiscono proprietà di contenuto XAML che alzano di livello un markup XAML semplificato per il contenuto e i modelli di contenimento.  Poiché è possibile definire un solo membro come proprietà di contenuto XAML, talvolta è necessario attuare scelte di progettazione in merito a quale proprietà del contenitore di un tipo debba essere definita come proprietà di contenuto XAML.  Le altre proprietà del contenitore devono essere utilizzate con elementi delle proprietà espliciti.  
  
 Nel flusso del nodo XAML, le proprietà di contenuto XAML producono ancora i nodi `StartMember` e `EndMember`, utilizzando il nome della proprietà per <xref:System.Xaml.XamlMember>.  Per determinare se un membro è la proprietà di contenuto XAML, esaminare il valore di <xref:System.Xaml.XamlType> dalla posizione `StartObject` e ottenere il valore di <xref:System.Xaml.XamlType.ContentProperty%2A>.  
  
### ContentWrapperAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.ContentWrapperAttribute>  
  
 **Si applica a:** Class, in particolare ai tipi Collection.  
  
 **Argomenti:** un oggetto <xref:System.Type> che specifica il tipo da utilizzare come tipo di wrapper del contenuto per il contenuto esterno.  
  
 <xref:System.Windows.Markup.ContentWrapperAttribute> specifica uno o più tipi nel tipo di raccolta associato che verrà utilizzato per eseguire il wrapping di contenuto esterno.  Quest'ultimo si riferisce ai casi in cui i vincoli del sistema di tipi sul tipo della proprietà di contenuto non acquisiscono tutti i possibili casi di contenuto che verrebbero supportati dall'utilizzo di XAML per il tipo proprietario.  Ad esempio, il supporto XAML per il contenuto di un particolare tipo può supportare le stringhe in un oggetto <xref:System.Collections.ObjectModel.Collection%601> generico fortemente tipizzato.  I wrapper del contenuto sono utili per la migrazione di convenzioni del markup preesistenti nella concezione di XAML di valori assegnabili per le raccolte, ad esempio la migrazione di modelli di contenuto correlati al testo.  
  
 Per specificare più tipi di wrapper del contenuto, applicare più volte l'attributo.  
  
### DependsOnAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.DependsOnAttribute>  
  
 **Si applica a:** proprietà  
  
 **Argomenti:** stringa che specifica il nome di un altro membro del tipo con attributo.  
  
 <xref:System.Windows.Markup.DependsOnAttribute> indica che la proprietà con attributi dipende dal valore di un'altra proprietà.  L'applicazione di questo attributo a una definizione della proprietà garantisce che le proprietà dipendenti vengano elaborate per prime nella scrittura di oggetti XAML.  Gli utilizzi di <xref:System.Windows.Markup.DependsOnAttribute> specificano i casi eccezionali di proprietà in tipi in cui è necessario seguire un ordine di analisi specifico per creare oggetti validi.  
  
 È possibile applicare più casi di <xref:System.Windows.Markup.DependsOnAttribute> a una definizione di proprietà.  
  
### MarkupExtensionReturnTypeAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>  
  
 **Si applica a:** classe, che si prevede sia un tipo derivato da <xref:System.Windows.Markup.MarkupExtension>.  
  
 **Argomenti:** oggetto <xref:System.Type> che specifica il tipo più preciso previsto come risultato di `ProvideValue` dell'oggetto <xref:System.Windows.Markup.MarkupExtension> con attributi.  
  
 Per ulteriori informazioni, vedere [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md).  
  
### NameScopePropertyAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.NameScopePropertyAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** supporta le due forme di attribuzione indicate di seguito.  
  
-   Una stringa che specifica il nome di una proprietà nel tipo a cui è stato applicato l'attributo.  
  
-   Una stringa che specifica il nome di una proprietà e un oggetto <xref:System.Type> per il tipo che definisce la proprietà denominata.  Questa forma serve a specificare un membro associabile come proprietà del NameScope XAML.  
  
 <xref:System.Windows.Markup.NameScopePropertyAttribute> specifica una proprietà che fornisce il valore del NameScope XAML per la classe a cui è stato applicato l'attributo.  La proprietà del NameScope XAML deve fare riferimento a un oggetto che implementa <xref:System.Windows.Markup.INameScope> e contiene il NameScope XAML effettivo, con il relativo archivio e comportamento.  
  
### RuntimeNamePropertyAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** stringa che specifica il nome della proprietà del nome runtime nel tipo a cui è stato applicato l'attributo.  
  
 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> segnala una proprietà del tipo con attributo che esegue il mapping alla direttiva [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md) XAML.  La proprietà deve essere di tipo <xref:System.String> e deve essere inoltre di lettura\/scrittura.  
  
 La definizione eredita in tutti i tipi derivati assegnabili al tipo di definizione.  È possibile eseguire l'override della definizione in un tipo derivato specifico applicando <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> nel tipo in questione.  
  
### TrimSurroundingWhitespaceAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>  
  
 **Si applica a:** tipi  
  
 **Argomenti:** nessuno.  
  
 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute> viene applicato a tipi specifici che possono essere visualizzati come elementi figlio all'interno di contenuto con spazi vuoti significativi, ovvero il contenuto di una raccolta che dispone di <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>.  <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute> riguarda principalmente il percorso di salvataggio, ma può essere ottenuto nel sistema di tipi XAML nel percorso di caricamento esaminando <xref:System.Xaml.XamlType.TrimSurroundingWhitespace%2A?displayProperty=fullName>.  Per ulteriori informazioni, vedere [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
### TypeConverterAttribute  
 **Documentazione di riferimento:**  <xref:System.ComponentModel.TypeConverterAttribute>  
  
 **Si applica a:** classe, proprietà, metodo \(l'unico caso di metodo valido per XAML è una funzione di accesso `get` che supporta un membro associabile\).  
  
 **Argomenti:** oggetto <xref:System.Type> di <xref:System.ComponentModel.TypeConverter>.  
  
 <xref:System.ComponentModel.TypeConverterAttribute>, in un contesto XAML, fa riferimento a un oggetto <xref:System.ComponentModel.TypeConverter> personalizzato.  <xref:System.ComponentModel.TypeConverter> fornisce il comportamento di conversione dei tipi per i tipi personalizzati o i membri del tipo in questione.  
  
 Si applica l'attributo <xref:System.ComponentModel.TypeConverterAttribute> al tipo facendo riferimento all'implementazione del convertitore di tipi.  È possibile definire i convertitori di tipi per XAML nelle classi, nelle strutture o nelle interfacce.  Non è necessario fornire la conversione di tipi per le enumerazioni in quanto è abilitata a livello nativo.  
  
 Il convertitore di tipi deve essere in grado di convertire nel tipo di destinazione desiderato una stringa utilizzata per gli attributi o per il testo di inizializzazione nel markup.  Per ulteriori informazioni, vedere [TypeConverter e XAML](../../../ocs/framework/wpf/advanced/typeconverters-and-xaml.md).  
  
 Anziché essere applicato a tutti i valori di un tipo, un comportamento del convertitore di tipi per XAML può anche essere impostato per una proprietà specifica.  In questo caso, si applica <xref:System.ComponentModel.TypeConverterAttribute> alla definizione della proprietà \(la definizione esterna, non le definizioni `get` e `set` specifiche\).  
  
 Un comportamento del convertitore di tipi per l'utilizzo di XAML di un membro associabile personalizzato può essere assegnato applicando <xref:System.ComponentModel.TypeConverterAttribute> alla funzione di accesso `get` del metodo che supporta l'utilizzo di XAML.  
  
 Analogamente a <xref:System.ComponentModel.TypeConverter>, <xref:System.ComponentModel.TypeConverterAttribute> esisteva in .NET Framework prima che fosse introdotto XAML e il modello del convertitore di tipi serviva ad altri scopi.  Per utilizzare e fare riferimento a <xref:System.ComponentModel.TypeConverterAttribute>, è necessario indicare il nome completo dell'attributo o fornire un'istruzione `using` per <xref:System.ComponentModel>.  È inoltre necessario includere l'assembly di sistema nel progetto.  
  
### UidPropertyAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.UidPropertyAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** una stringa che fa riferimento alla proprietà pertinente in base al nome.  
  
 Indica la proprietà CLR di una classe che definisce un alias per [x:Uid Directive](../../../docs/framework/xaml-services/x-uid-directive.md).  
  
### UsableDuringInitializationAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.UsableDuringInitializationAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** un valore booleano.  Se utilizzato per lo scopo previsto dell'attributo, il valore specificato deve sempre essere `true`.  
  
 Indica se questo tipo è compilato dall'alto verso il basso durante la creazione di un oggetto grafico di XAML.  Si tratta di un concetto avanzato, con ogni probabilità strettamente correlato alla definizione del modello di programmazione.  Per ulteriori informazioni, vedere <xref:System.Windows.Markup.UsableDuringInitializationAttribute>.  
  
### ValueSerializerAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.ValueSerializerAttribute>  
  
 **Si applica a:** classe, proprietà, metodo \(l'unico caso di metodo valido per XAML è una funzione di accesso `get` che supporta un membro associabile\).  
  
 **Argomenti:** un oggetto <xref:System.Type> che specifica la classe di supporto del serializzatore di valori da utilizzare quando si serializzano tutte le proprietà del tipo a cui è stato applicato l'attributo o la proprietà con attributo specifica.  
  
 <xref:System.Windows.Markup.ValueSerializer> specifica una classe di serializzazione di valori che necessita di stato e contesto più precisi rispetto a <xref:System.ComponentModel.TypeConverter>.  <xref:System.Windows.Markup.ValueSerializer> può essere associato a un membro associabile applicando l'attributo <xref:System.Windows.Markup.ValueSerializerAttribute> nel metodo della funzione di accesso `get` statica per il membro associabile.  La serializzazione di valori è inoltre applicabile a enumerazioni, interfacce e strutture, ma non ai delegati.  
  
### WhitespaceSignificantCollectionAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>  
  
 **Si applica a:** Class, in particolare ai tipi Collection che devono ospitare contenuto misto, in cui lo spazio vuoto attorno agli elementi Object può essere significativo ai fini della rappresentazione dell'interfaccia utente.  
  
 **Argomenti:** nessuno.  
  
 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> indica che un tipo di raccolta deve essere elaborato da un processore XAML come raccolta con spazi vuoti significativi, il che influisce sulla costruzione dei nodi di valori del flusso del nodo XAML all'interno della raccolta.  Per ulteriori informazioni, vedere [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md).  
  
### XamlDeferLoadAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XamlDeferLoadAttribute>  
  
 **Si applica a:** classe, proprietà.  
  
 **Argomenti:** supporta due tipi di forme di attribuzione, ovvero tipi come stringhe o tipi come <xref:System.Type>.  Vedere <xref:System.Windows.Markup.XamlDeferLoadAttribute>.  
  
 Indica che una classe o una proprietà prevede l'utilizzo del caricamento posticipato per XAML \(come il comportamento dei modelli\) e segnala la classe che consente tale comportamento e il relativo tipo di contenuto\/destinazione.  
  
### XamlSetMarkupExtensionAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** denomina il callback.  
  
 Indica che una classe può utilizzare un'estensione di markup per fornire un valore per una o più proprietà e fa riferimento a un gestore che deve essere chiamato da un writer XAML prima di eseguire un'operazione di impostazione dell'estensione di markup in qualsiasi proprietà della classe.  
  
### XamlSetTypeConverterAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XamlSetTypeConverterAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** denomina il callback.  
  
 Indica che una classe può utilizzare un convertitore di tipi per fornire un valore per una o più proprietà e fa riferimento a un gestore che deve essere chiamato da un writer XAML prima di eseguire un'operazione di impostazione del convertitore di tipi in qualsiasi proprietà della classe.  
  
### XmlLangPropertyAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XmlLangPropertyAttribute>  
  
 **Si applica a:** classe  
  
 **Argomenti:** una stringa che specifica il nome della proprietà per la quale definire l'alias `xml:lang` nel tipo a cui è stato applicato l'attributo.  
  
 <xref:System.Windows.Markup.XmlLangPropertyAttribute> segnala una proprietà del tipo con attributo che esegue il mapping alla direttiva `lang` XML.  La proprietà non è necessariamente di tipo <xref:System.String> ma deve essere assegnabile da una stringa, ad esempio associando un convertitore di tipi al tipo della proprietà o alla proprietà specifica.  La proprietà deve essere di lettura\/scrittura.  
  
 Lo scenario per il mapping di `xml:lang` è tale che un modello a oggetti runtime può accedere alle informazioni sul linguaggio specificate da XML senza alcuna elaborazione specifica con un oggetto XMLDOM.  
  
 La definizione eredita in tutti i tipi derivati assegnabili al tipo di definizione.  È possibile eseguire l'override della definizione in un tipo derivato specifico applicando <xref:System.Windows.Markup.XmlLangPropertyAttribute> nel tipo in questione, benché questo non sia uno scenario comune.  
  
## Attributi CLR correlati a XAML a livello di assembly  
 Nelle sezioni che seguono sono descritti gli attributi correlati a XAML che non vengono applicati a tipi o a definizioni di membri, bensì ad assembly.  Questi attributi riguardano l'obiettivo complessivo di definire una libreria contenente tipi personalizzati da utilizzare nel codice XAML.  Alcuni degli attributi non influiscono necessariamente in modo diretto sul flusso del nodo XAML, ma vengono passati nel flusso del nodo per l'utilizzo da parte di altri consumer.  I consumer delle informazioni includono gli ambienti di progettazione o i processi di serializzazione che necessitano delle informazioni sullo spazio dei nomi XAML e sul prefisso associato.  Queste informazioni vengono inoltre utilizzate dai contesti di schemi XAML, incluso quello predefinito dei servizi XAML di .NET Framework.  
  
### XmlnsCompatibleWithAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>  
  
 **Argomenti:**  
  
-   Una stringa che specifica l'identificatore dello spazio dei nomi XAML da classificare.  
  
-   Una stringa che specifica l'identificatore dello spazio dei nomi XAML che può classificare lo spazio dei nomi XAML dell'argomento precedente.  
  
 <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute> specifica che uno spazio dei nomi XAML può essere classificato da un altro spazio dei nomi XAML.  In genere, lo spazio dei nomi XAML classificato è indicato in un oggetto <xref:System.Windows.Markup.XmlnsDefinitionAttribute> precedentemente definito.  Questa tecnica può essere utilizzata per controllare le versioni di un vocabolario XAML in una libreria e renderlo compatibile con il markup precedentemente definito per il vocabolario della versione precedente.  
  
### XmlnsDefinitionAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XmlnsDefinitionAttribute>  
  
 **Argomenti:**  
  
-   Una stringa che specifica l'identificatore dello spazio dei nomi XAML da definire.  
  
-   Una stringa che denomina uno spazio dei nomi CLR.  Lo spazio dei nomi CLR deve definire tipi pubblici nell'assembly e, almeno uno dei tipi dello spazio dei nomi CLR deve essere destinato all'utilizzo nel codice XAML.  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> specifica un mapping basato su assembly tra uno spazio dei nomi XAML e uno spazio dei nomi CLR, il quale verrà utilizzato da un writer di oggetti XAML o dal contesto dello schema XAML per la risoluzione del tipo.  
  
 Più oggetti <xref:System.Windows.Markup.XmlnsDefinitionAttribute> possono essere applicati a un assembly  per qualsiasi combinazione dei seguenti motivi:  
  
-   La progettazione della libreria contiene più spazi dei nomi CLR per l'organizzazione logica dell'accesso alle API in fase di esecuzione, tuttavia si desidera che tutti i tipi in tali spazi dei nomi siano utilizzabili con XAML facendo riferimento allo stesso spazio dei nomi XAML.  In questo caso si applicano diversi attributi <xref:System.Windows.Markup.XmlnsDefinitionAttribute> utilizzando lo stesso valore di <xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> ma valori diversi di <xref:System.Windows.Markup.XmlnsDefinitionAttribute.ClrNamespace%2A>.  Questa procedura è particolarmente utile se si definiscono mapping per lo spazio dei nomi XAML considerato dal framework o dall'applicazione come lo spazio dei nomi XAML predefinito nell'utilizzo comune.  
  
-   La progettazione della libreria contiene più spazi dei nomi CLR e si desidera una separazione intenzionale degli spazi dei nomi XAML tra gli utilizzi dei tipi negli spazi dei nomi CLR.  
  
-   Si definisce uno spazio dei nomi CLR nell'assembly e si desidera che sia accessibile tramite più spazi dei nomi XAML.  Questo scenario ha luogo in caso di supporto di più vocabolari con la stessa codebase.  
  
-   Si definisce il supporto del linguaggio XAML in uno o più spazi dei nomi CLR.  Per questi il valore di <xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> deve essere `http://schemas.microsoft.com/winfx/2006/xaml`.  
  
### XmlnsPrefixAttribute  
 **Documentazione di riferimento:**  <xref:System.Windows.Markup.XmlnsPrefixAttribute>  
  
 **Argomenti:**  
  
-   Una stringa che specifica l'identificatore di uno spazio dei nomi XAML.  
  
-   Una stringa che specifica un prefisso consigliato.  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> specifica un prefisso consigliato da utilizzare per uno spazio dei nomi XAML.  Il prefisso è utile in caso di scrittura di elementi e attributi in un file XAML serializzato dall'oggetto <xref:System.Xaml.XamlXmlWriter> dei servizi XAML di .NET Framework, oppure in caso di interazione tra una libreria di implementazione XAML con un ambiente di progettazione che dispone di funzionalità di modifica XAML.  
  
 Più oggetti <xref:System.Windows.Markup.XmlnsPrefixAttribute> possono essere applicati a un assembly  per qualsiasi combinazione dei seguenti motivi:  
  
-   L'assembly definisce tipi per più spazi dei nomi XAML.  In questo caso è necessario definire valori di prefisso diversi per ogni spazio dei nomi XAML.  
  
-   Si supportano più vocabolari e si utilizzano prefissi diversi per ogni vocabolario e spazio dei nomi XAML.  
  
-   Si definisce il supporto del linguaggio XAML nell'assembly e si dispone di un oggetto <xref:System.Windows.Markup.XmlnsDefinitionAttribute> per `http://schemas.microsoft.com/winfx/2006/xaml`.  In questo caso, in genere, è necessario alzare di livello il prefisso `x`.  
  
> [!NOTE]
>  I servizi XAML di .NET Framework definiscono inoltre l'attributo correlato a XAML <xref:System.Windows.Markup.RootNamespaceAttribute>.  Si tratta di un attributo a livello di assembly per il supporto del sistema del progetto che non riguarda i tipi personalizzati XAML.  
  
## Vedere anche  
 <xref:System.Attribute>   
 [Defining Custom Types for Use with .NET Framework XAML Services](../../../docs/framework/xaml-services/defining-custom-types-for-use-with-net-framework-xaml-services.md)