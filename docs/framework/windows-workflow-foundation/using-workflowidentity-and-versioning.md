---
title: "Utilizzo di WorkflowIdentity e controllo delle versioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8451735-8046-478f-912b-40870a6c0c3a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Utilizzo di WorkflowIdentity e controllo delle versioni
<xref:System.Activities.WorkflowIdentity> offre agli sviluppatori di applicazioni flusso di lavoro un modo per associare un nome e un elemento <xref:System.Version> a una definizione del flusso di lavoro. Consente inoltre di associare queste informazioni a un'istanza persistente del flusso di lavoro.Queste informazioni di identità possono essere utilizzate dagli sviluppatori di applicazioni flusso di lavoro per scenari quali l'esecuzione affiancata di più versioni di una definizione del flusso di lavoro e costituiscono un elemento fondamentale per altre funzionalità come l'aggiornamento dinamico.In questo argomento viene fornita una panoramica sull'utilizzo di <xref:System.Activities.WorkflowIdentity> con hosting <xref:System.Activities.WorkflowApplication>.Per informazioni sull'esecuzione affiancata di definizioni di flusso di lavoro in un servizio di flusso di lavoro, vedere [Gestione di più versioni in WorkflowServiceHost](../../../docs/framework/wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md).Per informazioni sull'aggiornamento dinamico, vedere [Aggiornamento dinamico](../../../docs/framework/windows-workflow-foundation//dynamic-update.md).  
  
## In questo argomento  
  
-   [Utilizzo di WorkflowIdentity](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UsingWorkflowIdentity)  
  
    -   [Esecuzione affiancata utilizzando WorkflowIdentity](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#SxS)  
  
-   [Aggiornamento del database di persistenza di .NET Framework 4 per supportare il controllo delle versioni del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)  
  
    -   [Per aggiornare lo schema di database](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#ToUpgrade)  
  
##  <a name="UsingWorkflowIdentity"></a> Utilizzo di WorkflowIdentity  
 Per utilizzare <xref:System.Activities.WorkflowIdentity>, creare un'istanza, configurarla e associarla a un'istanza di <xref:System.Activities.WorkflowApplication>.L'istanza di <xref:System.Activities.WorkflowIdentity> contiene tre informazioni di identificazione.Le proprietà <xref:System.Activities.WorkflowIdentity.Name%2A> e <xref:System.Activities.WorkflowIdentity.Version%2A> contengono un nome e un oggetto <xref:System.Version> e sono obbligatorie, mentre la proprietà <xref:System.Activities.WorkflowIdentity.Package%2A> è facoltativa e può essere utilizzata per specificare una stringa aggiuntiva che contiene informazioni quali il nome dell'assembly o altre informazioni desiderate.Un oggetto <xref:System.Activities.WorkflowIdentity> è univoco se una qualsiasi delle tre relative proprietà è diversa da un altro oggetto <xref:System.Activities.WorkflowIdentity>.  
  
> [!IMPORTANT]
>  <xref:System.Activities.WorkflowIdentity> non deve contenere eventuali informazioni identificabili personalmente \(PII\).Le informazioni su <xref:System.Activities.WorkflowIdentity> utilizzate per creare un'istanza vengono generate a tutti i servizi di rilevamento configurati in vari punti del ciclo di vita di attività dal runtime.La verifica di WF non ha alcun meccanismo per nascondere i PII \(dati riservati dell'utente\).Di conseguenza, un'istanza di <xref:System.Activities.WorkflowIdentity> non deve contenere dati di PII poiché verrebbe generata dal runtime nei record di rilevamento e può essere visibile agli utenti con accesso alla visualizzazione dei record di rilevamento.  
  
 Nell'esempio riportato di seguito, un oggetto <xref:System.Activities.WorkflowIdentity> viene creato e associato a un'istanza di un flusso di lavoro creato utilizzando una definizione del flusso di lavoro di `MortgageWorkflow`.  
  
```csharp  
WorkflowIdentity identityV1 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v1",  
    Version = new Version(1, 0, 0, 0)  
};  
  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Run the workflow.  
wfApp.Run();  
```  
  
 Quando un flusso di lavoro viene nuovamente caricato e ripreso, è necessario utilizzare un oggetto <xref:System.Activities.WorkflowIdentity> configurato per corrispondere all'oggetto <xref:System.Activities.WorkflowIdentity> dell'istanza persistente del flusso di lavoro.  
  
```csharp  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Load the workflow.  
wfApp.Load(instanceId);  
  
// Resume the workflow...  
```  
  
 Se l'oggetto <xref:System.Activities.WorkflowIdentity> utilizzato durante la ricarica dell'istanza del flusso di lavoro non corrisponde l'oggetto <xref:System.Activities.WorkflowIdentity> persistente, viene generata un'eccezione <xref:System.Activities.VersionMismatchException>.Nell'esempio riportato di seguito viene effettuato un tentativo di caricamento dell'istanza di `MortgageWorkflow` che è stata resa persistente nell'esempio precedente.Questo tentativo di caricamento viene eseguito mediante <xref:System.Activities.WorkflowIdentity> configurato per una versione più recente del flusso di lavoro relativo a un'ipoteca che non corrisponde all'istanza persistente.  
  
```csharp  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow_v2(), identityV2);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Attempt to load the workflow instance.  
wfApp.Load(instanceId);  
  
// Resume the workflow...  
```  
  
 Quando viene eseguito il codice precedente, viene generata la seguente eccezione <xref:System.Activities.VersionMismatchException>.  
  
 **L'oggetto WorkflowIdentity \(" MortgageWorkflow v1; Version\= 1.0.0.0 "\) dell'istanza caricata non corrisponde all'oggetto WorkflowIdentity \(" MortgageWorkflow v2; Version\= 2.0.0.0 "\) della definizione del flusso di lavoro fornita.L'istanza può essere caricata mediante una definizione diversa o aggiornata mediante l'aggiornamento automatico.**   
###  <a name="SxS"></a> Esecuzione affiancata utilizzando WorkflowIdentity  
 <xref:System.Activities.WorkflowIdentity> può essere utilizzato per facilitare l'esecuzione di più versioni di un flusso di lavoro affiancate.Uno scenario comune consiste nella modifica dei requisiti aziendali in un flusso di lavoro di lunga durata.Molte istanze di un flusso di lavoro potrebbero essere in esecuzione quando una versione aggiornata viene distribuita.L'applicazione host può essere configurata per utilizzare la definizione aggiornata del flusso di lavoro all'avvio di nuove istanze. È responsabilità dell'applicazione host fornire la definizione del flusso di lavoro corretta quando vengono riprese le istanze.<xref:System.Activities.WorkflowIdentity> può essere utilizzato per identificare e fornire la definizione corrispondente del flusso di lavoro quando vengono riprese le istanze del flusso di lavoro.  
  
 Per recuperare l'oggetto <xref:System.Activities.WorkflowIdentity> di un'istanza persistente del flusso di lavoro, viene utilizzato il metodo <xref:System.Activities.WorkflowApplication.GetInstance%2A>.Il metodo <xref:System.Activities.WorkflowApplication.GetInstance%2A> accetta l'oggetto <xref:System.Activities.WorkflowApplication.Id%2A> dell'istanza persistente del flusso di lavoro e l'oggetto <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> contenente l'istanza persistente e restituisce un oggetto <xref:System.Activities.WorkflowApplicationInstance>.Un oggetto <xref:System.Activities.WorkflowApplicationInstance> contiene informazioni su un'istanza persistente del flusso di lavoro, incluso il relativo oggetto <xref:System.Activities.WorkflowIdentity> associato.Questo oggetto <xref:System.Activities.WorkflowIdentity> associato può essere utilizzato dall'host per fornire la definizione del flusso di lavoro corretta durante il caricamento e la ripresa dell'istanza del flusso di lavoro.  
  
> [!NOTE]
>  Un oggetto <xref:System.Activities.WorkflowIdentity> null è valido e può essere utilizzato dall'host per eseguire il mapping delle istanze che sono state salvate in modo permanente senza alcun <xref:System.Activities.WorkflowIdentity> associato alla definizione appropriata del flusso di lavoro.Questo scenario può verificarsi quando un'applicazione flusso di lavoro inizialmente non è stata scritta con il controllo delle versioni del flusso di lavoro o quando un'applicazione viene aggiornata da [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)].[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Aggiornamento del database di persistenza di .NET Framework 4 per supportare il controllo delle versioni del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases).  
  
 Nell'esempio riportato di seguito viene utilizzato un oggetto `Dictionary<WorkflowIdentity, Activity>` per associare le istanze di <xref:System.Activities.WorkflowIdentity> alle definizioni corrispondenti del flusso di lavoro; viene inoltre avviato un flusso di lavoro utilizzando la definizione del flusso di lavoro `MortgageWorkflow`, che è associata all'oggetto `identityV1` <xref:System.Activities.WorkflowIdentity>.  
  
```csharp  
WorkflowIdentity identityV1 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v1",  
    Version = new Version(1, 0, 0, 0)  
};  
  
WorkflowIdentity identityV2 = new WorkflowIdentity  
{  
    Name = "MortgageWorkflow v2",  
    Version = new Version(2, 0, 0, 0)  
};  
  
Dictionary<WorkflowIdentity, Activity> WorkflowVersionMap = new Dictionary<WorkflowIdentity, Activity>();  
WorkflowVersionMap.Add(identityV1, new MortgageWorkflow());  
WorkflowVersionMap.Add(identityV2, new MortgageWorkflow_v2());  
  
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Run the workflow.  
wfApp.Run();  
```  
  
 Nell'esempio riportato di seguito, le informazioni sull'istanza persistente del flusso di lavoro derivante dall'esempio precedente vengono recuperate chiamando il metodo <xref:System.Activities.WorkflowApplication.GetInstance%2A>; le informazioni relative all'oggetto <xref:System.Activities.WorkflowIdentity> persistente vengono utilizzate per recuperare la definizione corrispondente del flusso di lavoro.Queste informazioni vengono utilizzate per configurare <xref:System.Activities.WorkflowApplication>, quindi il flusso di lavoro viene caricato.Si noti che dal momento che viene utilizzato l'overload <xref:System.Activities.WorkflowApplication.Load%2A> che accetta <xref:System.Activities.WorkflowApplicationInstance>, l'oggetto <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> che era configurato nell'oggetto <xref:System.Activities.WorkflowApplicationInstance> viene utilizzato da <xref:System.Activities.WorkflowApplication>, di conseguenza la relativa proprietà <xref:System.Activities.WorkflowApplication.InstanceStore%2A> non necessita di configurazione.  
  
> [!NOTE]
>  Se la proprietà <xref:System.Activities.WorkflowApplication.InstanceStore%2A> è impostata, deve essere impostata con la stessa istanza di <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> utilizzata da <xref:System.Activities.WorkflowApplicationInstance>, altrimenti verrà generata un'eccezione <xref:System.ArgumentException> con il messaggio seguente: `The instance is configured with a different InstanceStore than this WorkflowApplication.`.  
  
```csharp  
// Get the WorkflowApplicationInstance of the desired workflow from the specified  
// SqlWorkflowInstanceStore.  
WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(instanceId, store);  
  
// Use the persisted WorkflowIdentity to retrieve the correct workflow  
// definition from the dictionary.  
Activity definition = WorkflowVersionMap[instance.DefinitionIdentity];  
  
WorkflowApplication wfApp = new WorkflowApplication(definition, instance.DefinitionIdentity);  
  
// Configure the WorkflowApplication with persistence and desired workflow event handlers.  
ConfigureWorkflowApplication(wfApp);  
  
// Load the persisted workflow instance.  
wfApp.Load(instance);  
  
// Resume the workflow...  
```  
  
##  <a name="UpdatingWF4PersistenceDatabases"></a> Aggiornamento del database di persistenza di .NET Framework 4 per supportare il controllo delle versioni del flusso di lavoro  
 Uno script del database SqlWorkflowInstanceStoreSchemaUpgrade.sql viene fornito per aggiornare i database di persistenza creati mediante gli script del database di [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)].Questo script aggiorna i database per supportare nuove funzionalità di controllo delle versioni introdotte in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].Le istanze persistenti del flusso di lavoro nei database sono valori predefiniti specificati per il controllo delle versioni e quindi possono partecipare all'esecuzione side\-by\-side e all'aggiornamento dinamico.  
  
 Se un'applicazione flusso di lavoro [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] tenta un'operazione di persistenza che utilizza il nuovo controllo delle versioni in un database di persistenza che non è stato aggiornato mediante lo script fornito, viene generata l'eccezione <xref:System.Runtime.DurableInstancing.InstancePersistenceCommandException> con un messaggio simile al seguente.  
  
 **L'elemento SqlWorkflowInstanceStore ha una versione di database di '4.0.0.0'.Impossibile eseguire InstancePersistenceCommand 'System.Activities.DurableInstancing.CreateWorkflowOwnerWithIdentityCommand' in relazione a questa versione di database.Aggiornare il database a '4.5.0.0'.**   
