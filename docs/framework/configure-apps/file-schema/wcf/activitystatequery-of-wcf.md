---
title: "&lt;activityStateQuery&gt; di WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d6cdc04b-6f3a-4097-a623-ee4a1be3b5c4
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;activityStateQuery&gt; di WCF
Rappresenta una query usata per rilevare le modifiche al ciclo di vita delle attività che costituiscono un'istanza del flusso di lavoro.  È ad esempio possibile tenere traccia di tutte le volte in cui l'attività "Invia messaggio" viene completata all'interno di un'istanza del flusso di lavoro.  Questa query è necessaria affinché un partecipante del rilevamento sottoscriva gli oggetti record di stato.  Gli stati disponibili per la sottoscrizione sono specificati in ActivityStates.  
  
 Per altre informazioni sulle query relative ai profili di rilevamento, vedere [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md).  
  
## Sintassi  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <activityStateQueries>  
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
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|activityName|Stringa che specifica il nome dell'attività per la quale filtrare istanze di <xref:System.Activities.Tracking.ActivityStateRecord>.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<arguments\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/arguments.md)|Raccolta di argomenti associati a questa query di attività.|  
|[\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md)|Raccolta di elementi di configurazione contenenti gli stati dell'attività sottoscritta per la quale deve essere generato un record di rilevamento.|  
|[\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md)|Raccolta di variabili associate a questa query di attività.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<faultPropagationQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/faultpropagationquery.md)|Rappresenta un elenco di elementi di configurazione usati per rilevare le richieste di annullamento di un'attività figlio da parte dell'attività padre.  La query è necessaria affinché un partecipante del rilevamento esegua la sottoscrizione per annullare oggetti record richiesti.|  
  
## Note  
 Una funzionalità univoca di un elemento ActivityStateQuery è rappresentata dalla possibilità di estrarre dati durante il rilevamento dell'esecuzione di un flusso di lavoro.  Tali dati offrono un contesto aggiuntivo quando si accede ai record di rilevamento durante la fase di post\-esecuzione.  È possibile usare gli elementi [\<arguments\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/arguments.md), [\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md) e [\<states\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md) per estrarre qualsiasi variabile o argomento da qualsiasi attività di un flusso di lavoro. Nell'esempio seguente viene mostrata una query sullo stato dell'attività che estrae variabili e argomenti quando viene generato il record di rilevamento `Closed`dell'attività.  Le variabili e gli argomenti possono essere estratti solo con un ActivityStateRecord e quindi essere sottoscritti all'interno di un profilo di rilevamento usando [\<activityStateQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/activitystatequery.md).  
  
```  
  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
  
```  
  
## Vedere anche  
 [System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.ActivityStateQuery](assetId:///System.Activities.Tracking.ActivityStateQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Rilevamento e traccia del flusso di lavoro](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Profili di rilevamento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)