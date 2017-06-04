---
title: "Sviluppo e distribuzione di WCF Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, sviluppo"
  - "WCF Data Services, distribuzione"
  - "distribuzione [WCF Data Services]"
  - "sviluppo di applicazioni [WCF Data Services]"
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Sviluppo e distribuzione di WCF Data Services
In questo argomento vengono fornite informazioni sullo sviluppo e sulla distribuzione di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]. Per informazioni di base su [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)], vedere [Guida introduttiva](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md) e [Cenni preliminari](../../../../docs/framework/data/wcf/wcf-data-services-overview.md).  
  
## Sviluppo di WCF Data Services  
 Quando si usa [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per creare un servizio dati che supporta [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)], è necessario effettuare le seguenti attività di base durante lo sviluppo:  
  
1.  **Definizione del modello di dati**  
  
     [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] supporta diversi provider di servizi dati che consentono di definire un modello di dati basato su dati di varie origini, dai database relazionali ai tipi di dati ad associazione tardiva. Per altre informazioni, vedere [Provider di servizi dati](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md).  
  
2.  **Creazione del servizio dati**  
  
     La maggior parte dei servizi di base espone una classe che eredita dalla classe <xref:System.Data.Services.DataService%601>, con un tipo `T` che corrisponde al nome completo dello spazio dei nomi del contenitore di entità. Per altre informazioni, vedere [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md).  
  
3.  **Configurazione del servizio dati**  
  
     Per impostazione predefinita, [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] disabilita l'accesso alle risorse esposte da un contenitore di entità. L'interfaccia <xref:System.Data.Services.DataServiceConfiguration> consente di configurare l'accesso a risorse e operazioni del servizio, di specificare la versione supportata di [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] e di definire altri comportamenti a livello di server, ad esempio i comportamenti di invio in batch o il numero massimo di entità che è possibile restituire in un unico feed di risposta. Per altre informazioni, vedere [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md).  
  
 In questo argomento si analizza principalmente lo sviluppo e la distribuzione dei servizi dati tramite [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Per informazioni sulla flessibilità offerta da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] per esporre i dati come feed [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)], vedere [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md).  
  
### Scelta di un server Web di sviluppo  
 Quando si sviluppa un servizio WCF Data Services come un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] o un sito Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] tramite [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)], si dispone di una scelta di server Web su cui eseguire il servizio dati durante lo sviluppo. I server Web seguenti si integrano con [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] per facilitare le operazioni di test e debug dei servizi dati sul computer locale.  
  
1.  **Server IIS locale**  
  
     Quando si crea un servizio dati che è un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] o un sito Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] eseguito su Internet Information Services \(IIS\), si consiglia di sviluppare e testare il servizio dati tramite IIS sul computer locale. L'esecuzione del servizio dati su IIS facilita l'esecuzione della traccia delle richieste HTTP durante l'esecuzione il debug. Consente inoltre di determinare in anticipo i diritti necessari richiesti da IIS per accedere a file, database e altre risorse richieste dal servizio dati. Per eseguire il servizio dati su IIS, è necessario assicurarsi che IIS e [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] siano installati e configurati correttamente e che l'accesso sia stato concesso agli account IIS nel file system e nei database. Per altre informazioni, vedere [Procedura: sviluppare un servizio WCF in esecuzione in IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md).  
  
    > [!NOTE]
    >  È necessario eseguire [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] con i diritti di amministratore per abilitare l'ambiente di sviluppo alla configurazione del server IIS locale.  
  
