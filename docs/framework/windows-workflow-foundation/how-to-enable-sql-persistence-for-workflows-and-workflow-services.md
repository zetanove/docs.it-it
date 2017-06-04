---
title: "Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ca7bf77f-3e5d-4b23-b17a-d0b60f46411d
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# Procedura: abilitare la persistenza SQL per i flussi di lavoro e i relativi servizi
In questo argomento viene descritto come configurare la funzionalità di archivio di istanze del flusso di lavoro SQL per abilitare la persistenza per i flussi di lavoro e i relativi servizi sia a livello di codice sia tramite un file di configurazione.  
  
 Windows Server AppFabric semplifica il processo di configurazione della persistenza.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Configurazione della persistenza in AppFabric](http://go.microsoft.com/fwlink/?LinkId=201204)  
  
 Prima di utilizzare tale funzionalità, creare un database utilizzato dalla funzionalità per rendere persistenti le istanze del flusso di lavoro.Il programma di installazione di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] copia i file di script SQL associati alla funzionalità di archivio di istanze del flusso di lavoro SQL nella cartella %WINDIR%\\Microsoft.NET\\Framework\\v4.xxx\\SQL\\EN.Eseguire questi file di script in un database di SQL Server 2005 o SQL Server 2008 che si desidera venga utilizzato dall'archivio di istanze del flusso di lavoro SQL per rendere persistenti le istanze del flusso di lavoro.Eseguire innanzitutto il file SqlWorkflowInstanceStoreSchema.sql, quindi il file SqlWorkflowInstanceStoreLogic.sql.  
  
> [!NOTE]
>  Per pulire il database di persistenza per avere un database aggiornato, eseguire gli script in %WINDIR%\\Microsoft.NET\\Framework\\v4.xxx\\SQL\\EN nell'ordine seguente.  
>   
>  1.  SqlWorkflowInstanceStoreSchema.sql  
> 2.  SqlWorkflowInstanceStoreLogic.sql  
  
> [!IMPORTANT]
>  Se non si crea un database di persistenza, la funzionalità di archivio di istanze del flusso di lavoro SQL genera un'eccezione simile alla seguente quando un host tenta di rendere persistenti i flussi di lavoro.  
>   
>  System.Data.SqlClient.SqlException: Impossibile trovare la stored procedure 'System.Activities.DurableInstancing.CreateLockOwner'  
  
 Nelle sezioni seguenti viene descritto come abilitare la persistenza per i flussi di lavoro e i relativi servizi utilizzando l'archivio di istanze del flusso di lavoro SQL.[!INCLUDE[crabout](../../../includes/crabout-md.md)]lle proprietà di Archivio di istanze del flusso di lavoro SQL, vedere [Proprietà dell'archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//properties-of-sql-workflow-instance-store.md).  
  
## Abilitazione della persistenza per i flussi di lavoro indipendenti che utilizzano l'oggetto WorkflowApplication  
 È possibile abilitare la persistenza per i flussi di lavoro indipendenti che utilizzano l'oggetto <xref:System.Activities.WorkflowApplication> a livello di codice tramite il modello a oggetti <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>.Nella procedura seguente sono inclusi i passaggi per eseguire questa operazione.  
  
#### Per abilitare la persistenza per i flussi di lavoro indipendenti  
  
1.  Aggiungere un riferimento a System.Activites.DurableInstancing.dll.  
  
2.  Aggiungere l'istruzione seguente all'inizio del file di origine dopo le istruzioni "using" esistenti.  
  
    ```csharp  
    using System.Activities.DurableInstancing;  
    ```  
  
3.  Costruire un oggetto <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> e assegnarlo alla proprietà <xref:System.Activities.WorkflowApplication.InstanceStore%2A> dell'oggetto <xref:System.Activities.WorkflowApplication> come mostrato nell'esempio di codice seguente.  
  
    ```csharp  
  
    SqlWorkflowInstanceStore store =   
        new SqlWorkflowInstanceStore("Server=.\\SQLEXPRESS;Initial Catalog=Persistence;Integrated Security=SSPI");  
  
    WorkflowApplication wfApp =  
        new WorkflowApplication(new Workflow1());  
  
    wfApp.InstanceStore = store;  
  
    ```  
  
    > [!NOTE]
    >  Il nome del server della stringa di connessione potrebbe essere diverso a seconda dell'edizione di SQL Server.  
  
