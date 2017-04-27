---
title: "Serializzazione e archiviazione di documenti | Microsoft Docs"
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
  - "documenti, serializzazione"
  - "documenti, storage"
  - "serializzazione di documenti"
  - "archiviazione di documenti"
ms.assetid: 4839cd87-e206-4571-803f-0200098ad37b
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# Serializzazione e archiviazione di documenti
[!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] offre un ambiente avanzato per la creazione e la visualizzazione di documenti di alta qualità.  Funzionalità avanzate che supportano documenti sia statici sia dinamici e controlli di visualizzazione avanzati combinati con potenti funzionalità grafiche 2D e 3D consentono la creazione di applicazioni [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] di livello elevato in termini di qualità ed esperienza utente.  La possibilità di gestire in modo flessibile la rappresentazione in memoria di un documento è una funzionalità chiave di [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] e la capacità di salvare e caricare documenti in modo efficiente da un archivio dati è l'esigenza di ogni applicazione.  Il processo di conversione di un documento da una rappresentazione in memoria interna a un archivio dati esterno è detto [serializzazione](GTMT).  Il processo inverso di lettura di un archivio dati e creazione dell'istanza in memoria originale è detto deserializzazione.  
  
   
  
<a name="AboutSerialization"></a>   
## Informazioni sulla serializzazione di documenti  
 In teoria, il processo di [serializzazione](GTMT) e deserializzazione di un documento in memoria è trasparente all'applicazione.  L'applicazione chiama un metodo di scrittura del serializzatore per salvare il documento, mentre un metodo di lettura del deserializzatore accede all'archivio dati e crea nuovamente l'istanza originale in memoria.  Il formato specifico in cui vengono archiviati i dati non costituisce in genere motivo di preoccupazione per l'applicazione, purché il processo di serializzazione e deserializzazione ricrei il documento nel formato originale.  
  
 Nelle applicazioni sono spesso disponibili varie opzioni di serializzazione che consentono all'utente di salvare documenti in supporti o formati diversi.  Ad esempio, è possibile che in un'applicazione siano disponibili opzioni "Salva con nome" per l'archiviazione di un file su disco, in un database o come servizio Web.  Allo stesso modo, serializzatori diversi potrebbero archiviare il documento in formati diversi quali HTML, RTF, XML, XPS o, in alternativa, in un formato di terze parti.  Per l'applicazione, la serializzazione definisce un'interfaccia che isola i dettagli del supporto di archiviazione nell'implementazione di ogni specifico serializzatore.  Oltre ai vantaggi offerti dalla possibilità di incapsulare i dettagli di archiviazione, le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] <xref:System.Windows.Documents.Serialization> [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] forniscono altre importanti funzionalità.  
  
### Funzionalità dei serializzatori di documenti di .NET Framework 3.0  
  
-   L'accesso diretto agli oggetti documento di alto livello \([albero logico](GTMT) ed elementi visivi\) consente di archiviare in modo efficiente contenuto impaginato, elementi 2D\/3D, immagini, supporti, collegamenti ipertestuali, annotazioni e altro contenuto di supporto.  
  
-   Operazione [sincrona](GTMT) e [asincrona](GTMT).  
  
-   Supporto per serializzatori plug\-in con funzionalità avanzate:  
  
    -   Accesso a livello di sistema disponibile da tutte le applicazioni [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)].  
  
    -   Individuazione semplice dei plug\-in dell'applicazione.  
  
    -   Facilità di distribuzione, installazione e aggiornamento per i plug\-in di terze parti personalizzati.  
  
    -   Supporto dell'interfaccia utente per impostazioni e opzioni di runtime personalizzate.  
  
### Percorso di stampa XPS  
 Il percorso di stampa [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] di [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] offre inoltre un meccanismo estensibile per la scrittura di documenti tramite l'output di stampa.  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] funge sia da formato di file di documento sia da formato nativo dello spooling di stampa per documenti [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  I documenti [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] possono essere inviati direttamente alle stampanti conformi a [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] senza la necessità di conversione in un formato intermedio.  Per ulteriori informazioni sulle opzioni e le funzionalità dell'output del percorso di stampa, vedere [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md).  
  
