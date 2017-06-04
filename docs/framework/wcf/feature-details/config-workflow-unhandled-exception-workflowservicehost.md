---
title: "Procedura: configurare il comportamento di eccezione non gestita del flusso di lavoro con WorkflowServiceHost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Procedura: configurare il comportamento di eccezione non gestita del flusso di lavoro con WorkflowServiceHost
<xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> è un comportamento che consente di specificare l'azione da eseguire se si verifica un'eccezione non gestita all'interno di un flusso di lavoro ospitato in <xref:System.ServiceModel.Activities.WorkflowServiceHost>.In questo argomento viene illustrato come configurare il comportamento in un file di configurazione.  
  
### Per configurare WorkflowUnhandledExceptionBehavior  
  
1.  Aggiungere l'elemento \<`workflowUnhandledException`\> in un elemento \<`behavior`\> all'interno di un elemento \<`serviceBehaviors`\>, utilizzando l'attributo `action` per specificare l'azione da eseguire se si verifica un'eccezione non gestita, come indicato nell'esempio seguente.  
  
    ```  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>   
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    ```  
  
    > [!NOTE]
    >  L'esempio di configurazione precedente utilizza la configurazione semplificata.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md).  
  
     È possibile configurare questo comportamento nel codice, come indicato nell'esempio seguente.  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
  
    ```  
  
     È possibile impostare l'attributo `action` dell'elemento \<`workflowUnhandledException`\> su uno dei valori indicati di seguito.  
  
     **abandon**  
     Interrompe l'istanza in memoria senza modificare lo stato dell'istanza persistente \(ovvero, senza eseguire il rollback all'ultimo punto persistente\).  
  
     **abandonAndSuspend**  
     Interrompe l'istanza in memoria e aggiorna l'istanza persistente da sospendere.  
  
     **cancel**  
     Chiama i gestori annullamento per l'istanza, quindi completa l'istanza in memoria, che può rimuoverlo anche dall'archivio di istanze  
  
     **terminate**  
     Completa l'istanza in memoria e la rimuove dall'archivio di istanze.  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>, vedere [Estensibilità host del servizio flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md).  
  
## Vedere anche  
 [Estensibilità host del servizio flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md)   
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)