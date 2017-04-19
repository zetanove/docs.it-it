---
title: Sviluppo di applicazioni | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WPF, about application development
- application development [WPF], about
ms.assetid: 2996ce5e-81e9-49ae-881b-952db3dd1b7e
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: aa6ebe6c4ddc9b5cdec267cb2fc114440c189f0c
ms.lasthandoff: 04/08/2017

---
# <a name="application-development"></a>Sviluppo di applicazioni
<a name="introduction"></a> [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] è un framework di presentazione che può essere usato per sviluppare i tipi seguenti di applicazioni:  
  
-   Applicazioni autonome, ovvero applicazioni [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] dallo stile tradizionale compilate come assembly eseguibili installati nel computer client, da cui vengono eseguite.  
  
-   Applicazioni [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)], ovvero applicazioni costituite da riquadri di navigazione compilate come assembly eseguibili e ospitate da Web browser come [!INCLUDE[TLA#tla_ie](../../../../includes/tlasharptla-ie-md.md)] o Mozilla Firefox.  
  
-   Librerie di controlli personalizzati, ovvero assembly non eseguibili contenenti controlli riutilizzabili.  
  
-   Librerie di classi, ovvero assembly non eseguibili contenenti classi riutilizzabili.  
  
> [!NOTE]
>  L'uso di tipi WPF in un servizio Windows è fortemente sconsigliato. Se usate in un servizio Windows, queste funzionalità potrebbero non funzionare nel modo previsto.  
  
 Per compilare questo set di applicazioni, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] implementa una serie di servizi. Questo argomento offre una panoramica dei servizi, con indicazioni sulle risorse in cui trovare altre informazioni.  
  

  
<a name="Application_Management"></a>   
## <a name="application-management"></a>Gestione applicazioni  
 Le applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] eseguibili richiedono un set di funzionalità di base, incluse le seguenti:  
  
-   Creazione e gestione dell'infrastruttura di applicazioni comuni, inclusa la creazione di un metodo del punto di ingresso e di un loop di messaggi di Windows per la ricezione di messaggi di sistema e di input.  
  
-   Interazione con il ciclo di vita dell'applicazione e relativa verifica.  
  
-   Recupero ed elaborazione di parametri della riga di comando.  
  
-   Condivisione di proprietà con ambito di applicazione e risorse dell'[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)].  
  
-   Rilevamento ed elaborazione di eccezioni non gestite.  
  
-   Restituzione di codici di uscita.  
  
-   Gestione delle finestre in applicazioni autonome.  
  
-   Gestione della navigazione in applicazioni [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] e autonome con finestre e frame di navigazione.  
  
 Queste funzionalità vengono implementate dalla classe <xref:System.Windows.Application>, che deve essere aggiunta alle applicazioni usando una *definizione di applicazione*.  
  
 Per altre informazioni, vedere [Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
<a name="WPF_Application_Resource__Content__and_Data_Files"></a>   
## <a name="wpf-application-resource-content-and-data-files"></a>File di dati e di risorse dell'applicazione WPF.  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] estende il supporto di base per le risorse incorporate disponibile in [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] con il supporto per tre tipi di file di dati non eseguibili: file di risorse, di contenuto e di dati. Per altre informazioni, vedere [File di dati e di risorse dell'applicazione WPF](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md).  
  
 Un componente chiave del supporto per file di dati non eseguibili di WPF è la possibilità di identificarli e caricarli usando uno [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] univoco. Per altre informazioni, vedere [URI di tipo pack in WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md).  
  
<a name="Windows_and_Dialog_Boxes"></a>   
## <a name="windows-and-dialog-boxes"></a>Finestre e finestre di dialogo  
 Gli utenti interagiscono con applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] autonome tramite le finestre. Lo scopo di una finestra è ospitare il contenuto dell'applicazione ed esporre le funzionalità dell'applicazione che in genere permettono agli utenti di interagire con il contenuto. In [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] le finestre sono incapsulate dalla classe <xref:System.Windows.Window>, che supporta:  
  
-   Creazione e visualizzazione di finestre.  
  
-   Definizione di relazioni tra finestre proprietarie/finestre di proprietà.  
  
-   Configurazione dell'aspetto delle finestre, ad esempio dimensioni, posizione, icone, testo della barra del titolo e bordo.  
  
-   Interazione con il ciclo di vita di una finestra e relativa verifica.  
  
 Per altre informazioni, vedere [Cenni preliminari sulle finestre di WPF](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md).  
  
 <xref:System.Windows.Window> permette di creare un tipo speciale di finestra, chiamata finestra di dialogo. È possibile creare tipi di finestre di dialogo modali e non modali.  
  
 Per motivi di praticità e a causa dei vantaggi della riusabilità e di un'esperienza utente uniforme tra applicazioni, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] espone tre delle finestre di dialogo più comuni di [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)]: <xref:Microsoft.Win32.OpenFileDialog>, <xref:Microsoft.Win32.SaveFileDialog> e <xref:System.Windows.Controls.PrintDialog>.  
  
 Una finestra di messaggio è un tipo speciale di finestra di dialogo che permette di visualizzare agli utenti informazioni testuali importanti e di porre semplici domande con risposta Sì/No/OK/Annulla. Per creare e mostrare finestre di messaggio, è necessario usare la classe <xref:System.Windows.MessageBox>.  
  
 Per altre informazioni, vedere [Cenni preliminari sulle finestre di dialogo](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md).  
  