<a name="PluginSerializers"></a>   
## Serializzatori plug\-in  
 Le API <xref:System.Windows.Documents.Serialization> offrono supporto per serializzatori plug\-in e serializzatori collegati installati separatamente dall'applicazione, associati in fase di esecuzione e a cui si accede utilizzando il meccanismo di individuazione di <xref:System.Windows.Documents.Serialization.SerializerProvider>.  I serializzatori plug\-in offrono notevoli vantaggi in termini di facilità di distribuzione e utilizzo a livello di sistema.  I serializzatori collegati possono anche essere implementati per ambienti [parzialmente attendibili](GTMT), ad esempio applicazioni [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] in cui non sono accessibili serializzatori plug\-in.  I serializzatori collegati, basati su un'implementazione derivata della classe <xref:System.Windows.Documents.Serialization.SerializerWriter>, vengono compilati e collegati direttamente nell'applicazione.  Sia i serializzatori plug\-in, sia i serializzatori collegati funzionano tramite eventi e metodi pubblici identici che semplificano l'utilizzo di uno o di entrambi i tipi di serializzatori nella stessa applicazione.  
  
 I serializzatori plug\-in offrono agli sviluppatori di applicazioni estensibilità per nuovi progetti di archiviazione e formati di file senza la necessità di scrivere direttamente codice per ogni potenziale formato in fase di compilazione.  I serializzatori plug\-in sono inoltre utili agli sviluppatori di terze parti in quanto forniscono un mezzo standardizzato per distribuire, installare e aggiornare plug\-in accessibili al sistema per formati di file personalizzati o proprietari.  
  
