---
title: "Amministrazione e diagnostica | Microsoft Docs"
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
  - "amministrazione [WCF]"
  - "diagnostica [WCF]"
  - "WCF, amministrazione"
  - "WCF, diagnostics"
  - "Windows Communication Foundation, amministrazione"
  - "Windows Communication Foundation, diagnostics"
ms.assetid: 34c81c08-0e0f-4fbc-9ae8-91948640ee43
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Amministrazione e diagnostica
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce numerose funzionalità che possono aiutare a monitorare le varie fasi della vita di un'applicazione.È ad esempio possibile utilizzare la configurazione per impostare servizi e client in fase di distribuzione.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include un vasto set di contatori delle prestazioni che consentono di misurare le prestazioni dell'applicazione.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] espone inoltre i dati dell'ispezione di un servizio in fase di esecuzione tramite un provider di Strumentazione gestione Windows \(WMI\) di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].In caso di errore dell'applicazione o di comportamento non corretto, è possibile utilizzare il Registro eventi per controllare se si è verificato qualcosa di grave.È inoltre possibile utilizzare la registrazione messaggi e le tracce per controllare gli eventi end\-to\-end in corso nell'applicazione.Queste funzionalità aiutano sia gli sviluppatori che i professionisti IT a identificare e risolvere i problemi di un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando non si comporta correttamente.  
  
> [!NOTE]
>  Se si ricevono errori senza informazioni dettagliate specifiche, è necessario abilitare l'attributo `includeExceptionDetailInFaults` dell'elemento di configurazione [\<debugServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md).In tal modo [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] invia i dettagli relativi alle eccezioni ai client e consente di individuare i problemi più comuni senza dover eseguire diagnosi più avanzate.Per ulteriori informazioni, vedere [Invio e ricezione degli errori](../../../../docs/framework/wcf/sending-and-receiving-faults.md).  
  
## Funzionalità di diagnostica fornite da WCF  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce le funzionalità di diagnostica seguenti:  
  
-   Le tracce end\-to\-end forniscono dati di strumentazione per risolvere i problemi di un'applicazione senza utilizzare un debugger.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] esegue l'output delle tracce sia per le attività cardine del processo sia per i messaggi di errore.Tale processo può comprendere l'apertura di una channel factory o l'invio e ricezione di messaggi tramite un host del servizio.È possibile attivare le tracce per consentire di monitorare lo stato di avanzamento in un'applicazione in esecuzione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Traccia](../../../../docs/framework/wcf/diagnostics/tracing/index.md).Per capire come utilizzare le tracce per eseguire il debug dell'applicazione, vedere l'argomento [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md).  
  
-   La registrazione dei messaggi consente di vedere il loro aspetto prima e dopo la trasmissione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Registrazione messaggi](../../../../docs/framework/wcf/diagnostics/message-logging.md).  
  
-   La traccia eventi scrive gli eventi nel Registro eventi per qualsiasi problema importante.È quindi possibile utilizzare il Visualizzatore eventi per esaminare qualsiasi anomalia.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Registrazione eventi](../../../../docs/framework/wcf/diagnostics/event-logging/index.md).  
  
-   I contatori delle prestazioni esposti tramite Performance Monitor consentono di monitorare l'integrità dell'applicazione e del sistema.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Contatori di prestazioni](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md).  
  
-   Lo spazio dei nomi <xref:System.ServiceModel.Configuration> consente di caricare file di configurazione e configurare un endpoint del servizio o client.È possibile utilizzare il modello a oggetti per inserire in uno script le modifiche a numerose applicazioni quando è necessario distribuire gli aggiornamenti a più computer.In alternativa, è possibile utilizzare [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) per modificare le impostazioni di configurazione utilizzando una procedura guidata GUI.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Configurazione dell'applicazione](../../../../docs/framework/wcf/diagnostics/configuring-your-application.md).  
  
-   WMI consente di scoprire i servizi in ascolto in un computer e le associazioni utilizzate.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Utilizzo di Strumentazione gestione Windows \(WMI\) per la diagnostica](../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce inoltre numerosi strumenti della riga di comando e GUI per semplificare la creazione, distribuzione e gestione di applicazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Windows Communication Foundation Tools](../../../../docs/framework/wcf/tools.md).È ad esempio possibile utilizzare [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md) per creare e modificare le impostazioni di configurazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando una procedura guidata, anziché modificare direttamente il codice XML.È inoltre possibile utilizzare [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) per visualizzare, raggruppare e filtrare messaggi di traccia allo scopo di diagnosticare, riparare e verificare i problemi dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Vedere anche  
 [Configurazione dell'applicazione](../../../../docs/framework/wcf/diagnostics/configuring-your-application.md)   
 [Distribuzione di servizi](../../../../docs/framework/wcf/diagnostics/deploying-services.md)   
 [Riferimenti per le eccezioni](../../../../docs/framework/wcf/diagnostics/exceptions-reference/index.md)   
 [Registrazione eventi](../../../../docs/framework/wcf/diagnostics/event-logging/index.md)   
 [Registrazione messaggi](../../../../docs/framework/wcf/diagnostics/message-logging.md)   
 [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)   
 [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)   
 [Strumento di registrazione di ServiceModel](../../../../docs/framework/wcf/diagnostics/servicemodel-registration-tool.md)   
 [Traccia](../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [Utilizzo di Strumentazione gestione Windows \(WMI\) per la diagnostica](../../../../docs/framework/wcf/diagnostics/wmi/index.md)   
 [Contatori di prestazioni](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)   
 [Windows Communication Foundation Tools](../../../../docs/framework/wcf/tools.md)