4.  Richiamare il metodo <xref:System.Activities.WorkflowApplication.Persist%2A> sull'oggetto <xref:System.Activities.WorkflowApplication> per rendere persistente un flusso di lavoro o il metodo <xref:System.Activities.WorkflowApplication.Unload%2A> per rendere persistente e scaricare un flusso di lavoro.È anche possibile gestire l'evento <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> generato dall'oggetto <xref:System.Activities.WorkflowApplication> e restituire il membro \(<xref:System.Activities.PersistableIdleAction> o <xref:System.Activities.PersistableIdleAction>\) appropriato dell'oggetto <xref:System.Activities.PersistableIdleAction>.  
  
    ```csharp  
    wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)  
    {  
        return PersistableIdleAction.Persist;  
    };  
    ```  
  
> [!NOTE]
>  Per informazioni sull'abilitazione della persistenza per i flussi di lavoro tramite l'oggetto <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> e il passaggio [Procedura: creare ed eseguire un flusso di lavoro con esecuzione prolungata](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md) dell'[Esercitazione introduttiva](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md) per istruzioni dettagliate, vedere l'esempio [Persistenza di un'applicazione flusso di lavoro](../../../docs/framework/windows-workflow-foundation/samples/persisting-a-workflow-application.md) in [Persistenza](../../../docs/framework/windows-workflow-foundation/samples/persistence.md).  
  
## Abilitazione della persistenza per i servizi flussi di lavoro indipendenti che utilizzano l'oggetto WorkflowServiceHost  
 È possibile abilitare la persistenza per i servizi flussi di lavoro indipendenti che utilizzano l'oggetto <xref:System.ServiceModel.WorkflowServiceHost> a livello di codice tramite la classe <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> o <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A>.  
  
### Utilizzo della classe SqlWorkflowInstanceStoreBehavior  
 Nella procedura seguente sono contenuti i passaggi per utilizzare la classe <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> al fine di abilitare la persistenza per i servizi flussi di lavoro indipendenti.  
  
##### Per abilitare la persistenza tramite l'oggetto SqlWorkflowInstanceStoreBehavior  
  
1.  Aggiungere un riferimento a System.ServiceModel.dll.  
  
2.  Aggiungere l'istruzione seguente all'inizio del file di origine dopo le istruzioni "using" esistenti.  
  
    ```csharp  
    using System.ServiceModel.Activities.Description;  
    ```  
  
3.  Creare un'istanza dell'oggetto `WorkflowServiceHost` e aggiungere gli endpoint per il servizio flusso di lavoro.  
  
    ```  
  
    WorkflowServiceHost host = new WorkflowServiceHost(new CountingWorkflow(), new Uri(hostBaseAddress));  
    host.AddServiceEndpoint("ICountingWorkflow", new BasicHttpBinding(), "");  
  
    ```  
  
4.  Costruire un oggetto `SqlWorkflowInstanceStoreBehavior` e impostare le proprietà dell'oggetto di comportamento.  
  
    ```csharp  
  
    SqlWorkflowInstanceStoreBehavior instanceStoreBehavior = new SqlWorkflowInstanceStoreBehavior(connectionString);  
    instanceStoreBehavior.HostLockRenewalPeriod = new TimeSpan(0, 0, 5);  
    instanceStoreBehavior.InstanceCompletionAction = InstanceCompletionAction.DeleteAll;  
    instanceStoreBehavior.InstanceLockedExceptionAction = InstanceLockedExceptionAction.AggressiveRetry;  
    instanceStoreBehavior.InstanceEncodingOption = InstanceEncodingOption.GZip;  
    instanceStoreBehavior.RunnableInstancesDetectionPeriod = new TimeSpan("00:00:02");  
    host.Description.Behaviors.Add(instanceStoreBehavior);  
  
    ```  
  
5.  Aprire l'host del servizio flusso di lavoro.  
  
    ```vb  
  
    host.Open();  
  
    ```  
  
> [!IMPORTANT]
>  Per informazioni sull'abilitazione della persistenza per i servizi flussi di lavoro tramite la classe `SqlWorkflowInstanceStoreBehavior`, vedere l'esempio [Configurazione predefinita](../../../docs/framework/windows-workflow-foundation/samples/built-in-configuration.md) in [Persistenza](../../../docs/framework/windows-workflow-foundation/samples/persistence.md).  
  
### Utilizzo della proprietà DurableInstancingOptions  
 Quando l'oggetto `SqlWorkflowInstanceStoreBehavior` è applicato, l'oggetto `DurableInstancingOptions.InstanceStore` in `WorkflowServiceHost` viene impostato sull'oggetto `SqlWorkflowInstanceStore` creato utilizzando i valori di configurazione.Tale operazione può essere eseguita anche a livello di codice per impostare la proprietà <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A> dell'oggetto `WorkflowServiceHost` senza utilizzare la classe `SqlWorkflowInstanceStoreBehavior` come mostrato nell'esempio di codice seguente.  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
## Abilitazione della persistenza per i servizi flussi di lavoro ospitati nel servizio WAS che utilizzano l'oggetto WorkflowServiceHost tramite un file di configurazione  
 È possibile abilitare la persistenza per i servizi flussi di lavori indipendenti oppure ospitati nel servizio WAS tramite un file di configurazione.Un servizio flusso di lavoro ospitato nel servizio WAS utilizza l'oggetto WorkflowServiceHost come servizi flussi di lavoro indipendenti.  
  
 L'oggetto `SqlWorkflowInstanceStoreBehavior` è un comportamento del servizio che consente di modificare in modo semplice le proprietà [Archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md) tramite la configurazione XML.Per i servizi flussi di lavoro ospitati nel servizio WAS, utilizzare il file Web.config.Nell'esempio di configurazione seguente viene mostrato come configurare l'archivio di istanze del flusso di lavoro SQL tramite l'elemento del comportamento `sqlWorkflowInstanceStore` in un file di configurazione.  
  
```  
  
<serviceBehaviors>  
    <behavior name="">  
        <sqlWorkflowInstanceStore   
                    connectionString="Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                    instanceEncodingOption="GZip | None"  
                    instanceCompletionAction="DeleteAll | DeleteNothing"  
                    instanceLockedExceptionAction="NoRetry | BasicRetry |AggressiveRetry"  
                    hostLockRenewalPeriod="00:00:30"   
                    runnableInstancesDetectionPeriod="00:00:05">  
  
        <sqlWorkflowInstanceStore/>  
    </behavior>  
</serviceBehaviors>  
  
```  
  
 Se non si impostano i valori per la proprietà `connectionString` o `connectionStringName`, l'archivio di istanze del flusso di lavoro SQL utilizza la stringa di connessione predefinita denominata `DefaultSqlWorkflowInstanceStoreConnectionString`.  
  
 Quando l'oggetto `SqlWorkflowInstanceStoreBehavior` è applicato, l'oggetto `DurableInstancingOptions.InstanceStore` in `WorkflowServiceHost` viene impostato sull'oggetto `SqlWorkflowInstanceStore` creato utilizzando i valori di configurazione.Tale operazione può essere eseguita anche a livello di codice per utilizzare l'oggetto `SqlWorkflowInstanceStore` con l'oggetto `WorkflowServiceHost` senza utilizzare l'elemento del comportamento del servizio.  
  
```  
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;  
```  
  
> [!IMPORTANT]
>  È consigliabile non archiviare nel file Web.config informazioni riservate, quali nomi utente e password.In caso contrario, è necessario proteggere l'accesso a tale file tramite gli elenchi di controllo di accesso \(ACL\) del file system.Inoltre, è anche possibile proteggere i valori di configurazione all'interno di un file di configurazione come illustrato in [Crittografia delle informazioni di configurazione utilizzando la configurazione protetta](http://go.microsoft.com/fwlink/?LinkId=178419).  
  
### Elementi Machine.config correlati alla funzionalità di archivio di istanze del flusso di lavoro SQL  
 L'installazione di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] comporta l'aggiunta degli elementi seguenti correlati alla funzionalità di archivio di istanze del flusso di lavoro SQL al file Machine.config:  
  
-   Aggiungere il seguente elemento di estensione del comportamento al file Machine.config in modo da poter utilizzare l'elemento del comportamento del servizio \<`sqlWorkflowInstanceStore`\> nel di configurazione per configurare la persistenza per i servizi.  
  
    ```  
  
    <configuration>  
        <system.serviceModel>  
            <extensions>  
                <behaviorExtensions>  
                    <add name="sqlWorkflowInstanceStore" type="System.Activities.DurableInstancing.SqlWorkflowInstanceStoreElement, System.Activities.DurableInstancing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />  
                </behaviorExtensions>  
            </extensions>  
        <system.serviceModel>  
    <configuration>  
  
    ```