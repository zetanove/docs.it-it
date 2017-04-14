---
title: "Processo di assunzione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5fcacbb-c884-4b37-a5d6-02b1b8eec7b4
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Processo di assunzione
In questo esempio viene illustrato come implementare un processo aziendale tramite attività di messaggistica e due flussi di lavoro ospitati come servizi di flusso di lavoroe appartenenti all'infrastruttura IT di una società fittizia denominata Contoso, Inc.  
  
 Il processo del flusso di lavoro `HiringRequest`, implementato come un oggetto <xref:System.Activities.Statements.Flowchart>, chiede l'autorizzazione a diversi responsabili nell'organizzazione.Per raggiungere questo obiettivo, nel flusso di lavoro vengono utilizzati altri servizi esistenti nell'organizzazione, in questo caso un servizio di posta in arrivo e un servizio dati organizzativo implementati come servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] normali.  
  
 Il flusso di lavoro `ResumeRequest`, implementato come un oggetto <xref:System.Activities.Statements.Sequence>, pubblica un elenco di offerte di lavoro nel sito Web esterno delle carriere di Contoso e gestisce l'acquisizione dei curriculum.Tale elenco è disponibile nel sito Web esterno per un periodo fisso di tempo, ovvero fino alla scadenza di un timeout, o fino a quando un dipendente di Contoso non decide di rimuoverlo.  
  
 In questo esempio vengono illustrate le funzionalità [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] seguenti:  
  
-   Flussi di lavoro <xref:System.Activities.Statements.Flowchart> e <xref:System.Activities.Statements.Sequence> per modellare processi aziendali  
  
-   Servizi di flusso di lavoro  
  
-   Attività di messaggistica  
  
-   Correlazione basata sul contenuto  
  
-   Attività personalizzate \(dichiarative e basate sul codice\)  
  
-   Persistenza di SQL Server fornita dal sistema  
  
-   Oggetto <xref:System.Activities.Persistence.PersistenceParticipant> personalizzato  
  
-   Rilevamento personalizzato  
  
-   Rilevamento ETW \(Event Tracking for Windows\)  
  
-   Composizione di attività  
  
-   Attività <xref:System.Activities.Statements.Parallel>  
  
-   Attività <xref:System.Activities.Statements.CancellationScope>  
  
-   Timer durevoli \(attività <xref:System.Activities.Statements.Delay>\)  
  
-   Transazioni  
  
