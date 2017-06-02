---
title: "Panoramica dell&#39;hosting dei servizi flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19f3704f-06bf-4eeb-8724-5224e02d7ead
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Panoramica dell&#39;hosting dei servizi flusso di lavoro
I servizi flusso di lavoro devono essere ospitati per poter essere eseguiti.L'oggetto <xref:System.ServiceModel.WorkflowServiceHost> è l'host del flusso di lavoro predefinito che supporta più istanze, la configurazione e la messaggistica di WCF, anche se per ospitare i flussi di lavoro non è necessario utilizzare la messaggistica.Inoltre si integra con la persistenza, il rilevamento e il controllo dell'istanza tramite un set di comportamenti del servizio.Analogamente all'oggetto <xref:System.ServiceModel.ServiceHost> di WCF, l'oggetto <xref:System.ServiceModel.WorkflowServiceHost> può essere un servizio indipendente ospitato in qualsiasi applicazione .NET gestita o un servizio ospitato su Web \(come un file con estensione xamlx\) in IIS\/WAS.Negli argomenti in questa sezione viene descritto come ospitare un servizio flusso di lavoro.  
  
## In questa sezione  
 [Hosting di servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/hosting-workflow-services.md)  
 Viene descritto l'hosting dei servizi flusso di lavoro.  
  
 [Elementi interni dell'host del servizio di flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)  
 Viene descritta l'elaborazione dei messaggi in arrivo da parte di <xref:System.ServiceModel.WorkflowServiceHost>.  
  
 [Estensibilità host del servizio flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)  
 Viene descritto come estendere la funzionalità dell'host del servizio flusso di lavoro.  
  
 [Endpoint di controllo del flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-control-endpoint.md)  
 Viene descritto come definire un endpoint che consente di creare istanze del flusso di lavoro.  
  
 [Procedura: ospitare un flusso di lavoro non di servizio in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-non-service-workflow-in-iis.md)  
 Viene illustrato l'hosting di un flusso di lavoro che non è un servizio flusso di lavoro in IIS.  
  
 [Procedura: ospitare un servizio di flusso di lavoro con Windows Server AppFabric](../../../../docs/framework/wcf/feature-details/how-to-host-a-workflow-service-with-windows-server-app-fabric.md)  
 Viene illustrato come ospitare un servizio flusso di lavoro esistente in Windows Server AppFabric.  
  
 [Configurazione di WorkflowServiceHost](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)  
 Viene descritto come controllare il comportamento di persistenza, di rilevamento, di inattività e dell'eccezione non gestita.  
  
## Riferimenti  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
 <xref:System.ServiceModel.Activities.WorkflowService>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>  
  
 <xref:System.ServiceModel.Activation.WorkflowServiceHostFactory>  
  
## Sezioni correlate  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)