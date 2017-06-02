---
title: "Profili di rilevamento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22682566-1cd9-4672-9791-fb3523638e18
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Profili di rilevamento
I profili di rilevamento contengono query di rilevamento che consentono a un partecipante del rilevamento di sottoscrivere gli eventi del flusso di lavoro creati quando lo stato di un'istanza del flusso di lavoro viene modificato in fase di esecuzione.  
  
## Profili di rilevamento  
 I profili di rilevamento vengono utilizzati per specificare le informazioni di rilevamento generate per un'istanza del flusso di lavoro.Se non è specificato alcun profilo, vengono generati tutti gli eventi di rilevamento.Se viene specificato un profilo, verranno generati gli eventi di rilevamento specificati nel profilo.A seconda dei requisiti di monitoraggio, è possibile scrivere un profilo molto generale che sottoscrive un piccolo set di modifiche dello stato di alto livello in un flusso di lavorooppure creare un profilo molto dettagliato i cui eventi risultanti sono sufficientemente precisi per ricostruire un flusso di esecuzione dettagliato in un secondo momento.  
  
 I profili di rilevamento si manifestano come elementi XML all'interno di un file di configurazione standard di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] o specificati nel codice.Nell'esempio seguente è illustrato un profilo di rilevamento di [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] in un file di configurazione che consente a un partecipante del rilevamento di sottoscrivere gli eventi del flusso di lavoro `Started` e `Completed`.  
  
```  
<system.serviceModel>  
    ...  
    <tracking>    
      <trackingProfile name="Sample Tracking Profile">  
        <workflow activityDefinitionId="*">  
          <workflowInstanceQueries>  
            <workflowInstanceQuery>  
              <states>  
                <state name="Started"/>  
                <state name="Completed"/>  
              </states>  
            </workflowInstanceQuery>  
          </workflowInstanceQueries>  
        </workflow>  
      </trackingProfile>          
    </profiles>  
  </tracking>  
    ...  
</system.serviceModel>  
  
```  
  
 Nell'esempio seguente viene illustrato il profilo di rilevamento equivalente creato utilizzando il codice.  
  
```csharp  
TrackingProfile profile = new TrackingProfile()  
{  
    Name = "CustomTrackingProfile",  
    Queries =   
    {  
        new WorkflowInstanceQuery()  
        {  
            // Limit workflow instance tracking records for started and  
            // completed workflow states.  
            States = { WorkflowInstanceStates.Started, WorkflowInstanceStates.Completed },  
        }  
    }  
};  
  
```  
  
 I record di rilevamento vengono filtrati tramite la modalità di visibilità all'interno di un profilo di rilevamento utilizzando l'attributo <xref:System.Activities.Tracking.ImplementationVisibility>.Un'attività composita è un'attività di primo livello che contiene le altre attività che formano l'implementazione.La modalità di visibilità specifica i record di rilevamento creati dalle attività composite all'interno di un'attività di flusso di lavoro per specificare se le attività che formano l'implementazione vengono rilevate.La modalità di visibilità si applica a livello del profilo di rilevamento.L'applicazione di filtri ai record di rilevamento per singole attività all'interno di un flusso di lavoro viene controllata dalle query incluse nel profilo di rilevamento.Per ulteriori informazioni, vedere la sezione **Tipi di query del profilo di rilevamento** in questo documento.  
  
 Le due modalità di visibilità specificate dall'attributo `implementationVisibility` nel profilo di rilevamento sono: `RootScope` e `All`.Utilizzando la modalità `RootScope` vengono eliminati i record di rilevamento per le attività che formano l'implementazione di un'attività nel caso in cui un'attività composita non costituisca la radice di un flusso di lavoro.Di conseguenza, quando un'attività implementata tramite altre attività viene aggiunta a un flusso di lavoro e l'attributo `implementationVisibility` viene impostato su RootScope, viene rilevata solo l'attività di primo livello all'interno di tale attività composita.Se un'attività costituisce la radice del flusso di lavoro, l'implementazione dell'attività è il flusso di lavoro stesso e i record di rilevamento vengono creati per le attività che formano l'implementazione.Tramite la modalità All, tutti i record di rilevamento possono essere creati per l'attività radice e tutte le relative attività composite.  
  
 Ad esempio, si supponga che *MyActivity* sia un'attività composita la cui implementazione contiene due attività, *Activity1* e *Activity2*.Quando questa attività viene aggiunta a un flusso di lavoro e il rilevamento viene abilitato con un profilo di rilevamento con l'attributo `implementationVisibility` impostato su `RootScope`, i record di rilevamento vengono creati solo per *MyActivity*e non per le attività *Activity1* e *Activity2*.  
  
 Tuttavia, se l'attributo `implementationVisisbility` per il profilo di rilevamento viene impostato su `All`, i record di rilevamento non vengono creati solo per *MyActivity*, ma anche per le attività *Activity1* e *Activity2*.  
  
 Il flag `implementationVisibility` si applica ai seguenti tipi di record di rilevamento:  
  
