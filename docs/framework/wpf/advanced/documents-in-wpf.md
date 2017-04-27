---
title: "Documenti in WPF | Microsoft Docs"
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
  - "documenti visualizzabili su browser"
  - "documenti, visualizzabili su browser"
  - "documenti, controlli"
  - "documenti, creazione di pacchetti"
  - "documenti, layout del testo"
  - "documenti, tipi"
  - "documenti, XPS"
  - "assemblaggio di documenti"
  - "XPS (documenti)"
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
caps.latest.revision: 36
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 35
---
# Documenti in WPF
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] offre un'ampia gamma di funzionalità dedicate ai documenti per la creazione di contenuto ad alta fedeltà progettato per garantire un accesso e una lettura semplificati rispetto alle generazioni precedenti di [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)].  Oltre a caratteristiche avanzate in termini di funzionalità e qualità, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] offre servizi integrati per la visualizzazione, l'assemblaggio e la sicurezza dei documenti.  In questo argomento viene fornita un'introduzione ai tipi di documenti [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e al loro assemblaggio.  
  
   
  
<a name="types_of_documents"></a>   
## Tipi di documenti  
 In [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] i documenti si suddividono in due categorie generali in base all'utilizzo previsto: documenti statici e documenti dinamici.  
  
 I documenti statici sono destinati ad applicazioni che richiedono una presentazione [!INCLUDE[TLA#tla_wys](../../../../includes/tlasharptla-wys-md.md)] precisa, indipendente dall'hardware di visualizzazione o di stampa.  Tra gli utilizzi tipici dei documenti statici sono incluse le attività di desktop publishing, elaborazione di testi e layout di form, in cui la corrispondenza alla progettazione della pagina originale è essenziale.  Come parte del layout, in un documento statico viene mantenuta la disposizione precisa degli elementi di contenuto indipendentemente dal dispositivo di visualizzazione o di stampa in uso.  Ad esempio, la pagina di un documento statico visualizzata con un'impostazione di 96 dpi non varia quando viene stampata con una stampante laser a 600 dpi o con un compositore di foto a 4800 dpi.  Il layout della pagina rimane invariato in ogni caso, sebbene la qualità del documento dipenda dalle capacità del dispositivo utilizzato.  
  
 Per contro, i documenti dinamici sono progettati per ottimizzare la visualizzazione e la leggibilità e sono particolarmente adatti quando la facilità di lettura è il principale requisito di utilizzo del documento.  Anziché essere impostati su un layout predefinito, questi documenti consentono di regolare e di far scorrere il contenuto in modo dinamico in base alle variabili in fase di esecuzione, ad esempio, le dimensioni della finestra, la risoluzione del dispositivo e le preferenze facoltative dell'utente.  Una pagina Web è un esempio semplice di documento dinamico in cui il contenuto delle pagine viene formattato in modo dinamico per adattarsi alla finestra corrente.  I documenti dinamici ottimizzano l'esperienza di visualizzazione e di lettura per l'utente, in base all'ambiente di runtime.  Ad esempio, lo stesso documento dinamico verrà riformattato in modo dinamico per una leggibilità ottimale sia su dispositivi di visualizzazione da 19 pollici ad alta risoluzione sia su piccoli schermi PDA da 2 x 3 pollici.  Tali documenti dispongono inoltre di numerose funzionalità incorporate tra cui la ricerca, le modalità di visualizzazione che ottimizzano la leggibilità e la possibilità di modificare le dimensioni e l'aspetto dei tipi di carattere.  Per figure, esempi e informazioni approfondite sui documenti dinamici, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  
  
<a name="document_viewer"></a>   
## Controlli dei documenti e layout del testo  
 In [!INCLUDE[TLA2#tla_avalonwinfx](../../../../includes/tla2sharptla-avalonwinfx-md.md)] è disponibile un set di controlli precompilati che semplificano l'utilizzo di documenti statici, documenti dinamici e testo generico in un'applicazione.  La visualizzazione del contenuto dei documenti statici è supportata tramite il controllo <xref:System.Windows.Controls.DocumentViewer>.  La visualizzazione del contenuto dei documenti dinamici è supportata da tre controlli: <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer> e <xref:System.Windows.Controls.FlowDocumentScrollViewer> che eseguono il mapping su scenari utente diversi \(vedere le sezioni riportate di seguito\).  Altri controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] forniscono un layout semplificato per supportare l'utilizzo generale di testo \(vedere la sezione [Testo nell'interfaccia utente](#text_in_the_user_interface) di seguito\).  
  
### Controllo dei documenti statici: DocumentViewer  
 Il controllo <xref:System.Windows.Controls.DocumentViewer> è progettato per visualizzare il contenuto di <xref:System.Windows.Documents.FixedDocument>.  Il controllo <xref:System.Windows.Controls.DocumentViewer> offre un'interfaccia utente intuitiva con supporto incorporato per operazioni comuni, tra cui stampa dell'output, copia negli Appunti, zoom e funzionalità di ricerca nel testo.  Il controllo consente di accedere a pagine di contenuto attraverso un meccanismo di scorrimento intuitivo.  Come tutti i controlli [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], <xref:System.Windows.Controls.DocumentViewer> supporta la modifica completa o parziale dello stile, che consente l'integrazione visiva del controllo praticamente in qualsiasi applicazione o ambiente.  
  
 <xref:System.Windows.Controls.DocumentViewer> è progettato per visualizzare il contenuto in sola lettura, mentre la modifica del contenuto non è disponibile e non è supportata.  
  
<a name="flow_document"></a>   
### Controlli dei documenti dinamici  
 **Nota:** per informazioni più dettagliate sulle funzionalità dei documenti dinamici e su come crearli, vedere [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md).  
  
 La visualizzazione del contenuto dei documenti dinamici è supportata da tre controlli: <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer> e <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
#### Controllo FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> include funzionalità che consentono all'utente di scegliere dinamicamente tra le varie modalità di visualizzazione, inclusa una modalità di visualizzazione a pagina singola \(una pagina per volta\), una modalità di visualizzazione a pagina doppia \(formato lettura libro\) e una modalità di visualizzazione a spostamento continuo \(infinito\).  Per ulteriori informazioni sulle modalità di visualizzazione, vedere <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>.  Se la possibilità di passare dinamicamente da una modalità di visualizzazione all'altra non è necessaria, i controlli <xref:System.Windows.Controls.FlowDocumentPageViewer> e <xref:System.Windows.Controls.FlowDocumentScrollViewer> forniscono visualizzatori di contenuto del flusso più semplici che sono fissi a una modalità di visualizzazione particolare.  
  
#### Controlli FlowDocumentPageViewer e FlowDocumentScrollViewer  
 Il controllo <xref:System.Windows.Controls.FlowDocumentPageViewer> visualizza il contenuto nella modalità di visualizzazione di una pagina alla volta mentre il controllo <xref:System.Windows.Controls.FlowDocumentScrollViewer> visualizza il contenuto nella modalità di scorrimento continuo.  <xref:System.Windows.Controls.FlowDocumentPageViewer> e <xref:System.Windows.Controls.FlowDocumentScrollViewer> rimangono fissi in una particolare modalità di visualizzazione.  Effettuare il confronto con il controllo <xref:System.Windows.Controls.FlowDocumentReader>, che include funzionalità che consentono all'utente di scegliere in modo dinamico tra le varie modalità di visualizzazione \(fornite dall'enumerazione <xref:System.Windows.Controls.FlowDocumentReaderViewingMode>\), a discapito di un utilizzo di risorse maggiore rispetto a <xref:System.Windows.Controls.FlowDocumentPageViewer> o <xref:System.Windows.Controls.FlowDocumentScrollViewer>.  
  
 Per impostazione predefinita, viene sempre visualizzata una barra di scorrimento verticale e diventa visibile una barra di scorrimento orizzontale, se necessario.  L'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] predefinita di <xref:System.Windows.Controls.FlowDocumentScrollViewer> non include una barra degli strumenti, ma la proprietà <xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> può essere utilizzata per abilitare una barra degli strumenti incorporata.  
  
<a name="text_in_the_user_interface"></a>   
### Testo nell'interfaccia utente  
 Oltre all'aggiunta di testo ai documenti, è ovviamente possibile utilizzare testo nell'interfaccia utente delle applicazioni, ad esempio nei form.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] include più controlli per la creazione di testo sullo schermo.  Ogni controllo è destinato a uno scenario diverso e dispone di un proprio elenco di funzionalità e limitazioni.  In genere, è opportuno utilizzare l'elemento <xref:System.Windows.Controls.TextBlock> quando è necessario un supporto limitato del testo, ad esempio una breve frase in un'[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)].  Quando è necessario un supporto minimo del testo, è possibile utilizzare <xref:System.Windows.Controls.Label>.  Per ulteriori informazioni, vedere [Cenni preliminari sul controllo TextBlock](../../../../docs/framework/wpf/controls/textblock-overview.md).  
  
<a name="packaging"></a>   
## Assemblaggio di documenti  
 Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] <xref:System.IO.Packaging> costituiscono un mezzo efficace per organizzare i dati dell'applicazione, il contenuto dei documenti e le relative risorse in un unico contenitore portabile e facilmente accessibile e distribuibile.  Un file ZIP è un esempio di un tipo di <xref:System.IO.Packaging.Package> in grado di contenere più oggetti come unità singola.  Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di assemblaggio forniscono un'implementazione <xref:System.IO.Packaging.ZipPackage> predefinita progettata tramite uno standard Open Packaging Conventions con architettura di file XML e ZIP.  Le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] di assemblaggio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] semplificano la creazione di package, oltre all'archiviazione e all'accesso agli oggetti che contengono.  Un oggetto archiviato in <xref:System.IO.Packaging.Package> viene denominato <xref:System.IO.Packaging.PackagePart> \("parte"\).  I package possono anche includere certificati digitali firmati utilizzabili per identificare il creatore di una parte e per confermare che il contenuto di un package non è stato modificato.  I package includono inoltre una funzionalità <xref:System.IO.Packaging.PackageRelationship> che consente l'aggiunta di ulteriori informazioni a un package o l'associazione di tali informazioni a parti specifiche senza modificare il contenuto delle parti esistenti.  I servizi di package supportano anche [!INCLUDE[TLA#tla_rm](../../../../includes/tlasharptla-rm-md.md)].  
  
 L'architettura dei package [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] costituisce la base per numerose tecnologie chiave:  
  
-   Documenti [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] conformi a [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)].  
  
-   Documenti in formato XML aperto di Microsoft Office "12" \(docx\)  
  
-   Formati di archiviazione personalizzati per la progettazione delle applicazioni.  
  
 In base alle API di assemblaggio, un oggetto <xref:System.Windows.Xps.Packaging.XpsDocument> viene specificamente progettato per l'archiviazione di documenti statici di [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  <xref:System.Windows.Xps.Packaging.XpsDocument> è un documento autonomo che può essere aperto in un visualizzatore, visualizzato in un controllo <xref:System.Windows.Controls.DocumentViewer>, indirizzato a uno spool di stampa o stampato direttamente con una stampante compatibile con [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  
  
 Nelle sezioni riportate di seguito vengono fornite informazioni aggiuntive sugli oggetti <xref:System.IO.Packaging.Package> e <xref:System.Windows.Xps.Packaging.XpsDocument> [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] forniti con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
<a name="packages"></a>   
### Componenti dei package  
 Le API di assemblaggio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consentono l'organizzazione dei dati delle applicazioni e dei documenti in un'unica unità portabile.  Uno dei tipi di pacchetto più comuni è il file ZIP, il tipo predefinito fornito con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  <xref:System.IO.Packaging.Package> è una classe astratta da cui viene implementato <xref:System.IO.Packaging.ZipPackage> tramite l'architettura basata sugli standard aperti dei file XML e ZIP.  Il metodo <xref:System.IO.Packaging.Package.Open%2A> utilizza <xref:System.IO.Packaging.ZipPackage> per creare e utilizzare file ZIP per impostazione predefinita.  Un pacchetto può contenere tre tipi di elementi di base:  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|Contenuto di applicazioni, dati, documenti e file di risorse.|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|[Certificato X.509](GTMT) per l'identificazione, l'autenticazione e la convalida.|  
|<xref:System.IO.Packaging.PackageRelationship>|Informazioni aggiunte relative al pacchetto o a una parte specifica.|  
  
<a name="PackageParts"></a>   
#### PackagePart  
 <xref:System.IO.Packaging.PackagePart> \("parte"\) è una classe astratta che fa riferimento a un oggetto archiviato in un oggetto <xref:System.IO.Packaging.Package>.  In un file ZIP, le parti del pacchetto corrispondono ai singoli file archiviati nel file ZIP.  <xref:System.IO.Packaging.ZipPackagePart> fornisce l'implementazione predefinita per gli oggetti serializzabili archiviati in un oggetto <xref:System.IO.Packaging.ZipPackage>.  Analogamente a un file system, le parti contenute nel pacchetto vengono archiviate secondo un'organizzazione di directory o cartelle di tipo gerarchico.  Grazie alle API di assemblaggio [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], è possibile scrivere, archiviare e leggere più oggetti <xref:System.IO.Packaging.PackagePart> dalle applicazioni in un unico contenitore di file ZIP.  
  
<a name="PackageDigitalSignatures"></a>   
#### PackageDigitalSignature  
 Per motivi di sicurezza, un oggetto <xref:System.IO.Packaging.PackageDigitalSignature> \("firma digitale"\) può essere associato alle parti di un pacchetto.  <xref:System.IO.Packaging.PackageDigitalSignature> incorpora un certificato [509](GTMT) che fornisce due funzionalità:  
  
1.  Identifica e autentica il creatore della parte.  
  
2.  Conferma che la parte non è stata modificata.  
  
 La firma digitale non impedisce la modifica di una parte, ma il controllo di convalida della firma digitale avrà esito negativo se la parte è stata modificata.  Nell'applicazione sarà quindi possibile intraprendere un'azione appropriata, ad esempio il blocco dell'apertura della parte o la notifica all'utente che la parte è stata modificata e non è sicura.  
  
<a name="PackageRelationships"></a>   
#### PackageRelationship  
 Un oggetto <xref:System.IO.Packaging.PackageRelationship> \("relazione"\) offre un meccanismo per l'associazione di informazioni aggiuntive al pacchetto o a una relativa parte.  Una relazione è una funzionalità a livello di pacchetto in grado di associare informazioni aggiuntive a una parte senza modificarne il contenuto.  L'inserimento di nuovi dati direttamente nel contenuto della parte spesso non è un'operazione pratica:  
  
-   Il tipo effettivo della parte e il relativo schema di contenuto non sono noti.  
  
-   Anche se è noto, lo schema di contenuto potrebbe non offrire un metodo per l'aggiunta di nuove informazioni.  
  
-   La parte potrebbe essere crittografata o firmata digitalmente, condizioni che impediscono qualsiasi modifica.  
  
 Le relazioni dei pacchetti offrono un metodo individuabile per aggiungere e associare ulteriori informazioni a singole parti o all'intero pacchetto.  Le relazioni dei pacchetti vengono utilizzate per due funzioni principali:  
  
1.  Definire le relazioni di dipendenza tra le parti.  
  
2.  Definire le relazioni delle informazioni che aggiungono note o altri dati correlati alla parte.  
  
 <xref:System.IO.Packaging.PackageRelationship> costituisce un modo rapido e individuabile per definire le dipendenze e aggiungere altre informazioni associate a una parte o all'intero pacchetto.  
  
<a name="Dependency_Relationships"></a>   
##### Relazioni di dipendenza  
 Le relazioni di dipendenza vengono utilizzate per descrivere le dipendenze tra le parti.  Ad esempio, un pacchetto può contenere una parte HTML che include uno o più tag immagine \<img\>.  I tag immagine fanno riferimento a immagini situate come altre parti interne o esterne al pacchetto \(ad esempio accessibili tramite Internet\).  La creazione di un oggetto <xref:System.IO.Packaging.PackageRelationship> associato con un file HTML consente di individuare e accedere alle risorse dipendenti in modo semplice e rapido.  Un'applicazione browser o visualizzatore può accedere direttamente alle relazioni delle parti e avviare immediatamente l'assemblaggio delle risorse dipendenti senza conoscere lo schema, né analizzare il documento.  
  
<a name="Information_Relationships"></a>   
##### Relazioni delle informazioni  
 Simile a una nota o a un'annotazione, un oggetto <xref:System.IO.Packaging.PackageRelationship> può anche essere utilizzato per archiviare altri tipi di informazioni da associare a una parte senza dover effettivamente modificare il contenuto della parte.  
  
<a name="XPS_Documents"></a>   
## Documenti XPS  
 Un documento [!INCLUDE[TLA#tla_xps](../../../../includes/tlasharptla-xps-md.md)] è un pacchetto contenente uno o più documenti statici insieme a tutte le risorse e le informazioni necessarie per il rendering.  [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] è anche il formato di file nativo dello spool di stampa di [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  <xref:System.Windows.Xps.Packaging.XpsDocument> viene archiviato in un dataset ZIP standard e può includere una combinazione di componenti XML e binari, ad esempio file di immagine e di tipi di carattere. Gli oggetti [PackageRelationships](#PackageRelationships) vengono utilizzati per definire le dipendenze tra il contenuto e le risorse necessarie per eseguire il rendering completo del documento.  La progettazione di <xref:System.Windows.Xps.Packaging.XpsDocument> offre una soluzione per documenti unica e ad alta fedeltà che supporta più utilizzi:  
  
-   Lettura, scrittura e archiviazione di contenuto di documenti statici e risorse come un file singolo, portabile e facile da distribuire.  
  
-   Visualizzazione di documenti con l'applicazione [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)] Viewer.  
  
-   Produzione di documenti nel formato di output nativo dello spool di stampa di [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)].  
  
-   Routing diretto dei documenti a una stampante compatibile con [!INCLUDE[TLA2#tla_xps](../../../../includes/tla2sharptla-xps-md.md)].  
  
## Vedere anche  
 <xref:System.Windows.Documents.FixedDocument>   
 <xref:System.Windows.Documents.FlowDocument>   
 <xref:System.Windows.Xps.Packaging.XpsDocument>   
 <xref:System.IO.Packaging.ZipPackage>   
 <xref:System.IO.Packaging.ZipPackagePart>   
 <xref:System.IO.Packaging.PackageRelationship>   
 <xref:System.Windows.Controls.DocumentViewer>   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [Cenni preliminari sui documenti dinamici](../../../../docs/framework/wpf/advanced/flow-document-overview.md)   
 [Cenni preliminari sulla stampa](../../../../docs/framework/wpf/advanced/printing-overview.md)   
 [Serializzazione e archiviazione di documenti](../../../../docs/framework/wpf/advanced/document-serialization-and-storage.md)