### Utilizzo di un serializzatore plug\-in  
 I serializzatori plug\-in sono semplici da utilizzare.  La classe <xref:System.Windows.Documents.Serialization.SerializerProvider> enumera un oggetto <xref:System.Windows.Documents.Serialization.SerializerDescriptor> per ogni plug\-in installato nel sistema.  La proprietà <xref:System.Windows.Documents.Serialization.SerializerDescriptor.IsLoadable%2A> filtra i plug\-in installati in base alla configurazione corrente e verifica che il serializzatore possa essere caricato e utilizzato dall'applicazione.  L'oggetto <xref:System.Windows.Documents.Serialization.SerializerDescriptor> fornisce anche altre proprietà, quali <xref:System.Windows.Documents.Serialization.SerializerDescriptor.DisplayName%2A> e <xref:System.Windows.Documents.Serialization.SerializerDescriptor.DefaultFileExtension%2A>, che possono essere utilizzate dall'applicazione per richiedere all'utente la selezione di un serializzatore per un formato di output disponibile.  Un serializzatore plug\-in predefinito per [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] viene fornito con [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] ed è sempre enumerato.  Dopo la selezione di un formato di output da parte dell'utente, viene utilizzato il metodo <xref:System.Windows.Documents.Serialization.SerializerProvider.CreateSerializerWriter%2A> per creare un oggetto <xref:System.Windows.Documents.Serialization.SerializerWriter> per il formato specifico.  È quindi possibile chiamare il metodo <xref:System.Windows.Documents.Serialization.SerializerWriter>.<xref:System.Windows.Documents.Serialization.SerializerWriter.Write%2A> per restituire il flusso del documento all'archivio dati.  
  
 Nell'esempio riportato di seguito viene illustrata un'applicazione che utilizza il metodo <xref:System.Windows.Documents.Serialization.SerializerProvider> in una proprietà "PlugInFileFilter".  Questa proprietà enumera i plug\-in installati e compila una stringa di filtro con le opzioni di file disponibili per un oggetto <xref:Microsoft.Win32.SaveFileDialog>.  
  
 [!code-csharp[DocumentSerialize#DocSerializeFileFilter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocumentSerialize/CSharp/ThumbViewer.cs#docserializefilefilter)]  
  
 Dopo la selezione di un nome file di output da parte dell'utente, nell'esempio riportato di seguito viene illustrato l'utilizzo del metodo <xref:System.Windows.Documents.Serialization.SerializerProvider.CreateSerializerWriter%2A> per archiviare un determinato documento in un formato specificato.  
  
 [!code-csharp[DocumentSerialize#DocSerializePlugIn](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DocumentSerialize/CSharp/ThumbViewer.cs#docserializeplugin)]  
  
<a name="InstallingPluginSerializers"></a>   
### Installazione di serializzatori plug\-in  
 La classe <xref:System.Windows.Documents.Serialization.SerializerProvider> fornisce l'interfaccia dell'applicazione di livello superiore per l'individuazione e l'accesso al serializzatore plug\-in.  <xref:System.Windows.Documents.Serialization.SerializerProvider> individua e fornisce all'applicazione un elenco dei serializzatori installati e accessibili nel sistema.  Le specifiche dei serializzatori installati vengono definite tramite le impostazioni del Registro di sistema.  È possibile aggiungere i serializzatori plug\-in al Registro di sistema tramite il metodo <xref:System.Windows.Documents.Serialization.SerializerProvider.RegisterSerializer%2A>. In alternativa, se [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] non è ancora installato, è possibile impostare direttamente i valori del Registro di sistema tramite lo script di installazione del plug\-in.  È possibile utilizzare il metodo <xref:System.Windows.Documents.Serialization.SerializerProvider.UnregisterSerializer%2A> per rimuovere un plug\-in installato in precedenza oppure reimpostare le impostazioni del Registro di sistema in modo analogo tramite uno script di disinstallazione.  
  
### Creazione di un serializzatore plug\-in  
 Sia i serializzatori plug\-in sia i serializzatori collegati utilizzano gli stessi eventi e metodi pubblici esposti e possono essere progettati in modo analogo per funzionare in modalità [sincrona](GTMT) o [asincrona](GTMT).  Sono tre i passaggi in genere eseguiti per creare un serializzatore plug\-in:  
  
1.  Implementare ed eseguire il debug del serializzatore innanzitutto come serializzatore collegato.  La creazione iniziale di un serializzatore compilato e collegato direttamente in un'applicazione di prova consente l'accesso completo ai punti di interruzione e ad altri servizi di debug utili ai fini di test.  
  
2.  Dopo il test completo del serializzatore, viene aggiunta un'interfaccia <xref:System.Windows.Documents.Serialization.ISerializerFactory> per creare un plug\-in.  L'interfaccia <xref:System.Windows.Documents.Serialization.ISerializerFactory> offre l'accesso completo a tutti gli oggetti [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] che includono l'albero logico, agli oggetti <xref:System.Windows.UIElement> e agli elementi <xref:System.Windows.Documents.IDocumentPaginatorSource> e <xref:System.Windows.Media.Visual>.  Inoltre, <xref:System.Windows.Documents.Serialization.ISerializerFactory> fornisce gli stessi metodi ed eventi sincroni e asincroni utilizzati dai serializzatori collegati.  Poiché l'output dei documenti di grandi dimensioni richiede tempo, le operazioni asincrone sono consigliate per garantire l'interazione dell'utente e fornire un'opzione "Annulla" se si verifica un problema relativo all'archivio dati.  
  
3.  Dopo la creazione del serializzatore plug\-in, viene implementato uno script di installazione per la distribuzione e l'installazione e la disinstallazione del plug\-in \(vedere la sezione precedente "[Installazione di serializzatori plug\-in](#InstallingPluginSerializers)"\).  
  
## Vedere anche  
 <xref:System.Windows.Documents.Serialization>   
 <xref:System.Windows.Xps.XpsDocumentWriter>   
 <xref:System.Windows.Xps.Packaging.XpsDocument>   
 [Documenti in WPF](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [XML Paper Specification: cenni preliminari](http://go.microsoft.com/fwlink/?LinkID=106246)