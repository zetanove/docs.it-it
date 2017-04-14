---
title: "&lt;traccia&gt; di WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70cfaf24-a91c-4e56-ac47-d2ed87a963b3
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;traccia&gt; di WCF
Rappresenta una sezione di configurazione per la definizione delle impostazioni di rilevamento di un servizio flusso di lavoro.  
  
 Per altre informazioni sul rilevamento del flusso di lavoro e sulla relativa configurazione, vedere [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md) e [Configurazione del rilevamento per un flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md).  
  
## Sintassi  
  
```vb  
  
<system.serviceModel>  
  <tracking>    
     <participants>   
      <add name="String"   
           profileName="String"  
           type="String" />   
     </participants>   
    <trackingProfile name="String">  
      <workflow activityDefinitionId="String">  
          <activityScheduledQueries>  
             <activityScheduledQuery activityName="String"  
                 childActivityName="String"/>  
          </activityScheduledQueries>  
             <activityStateQuery activityName="String" />  
                <arguments>  
                   <argument name="String"/>  
                </arguments>  
                <states>  
                   <state name="String"/>  
                </states>  
                <variables>  
                   <variable name="String"/>  
                </variables>  
          </activityStateQueries>  
          <bookmarkResumptionQueries>  
             <bookmarkResumptionQuery name="String" />  
          </bookmarkResumptionQueries>  
          <cancelRequestQueries>  
             <cancelRequestQuery activityName="String"  
                 childActivityName="String"/>  
          </cancelRequestQueries>  
          <customTrackingQueries>  
             <customTrackingQuery activityName="String"  
                 name="String"/>  
          </customTrackingQueries>  
          <faultPropagationQueries>  
             <faultPropagationQuery activityName="String"  
                 faultHandlerActivityName="String"/>  
          </faultPropagationQueries>  
         <workflowInstanceQueries>  
            <workflowInstanceQuery>  
              <states>  
                 <state name="String"/>  
              </states>  
          </workflowInstanceQuery>  
        </workflowInstanceQueries>  
      </workflow>  
    </trackingProfile>          
   </profiles>  
  </tracking>  
</system.serviceModel>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
 Nessuno.  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<participants\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/participants.md)|Raccolta di elementi di configurazione che definiscono partecipanti che sottoscrivono record di rilevamento.  I partecipanti del rilevamento contengono la logica per elaborare il payload dai record di rilevamento, ad esempio possono scegliere di scrivere in un file.|  
|[\<trackingProfile\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/trackingprofile.md)|Profilo di rilevamento che consente di filtrare i record di rilevamento generati da un'istanza del flusso di lavoro.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|system.ServiceModel|Elemento radice di tutti gli elementi di configurazione del flusso di lavoro.|  
  
## Note  
 Il rilevamento consente di esaminare l'esecuzione di un flusso di lavoro.  L'infrastruttura di rilevamento del flusso di lavoro instrumenta un flusso di lavoro per generare record che riflettono gli eventi principali che si verificano durante l'esecuzione.  Vengono ad esempio generati record di rilevamento quando viene avviata o completata un'istanza del flusso di lavoro.  Il rilevamento consente inoltre di estrarre dati aziendali rilevanti associati alle variabili del flusso di lavoro.  Se, ad esempio, il flusso di lavoro rappresenta un sistema di elaborazione degli ordini, è possibile estrarre l'ID dell'ordine insieme al record di rilevamento.  In generale, l'abilitazione del rilevamento WF semplifica la diagnostica o l'analisi aziendale dell'esecuzione di un flusso di lavoro.  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.TrackingSection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.TrackingSection?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)