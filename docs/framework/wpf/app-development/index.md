---
title: "Sviluppo di applicazioni | Microsoft Docs"
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
  - "sviluppo di applicazioni [WPF], informazioni"
  - "WPF, informazioni sullo sviluppo di applicazioni"
ms.assetid: 2996ce5e-81e9-49ae-881b-952db3dd1b7e
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Sviluppo di applicazioni
<a name="introduction"></a> [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] è un framework di presentazione che può essere utilizzato per compilare i seguenti tipi di applicazioni:  
  
-   Applicazioni autonome: applicazioni [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] tradizionali compilate come assembly eseguibili installati ed eseguiti nel computer client.  
  
-   [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]: applicazioni composte da pagine di navigazione compilate come assembly eseguibili e ospitate da Web browser quali [!INCLUDE[TLA#tla_ie](../../../../includes/tlasharptla-ie-md.md)] Mozilla Firefox.  
  
-   Librerie di controlli personalizzati: assembly non eseguibili che contengono controlli riutilizzabili.  
  
-   Librerie di classi: assembly non eseguibili che contengono classi riutilizzabili.  
  
> [!NOTE]
>  L'utilizzo di tipi WPF in un servizio Windows è fortemente sconsigliato.  Se si tenta di utilizzare queste funzionalità in un servizio Windows, è possibile che non funzionino come previsto.  
  
 Per compilare questo insieme di applicazioni, in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] viene implementato un host di servizi.  In questo argomento vengono presentati cenni preliminari su questi servizi e vengono fornite indicazioni per reperire ulteriori informazioni.  
  
   
  
<a name="Application_Management"></a>   
## Gestione delle applicazioni  
 Le applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguibili richiedono in genere un set di funzionalità di base, tra le quali:  
  
-   Creazione e gestione di infrastrutture di applicazioni comuni, inclusa la creazione di un metodo del punto di ingresso e un ciclo di messaggi di Windows per ricevere messaggi di sistema e di input.  
  
-   Rilevamento della durata di un'applicazione e interazione con essa.  
  
-   Recupero ed elaborazione dei parametri della riga di comando.  
  
-   Condivisione di proprietà e risorse dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] con ambito applicazione.  
  
-   Rilevamento ed elaborazione di eccezioni non gestite.  
  
-   Restituzione di codici di uscita.  
  
-   Gestione di finestre in applicazioni autonome.  
  
-   Rilevamento della navigazione nelle [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] e nelle applicazioni autonome con finestre e frame di navigazione.  
  
 Queste funzionalità vengono implementate dalla classe <xref:System.Windows.Application>, che viene aggiunta alle applicazioni tramite una *definizione di applicazione*.  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
<a name="WPF_Application_Resource__Content__and_Data_Files"></a>   
## File di dati e di risorse dell'applicazione WPF.  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende il supporto di base di [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] per risorse incorporate offrendo supporto per tre tipi di file di dati non eseguibili: risorse, contenuto e dati. Per ulteriori informazioni, vedere [File di dati e di risorse dell'applicazione WPF.](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md).  
  
 Un componente chiave del supporto per i file di dati non eseguibili WPF è la possibilità di identificare e caricare tali file utilizzando un [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] univoco. Per ulteriori informazioni, vedere [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md).  
  
<a name="Windows_and_Dialog_Boxes"></a>   
## Finestre e finestre di dialogo  
 Le finestre consentono l'interazione degli utenti con le applicazioni autonome [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  Una finestra ha lo scopo di ospitare il contenuto dell'applicazione e di esporre le funzionalità che di solito consentono agli utenti di interagire con il contenuto.  In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] le finestre sono incapsulate dalla classe <xref:System.Windows.Window>, che supporta le operazioni seguenti:  
  
-   Creazione e visualizzazione delle finestre.  
  
-   Definizione delle relazioni tra proprietario e finestra.  
  
-   Configurazione dell'aspetto della finestra, ad esempio dimensione, percorso, icone, testo della barra del titolo, bordo.  
  
-   Rilevamento della durata di una finestra e interazione con essa.  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulle finestre WPF](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md).  
  
 <xref:System.Windows.Window> supporta la possibilità di creare un tipo speciale di finestra noto come finestra di dialogo.  È possibile creare sia tipi modali sia tipi non modali di finestre di dialogo.  
  
 Per motivi di praticità, per i vantaggi offerti dalla riusabilità e per offrire un'esperienza utente coerente tra diverse applicazioni, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] espone tre delle finestre di dialogo di [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] comuni: <xref:Microsoft.Win32.OpenFileDialog>, <xref:Microsoft.Win32.SaveFileDialog> e <xref:System.Windows.Controls.PrintDialog>.  
  
 Una finestra di messaggio è un tipo speciale di finestra di dialogo che consente di visualizzare informazioni testuali importanti per gli utenti e di formulare domande con risposta di tipo Sì\/No\/OK\/Annulla.  Per creare e visualizzare le finestre di messaggio, utilizzare la classe <xref:System.Windows.MessageBox>.  
  
 Per ulteriori informazioni, vedere [Cenni preliminari sulle finestre di dialogo](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md).  
  
