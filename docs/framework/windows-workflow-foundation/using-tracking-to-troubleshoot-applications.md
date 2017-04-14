---
title: "Utilizzo del rilevamento per la risoluzione dei problemi relativi alle applicazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Utilizzo del rilevamento per la risoluzione dei problemi relativi alle applicazioni
[!INCLUDE[wf](../../../includes/wf-md.md)] consente di rilevare informazioni correlate al flusso di lavoro per fornire dettagli nell'esecuzione di un'applicazione o un servizio di [!INCLUDE[wf2](../../../includes/wf2-md.md)].Gli host di [!INCLUDE[wf2](../../../includes/wf2-md.md)] possono acquisire gli eventi del flusso di lavoro durante l'esecuzione di un'istanza del flusso di lavoro.Se il flusso di lavoro genera errori o eccezioni, è possibile utilizzare i dettagli di rilevamento di [!INCLUDE[wf2](../../../includes/wf2-md.md)] per risolvere i problemi relativi all'elaborazione.  
  
## Risoluzione dei problemi relativi a un'attività WF tramite il rilevamento di WF  
 Per rilevare gli errori all'interno dell'elaborazione di un'attività [!INCLUDE[wf2](../../../includes/wf2-md.md)], è possibile abilitare il rilevamento con un apposito profilo che esegue query per un oggetto <xref:System.Activities.Tracking.ActivityStateRecord> con lo stato Faulted.La query corrispondente viene specificata nel codice seguente:  
  
```  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 Se un errore viene propagato e gestito all'interno di un gestore fault \(ad esempio un'attività <xref:System.Activities.Statements.TryCatch>\), può essere rilevato tramite un oggetto <xref:System.Activities.Tracking.FaultPropagationRecord>.<xref:System.Activities.Tracking.FaultPropagationRecord> indica l'attività di origine dell'errore e il nome del gestore fault.<xref:System.Activities.Tracking.FaultPropagationRecord> contiene i dettagli dell'errore sotto forma di stack dell'eccezione per l'errore. La query da sottoscrivere per un oggetto <xref:System.Activities.Tracking.FaultPropagationRecord> è illustrata nell'esempio seguente:  
  
```  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
  
```  
  
 Se un errore non viene gestito all'interno del flusso di lavoro, comporta un'eccezione non gestita nell'istanza del flusso di lavoro che viene quindi interrotta.Per capire i dettagli dell'eccezione non gestita, il profilo di rilevamento deve eseguire una query sul record di istanza del flusso di lavoro con `state name=”UnhandledException”` come specificato nell'esempio seguente.  
  
```  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 Quando un'istanza del flusso di lavoro rileva un'eccezione non gestita, viene generato un oggetto <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> se è stato abilitato il rilevamento [!INCLUDE[wf2](../../../includes/wf2-md.md)].  
  
 Questo record di rilevamento contiene i dettagli dell'errore nel formato di stack dell'eccezione.Include dettagli dell'origine dell'errore \(ad esempio l'attività\) che si è verificato e ha comportato l'eccezione non gestita. Per sottoscrivere gli eventi dell'errore da un servizio [!INCLUDE[wf2](../../../includes/wf2-md.md)], abilitare il rilevamento aggiungendo un partecipante di rilevamento,configurandolo con un profilo di rilevamento che esegue query per `ActivityStateQuery (state=”Faulted”)`, <xref:System.Activities.Tracking.FaultPropagationRecord>e `WorkflowInstanceQuery (state=”UnhandledException”)`.  
  
 Se il rilevamento viene abilitato utilizzando il partecipante del rilevamento ETW, gli eventi dell'errore vengono creati in una sessione ETW.Questi eventi possono essere visualizzati utilizzando il Visualizzatore eventiche si trova nel nodo **Visualizzatore eventi\-\>Registri applicazioni e servizi\-\>Microsoft\-\>Windows\-\>Server applicazioni\-Applicazioni** nel canale analitico.  
  
## Vedere anche  
 [Concetti di monitoraggio](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Monitoraggio delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=201275)