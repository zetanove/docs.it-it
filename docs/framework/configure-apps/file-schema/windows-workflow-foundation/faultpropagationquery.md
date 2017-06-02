---
title: "&lt;faultPropagationQuery&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 4fb5c2b1-3dad-4eca-9c7f-3efb51899813
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;faultPropagationQuery&gt;
Rappresenta una query usata per rilevare la gestione degli errori che si verificano all'interno di un'attività.  Questo evento si verifica ogni volta che un FaultHandler elabora un errore.  È necessario usare tale query per rilevare la gestione degli errori che si verificano all'interno di un'attività.  La query è necessaria affinché un partecipante del rilevamento sottoscriva i record di propagazione degli errori.  
  
 Per altre informazioni sulle query relative ai profili di rilevamento, vedere [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## Sintassi  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <faultPropagationQueries>  
             <faultPropagationQuery activityName="String"  
                 faultHandlerActivityName="String"/>  
          </faultPropagationQueries>  
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|activityName|Stringa che specifica il nome dell'attività del gestore errori che ha propagato l'errore.  L'impostazione predefinita è \* che indica che i record di propagazione degli errori vengono restituiti per tutte le attività.|  
|faultHandlerActivityName|Stringa che specifica il nome dell'attività che ha originato l'errore.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<faultPropagationQueries\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/faultpropagationqueries.md)|Rappresenta un elenco di elementi di configurazione usati per rilevare la gestione degli errori che si verificano all'interno di un'attività.  Questo evento si verifica ogni volta che un FaultHandler elabora un errore.|  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.FaultPropagationQueryElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.FaultPropagationQueryElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.FaultPropagationQuery](assetId:///System.Activities.Tracking.FaultPropagationQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)