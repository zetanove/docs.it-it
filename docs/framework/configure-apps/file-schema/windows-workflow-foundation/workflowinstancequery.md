---
title: "&lt;workflowInstanceQuery&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 9096e812-626a-409a-9eda-c31a60b84c55
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;workflowInstanceQuery&gt;
Rappresenta una query che rileva modifiche del ciclo di vita dell'istanza del flusso di lavoro, come l'avvio o il completamento di un evento.  
  
 Per altre informazioni sulle query relative ai profili di rilevamento, vedere [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## Sintassi  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <workflowInstanceQueries>  
             <workflowInstanceQuery>  
                <states>  
                   <state name="Name"/>  
                </states>  
            </workflowInstanceQuery>  
         </workflowInstanceQueries>  
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md)|Raccolta di stati sottoscritti dell'istanza del flusso di lavoro rilevata che si riferiscono alla fase di creazione dei record di rilevamento.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<workflowInstanceQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancequeries.md)|Rappresenta una raccolta di elementi di configurazione che rilevano modifiche del ciclo di vita dell'istanza del flusso di lavoro, come l'avvio o il completamento di un evento.|  
  
## Note  
 L'oggetto <xref:System.Activities.Tracking.WorkflowInstanceQuery> viene usato per sottoscrivere gli oggetti <xref:System.Activities.Tracking.TrackingRecord> seguenti:  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceRecord>  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceAbortedRecord>  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord>  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceTerminatedRecord>  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceSuspendedRecord>  
  
## Esempio  
 La configurazione seguente sottoscrive i record di rilevamento a livello di istanza del flusso di lavoro per lo stato dell'istanza `Started` usando questa query.  
  
```  
  
<workflowInstanceQueries>  
    <workflowInstanceQuery>  
      <states>  
        <state name="Started"/>  
      </states>  
    </workflowInstanceQuery>  
</workflowInstanceQueries>  
  
```  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.WorkflowInstanceQuery](assetId:///System.Activities.Tracking.WorkflowInstanceQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)