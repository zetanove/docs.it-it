---
title: "Modelli di Visual Studio WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6a608575-3535-4190-89da-911e24c8374f
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# Modelli di Visual Studio WCF
I modelli di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] sono modelli di progetto e di elemento predefiniti che è possibile utilizzare in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per compilare rapidamente i servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e le relative applicazioni.  
  
## <a name="using-the-wcf-templates"></a>Utilizzo dei modelli di WCF  
 I modelli di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] offrono una struttura di classe di base per lo sviluppo di servizi. In particolare, questi modelli forniscono le definizioni di base per il contratto di servizio, contratto dati, implementazione del servizio e configurazione. È possibile utilizzare questi modelli per creare un semplice servizio con interazione di codice minima e come blocco predefinito per servizi più avanzati.  
  
### <a name="wcf-service-library-project-template"></a>Modello di progetto della libreria di servizi WCF  
 Il [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] modello di progetto libreria di servizi è disponibile nel nuovo progetto la finestra di dialogo in **Visual C# \WCF** e **Visual Basic\WCF**.  
  
 Quando si crea un nuovo progetto usando il **servizio WCF** modello, il nuovo progetto include automaticamente i tre file seguenti:  
  
-   File di contratto del servizio (IService1.cs o IService1.vb). Il file di contratto del servizio è un'interfaccia alla quale sono applicati gli attributi del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Questo file fornisce una definizione di un semplice servizio per indicare come definire i servizi e include operazioni basate su parametri e un semplice esempio di contratto dati. Questo è il file predefinito visualizzato nell'editor del codice dopo la creazione di un progetto di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
-   File di implementazione del servizio (Service1.cs o Service1.vb). Il file di implementazione del servizio implementa il contratto definito nel file del contratto di servizio.  
  
-   File di configurazione dell'applicazione (App.config). Il file di configurazione fornisce gli elementi di base di un modello di servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] con un'associazione HTTP protetta. Include anche un endpoint per il servizio e abilita scambio di metadati.  
  
> [!NOTE]
>  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]è configurato per riconoscere il file app. config come file di configurazione per il progetto quando viene eseguito utilizzando il [Host servizio WCF (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md), ovvero la configurazione predefinita. Se la libreria di servizi viene inserita in un eseguibile, è necessario spostare il codice di configurazione nel file di configurazione dell'eseguibile, in quanto i file di configurazione per le DLL non sono validi.  
  
### <a name="wcf-service-application-template"></a>Modello Applicazione di servizio WCF  
 Il [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] modello applicazione di servizio è disponibile nella finestra di dialogo Nuovo progetto in **Visual C# \WCF** e **Visual Basic\WCF**.  
  
 Quando si crea un nuovo progetto usando il **servizio applicazione Web WCF** modello, il progetto include i seguenti quattro file:  
  
-   File host del servizio (service1.svc).  
  
-   File di contratto del servizio (IService1.cs o IService1.vb).  
  
-   File di implementazione del servizio (Service1.svc.cs o Service1.svc.vb).  
  
-   File di configurazione Web (Web.config).  
  
 Il modello crea automaticamente un sito Web (da distribuire in una directory virtuale) e funge da host di un servizio.  
  
### <a name="wcf-web-site-template"></a>Modello sito Web del servizio WCF  
 Il [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] modello di sito Web è disponibile nella finestra di dialogo Nuovo progetto in **Visual C# \Web site\wcf Service** e **Visual Basic\Web Site\WCF Service**. In questo modo vengono creati gli stessi file del modello Applicazione di servizio WCF che viene però organizzato come se fosse un sito Web ASP.NET. Vengono create le cartelle App_Data e App_Code.  
  
### <a name="wcf-service-item-template"></a>Modello di elemento del servizio WCF  
 Il modello di elemento del servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è un modello personalizzato che fornisce un modo rapido per aggiungere servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] a progetti [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] esistenti.  
  
 Per utilizzare questo modello, andare alla **Esplora** riquadro, fare clic sul nome del progetto, scegliere **Aggiungi**e quindi fare clic su **nuovo elemento** per avviare il **Aggiungi nuovo elemento** la finestra di dialogo.  
  
 L'interfaccia del servizio e file di implementazione vengono inseriti nella cartella radice del progetto.  
  
 Il modello tenterà di unire la sezione di configurazione del nuovo servizio con il file di configurazione esistente, nel caso siano compatibili.  
  
 Se il progetto esistente è un progetto Web viene creato anche un file del host del servizio (service1.svc).  
  
