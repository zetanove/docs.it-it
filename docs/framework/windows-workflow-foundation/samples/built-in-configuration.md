---
title: "Configurazione predefinita | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34e85c9b-088d-4347-816c-0f77cb73ef2f
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Configurazione predefinita
In questo esempio vengono illustrati l'utilizzo e la configurazione dell'archivio di istanze del flusso di lavoro SQL.L'archivio di istanze del flusso di lavoro SQL è un'implementazione basata su SQL di un archivio di istanze.Consente a un'istanza di salvare e caricare il proprio stato da e verso un database SQL Server o SQL Server Express.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, visitare la pagina di download per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Persistence\BuiltInConfiguration`  
  
## Dettagli dell'esempio  
 Questo esempio è costituito da un flusso di lavoro che implementa un servizio di conteggio.Una volta richiamato il metodo di avvio del servizio, il servizio conta da 0 a 59.Il contatore viene incrementato una volta ogni 2 secondi.Dopo ogni conteggio, il flusso di lavoro viene salvato in modo permanente.  
  
 Il flusso di lavoro del conteggio è indipendente in un host del servizio flusso di lavoro.Il metodo `Main` del programma crea un'istanza dell'host del servizio flusso di lavoro che ospita il flusso di lavoro del conteggioe definisce gli endpoint in cui quest'ultimo può essere raggiunto.Definisce quindi un comportamento dell'archivio di istanze del flusso di lavoro SQL utilizzato per configurare l'archivio di istanze del flusso di lavoro SQL.Successivamente il programma crea un client che chiama il metodo di avvio del flusso di lavoro del conteggio.  
  
 Dopo l'avvio del programma, il contatore avvia automaticamente il conteggio.Notare che potrebbero essere necessari alcuni secondi per caricare l'istanza e configurare l'archivio di istanze del flusso di lavoro SQL.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]ll'archivio di istanze del flusso di lavoro, vedere [Archivio di istanze del flusso di lavoro SQL](../../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).  
  
 L'esempio è costituito da due parti:  
  
1.  InstanceStore1 illustra come viene configurato <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> utilizzando codice C\# \(vedere Program.cs\).  
  
2.  InstanceStore2 illustra come viene configurato <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> utilizzando codice XML \(vedere App.config\).  
  
 Per configurare il comportamento dell'archivio di istanze del flusso di lavoro SQL, sono disponibili le impostazioni seguenti:  
  
-   Impostare `HostLockRenewalPeriod`.Questo periodo definisce l'intervallo con il quale l'host rinnova il blocco di proprietà delle istanze che esegue.Le informazioni sul blocco vengono archiviate nell'archivio di istanze.Se la proprietà non viene rinnovata per due degli intervalli definiti in `HostLockRenewalPeriod`, l'istanza viene considerata abbandonata.Se un altro oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost> sta eseguendo lo stesso flusso di lavoro ed è connesso allo stesso archivio di istanze \(sullo stesso computer o uno diverso\), tale istanza viene ripristinata.\(Il ripristino dell'istanza non rientra nell'ambito per questo esempio\).  
  
-   Impostare `RunnableInstancesDetectionPeriod`.Questo periodo definisce l'intervallo nel quale l'host esegue il polling per cercare le istanze diventate eseguibili.Le istanze potrebbero diventare eseguibili se si verifica uno qualsiasi degli eventi seguenti:  
  
    -   Un timer durevole \(<xref:System.Activities.Statements.Delay>\) scade.  
  
    -   Un altro host non riceve il proprio heartbeat `HostLockRenewal` \(ad esempio, a causa di un arresto anomalo del sistema\) e l'istanza viene ripristinata.  
  
-   Impostare `InstanceCompletionAction`.Questa proprietà, se impostata su `DeleteNothing`, mantiene le istanze completate nell'archivio di istanze. Se impostata su `DeleteAll`, le istanze vengono eliminate dall'archivio al completamento.Notare che  
  
    > [!NOTE]
    >  Se l'host viene terminato premendo INVIO prima che il conteggio sia stato completato, l'istanza del flusso di lavoro non viene completata.  
  
