---
title: "XAML Services | Microsoft Docs"
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
  - "XAML [XAML Services], System.Xaml concepts"
  - "XAML Services in WPF [XAML Services]"
  - "System.Xaml [XAML Services], conceptual documentation"
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# XAML Services
In questo argomento vengono descritte le funzionalità di un set di tecnologie noto come servizi XAML di .NET Framework.  La maggior parte delle API e dei servizi descritti si trovano nell'assembly System.Xaml, introdotto con il set di assembly principali .NET di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].  I servizi includono reader e writer, classi dello schema e supporto dello schema, factory, assegnazione di attributi alle classi, supporto intrinseco del linguaggio XAML e altre funzionalità del linguaggio XAML.  
  
## Informazioni sulla documentazione  
 Nella documentazione concettuale sui servizi XAML di .NET Framework si presuppone che l'utente disponga di esperienza precedente nel linguaggio XAML e nella sua possibile applicazione a un framework specifico, ad esempio [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] o [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)], oppure in un'area di funzionalità di tecnologie specifiche, ad esempio le funzionalità di personalizzazione di compilazione in <xref:Microsoft.Build.Framework.XamlTypes>.  In questa documentazione non vengono spiegate le basi di XAML come linguaggio di markup, terminologia della sintassi XAML o altro materiale introduttivo.  Al contrario, viene posta l'attenzione sull'utilizzo specifico dei servizi XAML di .NET Framework abilitati nella libreria dell'assembly System.Xaml.  La maggior parte di queste API è destinata a scenari di integrazione ed estensibilità del linguaggio XAML.  Tra i vari scenari sono inclusi i seguenti:  
  
-   Estensione delle funzionalità dei reader XAML o writer XAML di base \(elaborazione diretta del flusso del nodo XAML; derivazione di un reader XAML o writer XAML personalizzato\).  
  
-   Definizione di tipi personalizzati utilizzabili in XAML privi di qualsiasi dipendenza da framework specifici e assegnazione di attributi ai tipi per indicare le caratteristiche del sistema di tipi XAML ai servizi XAML di .NET Framework.  
  
-   Hosting di reader e writer XAML come componente di un'applicazione, ad esempio una finestra di progettazione visiva o un editor interattivo per le origini del markup XAML.  
  
-   Scrittura di convertitori di valori XAML \(estensioni di markup; convertitori di tipi per tipi personalizzati\).  
  
-   Definizione del contesto dello schema XAML personalizzato \(tramite tecniche alternative di caricamento degli assembly per le origini di tipi di supporto; tramite tecniche di tipi noti anziché sempre tramite la riflessione di assembly; tramite concetti di assembly caricati che non utilizzano l'oggetto `AppDomain` CLR e il modello di sicurezza associato\).  
  
-   Estensione del sistema dei tipi XAML di base.  
  
-   Utilizzo delle tecniche `Lookup` o `Invoker` per influire sul sistema dei tipi XAML sulla modalità di valutazione dei supporti dei tipi.  
  
 Se si sta cercando materiale introduttivo su XAML come linguaggio, vedere [Cenni preliminari su XAML \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md).  Le informazioni su XAML fornite in questo argomento sono destinate agli utenti che non dispongono di esperienza nell'utilizzo di [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] e del markup XAML, nonché delle funzionalità del linguaggio XAML.  Un altro documento utile è il materiale introduttivo fornito nella pagina relativa alla [specifica del linguaggio XAML](http://go.microsoft.com/fwlink/?LinkId=114525).  
  
## Servizi XAML di .NET Framework e System.Xaml nell'architettura .NET  
 Nelle versioni precedenti di [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] il supporto per le funzionalità del linguaggio XAML veniva implementato da framework basati su [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] \([!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_workflow](../../../includes/tlasharptla-workflow-md.md)] e [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)]\) e pertanto, a seconda del framework specifico utilizzato, variavano il relativo comportamento e l'API utilizzata.  Questo aspetto riguardava il parser XAML e il meccanismo di creazione di oggetti grafici, gli intrinseci del linguaggio XAML, il supporto della serializzazione e così via.  
  
 In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] i servizi della struttura XAML di .NET e l'assemblea di System.Xaml definiscono molto di che cosa è necessario per l'appoggio delle caratteristiche di lingua di XAML.  incluse le classi di base per reader XAML e writer XAML.  La funzionalità più importante aggiunta ai servizi XAML di .NET Framework, assente in qualsiasi implementazione XAML specifica del framework, è una rappresentazione del sistema di tipi per XAML.  Nella rappresentazione del sistema di tipi XAML è presentato in un modo orientato agli oggetti che si concentra sulle funzionalità XAML senza accettare dipendenze da funzionalità specifiche dei framework.  
  
 Il sistema di tipi XAML non è limitato dalle specifiche del formato di markup o di runtime dell'origine di XAML, né da qualsiasi sistema del tipo di supporto specifico.  Il sistema di tipi XAML include rappresentazioni dell'oggetto per tipi, membri, contesti dello schema XAML, concetti a livello di XML e altri concetti del linguaggio XAML o intrinseci XAML.  L'utilizzo o l'estensione del sistema di tipi XAML rende possibile derivare da classi quali reader XAML e writer XAML e consente di estendere le funzionalità delle rappresentazioni XAML in funzionalità specifiche abilitate da un framework, da una tecnologia o un'applicazione che utilizza o crea XAML.  Il concetto di un contesto dello schema XAML consente operazioni di scrittura pratiche di oggetti grafici dalla combinazione dell'implementazione di un writer di oggetti XAML, del sistema di tipi di supporto di una tecnologia comunicato tramite informazioni sull'assembly nel contesto e dell'origine del nodo XAML.  Per ulteriori informazioni sul concetto dello schema XAML,  vedere [Default XAML Schema Context and WPF XAML Schema Context](../../../docs/framework/xaml-services/default-xaml-schema-context-and-wpf-xaml-schema-context.md).  
  