###  <a name="ToUpgrade"></a> Per aggiornare lo schema di database  
  
1.  Aprire SQL Server Management Studio e connettersi al server di database di persistenza, ad esempio **.\\SQLEXPRESS**.  
  
2.  Scegliere **Apri**, quindi **File** dal menu **File**.Individuare la seguente cartella: `C:\Windows\Microsoft.NET\Framework\4.0.30319\sql\en`  
  
3.  Selezionare **SqlWorkflowInstanceStoreSchemaUpgrade.sql** e fare clic su **Apri**.  
  
4.  Selezionare il nome del database di persistenza nell'elenco a discesa **Database disponibili**.  
  
5.  Scegliere **Esegui** dal menu **Query**.  
  
 Quando la query viene completata, lo schema di database verrà aggiornato e, se necessario, è possibile visualizzare l'identità predefinita del flusso di lavoro assegnata alle istanze persistenti del flusso di lavoro.In **Esplora oggetti**, espandere il database di persistenza nel nodo **Database**, quindi espandere il nodo **Visualizzazioni**.Fare clic con il pulsante destro del mouse su **System.Activities.DurableInstancing.Instances** e scegliere **Seleziona le prime 1000 righe**.Scorrere fino alla fine delle colonne e notare che sei ulteriori colonne sono state aggiunte alla visualizzazione: **IdentityName**, **IdentityPackage**, **Build**, **Major**, **Minor** e **Revision**.Tutti i flussi di lavoro persistenti avranno il valore **NULL** per questi campi, a rappresentazione di un'identità null del flusso di lavoro.