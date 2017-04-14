---
title: "&lt;behavior&gt; di &lt;serviceBehaviors&gt; del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6a4b718a-1b40-4957-935a-f6122819ab3c
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;behavior&gt; di &lt;serviceBehaviors&gt; del flusso di lavoro
L'elemento **behavior** contiene una raccolta di impostazioni per il comportamento di un servizio.  Ogni comportamento è indicizzato in base al relativo **name**.  I servizi sono in grado di collegarsi a ogni comportamento tramite tale nome usando l'attributo **behaviorConfiguration** dell'elemento [\<endpoint\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-element.md).  In questo modo gli endpoint possono condividere configurazioni del comportamento comuni senza ridefinire le impostazioni.  
  
## Sintassi  
  
```  
  
<system.ServiceModel>  
  <behaviors>  
    <serviceBehaviors>  
    <behavior name=String">  
      <bufferReceive maxPendingMessagesPerChannel=”Integer” />  
      <etwTracking profileName=”String” />  
     <sendMessageChannelCache allowUnsafeCaching="Boolean" >          
        <channelSettings idleTimeout="TimeSpan" leaseTimeout="TimeSpan" maxItemsInCache="Integer" />  
        <factorySettings idleTimeout="TimeSpan" leaseTimeout="TimeSpan" maxItemsInCache="Integer" />  
     </sendMessageChannelCache>  
      <sqlWorkflowInstanceStore   
          connectionStringName=”String”   
          honstLockRenewalPeriod=”TimeSpan”  
          instanceCompletionAction=”DeleteNothing/DeleteAll”  
          instanceEncodingAction=”None/GZip”  
          instanceLockedExceptionAction=”NoRetry/BasicRetry/AggressiveRetry”  
          runnableInstancesDetectionPeriod=”TimeSpan” />  
      <workflowIdle timeToPersist=”TimeSpan”  
          timeToUnload=”TimeSpan” />  
      <workflowUnhandledException action=”Abandon/AbandonAndSuspend/Cancel/Terminate” />  
    </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.ServiceModel>  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|name|Stringa univoca che contiene il nome di configurazione del comportamento.  Questo valore è una stringa definita dall'utente che deve essere univoca in quanto funge da stringa di identificazione dell'elemento.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<bufferReceive\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/bufferreceive.md)|Comportamento del servizio che consente a un servizio di usare l'elaborazione di ricezione memorizzata nel buffer per far sì che un servizio flusso di lavoro elabori messaggi non ordinati.|  
|[\<routing\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md)|Comportamento del servizio che consente a un servizio di usare il rilevamento ETW mediante un <xref:System.Activities.Tracking.ETWTrackingParticipant>.|  
|[\<sendMessageChannelCache\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sendmessagechannelcache.md)|Comportamento del servizio che consente la personalizzazione dei livelli di condivisione della cache, delle impostazioni della cache della channel factory e delle impostazioni della cache del canale per flussi di lavoro che inviano messaggi a endpoint di servizio usando attività della messaggistica di invio.|  
|[\<sqlWorkflowInstanceStore\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/sqlworkflowinstancestore.md)|Comportamento del servizio che consente di configurare la funzionalità <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, che supporta la persistenza delle informazioni sullo stato per le istanze del servizio flusso di lavoro in un database di SQL Server 2005 o di SQL Server 2008.|  
|[\<workflowIdle\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowidle.md)|Un comportamento del servizio che controlla quando istanze del flusso di lavoro inattive vengono scaricate e rese persistenti.|  
|[\<workflowInstanceManagement\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancemanagement.md)|Comportamento del servizio che consente di specificare impostazioni che controllano la modalità di esecuzione delle istanze del flusso di lavoro, inclusa la persistenza, il comportamento delle eccezioni non gestite e il comportamento di inattività.|  
|[\<workflowUnhandledException\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowunhandledexception.md)|Comportamento del servizio che consente di specificare l'azione da intraprendere quando si verifica un'eccezione non gestita all'interno di un servizio flusso di lavoro.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/servicebehaviors-of-workflow.md)|Raccolta di elementi di comportamento del servizio.|