-   ActivityStateRecord  
  
-   FaultPropagationRecord  
  
-   CancelRequestedRecord  
  
-   ActivityScheduledRecord  
  
> [!NOTE]
>  I record CustomTrackingRecords creati dall'implementazione di attività non vengono filtrati dall'impostazione implementationVisibility.  
  
 La funzionalità `implementationVisibility` viene specificata come <xref:System.Activities.Tracking.ImplementationVisibility> sul profilo di rilevamento nel codice nel seguente modo:  
  
```  
TrackingProfile sampleTrackingProfile = new TrackingProfile()  
{  
    Name = "Sample Tracking Profile",  
    ImplementationVisibility = ImplementationVisibility.RootScope  
};  
  
```  
  
 La funzionalità `implementationVisibility` viene specificata come <xref:System.Activities.Tracking.ImplementationVisibility> sul profilo di rilevamento in un file di configurazione come riportato di seguito:  
  
```  
<tracking>  
      <profiles>  
        <trackingProfile name="Shipping Monitoring" implementationVisibility="All">  
          <workflow activityDefinitionId="*">  
...  
         </workflow>  
        </trackingProfile>  
      </profiles>  
</tracking>  
  
```  
  
 L'impostazione `ImplementationVisibility` nel profilo di rilevamento è facoltativa.Per impostazione predefinita, il relativo valore è impostato su `RootScope`.Per i valori di questo attributo viene applicata la distinzione tra maiuscole e minuscole.  
  
### Tipi di query del profilo di rilevamento  
 I profili di rilevamento sono strutturati come sottoscrizioni dichiarative per i record di rilevamento che consentono di eseguire query sul runtime del flusso di lavoro per record di rilevamento specifici.Sono disponibili numerosi tipi di query che consentono di sottoscrivere classi differenti di oggetti <xref:System.Activities.Tracking.TrackingRecord>.I profili di rilevamento possono essere specificati nella configurazione o tramite codice.Di seguito sono riportati i tipi di query più comuni:  
  