## Flussi del nodo XAML, reader XAML e writer XAML  
 Per comprendere il ruolo svolto dai servizi XAML di .NET Framework nella relazione tra il linguaggio XAML e le tecnologie specifiche che utilizzano XAML come linguaggio, è utile approfondire il concetto di un flusso del nodo XAML e capire come questo concetto plasmi l'API e la terminologia.  Il flusso del nodo XAML è un elemento intermedio concettuale tra una rappresentazione del linguaggio XAML e l'oggetto grafico che XAML rappresenta o definisce.  
  
-   Un reader XAML è un'entità che elabora XAML in alcune forme e produce un flusso del nodo XAML.  Nell'API, un reader XAML viene rappresentato dalla classe di base <xref:System.Xaml.XamlReader>.  
  
-   Un writer XAML è un'entità che elabora un flusso del nodo XAML produce qualcos'altro.  Nell'API, un writer XAML viene rappresentato dalla classe di base <xref:System.Xaml.XamlWriter>.  
  
 I due scenari più comuni riguardanti XAML sono il caricamento di XAML per la creazione di un'istanza di un oggetto grafico e il salvataggio di un oggetto grafico da un'applicazione o da un strumento e la produzione di una rappresentazione XAML \(in genere in forma di markup salvato come file di testo\).  In questa documentazione il caricamento di XAML e la creazione di un oggetto grafico vengono spesso definiti come percorso di caricamento.  In questa documentazione il salvataggio o la serializzazione di un oggetto grafico esistente in XAML viene spesso definito come percorso di salvataggio.  
  
 È possibile descrivere il tipo più comune di percorso di caricamento nel modo seguente:  
  
-   Iniziare con una rappresentazione XAML, in formato XML con codifica UTF e salvata come file di testo.  
  
-   Caricare tale codice XAML in <xref:System.Xaml.XamlXmlReader>.  <xref:System.Xaml.XamlXmlReader> è una sottoclasse <xref:System.Xaml.XamlReader>.  
  
-   Il risultato è un flusso del nodo XAML.  È possibile accedere ai singoli nodi del flusso del nodo XAML utilizzando l'API <xref:System.Xaml.XamlXmlReader> \/ <xref:System.Xaml.XamlReader>.  L'operazione più tipica in questo caso è avanzare nel flusso del nodo XAML, elaborando ogni nodo con una metafora "record corrente".  
  
-   Passare i nodi risultanti dal flusso del nodo XAML a un'API <xref:System.Xaml.XamlObjectWriter>.  <xref:System.Xaml.XamlObjectWriter> è una sottoclasse <xref:System.Xaml.XamlWriter>.  
  
-   <xref:System.Xaml.XamlObjectWriter> scrive un oggetto grafico, un oggetto alla volta, in base all'avanzamento nel flusso del nodo XAML di origine.  Questa operazione viene eseguita con l'assistenza di un contesto dello schema XAML e di un'implementazione in grado di accedere agli assembly e ai tipi di un sistema di tipi di supporto e di un framework.  
  
-   Chiamare <xref:System.Xaml.XamlObjectWriter.Result%2A> alla fine del flusso del nodo XAML per ottenere l'oggetto radice dell'oggetto grafico.  
  
 È possibile descrivere il tipo più comune di percorso di salvataggio nel modo seguente:  
  
-   Iniziare con l'oggetto grafico di un intero runtime di applicazione, il contenuto dell'interfaccia utente e lo stato di un runtime o un segmento più piccolo della rappresentazione dell'oggetto di un'applicazione globale in fase di esecuzione.  
  
-   Da un oggetto di avvio logico, ad esempio la radice dell'applicazione o del documento, caricare gli oggetti in <xref:System.Xaml.XamlObjectReader>.  <xref:System.Xaml.XamlObjectReader> è una sottoclasse <xref:System.Xaml.XamlReader>.  
  