<a name="Navigation"></a>   
## Navigazione  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] supporta la navigazione di tipo Web tramite pagine \(<xref:System.Windows.Controls.Page>\) e collegamenti ipertestuali \(<xref:System.Windows.Documents.Hyperlink>\).  È possibile implementare la navigazione in diversi modi, ad esempio:  
  
-   Pagine autonome ospitate in un Web browser.  
  
-   Pagine compilate in un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] ospitata in un Web browser.  
  
-   Pagine compilate in un'applicazione autonoma e ospitate da una finestra di navigazione \(<xref:System.Windows.Navigation.NavigationWindow>\).  
  
-   Pagine ospitate da un frame \(<xref:System.Windows.Controls.Frame>\) che può essere ospitato in una pagina autonoma o in una pagina compilata in un'[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] o in un'applicazione autonoma.  
  
 Per semplificare la navigazione, in [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] vengono implementati gli elementi seguenti:  
  
-   <xref:System.Windows.Navigation.NavigationService>, il motore di navigazione condiviso per l'elaborazione delle richieste di navigazione utilizzato da <xref:System.Windows.Controls.Frame>, <xref:System.Windows.Navigation.NavigationWindow> e [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] per supportare la navigazione all'interno di un'applicazione.  
  
-   Metodi per avviare la navigazione.  
  
-   Eventi di navigazione per rilevare la durata della navigazione e interagire con essa.  
  
-   Utilizzo di un journal che può essere esaminato e modificato, per ricordare la navigazione in avanti e all'indietro.  
  
 Per informazioni, vedere [Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md).  
  
 In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è inoltre supportato un tipo speciale di navigazione noto come navigazione strutturata.  Tale tipo di navigazione può essere utilizzato per chiamare una o più pagine che restituiscono dati in modo strutturato e prevedibile, coerente con le funzioni chiamanti.  Questa funzionalità dipende dalla classe <xref:System.Windows.Navigation.PageFunction%601>, descritta ulteriormente in [Cenni preliminari sulla navigazione strutturata](../../../../docs/framework/wpf/app-development/structured-navigation-overview.md).  <xref:System.Windows.Navigation.PageFunction%601> consente inoltre di semplificare la creazione di topologie di navigazione complesse, descritte in [Cenni preliminari sulle topologie di navigazione](../../../../docs/framework/wpf/app-development/navigation-topologies-overview.md).  
  
<a name="Hosting"></a>   
## Hosting  
 Le applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] possono essere ospitate in [!INCLUDE[TLA#tla_ie](../../../../includes/tlasharptla-ie-md.md)] o Firefox.  A ogni modello di hosting si applicano considerazioni e vincoli specifici, trattati nell'argomento [Hosting](../../../../docs/framework/wpf/app-development/hosting-wpf-applications.md).  
  
<a name="Build_and_Deploy"></a>   
## Compilazione e distribuzione  
 Benché sia possibile compilare semplici applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] da un prompt dei comandi utilizzando compilatori da riga di comando, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] è integrato con [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] per fornire supporto aggiuntivo al fine di semplificare il processo di sviluppo e compilazione.  Per ulteriori informazioni, vedere [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md).  
  
 A seconda del tipo di applicazione compilata, è possibile scegliere una o più opzioni di distribuzione.  Per ulteriori informazioni, vedere [Distribuzione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md).  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md)|Vengono forniti cenni preliminari sulla classe <xref:System.Windows.Application>, inclusa la gestione della durata dell'applicazione, le finestre, le risorse dell'applicazione e la navigazione.|  
|[Windows in WPF](../../../../docs/framework/wpf/app-development/windows-in-wpf-applications.md)|Vengono forniti dettagli sulla gestione delle finestre dell'applicazione, incluse indicazioni di utilizzo della classe <xref:System.Windows.Window> e delle finestre di dialogo.|  
|[Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md)|Vengono forniti cenni preliminari sulla gestione della navigazione tra le pagine dell'applicazione.|  
|[Hosting](../../../../docs/framework/wpf/app-development/hosting-wpf-applications.md)|Vengono forniti cenni preliminari su [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].|  
|[Compilazione e distribuzione](../../../../docs/framework/wpf/app-development/building-and-deploying-wpf-applications.md)|Viene descritto come compilare e distribuire l'applicazione WPF.|  
|[Introduzione a WPF in Visual Studio 2015](../../../../docs/framework/wpf/getting-started/introduction-to-wpf-in-vs.md)|Vengono descritte le funzionalità principali di per la distribuzione di WPF.|  
|[Procedura dettagliata: introduzione a WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)|Procedura dettagliata in cui viene illustrato come creare un'applicazione WPF utilizzando navigazione tra le pagine, layout, controlli, immagini, stili e associazione.|