---
title: "&lt;activityScheduledQueries&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: ca6e82f1-54f2-48d6-899c-9873065b5547
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;activityScheduledQueries&gt;
Rappresenta una raccolta di query usate per rilevare un'attività pianificata per l'esecuzione da parte di un'attività padre.  La query è necessaria affinché un partecipante del rilevamento sottoscriva i record pianificati dell'attività.  
  
 Per altre informazioni sulle query relative ai profili di rilevamento, vedere [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## Sintassi  
  
```vb  
  
<tracking>  
     <trackingProfile name="Name">  
       <workflow>  
          <activityScheduledQueries>  
             <activityScheduledQuery activityName="String"  
                 childActivityName="String"/>  
          </activityScheduledQueries>  
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
|[\<activityScheduledQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activityscheduledquery.md)|Query usata per rilevare un'attività pianificata per l'esecuzione da parte di un'attività padre.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<workflow\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflow.md)|Elemento di configurazione contenente tutte le query per un flusso di lavoro specifico identificato dalla proprietà **activityDefinitionId**.|  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.ActivityScheduledQueryElementCollection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.ActivityScheduledQueryElementCollection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.ActivityScheduledQuery](assetId:///System.Activities.Tracking.ActivityScheduledQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)