-   Il risultato è un flusso del nodo XAML.  È possibile accedere ai singoli nodi del flusso del nodo XAML utilizzando le API <xref:System.Xaml.XamlObjectReader> e <xref:System.Xaml.XamlReader>.  L'operazione più tipica in questo caso è avanzare nel flusso del nodo XAML, elaborando ogni nodo con una metafora "record corrente".  
  
-   Passare i nodi risultanti dal flusso del nodo XAML a un'API <xref:System.Xaml.XamlXmlWriter>.  <xref:System.Xaml.XamlXmlWriter> è una sottoclasse <xref:System.Xaml.XamlWriter>.  
  
-   <xref:System.Xaml.XamlXmlWriter> scrive il codice XAML in XML con codifica UTF.  È possibile eseguirne il salvataggio come file di testo, come flusso o in altro formato.  
  
-   Chiamare <xref:System.Xaml.XamlXmlWriter.Flush%2A> per ottenere l'output finale.  
  
 Per ulteriori informazioni sui concetti dei flussi del nodo XAML, vedere [Understanding XAML Node Stream Structures and Concepts](../../../docs/framework/xaml-services/understanding-xaml-node-stream-structures-and-concepts.md).  
  
### Classe XamlServices  
 Non è sempre necessario gestire un flusso del nodo XAML.  Se si desidera un percorso di caricamento di base o un percorso di salvataggio di base, è possibile utilizzare le API nella classe <xref:System.Xaml.XamlServices>.  
  
-   Diverse firme di <xref:System.Xaml.XamlServices.Load%2A> implementano un percorso di caricamento.  È possibile caricare un file o un flusso oppure caricare un oggetto <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> o <xref:System.Xaml.XamlReader> che esegue il wrapping dell'input XAML tramite caricamento con le API di tale reader.  
  
-   Diverse firme di <xref:System.Xaml.XamlServices.Save%2A> salvano un oggetto grafico e producono l'output come flusso o file oppure come un'istanza di <xref:System.Xml.XmlWriter>\/<xref:System.IO.TextWriter>.  
  
-   <xref:System.Xaml.XamlServices.Transform%2A> esegue la conversione di XAML tramite il collegamento a un percorso di caricamento e a un percorso di salvataggio come una sola operazione.  Per <xref:System.Xaml.XamlReader> e <xref:System.Xaml.XamlWriter> è possibile utilizzare un contesto dello schema diverso o un sistema di tipi di supporto diverso, essendo questi gli elementi che influenzano il modo in cui il codice XAML risultante viene trasformato.  
  
 Per ulteriori informazioni sull'utilizzo di <xref:System.Xaml.XamlServices>, vedere [XAMLServices Class and Basic XAML Reading or Writing](../../../docs/framework/xaml-services/xamlservices-class-and-basic-xaml-reading-or-writing.md).  
  
## Sistema di tipi XAML  
 Il sistema di tipi XAML fornisce le API necessarie per utilizzare un determinato singolo nodo di un flusso del nodo XAML.  
  
 <xref:System.Xaml.XamlType> è la rappresentazione per un oggetto, ovvero il contenuto elaborato tra un nodo oggetto iniziale e un nodo oggetto finale.  
  
 <xref:System.Xaml.XamlMember> è la rappresentazione per un membro di un oggetto, ovvero il contenuto elaborato tra un nodo membro iniziale e un nodo membro finale.  
  
 Le API quali <xref:System.Xaml.XamlType.GetAllMembers%2A> e <xref:System.Xaml.XamlType.GetMember%2A> e <xref:System.Xaml.XamlMember.DeclaringType%2A> segnalano le relazioni tra un oggetto <xref:System.Xaml.XamlType> e <xref:System.Xaml.XamlMember>.  
  
 Il comportamento predefinito del sistema di tipi XAML implementato dai servizi XAML di .NET Framework si basa su Common Language Runtime \(CLR\) e sull'analisi statica di tipi CLR negli assembly tramite reflection.  Pertanto, per un tipo CLR specifico, l'implementazione predefinita del sistema di tipi XAML può esporre lo schema XAML di tale tipo e i relativi membri e segnalarlo nei termini del sistema di tipi XAML.  Nel sistema di tipi XAML predefinito il concetto di assegnabilità dei tipi è associato all'ereditarietà CLR e i concetti di istanze, tipi di valore e così via sono anch'essi associati ai comportamenti e alle funzionalità di supporto del linguaggio CLR.  
  
## Riferimento per funzionalità del linguaggio XAML  
 Per supportare XAML, i servizi XAML di .NET Framework forniscono un'implementazione specifica dei concetti del linguaggio XAML definiti per lo spazio dei nomi XAML del linguaggio XAML.  Questi vengono documentati come pagine di riferimento specifiche.  Le funzionalità del linguaggio vengono documentate dal punto di vista del relativo comportamento in caso di elaborazione da parte di un reader XAML o un writer XAML definito dai servizi XAML di .NET Framework.  Per ulteriori informazioni, vedere [XAML Namespace \(x:\) Language Features](../../../docs/framework/xaml-services/xaml-namespace-x-language-features.md).