-   Utilizzo di più di un flusso di lavoro nella stessa soluzione  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Application\HiringProcess`  
  
## Descrizione del processo  
 Contoso, Inc.desidera avere stretto controllo sul personale presente in ciascun reparto.Di conseguenza, tutte le volte che un dipendente desidera avviare un nuovo processo di assunzione deve passare attraverso un'approvazione del processo di richiesta di assunzione prima che la selezione possa effettivamente avere luogo.Tale processo è denominato richiesta del processo di assunzione \(definito nel progetto HiringRequestService\) ed è costituito dai passaggi seguenti.  
  
1.  Un dipendente \(il richiedente\) avvia la richiesta del processo di assunzione.  
  
2.  Il responsabile del richiedente deve approvare la richiesta:  
  
    1.  Il responsabile può rifiutare la richiesta.  
  
    2.  Il responsabile può restituire la richiesta al richiedente per ottenere informazioni aggiuntive.  
  
        1.  Il richiedente rivede la richiesta e la invia nuovamente al responsabile.  
  
    3.  Il responsabile può approvare la richiesta.  
  
3.  Dopo che il responsabile del richiedente ha concesso l'approvazione, la richiesta deve essere approvata dal responsabile del reparto:  
  
    1.  Il responsabile del reparto può rifiutare la richiesta.  
  
    2.  Il responsabile del reparto può approvare la richiesta.  
  
4.  Dopo che il responsabile del reparto ha concesso l'approvazione, è necessaria l'approvazione di 2 responsabili delle risorse umane o del CEO.  
  
    1.  Il processo può passare allo stato accettato o rifiutato.  
  
    2.  Se il processo viene accettato, verrà avviata una nuova istanza del flusso di lavoro `ResumeRequest` \(`ResumeRequest` è collegato a HiringRequest.csproj tramite un riferimento al servizio.\)  
  
 Dopo che i responsabili hanno approvato l'assunzione di un nuovo dipendente, il reparto risorse umane deve individuare il candidato adatto.Questo processo viene eseguito dal secondo flusso di lavoro \(`ResumeRequest`, definito in ResumeRequestService.csproj\).Tale flusso di lavoro definisce il processo per l'invio di un elenco di offerte di lavoro con un'opportunità di carriera al sito Web esterno delle carriere di Contoso, riceve i curriculum dei candidati ed esamina lo stato dell'elenco.Le posizioni sono disponibili per un periodo fisso di tempo, ovvero fino a una scadenza predeterminata, o fino a quando un dipendente di Contoso non decide di rimuoverle.Il flusso di lavoro `ResumeRequest` è costituito dai passaggi seguenti.  
  
1.  Un dipendente di Contoso inserisce le informazioni sulla posizione e una durata del timeout.Dopo che il dipendente ha inserito tali informazioni, la posizione viene pubblicata nel sito Web delle carriere.  
  
2.  Dopo la pubblicazione delle informazioni, le parti interessate possono inviare il curriculumche viene archiviato in un record collegato all'apertura della pratica.  
  
3.  I candidati possono inviare il proprio curriculum fino alla scadenza del timeout o fino a quando un appartenente al reparto risorse umane di Contoso non decide in modo esplicito di rimuovere l'elenco arrestando il processo.  
  
## Progetti presenti nell'esempio  
 Nella tabella seguente vengono illustrati i progetti presenti nella soluzione di esempio.  
  
|Progetto|Descrizione|  
|--------------|-----------------|  
|ContosoHR|Contiene contratti dati, oggetti business e classi del repository.|  
|HiringRequestService|Contiene la definizione del flusso di lavoro relativo al processo di richiesta di assunzione.<br /><br /> Il progetto viene implementato come un'applicazione console che ospita in modalità self\-hosting il flusso di lavoro \(file con estensione xaml\) come un servizio.|  
|ResumeRequestService|Servizio di flusso di lavoro che raccoglie i curriculum dei candidati fino alla scadenza di un timeout o fino a quando qualcuno non decide che il processo deve essere arrestato.<br /><br /> Il progetto viene implementato come un servizio di flusso di lavoro dichiarativo \(file con estensione xamlx\).|  
|OrgService|Servizio che espone informazioni organizzative \(dipendenti, posizioni, tipi di posizioni e reparti\).Questo servizio può essere paragonato al modulo di organizzazione dell'azienda di una pianificazione ERP \(Enterprise Resource Plan\).<br /><br /> Il progetto viene implementato come un'applicazione console che espone un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].|  
|InboxService|Casella di posta in arrivo che contiene attività in base alle quali i dipendenti intraprendono un'azione.<br /><br /> Il progetto viene implementato come un'applicazione console che espone un servizio WCF.|  
|InternalClient|Applicazione Web per l'interazione con il processo.Gli utenti possono avviare e visualizzare i propri flussi di lavoro HiringProcess nonché parteciparvi.Grazie a questa applicazione, possono inoltre avviare e monitorare i processi ResumeRequest.<br /><br /> Questo sito viene implementato in modo che sia interno alla rete Intranet di Contoso,mentre il progetto viene implementato come un sito Web ASP.NET.|  
|CareersWebSite|Sito Web esterno che espone le posizioni aperte in Contoso.Qualsiasi candidato potenziale può spostarsi in questo sito e inviare un curriculum.|  
  
## Riepilogo delle funzionalità  
 Nella tabella seguente vengono descritte le modalità di utilizzo di ogni funzionalità nell'esempio.  
  
|Funzionalità|Descrizione|Progetto|  
|------------------|-----------------|--------------|  
|Diagramma di flusso|Il processo aziendale viene rappresentato come un diagramma di flussola cui descrizione rappresenta il processo in modo analogo a quello in cui un'azienda l'avrebbe riportato su una lavagna.|HiringRequestService|  
|Servizi di flusso di lavoro|Il diagramma di flusso con la definizione del processo è ospitato in un servizio \(in questo esempio il servizio è ospitato in un'applicazione console\).|HiringRequestService|  
|Attività di messaggistica|Il diagramma di flusso utilizza le attività di messaggistica per gli scopi seguenti:<br /><br /> -   Recupero di informazioni dall'utente \(per ricevere le decisioni e le informazioni correlate in ogni passaggio del processo di approvazione\).<br />-   Interazione con gli altri servizi esistenti \(InboxService e OrgDataService, utilizzati tramite riferimenti al servizio\).|HiringRequestService|  
|Correlazione basata sul contenuto|I messaggi di approvazione sono correlati alla proprietà ID della richiesta di assunzione:<br /><br /> -   Quando un processo viene avviato, l'handle di correlazione viene inizializzato con l'ID della richiesta.<br />-   I messaggi di approvazione in ingresso sono correlati al relativo ID \(il primo parametro di ogni messaggio di approvazione è l'ID della richiesta\).|HiringRequestService \/ ResumeRequestService|  
|Attività personalizzate \(dichiarative e basate sul codice\)|Nell'esempio sono presenti diverse attività personalizzate:<br /><br /> -   `SaveActionTracking`. Questa attività genera un oggetto <xref:System.Activities.Tracking.TrackingRecord> personalizzato \(tramite <xref:System.Activities.NativeActivityContext.Track%2A>\).L'attività è stata creata utilizzando codice imperativo che estende <xref:System.Activities.NativeActivity>.<br />-   `GetEmployeesByPositionTypes`. Questa attività riceve un elenco di ID di tipi di posizione e restituisce un elenco di persone con tale posizione in Contoso.L'attività è stata creata in modo dichiarativo \(utilizzando la finestra di progettazione delle attività\).<br />-   `SaveHiringRequestInfo`. Questa attività salva le informazioni di un processo `HiringRequest` \(tramite `HiringRequestRepository.Save`\).L'attività è stata creata utilizzando codice imperativo che estende <xref:System.Activities.CodeActivity>.|HiringRequestService|  
|Persistenza di SQL Server fornita dal sistema|L'istanza di <xref:System.ServiceModel.Activities.WorkflowServiceHost> che ospita la definizione del processo del diagramma di flusso è configurata per utilizzare la persistenza di SQL Server fornita dal sistema.|HiringRequestService \/ ResumeRequestService|  
|Rilevamento personalizzato|Nell'esempio è incluso un partecipante del rilevamento personalizzato che salva la cronologia di un processo `HiringRequestProcess` \(quest'ultimo registra l'azione eseguita nonché l'autore e il momento dell'esecuzione\).Il codice sorgente si trova nella cartella Tracking di HiringRequestService.|HiringRequestService|  
|Rilevamento ETW|Il rilevamento ETW fornito dal sistema viene configurato nel file App.config nel servizio HiringRequestService.|HiringRequestService|  
|Composizione di attività|La definizione del processo utilizza la composizione libera di <xref:System.Activities.Activity>.Il diagramma di flusso contiene diverse attività Sequence e Parallel che a loro volta ne contengono altre e così via.|HiringRequestService|  
|Attività parallele|-   <xref:System.Activities.Statements.ParallelForEach%601> viene utilizzato per effettuare la registrazione in parallelo nella casella di posta in arrivo del CEO e dei responsabili delle risorse umane \(in attesa dell'approvazione dei due responsabili\).<br />-   <xref:System.Activities.Statements.Parallel> viene utilizzato per eseguire alcune attività di pulizia nei passaggi di completamento e rifiuto.|HiringRequestService|  
|Annullamento del modello|Nel diagramma di flusso viene utilizzato <xref:System.Activities.Statements.CancellationScope> per applicare l'annullamento \(in questo caso eseguendo attività di pulizia\).|HiringRequestService|  
|Partecipante di persistenza personalizzato|`HiringRequestPersistenceParticipant` salva i dati da una variabile del flusso di lavoro in una tabella archiviata nel database delle risorse umane di Contoso.|HiringRequestService|  
|Servizi di flusso di lavoro|`ResumeRequestService` viene implementato utilizzando servizi di flusso di lavoro.La definizione del flusso di lavoro e le informazioni sul servizio sono contenute nel file ResumeRequestService.xamlx.Il servizio è configurato per utilizzare la persistenza e il rilevamento.|ResumeRequestService|  
|Timer durevoli|In `ResumeRequestService` vengono utilizzati timer durevoli per definire la durata di un elenco di offerte di lavoro \(quando un timeout scade, le offerte vengono chiuse\).|ResumeRequestService|  
|Transazioni|<xref:System.Activities.Statements.TransactionScope> viene utilizzato per garantire la coerenza dei dati durante l'esecuzione di diverse attività \(quando viene ricevuto un nuovo curriculum\).|ResumeRequestService|  
|Transazioni|Il partecipante di persistenza \(`HiringRequestPersistenceParticipant`\) e il partecipante del rilevamento personalizzati \(`HistoryFileTrackingParticipant`\) utilizzano la stessa transazione.|HiringRequestService|  
|Utilizzo di [!INCLUDE[wf1](../../../../includes/wf1-md.md)] in applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].|L'accesso ai flussi di lavoro viene eseguito da due applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].|InternalClient \/ CareersWebSite|  
  
## Archivio dati  
 I dati vengono archiviati in un database di SQL Server denominato `ContosoHR` \(lo script per la creazione di questo database si trova nella cartella `DbSetup`\),mentre le istanze di flusso di lavoro vengono archiviate in un database di SQL Server denominato `InstanceStore` \(gli script per la creazione per l'archivio di istanze sono parte della distribuzione di [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)]\).  
  
 Entrambi i database vengono creati eseguendo lo script Setup.cmd da un prompt dei comandi di [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
## Esecuzione dell'esempio  
  
#### Per creare i database  
  
1.  Aprire un prompt dei comandi di [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
2.  Passare alla cartella dell'esempio.  
  
3.  Eseguire Setup.cmd.  
  
4.  Verificare che i due database `ContosoHR` e `InstanceStore` siano creati in SQL Express.  
  
#### Per configurare la soluzione per l'esecuzione  
  
1.  Eseguire [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] come amministratore.Aprire HiringRequest.sln.  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla soluzione, quindi scegliere **Proprietà**.  
  
3.  Selezionare l'opzione **Progetti di avvio multipli**, quindi impostare **CareersWebSite**, **InternalClient**, **HiringRequestService** e **ResumeRequestService** su **Start**.Lasciare **ContosoHR**, **InboxService** e **OrgService** su None.  
  
4.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,quindi verificare che la compilazione sia stata eseguita in modo corretto.  
  
#### Per eseguire la soluzione  
  
1.  Dopo che la soluzione è stata compilata, premere CTRL\+F5 per eseguirla senza debug.Verificare che tutti i servizi siano stati avviati.  
  
2.  Nella soluzione fare clic con il pulsante destro del mouse su **InternalClient**, quindi scegliere **Visualizza nel browser**.Verrà visualizzata la pagina predefinita per `InternalClient`.Verificare che i servizi siano in esecuzione, quindi fare clic sul collegamento.  
  
3.  Verrà visualizzato il modulo **HiringRequest**.È possibile seguire lo scenario descritto in questo punto.  
  
4.  Una volta che `HiringRequest` è completo, è possibile avviare `ResumeRequest`.È possibile seguire lo scenario descritto in questo punto.  
  
5.  Quando `ResumeRequest` viene pubblicato, sarà disponibile nel sito Web pubblico \(sito Web delle carriere di Contoso\).Per visualizzare l'elenco delle offerte di lavoro e candidarsi per la posizione, spostarsi su tale sito.  
  
6.  Nella soluzione fare clic con il pulsante destro del mouse su **CareersWebSite**, quindi scegliere **Visualizza nel browser**.  
  
7.  Nella soluzione fare clic con il pulsante destro del mouse su **InternalClient**, quindi scegliere **Visualizza nel browser** per spostarsi di nuovo in `InternalClient`.  
  
8.  Andare alla sezione **JobPostings** facendo clic sul collegamento relativo all'elenco di offerte di lavoro nel menu superiore della casella di posta in arrivo.È possibile seguire lo scenario descritto in questo punto.  
  
## Scenari  
  
### Richiesta di assunzione  
  
1.  Michael Alexander \(programmatore\) desidera richiedere una nuova posizione per assumere un esperto in testing \(SDET\) nel reparto tecnico con almeno tre anni di esperienza nel linguaggio di programmazione C\#.  
  
2.  Dopo la creazione, la richiesta viene visualizzata nella casella di posta in arrivo di Michael \(fare clic su **Aggiorna** se non viene visualizzata\) in attesa dell'approvazione di Peter Brehm, responsabile di Michael.  
  
3.  Peter desidera intervenire sulla richiesta di Michaelpoiché ritiene che la posizione richieda 5 anni di esperienza nel linguaggio C\# anziché 3 e pertanto invia i propri commenti per la revisione.  
  
4.  Michael riceve un messaggio nella casella di posta in arrivo proveniente dal responsabilee dopo aver esaminato la cronologia della richiesta di posizione concorda con Peter.Michael modifica pertanto la descrizione per richiedere 5 anni di esperienza nel linguaggio C\# e accetta la modifica.  
  
5.  Peter interviene sulla richiesta modificata di Michael e l'accetta.A questo punto la richiesta deve essere approvata dal direttore del reparto tecnico, Tsvi Reiter.  
  
6.  Tsvi Reiter desidera accelerare la richiesta, pertanto inserisce un commento per indicare che la richiesta è urgente e l'accetta.  
  
7.  La richiesta deve ora essere approvata da due responsabili delle risorse umane o dal CEO.Quest'ultimo, Brian Richard Goldstein, vede la richiesta urgente di Tsvie interviene accettandola, precedendo l'approvazione dei due responsabili delle risorse umane.  
  
8.  La richiesta viene rimossa dalla casella di posta in arrivo di Michael e il processo di assunzione di un esperto SDET è stato avviato.  
  
### Avviare la richiesta di curriculum  
  
1.  A questo punto la posizione lavorativa è in attesa di essere pubblicata in un sito Web esterno a cui le persone possono inviare i curriculum \(per visualizzarlo, fare clic sul collegamento relativo all'elenco di offerte di lavoro.Attualmente, la posizione lavorativa deve essere completata da un addetto delle risorse umane responsabile della finalizzazione e della pubblicazione della posizione.  
  
2.  Il reparto risorse umane desidera modificare la posizione lavorativa \(tramite il collegamento per la modifica\) impostando un timeout di 60 minuti \(in uno scenario reale questo valore potrebbe essere rappresentato da giorni o settimane\).Il timeout consente che la posizione lavorativa venga eliminata dal sito Web esterno dopo il tempo specificato.  
  
3.  Dopo che è stata modificata e salvata, la posizione lavorativa viene visualizzata nella scheda relativa alla ricezione dei curriculum \(aggiornare la pagina Web per visualizzarla\).  
  
### Raccolta di curriculum  
  
1.  La posizione lavorativa dovrebbe essere visualizzata sul sito Web esterno.Una persona interessata può pertanto candidarsi per la posizione e inviare il proprio curriculum.  
  
2.  Se si torna al servizio relativo all'elenco di offerte di lavoro, è possibile visualizzare i curriculum raccolti fino al momento attuale.  
  
3.  Il reparto risorse umane può decidere di interrompere la raccolta, ad esempio se il candidato appropriato è stato identificato.  
  
## Risoluzione dei problemi  
  
1.  Accertarsi di eseguire [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] con privilegi di amministratore.  
  
2.  Se non è possibile compilare la soluzione, verificare l'elemento seguente:  
  
    -   Nel riferimento a `ContosoHR` non deve mancare il progetto `InternalClient` o `CareersWebSite`.  
  
3.  Se non è possibile eseguire la soluzione, verificare gli elementi seguenti:  
  
    1.  Tutti i servizi sono in esecuzione.  
  
    2.  I riferimenti al servizio sono aggiornati.  
  
        1.  Aprire la cartella App\_WebReferences.  
  
        2.  Fare clic con il pulsante destro del mouse su **Contoso**, quindi scegliere **Aggiorna riferimenti Web\/al servizio**.  
  
        3.  Premere CTRL\+MAIUSC\+B per ricompilare la soluzione in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
## Disinstallazione  
  
1.  Eliminare l'archivio dell'istanza di SQL Server eseguendo Cleanup.bat, disponibile nella cartella DbSetup.  
  
2.  Eliminare il codice sorgente dal disco rigido.  
  
## Vedere anche