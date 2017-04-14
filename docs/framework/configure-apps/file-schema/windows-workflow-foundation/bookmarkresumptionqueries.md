---
title: "&lt;bookmarkResumptionQueries&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 8ed61a7f-4254-439c-bdd8-b474971533f7
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;bookmarkResumptionQueries&gt;
Rappresenta una raccolta di query usate per rilevare la riassunzione di un segnalibro all'interno di un'istanza del flusso di lavoro.  La query è necessaria affinché un partecipante del rilevamento sottoscriva i record di riassunzione dei segnalibri.  
  
 Per altre informazioni sulle query relative ai profili di rilevamento, vedere [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## Sintassi  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <bookmarkResumptionQueries>  
             <bookmarkResumptionQuery name="String" />  
          </bookmarkResumptionQueries>  
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
|[\<bookmarkResumptionQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/bookmarkresumptionquery.md)|Query usata per rilevare la riassunzione di un segnalibro all'interno di un'istanza del flusso di lavoro.  La query è necessaria affinché un partecipante del rilevamento sottoscriva i record di riassunzione dei segnalibri.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<workflow\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflow.md)|Elemento di configurazione contenente tutte le query per un flusso di lavoro specifico identificato dalla proprietà **activityDefinitionId**.|  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.BookmarkResumptionQueryElementCollection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.BookmarkResumptionQueryElementCollection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.BookmarkResumptionQuery](assetId:///System.Activities.Tracking.BookmarkResumptionQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)