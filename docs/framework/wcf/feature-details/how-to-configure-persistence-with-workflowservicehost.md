---
title: "Procedura: configurare la persistenza con WorkflowServiceHost | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: configurare la persistenza con WorkflowServiceHost
In questo argomento viene descritto come configurare la funzionalità di archivio di istanze del flusso di lavoro SQL per abilitare la persistenza per i flussi di lavoro ospitati in <xref:System.ServiceHost.Activities.WorkflowServiceHost> tramite un file di configurazione.  Prima di usare tale funzionalità è necessario creare un database SQL usato per rendere persistenti le istanze del flusso di lavoro.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  
  
### Per configurare l'archivio di istanze del flusso di lavoro SQL nella configurazione  
  
1.  È possibile configurare le proprietà dell'archivio di istanze del flusso di lavoro SQL mediante <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, un comportamento del servizio che consente di modificare le impostazioni tramite la configurazione XML.  L'esempio di configurazione seguente mostra come configurare l'archivio di istanze del flusso di lavoro SQL tramite l'elemento del comportamento \<`sqlWorkflowInstanceStore`\> in un file di configurazione.  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore   
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"   
                 runnableInstancesDetectionPeriod="00:00:05">  
            <sqlWorkflowInstanceStore/>  
        </behavior>  
    </serviceBehaviors>  
  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] configurare l'archivio di istanze del flusso di lavoro SQL, vedere [Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle singole impostazioni per l'elemento del comportamento \<`sqlWorkflowInstanceStore`\>, vedere [Archivio di istanze del flusso di lavoro SQL](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).  Windows Server App Fabric fornisce un archivio di persistenza specifico.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Concetti di salvataggio permanente in Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=193121).  
  
    > [!NOTE]
    >  L'esempio di configurazione precedente usa la configurazione semplificata.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md)  
  
### Per configurare l'archivio di istanze del flusso di lavoro SQL nel codice  
  
1.  È possibile configurare le proprietà dell'archivio di istanze del flusso di lavoro SQL mediante <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, un comportamento del servizio che consente di modificare le impostazioni tramite il codice.  Nell'esempio seguente viene mostrato come configurare l'archivio di istanze del flusso di lavoro SQL tramite l'elemento del comportamento <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> nel codice.  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)] configurare l'archivio di istanze del flusso di lavoro SQL, vedere [Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi](../../../../docs/framework/windows-workflow-foundation//how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]lle singole impostazioni per l'elemento del comportamento <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, vedere [Archivio di istanze del flusso di lavoro SQL](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).  Windows Server App Fabric fornisce un archivio di persistenza specifico.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Concetti di salvataggio permanente in Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=193121).  
  
    > [!NOTE]
    >  L'esempio di configurazione precedente usa la configurazione semplificata.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md)  
  
     Per un esempio di come configurare la persistenza a livello di codice, vedere [Procedura: abilitare la persistenza per i flussi di lavoro e i relativi servizi](../../../../docs/framework/windows-workflow-foundation//how-to-enable-persistence-for-workflows-and-workflow-services.md).  
  
## Vedere anche  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Persistenza del flusso di lavoro](../../../../docs/framework/windows-workflow-foundation//workflow-persistence.md)   
 [Concetti di salvataggio permanente in Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=193121)