<a name="Navigation"></a>   
## <a name="navigation"></a>Navigazione  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] supporta la navigazione Web tramite pagine (<xref:System.Windows.Controls.Page>) e collegamenti ipertestuali (<xref:System.Windows.Documents.Hyperlink>). La navigazione può essere implementata in svariati modi, tra cui i seguenti:  
  
-   Pagine autonome ospitate in un Web browser.  
  
-   Pagine compilate in un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] ospitata in un Web browser.  
  
-   Pagine compilate in un'applicazione autonoma e ospitate da una finestra di navigazione (<xref:System.Windows.Navigation.NavigationWindow>).  
  
-   Pagine ospitate da un frame (<xref:System.Windows.Controls.Frame>), che può essere ospitato in una pagina autonoma, oppure una pagina compilata in un'applicazione [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] o autonoma.  
  
 Per semplificare la navigazione, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] implementa quanto segue:  
  
-   <xref:System.Windows.Navigation.NavigationService>, il motore di navigazione condiviso per l'elaborazione di richieste di navigazione usato da <xref:System.Windows.Controls.Frame>, <xref:System.Windows.Navigation.NavigationWindow> e da applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] per supportare la navigazione tra applicazioni.  
  
-   Metodi di navigazione per avviare la navigazione.  
  
-   Eventi di navigazione per interagire con il ciclo di vita della navigazione e verificarlo.  
  
-   Memorizzazione della navigazione all'indietro e in avanti tramite un giornale di registrazione, che può essere anche esaminato e modificato.  
  
 Per informazioni, vedere [Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md).  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] supporta anche un tipo speciale di navigazione chiamato navigazione strutturata. La navigazione strutturata può essere usata per chiamare una o più pagine che restituiscono dati in modo strutturato e prevedibile, coerentemente con le funzioni chiamanti. Questa funzionalità dipende dalla classe <xref:System.Windows.Navigation.PageFunction%601>, che viene descritta in modo più approfondito in [Cenni preliminari sulla navigazione strutturata](../../../../docs/framework/wpf/app-development/structured-navigation-overview.md). <xref:System.Windows.Navigation.PageFunction%601> ha anche lo scopo di semplificare la creazione di topologie di navigazione complesse, descritte in [Cenni preliminari sulle topologie di navigazione](../../../../docs/framework/wpf/app-development/navigation-topologies-overview.md).  
  
<a name="Hosting"></a>   
## <a name="hosting"></a>Hosting  
 Le applicazioni [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] possono essere ospitate in [!INCLUDE[TLA#tla_ie](../../../../includes/tlasharptla-ie-md.md)] o Firefox. Ogni modello di hosting è associato a un insieme di considerazioni e vincoli descritti in [Hosting](../../../../docs/framework/wpf/app-development/hosting-wpf-applications.md).  
  
<a name="Build_and_Deploy"></a>   
## <a name="build-and-deploy"></a>Compilazione e distribuzione  
 Benché sia possibile compilare semplici applicazioni [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] da un prompt dei comandi tramite compilatori della riga di comando, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] si integra con [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] per offrire supporto aggiuntivo che semplifica il processo di sviluppo e compilazione. Per altre informazioni, vedere [Compilazione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md).  
  
 A seconda del tipo di applicazione compilato, è possibile scegliere tra una o più opzioni di distribuzione. Per altre informazioni, vedere [Distribuzione di un'applicazione WPF](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md).  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Cenni preliminari sulla gestione di applicazioni](../../../../docs/framework/wpf/app-development/application-management-overview.md)|Offre una panoramica della classe <xref:System.Windows.Application>, con informazioni sulla gestione di ciclo di vita dell'applicazione, finestre, risorse dell'applicazione e navigazione.|  
|[Windows in WPF](../../../../docs/framework/wpf/app-development/windows-in-wpf-applications.md)|Offre informazioni dettagliate sulla gestione delle finestre nell'applicazione, tra cui come usare la classe <xref:System.Windows.Window> e le finestre di dialogo.|  
|[Cenni preliminari sulla navigazione](../../../../docs/framework/wpf/app-development/navigation-overview.md)|Offre una panoramica della gestione della navigazione tra pagine dell'applicazione.|  
|[Hosting](../../../../docs/framework/wpf/app-development/hosting-wpf-applications.md)|Viene fornita una panoramica su [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)].|  
|[Compilazione e distribuzione di applicazioni WPF](../../../../docs/framework/wpf/app-development/building-and-deploying-wpf-applications.md)|Descrive come compilare e distribuire un'applicazione WPF.|  
|[Introduzione a WPF in Visual Studio 2015](../../../../docs/framework/wpf/getting-started/introduction-to-wpf-in-vs.md)|Descrive le principali funzionalità di WPF.|  
|[Procedura dettagliata: Applicazione desktop WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)|Procedura dettagliata che mostra come creare un'applicazione WPF tramite navigazione tra le pagine, layout, controlli, immagini, stili e binding.|
