---
title: "Processo di acquisto aziendale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Processo di acquisto aziendale
In questo esempio viene illustrato come creare un semplice processo di acquisto basato su richieste di proposte \(RDP\) con la selezione automatica della proposta migliore.  Vengono combinati gli oggetti <xref:System.Activities.Statements.Parallel>, <xref:System.Activities.Statements.ParallelForEach%601> e <xref:System.Activities.Statements.ForEach%601>, nonché un'attività personalizzata per creare un flusso di lavoro che rappresenta il processo.  
  
 In questo esempio è presente un'applicazione client [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] che consente l'interazione con il processo come partecipanti diversi, ovvero come il richiedente originale o un fornitore particolare.  
  
## Requisiti  
  
-   [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
-   [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
## Dimostrazione  
  
-   Attività personalizzate.  
  
-   Composizione di attività  
  
-   Segnalibri.  
  
-   Persistenza.  
  
-   Persistenza schematizzata.  
  
-   Traccia.  
  
-   Rilevamento.  
  
-   Hosting di [!INCLUDE[wf1](../../../../includes/wf1-md.md)] in client diversi \(applicazioni Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e applicazioni WinForms\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## Descrizione del processo  
 In questo esempio viene illustrata un'implementazione di un programma [!INCLUDE[wf](../../../../includes/wf-md.md)] per raccogliere le proposte dei fornitori per una società generica.  
  
1.  Un dipendente della società X crea una richiesta di proposta \(RDP\).  
  
    1.  Il dipendente digita il titolo e la descrizione della RDP.  
  
    2.  Il dipendente seleziona i fornitori a cui desidera richiedere di inviare proposte.  
  
2.  Il dipendente invia la proposta.  
  
    1.  Viene creata un'istanza del flusso di lavoro.  
  
    2.  Il flusso di lavoro attende che tutti i fornitori inviino le proposte.  
  
3.  Una volta ricevute tutte le proposte, il flusso di lavoro scorre tutte le proposte ricevute e seleziona la migliore.  
  
    1.  A ogni fornitore è assegnata una valutazione \(in questo esempio l'elenco di valutazioni viene archiviato in VendorRepository.cs\).  
  
    2.  Il valore totale della proposta è determinato da \(valore digitato dal fornitore\) \* \(valutazione registrata del fornitore\) \/ 100.  
  
4.  Il richiedente originale può vedere tutte le proposte inviate.  La proposta migliore viene presentata in una sezione speciale del rapporto.  
  
## Definizione del processo  
 Nella logica principale dell'esempio viene usata un'attività <xref:System.Activities.Statements.ParallelForEach%601> che attende le offerte di ogni fornitore \(tramite un'attività personalizzata che crea un segnalibro\) e registra la proposta del fornitore come RDP \(tramite un'attività <xref:System.Activities.Statements.InvokeMethod>\).  
  
 Nell'esempio vengono quindi scorse tutte le proposte ricevute archiviate in `RfpRepository` calcolando il valore regolato \(tramite un'attività <xref:System.Activities.Statements.Assign> e le attività <xref:System.Activities.Expressions>\) e se il valore regolato è più interessante rispetto alla migliore offerta precedente, il nuovo valore viene considerato l'offerta migliore \(tramite le attività <xref:System.Activities.Statements.If> e <xref:System.Activities.Statements.Assign>\).  
  
## Progetti di questo esempio  
 In questo esempio sono contenuti i progetti seguenti.  
  
|Project|Descrizione|  
|-------------|-----------------|  
|Common|Oggetti entità usati all'interno del processo \(Richiesta di proposta, Fornitore e Proposta del fornitore\).|  
|WfDefinition|Definizione del processo \(come programma [!INCLUDE[wf1](../../../../includes/wf1-md.md)]\) e dell'host \(`PurchaseProcessHost`\) usati dalle applicazioni client per la creazione e l'uso di istanze del flusso di lavoro del processo di acquisto.|  
|WebClient|Applicazione client [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] che consente agli utenti di creare e partecipare alle istanze del processo di acquisto.  Viene usato un host creato in modo personalizzato per interagire con il motore del flusso di lavoro.|  
|WinFormsClient|Applicazione client Windows Form che consente agli utenti di creare e partecipare alle istanze del processo di acquisto.  Viene usato un host creato in modo personalizzato per interagire con il motore del flusso di lavoro.|  
  
### WfDefinition  
 Nella tabella seguente è contenuta una descrizione dei file più importanti del progetto WfDefinition.  
  
|File|Descrizione|  
|----------|-----------------|  
|IPurchaseProcessHost.cs|Interfaccia per l'host del flusso di lavoro.|  
|PurchaseProcessHost.cs|Implementazione di un host per il flusso di lavoro.  L'host estrae i dettagli dell'esecuzione del flusso di lavoro e viene usato in tutte le applicazioni client per caricare, eseguire e interagire con le istanze del flusso di lavoro `PurchaseProcess`.|  
|PurchaseProcessWorkflow.cs|Attività che contiene la definizione del flusso di lavoro del processo di acquisto \(deriva dall'oggetto <xref:System.Activities.Activity>\).<br /><br /> Le attività che derivano dall'oggetto <xref:System.Activities.Activity> compongono la funzionalità assemblando le attività personalizzate esistenti e le attività della libreria di attività di [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  L'assemblaggio di queste attività è il modo più comunemente usato per creare la funzionalità personalizzata.|  
|WaitForVendorProposal.cs|Questa attività personalizzata deriva dall'oggetto <xref:System.Activities.NativeActivity> e crea un segnalibro denominato che deve essere ripreso in un secondo momento da un fornitore quando invia la proposta.<br /><br /> Le attività che derivano dalla classe <xref:System.Activities.NativeActivity>, come quelle che derivano dalla classe <xref:System.Activities.CodeActivity> creano la funzionalità imperativa eseguendo l'override del metodo <xref:System.Activities.NativeActivity.Execute%2A>, ma dispongono anche dell'accesso a tutta la funzionalità del runtime del flusso di lavoro tramite la classe <xref:System.Activities.ActivityContext> che viene passata al metodo `Execute`.  Questo contesto dispone del supporto per la pianificazione e l'annullamento di attività figlio, per l'impostazione di aree di non persistenza \(blocchi di esecuzione durante i quali il runtime non rende persistenti i dati del flusso di lavoro, ad esempio all'interno di transazioni atomiche\), nonché per gli oggetti <xref:System.Activities.Bookmark> \(handle per la ripresa di flussi di lavoro in pausa\).|  
|TrackingParticipant.cs|Oggetto <xref:System.Activities.Tracking.TrackingParticipant> che riceve tutti gli eventi di rilevamento e li salva in un file di testo.<br /><br /> I partecipanti del rilevamento vengono aggiunti all'istanza del flusso di lavoro come estensioni.|  
|XmlWorkflowInstanceStore.cs|Oggetto <xref:System.Runtime.DurableInstancing.InstanceStore> personalizzato che salva le applicazioni flusso di lavoro in file XML.|  
|XmlPersistenceParticipant.cs|Oggetto <xref:System.Activities.Persistence.PersistenceParticipant> personalizzato che salva un'istanza di richiesta di proposta in un file XML.|  
|AsyncResult.cs\/CompletedAsyncResult.cs|Classi di supporto per l'implementazione del modello asincrono nei componenti della persistenza.|  
  
### Common  
 Nella tabella seguente è contenuta una descrizione delle classi più importanti del progetto Common.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|Vendor|Fornitore che invia proposte in una richiesta di proposte.|  
|RequestForProposal|Una richiesta di proposte \(RDP\) è un invito rivolto ai fornitori affinché inviino proposte per una merce o un servizio specifico.|  
|VendorProposal|Proposta inviata da un fornitore a una RDP concreta.|  
|VendorRepository|Repository di fornitori.  Questa implementazione contiene una raccolta in memoria di istanze del fornitore e di metodi per esporre tali istanze.|  
|RfpRepository|Repository delle richieste di proposte.  Questa implementazione usa Linq to XML per eseguire una query sul file XML di richieste di proposte generato dalla persistenza schematizzata.  Questa classe implementa l'oggetto <xref:System.Runtime.Persistence.IDataViewMapper>.|  
|IOHelper|Questa classe gestisce tutti i problemi di I\/O \(cartelle, percorsi e così via\).|  
  
### Client Web  
 Nella tabella seguente è contenuta una descrizione delle pagine Web più importanti del progetto WebClient.  
  
|||  
|-|-|  
|File|Descrizione|  
|CreateRfp.aspx|Crea e invia una nuova richiesta di proposte.|  
|Default.aspx|Mostra tutte le richieste di proposte attive e completate.|  
|GetVendorProposal.aspx|Ottiene una proposta da un fornitore in una richiesta di proposte concreta.  Questa pagina viene usata solo dai fornitori.|  
|ShowRfp.aspx|Mostra tutte le informazioni relative a una richiesta di proposte \(proposte ricevute, date, valori e altre informazioni\).  Questa pagina viene usata solo dall'autore della richiesta di proposta.|  
  
### WinFormsClient  
 Nella tabella seguente è contenuta una descrizione dei form più importanti del progetto WinFormsClient.  
  
|||  
|-|-|  
|Form|Descrizione|  
|NewRfp|Crea e invia una nuova richiesta di proposte.|  
|ShowProposals|Mostra tutte le richieste di proposte attive e completate. **Note:**  Potrebbe essere necessario fare clic sul pulsante **Aggiorna** nell'interfaccia utente per vedere le modifiche in tale schermata dopo aver creato o modificato una richiesta di proposta.|  
|SubmitProposal|Ottiene una proposta da un fornitore in una richiesta di proposte concreta.  Questa finestra viene usata solo dai fornitori.|  
|ViewRfp|Mostra tutte le informazioni relative a una richiesta di proposte \(proposte ricevute, date, valori e altre informazioni\).  Questa finestra viene usata solo dall'autore della richiesta di proposte.|  
  
### File di persistenza  
 Nella tabella seguente vengono mostrati i file generati dal provider di persistenza \(`XmlPersistenceProvider`\) che si trovano nel percorso della cartella temporanea del sistema corrente \(tramite il metodo <xref:System.IO.Path.GetTempPath%2A>\).  Il file di traccia viene creato nel percorso di esecuzione corrente.  
  
||||  
|-|-|-|  
|Nome file|Descrizione|Path|  
|rfps.xml|File XML con tutte le richieste di proposte attive e completate.|<xref:System.IO.Path.GetTempPath%2A>|  
|\[instanceid\]|In questo file sono contenute tutte le informazioni su un'istanza del flusso di lavoro.<br /><br /> Questo file viene generato dall'implementazione della persistenza schematizzata \(PersistenceParticipant in XmlPersistenceProvider\).|<xref:System.IO.Path.GetTempPath%2A>|  
|\[instanceId\].tracking|File di testo con tutti gli eventi che si sono verificati all'interno di un'istanza concreta.<br /><br /> Questo file viene generato da TrackingParticipant.|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|File di traccia generato dal flusso di lavoro in base ai parametri di configurazione dei file App.config o Web.config.|Percorso di esecuzione corrente|  
  
#### Per usare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione PurchaseProcess.sln.  
  
2.  Per eseguire il progetto WebClient, aprire **Esplora soluzioni** e fare clic con il pulsante destro del mouse sul progetto **WebClient**.  Selezionare **Imposta come progetto di avvio**.  
  
3.  Per eseguire il progetto WinFormsClient, aprire **Esplora soluzioni** e fare clic con il pulsante destro del mouse sul progetto **WinFormsClient**.  Selezionare **Imposta come progetto di avvio**.  
  
4.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
5.  Per eseguire la soluzione, premere CTRL\+F5.  
  
### Opzioni del progetto WebClient  
  
-   **Crea nuova RDP**: crea una nuova richiesta di proposte \(RDP\) e avvia un flusso di lavoro del processo di acquisto.  
  
-   **Aggiorna**: aggiorna l'elenco di RDP attive e completate nella finestra principale.  
  
-   **Visualizza**: mostra il contenuto di una RDP esistente.  I fornitori possono inviare le proposte \(se invitati o se la RDP non è completata\).  
  
-   Visualizza come: l'utente può accedere alla RDP tramite diverse identità selezionando il partecipante desiderato nella casella combinata **Visualizza come** nella griglia di RDP attive.  
  
### Opzioni del progetto WinFormsClient  
  
-   **Crea RDP**: crea una nuova richiesta di proposte \(RDP\) e avvia un flusso di lavoro del processo di acquisto.  
  
-   **Aggiorna**: aggiorna l'elenco di RDP attive e completate nella finestra principale.  
  
-   **Visualizza RDP**: mostra il contenuto di una RDP esistente.  I fornitori possono inviare le proposte \(se invitati o se la RDP non è completata\)  
  
-   **Connetti come**: l'utente può accedere alla RDP tramite diverse identità selezionando il partecipante desiderato nella casella combinata **Visualizza come** nella griglia di RDP attive.  
  
## Vedere anche