-   Impostare `InstanceLockedExceptionAction`.Questa impostazione definisce le operazioni che l'host deve eseguire per caricare un'istanza bloccata da un altro host.Sono disponibili le opzioni seguenti:  
  
    -   Se impostata su `NoRetry`: il caricamento non viene ritentato e viene restituito all'host un oggetto `InstanceLockedException`.  
  
    -   Se impostata su `BasicRetry`: i tentativi di caricamento dell'istanza vengono continuati.I tentativi sono pianificati in base a un algoritmo lineare semplice \(ad esempio, ritentare ogni 5 secondi\).  
  
    -   Se impostata su `AggressiveRetry`: i tentativi di caricamento dell'istanza vengono continuati.I tentativi sono pianificati in base a un algoritmo di interruzione temporanea esponenziale aggressivo.  
  
-   Impostare l'opzione di codifica.Questa impostazione definisce come viene archiviato lo stato dell'istanza nell'archivio di istanze del flusso di lavoro SQL.Sono disponibili le opzioni seguenti:  
  
    -   Lo stato dell'istanza viene compresso utilizzando l'algoritmo di compressione GZip.  
  
    -   Lo stato dell'istanza non viene compresso.  
  
#### Per utilizzare questo esempio  
  
1.  Aprire il prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] come amministratore, se sono disponibili autorizzazioni.  
  
2.  Passare alla directory di esempio \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\\CS\) ed eseguire CreateInstanceStore.cmd.  
  
3.  Se i privilegi di amministratore non sono disponibili, creare un account di accesso di SQL Server.Andare a `Security`, **Account di accesso**.Fare clic con il pulsante destro del mouse su **Account di accesso** e creare un nuovo accesso.  
  
4.  Aggiungere l'utente ACL al ruolo SQL.Aprire **Database**, **InstanceStore**, **Sicurezza**.Fare clic con il pulsante destro del mouse su **Utenti** e scegliere **Nuovi utenti**.Impostare **Nome account di accesso** sull'utente creato nel passaggio precedente.Aggiungere l'utente all'appartenenza ai ruoli del database **System.Activities.DurableInstancing.InstanceStoreUsers** \(e altri\).Notare che l'utente potrebbe essere già presente \(ad esempio, utente dbo\).  
  
5.  Aprire il file InstanceStore.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e compilare la soluzione premendo CTRL\+MAIUSC\+B.  
  
6.  In [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)] passare alla directory dell'esempio appropriata bin\\debug \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\\cs\\InstanceStore \(1 o 2\) \\bin\\debug\), fare clic con il pulsante destro del mouse su InstanceStore.exe e scegliere **Esegui come amministratore**.È necessario eseguire questo esempio con i privilegi di amministratore perché viene aperto un listener del canale.  
  
7.  Se è stato creato l'archivio di istanze in un database diverso da un'installazione locale di SQL Server Express, è necessario aggiornare la stringa di connessione al database \(`const string ConnectionString` in Program.cs del progetto InstanceStore1 e l'attributo `connectionString` in App.config del progetto InstanceStore2\) nell'esempio e ricompilarlo.  
  
#### Per verificare che l'esempio venga eseguito correttamente  
  
1.  Mentre l'esempio è in esecuzione, avviare SQL Server Management Studio.  
  
2.  In **Esplora oggetti** selezionare **Database**, **InstanceStore**, **Tabelle** e quindi **System.Activities.DurableInstancing.InstanceTable**.  
  
3.  Fare clic con il pulsante destro del mouse su **InstanceTable** e scegliere **Seleziona le prime 1000 righe**.  
  
4.  Osservare che è presente una nuova voce e che il valore di **Lock Expiration** viene modificato ogni 5 secondi \(fare clic sul pulsante **Esegui** sulla barra delle applicazioni per aggiornare la query\).Si tratta di una conseguenza dell'impostazione di **Host Lock Renewal Period** su 5.  
  
5.  Osservare che dopo il completamento del conteggio, la voce nella tabella dell'istanza viene rimossa.Si tratta di una conseguenza dell'impostazione di **Instance Completion Action** su **DeleteAll**.  
  
6.  Premere INVIO per terminare l'applicazione host del flusso di lavoro e osservare che la voce **LockOwnersTable** viene eliminata.  
  
#### Per disinstallare l'esempio  
  
1.  Eseguire RemoveInstanceStore.cmd nella directory di esempio \(\\WF\\Basic\\Persistence\\BuiltInConfiguration\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Persistence\BuiltInConfiguration`  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)