-   <xref:System.Activities.Tracking.WorkflowInstanceQuery>: utilizzare questo tipo per rilevare le modifiche del ciclo di vita dell'istanza del flusso di lavoro, ad esempio gli eventi `Started` e `Completed` dimostrati precedentemente.L'oggetto <xref:System.Activities.Tracking.WorkflowInstanceQuery> viene utilizzato per sottoscrivere gli oggetti <xref:System.Activities.Tracking.TrackingRecord> seguenti:  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceAbortedRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceTerminatedRecord>  
  
    -   <xref:System.Activities.Tracking.WorkflowInstanceSuspendedRecord>  
  
     Gli stati disponibili per la sottoscrizione sono specificati nella classe <xref:System.Activities.Tracking.WorkflowInstanceStates>.  
  
     La configurazione o il codice utilizzato per sottoscrivere i record di rilevamento a livello di istanza del flusso di lavoro per lo stato dell'istanza `Started` utilizzando l'oggetto <xref:System.Activities.Tracking.WorkflowInstanceQuery> è illustrato nell'esempio seguente.  
  
    ```  
    <workflowInstanceQueries>  
        <workflowInstanceQuery>  
          <states>  
            <state name="Started"/>  
          </states>  
        </workflowInstanceQuery>  
    </workflowInstanceQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new WorkflowInstanceQuery()  
            {  
                States = { WorkflowInstanceStates.Started}                                                                     
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.ActivityStateQuery>: utilizzare questo tipo per rilevare le modifiche del ciclo di vita delle attività che costituiscono un'istanza del flusso di lavoro.Ad esempio, potrebbe essere necessario tenere traccia di tutte le volte in cui l'attività "Invia messaggio" viene completata all'interno di un'istanza del flusso di lavoro.Questa query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.ActivityStateRecord>.Gli stati disponibili per la sottoscrizione sono specificati nell'oggetto <xref:System.Activities.Tracking.ActivityStates>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record di rilevamento dello stato dell'attività che utilizzano l'oggetto <xref:System.Activities.Tracking.ActivityStateQuery> per l'attività `SendEmailActivity` sono illustrati nell'esempio seguente.  
  
    ```  
    <activityStateQueries>  
      <activityStateQuery activityName="SendEmailActivity">  
        <states>  
          <state name="Closed"/>  
        </states>  
      </activityStateQuery>  
    </activityStateQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =  
        {  
            new ActivityStateQuery()  
            {                              
                ActivityName = "SendEmailActivity",  
                States = { ActivityStates.Closed }  
            }  
        }  
    };  
  
    ```  
  
    > [!NOTE]
    >  Se più elementi activityStateQuery hanno lo stesso nome, solo gli stati nell'ultimo elemento vengono utilizzati nel profilo di rilevamento.  
  
-   <xref:System.Activities.Tracking.ActivityScheduledQuery>: questa query consente di rilevare un'attività pianificata per l'esecuzione da parte di un'attività padre.La query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.ActivityScheduledRecord>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record relativi all'attività figlio `SendEmailActivity` in fase di pianificazione tramite l'oggetto <xref:System.Activities.Tracking.ActivityScheduledQuery> sono illustrati nell'esempio seguente.  
  
    ```  
    <activityScheduledQueries>  
      <activityScheduledQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />  
     </activityScheduledQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new ActivityScheduledQuery()  
            {  
                ActivityName = "ProcessNotificationsActivity",  
                ChildActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.FaultPropagationQuery>: utilizzare questo tipo per rilevare la gestione degli errori che si verificano all'interno di un'attività.La query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.FaultPropagationRecord>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record relativi alla propagazione degli errori tramite l'oggetto <xref:System.Activities.Tracking.FaultPropagationQuery> sono illustrati nell'esempio seguente.  
  
    ```  
    <faultPropagationQueries>  
      <faultPropagationQuery faultSourceActivityName="SendEmailActivity" faultHandlerActivityName="NotificationsFaultHandler" />  
    </faultPropagationQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =  
        {  
            new FaultPropagationQuery()  
            {  
                FaultSourceActivityName = "SendEmailActivity",  
                FaultHandlerActivityName = "NotificationsFaultHandler"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.CancelRequestedQuery>: utilizzare questo tipo per rilevare le richieste di annullamento di un'attività figlio da parte dell'attività padre.La query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.CancelRequestedRecord>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record relativi all'annullamento dell'attività tramite l'oggetto <xref:System.Activities.Tracking.CancelRequestedQuery> sono illustrati nell'esempio seguente.  
  
    ```  
    <cancelRequestedQueries>  
      <cancelRequestedQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />  
    </cancelRequestedQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new CancelRequestedQuery()  
            {  
                ActivityName = "ProcessNotificationsActivity",  
                ChildActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.CustomTrackingQuery>: utilizzare questo tipo per rilevare gli eventi definiti nelle attività del codice.La query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.CustomTrackingRecord>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record relativi ai record di rilevamento personalizzati tramite l'oggetto <xref:System.Activities.Tracking.CustomTrackingQuery> sono illustrati nell'esempio seguente.  
  
    ```  
    <customTrackingQueries>  
      <customTrackingQuery name="EmailAddress" activityName="SendEmailActivity" />  
    </customTrackingQueries>  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new CustomTrackingQuery()   
            {  
                Name = "EmailAddress",  
                ActivityName = "SendEmailActivity"  
            }  
        }  
    };  
  
    ```  
  
-   <xref:System.Activities.Tracking.BookmarkResumptionQuery>: utilizzare questo tipo per rilevare la ripresa di un segnalibro all'interno di un'istanza del flusso di lavoro.Questa query è necessaria affinché un oggetto <xref:System.Activities.Tracking.TrackingParticipant> sottoscriva gli oggetti <xref:System.Activities.Tracking.BookmarkResumptionRecord>.  
  
     La configurazione e il codice utilizzati per sottoscrivere i record relativi alla ripresa del segnalibro tramite l'oggetto <xref:System.Activities.Tracking.BookmarkResumptionQuery> sono illustrati nell'esempio seguente.  
  
    ```  
    <bookmarkResumptionQueries>  
      <bookmarkResumptionQuery name="SentEmailBookmark" />  
    </bookmarkResumptionQueries>  
  
    ```  
  
    ```  
    TrackingProfile sampleTrackingProfile = new TrackingProfile()  
    {  
        Name = "Sample Tracking Profile",  
        Queries =   
        {  
            new BookmarkResumptionQuery()  
            {  
                Name = "sentEmailBookmark"  
            }  
        }  
    };  
  
    ```  
  
### Annotazioni  
 Le annotazioni consentono di contrassegnare in modo arbitrario mediante tag i record di rilevamento con un valore che può essere configurato dopo la compilazione.È ad esempio possibile contrassegnare diversi record di rilevamento in più flussi di lavoro con il tag "Mail Server" \=\= "Mail Server1".Questo consente di individuare facilmente tutti i record con tale tag quando si esegue una query sui record di rilevamento in un secondo momento.  
  
 A tal fine, viene aggiunta un'annotazione a una query di rilevamento come mostrato nell'esempio seguente.  
  
```  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <annotations>  
    <annotation name="MailServer" value="Mail Server1"/>  
  </annotations>  
</activityStateQuery>  
  
```  
  
### Modalità di creazione di un profilo di rilevamento  
 Gli elementi della query di rilevamento vengono utilizzati per creare un profilo di rilevamento tramite un file di configurazione XML o il codice di [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)].Di seguito è riportato un esempio di un profilo di rilevamento creato utilizzando un file di configurazione.  
  
```  
<system.serviceModel>  
  <tracking>  
    <profiles>  
      <trackingProfile name="Sample Tracking Profile ">  
        <workflow activityDefinitionId="*">  
          <!--Specify the tracking profile query elements to subscribe for tracking records-->  
        </workflow>  
      </trackingProfile>  
    </profiles>  
  </tracking>  
</system.serviceModel>  
  
```  
  
> [!WARNING]
>  Per un servizio WF in cui viene utilizzato l'host del servizio del flusso di lavoro, il profilo di rilevamento viene generalmente creato utilizzando un file di configurazione.È anche possibile creare un profilo di rilevamento con il codice, utilizzando il profilo di rilevamento e l'API della query di rilevamento.  
  
 Un profilo configurato come file di configurazione XML viene applicato a un partecipante del rilevamento tramite un'estensione di comportamento.Questo viene aggiunto a un oggetto WorkflowServiceHost come illustrato nella sezione [Configurazione del rilevamento per un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md) riportata più avanti.  
  
 Il livello di dettaglio dei record di rilevamento creati dall'host è determinato dalle impostazioni di configurazione all'interno del profilo di rilevamento.Un partecipante del rilevamento sottoscrive i record di rilevamento aggiungendo query a un profilo di rilevamento.Per sottoscrivere tutti i record di rilevamento, il profilo di rilevamento deve specificare tutte le query di rilevamento utilizzando "\*" nei campi dei nomi di ogni query.  
  
 Di seguito sono riportati alcuni degli esempi comuni di profili di rilevamento.  
  
-   Profilo di rilevamento per ottenere i record dell'istanza del flusso di lavoro e gli errori.  
  
```  
<trackingProfile name="Instance and Fault Records">  
  <workflow activityDefinitionId="*">  
    <workflowInstanceQueries>  
      <workflowInstanceQuery>  
        <states>  
          <state name="*" />  
        </states>  
      </workflowInstanceQuery>  
    </workflowInstanceQueries>  
    <activityStateQueries>  
      <activityStateQuery activityName="*">  
        <states>  
          <state name="Faulted"/>  
        </states>  
      </activityStateQuery>  
    </activityStateQueries>  
  </workflow>  
</trackingProfile>  
  
```  
  
1.  Profilo di rilevamento per ottenere tutti i record di rilevamento personalizzati.  
  
```  
<trackingProfile name="Instance_And_Custom_Records">  
  <workflow activityDefinitionId="*">  
    <customTrackingQueries>  
      <customTrackingQuery name="*" activityName="*" />  
    </customTrackingQueries>  
  </workflow>  
</trackingProfile>  
  
```  
  
## Vedere anche  
 [Rilevamento SQL](../../../docs/framework/windows-workflow-foundation/samples/sql-tracking.md)   
 [Concetti di monitoraggio](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Monitoraggio delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=201275)