### <a name="wcf-wf-service-project-and-item-template"></a>Modello di elemento e progetto di servizio WF WCF.  
 Questi modelli creano servizi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] che fungono da host di un servizio flusso di lavoro al quale è possibile accedere come servizio Web. Sono disponibili modelli separati per XAML o modelli di programmazione imperativi. Mediante i modelli, è possibile creare un flusso di lavoro sequenziale o di macchina a stati. Per ulteriori informazioni su questi tipi di flusso di lavoro, vedere [esercitazioni di Windows Workflow Foundation](http://msdn.microsoft.com/it-it/e9705654-bd96-4b56-8d98-f1f118112d97). [!INCLUDE[crabout](../../../includes/crabout-md.md)]creazione di progetti flusso di lavoro, vedere [la creazione di progetti flusso di lavoro Legacy](../Topic/Creating%20Legacy%20Workflow%20Projects.md).  
  
 La finestra di progettazione di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] garantisce una risposta migliore quando vengono utilizzati flussi di lavoro di tipo XOML invece di quelli basati sul codice. XOML è il tipo di flusso predefinito che viene creato.  
  
### <a name="wcf-syndication-service-library-template"></a>Modello Libreria di servizi di diffusione WCF  
 Questo modello consente di esporre il feed in formato RSS o ATOM come servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Per ulteriori informazioni, vedere [diffusione WCF](../../../docs/framework/wcf/feature-details/wcf-syndication.md).  
  
#### <a name="changing-the-address-of-the-feed"></a>Modifica dell'indirizzo del feed  
 Il modello di pubblicazione utilizza Internet Explorer durante l'esecuzione. Quando si mouse sul progetto in **Esplora soluzioni** in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]selezionare **proprietà**, quindi selezionare il **Debug** scheda ed è possibile visualizzare l'indirizzo predefinito del modello. Internet Explorer tenterà di aprire il feed a questo indirizzo.  
  
 Se si modifica l'indirizzo del proprio feed, è necessario modificare anche l'indirizzo nel **Debug** scheda. In caso contrario, Internet Explorer tenterà di aprire il feed all'indirizzo predefinito e l'operazione avrà esito negativo.  
  
### <a name="ajax-enabled-wcf-service-item-template"></a>Modello di elemento del servizio WCF con supporto AJAX  
 Questo modello espone un controllo AJAX come servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Per ulteriori informazioni sui controlli AJAX, vedere il [documentazione controllo AJAX](http://go.microsoft.com/fwlink/?LinkId=96717).  
  
### <a name="silverlight-enabled-wcf-service-item-template"></a>Modello di elemento del servizio WCF con supporto Silverlight  
 Questo modello consente di creare un servizio Web che fornisce dati a un client Silverlight o front-end. È possibile aggiungere il modello a un sito Web o a un progetto di applicazione Web per creare un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] il quale include il codice e la configurazione del servizio che supportano la comunicazione con un client Silverlight. È quindi possibile utilizzare **Aggiungi riferimento al servizio** per aggiungere un proxy client del servizio al client e scambiare dati tra il client Silverlight e il servizio WCF con supporto Silverlight.  
  
 Per accedere a questo modello, fare doppio clic su un progetto di applicazione Web o sito Web in **Esplora**, fare clic su **aggiungere un nuovo elemento**, fare clic su **servizio WCF con supporto Silverlight**.  
  
> [!NOTE]
>  Il servizio WCF con supporto Silverlight espone un endpoint `basicHttpBinding` senza abilitare alcuna impostazione di sicurezza. Le informazioni sul servizio possono pertanto essere recuperate da tutti i client che si connettono a questo servizio. I messaggi scambiati tra il servizio e il client non sono inoltre firmati o crittografati. Per proteggere l'endpoint in modo appropriato, è necessario utilizzare l'autenticazione ASP.NET, HTTPS o altri meccanismi.  
  
## <a name="see-also"></a>Vedere anche  
 [Host servizio WCF (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)   
 [Client di prova WCF (WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)