2.  **Server di sviluppo di Visual Studio**  
  
     [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] include un server Web incorporato, [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server che è il server Web predefinito per i progetti [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. Questo server Web è progettato per eseguire progetti [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] sul computer locale durante lo sviluppo. Nella [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md) viene indicato come creare un servizio dati da eseguire in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server.  
  
     È opportuno tenere presenti le seguenti limitazioni quando si usa [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server per sviluppare il servizio dati:  
  
    -   L'accesso al server può essere eseguito solo sul computer locale.  
  
    -   Il server è in ascolto su `localhost` e su una porta specifica, non sulla porta 80 che è la porta predefinita per i messaggi HTTP. Per altre informazioni, vedere [Server Web in Visual Studio per progetti Web ASP.NET](http://msdn.microsoft.com/it-it/31d4f588-df59-4b7e-b9ea-e1f2dd204328).  
  
    -   Il server esegue il servizio dati nel contesto dell'account utente corrente. Se ad esempio l'utente corrente dispone di privilegi a livello di amministratore, un servizio dati eseguito in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server avrà i privilegi a livello di amministratore. È possibile che il servizio dati quindi sia in grado di accedere alle risorse che non ha diritto ad accedere se viene distribuito in un server IIS.  
  
    -   Il server non include le funzionalità aggiuntive di IIS, ad esempio l'autenticazione.  
  
    -   Il server non può gestire i flussi HTTP Chunked che vengono inviati per impostazione predefinita dal client [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] quando si esegue l'accesso a dati binari di grandi dimensioni dal servizio dati. Per altre informazioni, vedere [Provider di flusso](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md).  
  
    -   In questo server l'elaborazione del carattere punto \(`.`\) negli URL risulta problematica anche se il punto è supportato da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] nei valori delle chiavi.  
  
    > [!TIP]
    >  Anche se è possibile usare [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] Development Server per testare i servizi dati durante lo sviluppo, è necessario ripetere il testing dopo la distribuzione a un server Web che esegue IIS.  
  
3.  **Ambiente di sviluppo Microsoft Azure**  
  
     Gli strumenti di Microsoft Azure per [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] includono un set integrato di strumenti per lo sviluppo di servizi di Microsoft Azure in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Con questi strumenti, è possibile sviluppare un servizio dati che può essere distribuito a Microsoft Azure ed è possibile testare il servizio dati sul computer locale prima della distribuzione. Usare questi strumenti quando si usa [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] per sviluppare un servizio dati che viene eseguito sulla piattaforma Microsoft Azure. Gli strumenti di Microsoft Azure per [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] possono essere scaricati dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=201848).[!INCLUDE[crabout](../../../../includes/crabout-md.md)]llo sviluppo di un servizio dati in esecuzione in Microsoft Azure, vedere il post sulla [distribuzione di un servizio OData in Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=201847).  
  
### Suggerimenti per lo sviluppo  
 Quando si sviluppa un servizio dati è opportuno considerare quanto segue:  
  
-   Determinare i requisiti di sicurezza del servizio dati, se si pianifica di autenticare gli utenti o di limitare l'accesso a utenti specifici. Per altre informazioni, vedere [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md).  
  
-   Un programma di ispezione HTTP può essere molto utile quando si esegue il debug di un servizio dati in quanto permette di controllare il contenuto dei messaggi di risposta e richiesta. Qualsiasi analizzatore di pacchetti di rete in grado di visualizzare pacchetti non elaborati può essere usato per controllare le richieste HTTP e le risposte del servizio dati.  
  
-   Quando si esegue debug di un servizio dati, si potrebbe desiderare di ottenere altre informazioni su un errore dal servizio dati anziché durante l'operazione normale. È possibile ottenere altre informazioni sull'errore dal servizio dati impostando la proprietà <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> in <xref:System.Data.Services.DataServiceConfiguration> su `true` e impostando la proprietà <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> dell'attributo <xref:System.ServiceModel.Description.ServiceDebugBehavior> nella classe del servizio dati su `true`.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] il post sul [debug di WCF Data Services](http://go.microsoft.com/fwlink/?LinkId=201868). È possibile abilitare la traccia anche in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per visualizzare le eccezioni generate nel livello di messaggistica HTTP. Per altre informazioni, vedere [Configurazione delle funzionalità di traccia](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md).  
  
-   Un servizio dati viene generalmente sviluppato come progetto di applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], ma è possibile creare un servizio dati anche come progetto di sito Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Per altre informazioni sulle differenze tra i due tipi di progetti, vedere [Confronto tra progetti di applicazione Web e progetti di sito Web in Visual Studio](http://msdn.microsoft.com/it-it/2861815e-f5a2-4378-a2f8-b8a86dc012f5).  
  
-   Quando si crea un servizio dati tramite la finestra di dialogo **Aggiungi nuovo elemento** in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)], il servizio dati è ospitato da [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] in IIS.[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e IIS costituiscono l'host predefinito di un servizio dati, tuttavia sono supportate altre opzioni host. Per altre informazioni, vedere [Hosting del servizio dati](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md).  
  
## Distribuzione di WCF Data Services  
 WCF Data Services fornisce flessibilità di scelta per il processo che ospita il servizio dati. È possibile usare [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] per distribuire un servizio dati alle piattaforme seguenti:  
  
-   **Server Web ospitato in IIS**  
  
     Quando un servizio dati viene sviluppato come un progetto [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], può essere distribuito a un server Web IIS tramite i processi di distribuzione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] standard.[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] fornisce le tecnologie di distribuzione seguenti per [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], a seconda del tipo progetto [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] che ospita il servizio dati che si distribuisce.  
  
    -   **Tecnologie di distribuzione per applicazioni Web ASP.NET**  
  
        -   [Pacchetto di distribuzione Web](http://msdn.microsoft.com/it-it/1f9713c8-9540-494c-b80d-9893b970ad6f)  
  
        -   [Pubblicazione con un clic](http://msdn.microsoft.com/it-it/59226246-99ad-4aec-975d-7c61e8a8911c)  
  
    -   **Tecnologie di distribuzione per siti Web ASP.NET**  
  
        -   [Strumento Copia sito Web](../Topic/How%20to:%20Deploy%20a%20Web%20Site%20Project%20by%20using%20the%20Copy%20Web%20Site%20Tool.md)  
  
        -   [Strumento Pubblica sito Web](../Topic/How%20to:%20Deploy%20a%20Web%20Site%20Project%20by%20Using%20the%20Publish%20Web%20Site%20Tool.md)  
  
        -   [XCopy](../Topic/Walkthrough:%20Deploying%20a%20Web%20Site%20Project%20by%20Using%20XCOPY.md)  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle opzioni di distribuzione per un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], vedere [Panoramica della distribuzione di progetti di applicazione Web per Visual Studio e ASP.NET](http://msdn.microsoft.com/it-it/99bd1927-b59f-4e02-87b4-55c6ba2adbc3).  
  
    > [!TIP]
    >  Prima di tentare di distribuire il servizio dati a IIS, verificare che sia stata testata la distribuzione a un server Web che esegue IIS. Per altre informazioni, vedere [Procedura: sviluppare un servizio WCF in esecuzione in IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md).  
  
-   **Windows Azure**  
  
     È possibile distribuire un servizio dati a Microsoft Azure tramite Strumenti di Microsoft Azure per [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Gli strumenti di Microsoft Azure per [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] possono essere scaricati dall'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=201848).[!INCLUDE[crabout](../../../../includes/crabout-md.md)]lla distribuzione di un servizio dati in Microsoft Azure, vedere il post sulla [distribuzione di un servizio OData in Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=201847).  
  
### Considerazioni sulla distribuzione  
 Quando si distribuisce un servizio dati è opportuno considerare quanto segue:  
  
-   Quando si distribuisce un servizio dati che usa il provider [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] per accedere a un database SQL Server, è possibile che si debbano propagare anche strutture di dati, dati o entrambi gli elementi con la distribuzione del servizio dati.[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] è in grado di creare automaticamente script \(file con estensione sql\) per effettuare questa operazione nel database di destinazione e tali script possono essere inclusi nel pacchetto di distribuzione Web di un'applicazione [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]. Per altre informazioni, vedere [Procedura: Distribuire un database con un progetto di applicazione Web](http://msdn.microsoft.com/it-it/683b33f1-8a3d-45cf-af6e-61ab50fc518b). Per un sito Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], è possibile eseguire questa operazione usando **Database Publishing Wizard** in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]. Per altre informazioni, vedere [Deploying a Database by Using the Database Publishing Wizard](../Topic/Deploying%20a%20Database%20by%20Using%20the%20Database%20Publishing%20Wizard.md).  
  
-   Poiché [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] include un'implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base, è possibile usare Windows Server AppFabric per il monitoraggio di un servizio dati distribuito a IIS che è in esecuzione su Windows Server.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'uso di Windows Server AppFabric per monitorare un servizio dati, vedere il post sul [monitoraggio di WCF Data Services con Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=202005).  
  
## Vedere anche  
 [Hosting del servizio dati](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)   
 [Protezione di WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)   
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)