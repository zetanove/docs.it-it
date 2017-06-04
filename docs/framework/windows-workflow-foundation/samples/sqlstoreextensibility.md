---
title: "SQLStoreExtensibility | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5da1b5a3-f144-41ba-b9c4-02818b28b15d
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# SQLStoreExtensibility
In questo esempio vengono illustrati l'utilizzo e la configurazione delle proprietà promosse nell'archivio di istanze del flusso di lavoro SQL.L'archivio di istanze del flusso di lavoro SQL è un'implementazione basata su SQL di un archivio di istanze.Consente a un'istanza di salvare il relativo stato e caricarlo da e verso un database SQL Server o SQL Server Express.La funzionalità di estensibilità dell'archivio consente all'utente di definire le proprietà che vengono archiviate nell'archivio di istanze.Queste proprietà vengono riportate in una visualizzazione di proprietà promosse che consente all'utente di eseguire query relative alle stesse.  
  
 Questo esempio è costituito da un flusso di lavoro che implementa un servizio di conteggio.Una volta richiamato il metodo di avvio del servizio, il servizio conta da 0 a 29.Il contatore viene incrementato una volta ogni 2 secondi.Dopo ogni conteggio, il flusso di lavoro viene salvato in modo permanente.Il valore del contatore corrente viene archiviato nell'archivio di istanze come una proprietà promossa.  
  
 Il flusso di lavoro del conteggio è indipendente in un host del servizio flusso di lavoro.Il metodo `Main` del programma esegue le azioni riportate di seguito.  
  
-   Crea un'istanza dell'host del servizio flusso di lavoro che ospita il flusso di lavoro del conteggio e definisce gli endpoint in cui quest'ultimo può essere raggiunto.  
  
-   Definisce un comportamento dell'archivio di istanze del flusso di lavoro SQL utilizzato per configurare l'archivio di istanze del flusso di lavoro SQL.In base alle istruzioni l'archivio considera `CountStatus` come proprietà promossa.  
  
-   Crea un client che chiama il metodo di avvio del flusso di lavoro del conteggio.  
  
 Dopo l'avvio del programma, il contatore avvia automaticamente il conteggio.Notare che potrebbero essere necessari alcuni secondi per caricare l'istanza e configurare l'archivio di istanze del flusso di lavoro SQL.  
  
 Per promuovere il valore del contatore come una proprietà personalizzata, è necessario effettuare i passaggi seguenti:  
  
1.  La classe `CounterStatus` definisce un'estensione dell'istanza di tipo <xref:System.Activities.Persistence.PersistenceParticipant>, che è utilizzata dalle attività per fornire le variabili di stato.`Count` è definito come valore di sola scrittura.Quando un'istanza del flusso di lavoro raggiunge un punto di persistenza, l'estensione dell'istanza salva la proprietà `Count` nella raccolta dati di persistenza.  
  
2.  Quando viene creato l'archivio di istanze, viene definita la nuova proprietà `CountStatus` tramite il metodo `store.Promote()`.  
  
3.  L'attività `SaveCounter` del flusso di lavoro assegna il valore del contatore corrente al campo di stato `Count`.  
  
### Per utilizzare questo esempio  
  
1.  Creare il database dell'archivio di istanze.  
  
    1.  Aprire un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
    2.  Passare alla directory di esempio \(\\WF\\Basic\\Persistence\\SqlStoreExtensibility\\CS\) ed eseguire CreateInstanceStore.cmd al prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
        > [!WARNING]
        >  Lo script CreateInstanceStore.cmd tenta di creare il database nell'istanza predefinita di SQL Server 2008 Express.Se si desidera installare il database in un'istanza diversa, modificare lo script.  
  
2.  Aprire [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], caricare la soluzione SqlStoreExtensibility.sln ed eseguire la compilazione premendo CTRL\+MAIUSC\+B.  
  
    > [!WARNING]
    >  Se il database è stato installato in un'istanza non predefinita di SQL Server, aggiornare la stringa di connessione nel codice prima di compilare la soluzione.  
  
3.  Eseguire l'esempio con privilegi di amministratore passando alla directory bin del progetto \(\\WF\\Basic\\Persistence\\SqlStoreExtensibility\\bin\\Debug\) in [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)], facendo clic con il pulsante destro del mouse su SqlStoreExtensibility.exe e scegliendo **Esegui come amministratore**.  
  
### Per verificare che l'esempio funzioni correttamente  
  
1.  Utilizzare SQL Server Management Studio per visualizzare il contenuto della tabella dell'istanza selezionando **Database**, **InstanceStore** e quindi **System.ServiceModel.Activities.DurableInstancing.InstanceTable** in Esplora oggetti, fare clic con il pulsante destro del mouse  **su System.ServiceModel.Activities.DurableInstancing.InstanceTable** e scegliere **Seleziona le prime 1000 righe**.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] SQL Server Management Studio, vedere [Introduzione a SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkId=165645).  
  
2.  Osservare le istanze del flusso di lavoro elencate.  
  
3.  A un prompt dei comandi di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] eseguire lo script QueryInstanceStore.cmd che si trova nella directory di esempio \(\\WF\\Basic\\Persistence\\SqlStoreExtensibility\) .  
  
4.  Osservare il valore del contatore visualizzato sotto **CountStatus**.  
  
5.  Eseguire lo script alcune volte per vedere la modifica del valore di **CountStats**.  
  
6.  Premere INVIO per terminare l'applicazione flusso di lavoro.  
  
### Per disinstallare l'esempio  
  
1.  Rimuovere il database dell'archivio di istanze eseguendo lo script RemoveInstanceStore.cmd che si trova nella directory di esempio \(\\WF\\Basic\\Persistence\\SqlStoreExtensibility\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Persistence\SQLStoreExtensibility`  
  
## Vedere anche  
 [Persistenza del flusso di lavoro](../../../../docs/framework/windows-workflow-foundation//workflow-persistence.md)   
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)