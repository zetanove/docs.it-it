---
title: "How to: Create Windows Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Windows Service applications, creating"
  - "templates, Windows Service"
ms.assetid: 0f5e2cbb-d95d-477c-b2b5-4b990e6b86ff
caps.latest.revision: 18
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 18
---
# How to: Create Windows Services
Quando si crea un servizio, è possibile usare un modello di progetto di Visual Studio denominato **Servizio Windows**.  Questo modello esegue automaticamente una buona parte del lavoro facendo riferimento alle classi e agli spazi dei nomi appropriati, impostando l'ereditarietà dalla classe di base per i servizi ed eseguendo l'override di molti metodi, quando occorre.  
  
> [!WARNING]
>  Il modello di progetto Servizi Windows non è disponibile nell'edizione Express di Visual Studio.  
  
 Per creare un servizio funzionale è necessario eseguire almeno le operazioni seguenti:  
  
-   Impostare la proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A>.  
  
-   Creare i programmi di installazione necessari per l'applicazione di servizio.  
  
-   Eseguire l'override e specificare il codice dei metodi <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e <xref:System.ServiceProcess.ServiceBase.OnStop%2A> per personalizzare il comportamento del servizio.  
  
### Per creare un'applicazione di servizio Windows  
  
1.  Creare un progetto **Servizio Windows**.  
  
    > [!NOTE]
    >  Per istruzioni sulla scrittura di un servizio senza l'uso del modello, vedere [How to: Write Services Programmatically](../../../docs/framework/windows-services/how-to-write-services-programmatically.md).  
  
2.  Nella finestra **Proprietà** impostare la proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> per il servizio.  
  
     ![Impostare la proprietà ServiceName.](../../../docs/framework/windows-services/media/windowsservice-servicename.png "WindowsService\_ServiceName")  
  
    > [!NOTE]
    >  Il valore della proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> deve sempre corrispondere al nome registrato nelle classi del programma di installazione.  Se questa proprietà viene modificata, sarà necessario aggiornare anche la proprietà <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> delle classi del programma di installazione.  
  
3.  Per definire il funzionamento del servizio, impostare una delle proprietà seguenti.  
  
    |Proprietà|Impostazione|  
    |---------------|------------------|  
    |<xref:System.ServiceProcess.ServiceBase.CanStop%2A>|`True` per indicare che il servizio accetta le richieste di interruzione dell'esecuzione; `false` per impedire l'interruzione del servizio.|  
    |<xref:System.ServiceProcess.ServiceBase.CanShutdown%2A>|`True` per indicare che il servizio richiede una notifica alla chiusura del computer su cui viene eseguito, consentendo la chiamata alla routine <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>.|  
    |<xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A>|`True` per indicare che il servizio accetta le richieste di sospensione o di ripresa dell'esecuzione; `false` per impedire la sospensione e la ripresa del servizio.|  
    |<xref:System.ServiceProcess.ServiceBase.CanHandlePowerEvent%2A>|`True`  per indicare che il servizio può gestire la notifica delle variazioni dello stato di alimentazione del computer; `false` per impedire la ricezione di tali notifiche.|  
    |<xref:System.ServiceProcess.ServiceBase.AutoLog%2A>|`True` per scrivere informazioni nel log eventi dell'applicazione quando il servizio esegue un'operazione; `false` per disabilitare questa funzionalità.  Per altre informazioni, vedere [How to: Log Information About Services](../../../docs/framework/windows-services/how-to-log-information-about-services.md). **Note:**  Per impostazione predefinita, la proprietà <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> è impostata su `true`.|  
  
    > [!NOTE]
    >  Quando l'oggetto <xref:System.ServiceProcess.ServiceBase.CanStop%2A> `` o <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> ``  è impostato su `false`, **Gestione controllo servizi** disabiliterà le opzioni di menu corrispondenti per interrompere, sospendere o continuare il servizio.  
  
4.  Accedere all'editor di codice e definire il funzionamento desiderato per le routine <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e <xref:System.ServiceProcess.ServiceBase.OnStop%2A>.  
  
5.  Eseguire l'override di eventuali altri metodi per i quali si desidera definire la funzionalità.  
  
6.  Aggiungere i programmi di installazione necessari per l'applicazione di servizio.  Per altre informazioni, vedere [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md).  
  
7.  Compilare il progetto scegliendo **Compila soluzione** dal menu **Compila**.  
  
    > [!NOTE]
    >  Non è possibile eseguire un progetto di servizio premendo F5.  
  
8.  Installare il servizio.  Per altre informazioni, vedere [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md).  
  
## Vedere anche  
 [Introduction to Windows Service Applications](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [How to: Write Services Programmatically](../../../docs/framework/windows-services/how-to-write-services-programmatically.md)   
 [How to: Add Installers to Your Service Application](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [How to: Log Information About Services](../../../docs/framework/windows-services/how-to-log-information-about-services.md)   
 [How to: Start Services](../../../docs/framework/windows-services/how-to-start-services.md)   
 [How to: Specify the Security Context for Services](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md)   
 [How to: Install and Uninstall Services](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [Walkthrough: Creating a Windows Service Application in the Component Designer](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)