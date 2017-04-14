---
title: "Specifiche delle funzionalit&#224; di Windows Workflow Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Specifiche delle funzionalit&#224; di Windows Workflow Foundation
[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] aggiunge una serie di funzionalità a Windows Workflow Foundation.Questo documento descrive alcune delle nuove funzionalità e fornisce informazioni dettagliate sugli scenari nei quali potrebbero essere utili.  
  
## Attività di messaggistica  
 Le attività di messaggistica \(<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.ReceiveReply>\) vengono utilizzate per inviare e ricevere i messaggi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] dal flusso di lavoro. Le attività <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> vengono utilizzate per formare un'operazione del servizio [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] esposta tramite WSDL esattamente come i servizi Web standard di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> consentono di utilizzare un servizio Web simile a un <xref:System.ServiceModel.ChannelFactory> di WCF; anche per Workflow Foundation esiste un'esperienza **Aggiungi riferimento al servizio** che genera attività preconfigurate.  
  
### Introduzione alle attività di messaggistica  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un progetto Applicazione di servizi flusso di lavoro WCF.Nel canvas verrà posizionata la coppia <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply>.  
  
-   Fare clic con il pulsante destro del mouse sul progetto e selezionare **Aggiungi riferimento al servizio**. Scegliere un servizio Web WSDL esistente e fare clic su **OK**. Compilare il progetto per mostrare le attività generate \(implementate utilizzando <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply>\) nella casella degli strumenti.  
  
-   Esempi di queste attività sono disponibili nelle sezioni seguenti:  
  
    -   Esempi di base: [Servizi](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Scenari: [Services](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
-   [Documentazione concettuale](http://go.microsoft.com/fwlink/?LinkId=204801)  
  
-   [Documentazione della finestra di progettazione per le attività di messaggistica](http://go.microsoft.com/fwlink/?LinkId=204802)  
  
### Scenario di esempio relativo alle attività di messaggistica  
 Un servizio `BestPriceFinder` chiama più servizi di compagnie aeree per trovare il prezzo migliore del biglietto per una determinata destinazione. Per l'implementazione di questo scenario sarebbe necessario utilizzare le attività di messaggistica per ricevere la richiesta di prezzo, recuperare i prezzi dai servizi di back\-end e rispondere alla richiesta di prezzo con il prezzo migliore. Sarebbe inoltre necessario utilizzare altre attività predefinite per la creazione della logica di business per calcolare il prezzo migliore.  
  
## WorkflowServiceHost  
 <xref:System.ServiceModel.WorkflowServiceHost> è l'host del flusso di lavoro predefinito che supporta più istanze, la configurazione e la messaggistica di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], anche se per ospitare i flussi di lavoro non è necessario utilizzare la messaggistica. Inoltre si integra con la persistenza, il rilevamento e il controllo dell'istanza tramite un set di comportamenti del servizio. Analogamente a <xref:System.ServiceModel.ServiceHost> di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], <xref:System.ServiceModel.WorkflowServiceHost> può essere un servizio indipendente ospitato in una applicazione console\/WinForms\/WPF o in un servizio Windows oppure un servizio ospitato su Web \(come un file .xamlx\) in IIS o WAS.  
  
### Guida introduttiva all'host del servizio del flusso di lavoro  
  
-   In Visual Studio 2010, creare un progetto Applicazione di servizi flusso di lavoro di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Questo progetto verrà configurato per utilizzare <xref:System.ServiceModel.WorkflowServiceHost> in un ambiente ospitato su Web.  
  
-   Per ospitare un flusso di lavoro non di messaggistica, aggiungere un <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> personalizzato che creerà l'istanza basata su un messaggio.  
  
-   Le istanze del flusso di lavoro possono essere controllate \(ad esempiosospese o chiuse\) aggiungendo <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> a <xref:System.ServiceModel.WorkflowServiceHost> quindi utilizzando <xref:System.ServiceModel.Activities.WorkflowControlClient>.  
  
-   Esempi di <xref:System.ServiceModel.WorkflowServiceHost> sono disponibili nelle sezioni seguenti:  
  
    -   [Esecuzione](../../../docs/framework/windows-workflow-foundation/samples/execution.md)  
  
    -   Informazioni di base: [Services](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Scenari: [Services](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Applicazione: [Gestione dell'istanza sospesa](../../../docs/framework/windows-workflow-foundation/samples/suspended-instance-management.md)  
  
-   [Documentazione concettuale su WorkflowServiceHost](http://go.microsoft.com/fwlink/?LinkId=204807)  
  
### Scenario relativo a WorkflowServiceHost  
 Un servizio BestPriceFinder chiama più servizi di compagnie aeree per trovare il prezzo migliore del biglietto per una determinata destinazione. Per l'implementazione di questo scenario sarebbe necessario ospitare il flusso di lavoro in <xref:System.ServiceModel.WorkflowServiceHost>. Sarebbe inoltre necessario utilizzare le attività di messaggistica per ricevere la richiesta di prezzo, recuperare i prezzi dai servizi di back\-end e rispondere alla richiesta di prezzo con il prezzo migliore.  
  
## Correlazione  
 Una correlazione è una delle modalità seguenti:  
  
-   Una modalità di raggruppamento dei messaggi, ovvero la relazione tra un messaggio di richiesta e la sua risposta.  
  
-   Una modalità di mapping di un dato a un'istanza del servizio.  
  
### Introduzione  
  
-   Per iniziare a utilizzare la correlazione, creare un nuovo progetto in Visual Studio.Creare una variabile di tipo <xref:System.ServiceModel.Activities.CorrelationHandle>.  
  
-   Un esempio di correlazione utilizzata per raggruppare i messaggi è una correlazione Request\-Reply che raggruppa i messaggi.  
  
    -   In un'attività <xref:System.ServiceModel.Activities.Receive>, fare clic sulla proprietà <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> e aggiungere un <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> utilizzando il CorrelationHandle creato in precedenza nel primo passaggio.  
  
    -   Creare un'attività <xref:System.ServiceModel.Activities.SendReply> facendo clic con il pulsante destro del mouse su <xref:System.ServiceModel.Activities.Receive> e selezionando "Crea SendReply".Incollarla nel flusso di lavoro dopo l'attività <xref:System.ServiceModel.Activities.Receive>.  
  
-   Un esempio di mapping di un dato a un'istanza del servizio è una correlazione basata sul contenuto che associa un dato \(ad esempio un ID ordine\) a una determinata istanza del flusso di lavoro.  
  
    -   In un'attività di messaggistica qualsiasi, fare clic sulla proprietà `CorrelationInitializers` e aggiungere un <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> utilizzando la variabile <xref:System.ServiceModel.Activities.CorrelationHandle> creata in precedenza.Fare doppio clic sulla proprietà desiderata sul messaggio \(ad esempioOrderID\) dal menu a discesa.Impostare la proprietà `CorrelatesWith` sulla variabile <xref:System.ServiceModel.Activities.CorrelationHandle> utilizzata in precedenza.  
  
-   Esempi:  
  
    -   Esempi di base: [Services](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   Scenari: [Services](../../../docs/framework/windows-workflow-foundation/samples/services.md)  
  
    -   [Documentazione concettuale sulla correlazione](http://go.microsoft.com/fwlink/?LinkId=204939)  
  
### Scenario relativo alla correlazione  
 Un flusso di lavoro di elaborazione ordini viene utilizzato per gestire la creazione di un nuovo ordine e l'aggiornamento degli ordini esistenti in corso di elaborazione. Per l'implementazione di questo scenario sarebbe necessario ospitare il flusso di lavoro in <xref:System.ServiceModel.WorkflowServiceHost> e utilizzare le attività di messaggistica. Sarebbe inoltre necessaria la correlazione basata su `orderId` per garantire che gli aggiornamenti vengano eseguiti nel flusso di lavoro corretto.  
  
## Configurazione semplificata  
 Lo schema di configurazione di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è complesso e fornisce agli utenti molte funzionalità difficilmente reperibili.In [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], l'obiettivo è aiutare gli utenti di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] a configurare i servizi con le funzionalità seguenti:  
  
-   Eliminare la necessità della configurazione esplicita di ogni singolo servizio.Se non viene configurato nessun elemento \<service\> del servizio e il servizio non definisce a livello di codice nessun endpoint, viene aggiunto automaticamente al servizio un set di endpoint, uno per ogni indirizzo di base del servizio e per ogni contratto implementato dal servizio.  
  
-   Consentire all'utente di definire valori predefiniti per le associazioni e i comportamenti di WCF che verranno applicati ai servizi senza configurazione esplicita.  
  
-   Gli endpoint standard definiscono endpoint preconfigurati riutilizzabili, che dispongono di valori fissi per una o più delle proprietà dell'endpoint \(indirizzo, associazione e contratto\) e consentono la definizione di proprietà personalizzate.  
  
-   Infine, <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> consente all'utente la gestione centralizzata della configurazione del client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], utile in scenari nei quali la configurazione viene selezionata o modificata dopo la fase di caricamento del dominio dell'applicazione.  
  
### Introduzione  
  
-   [Guida per gli sviluppatori di WCF 4.0](http://go.microsoft.com/fwlink/?LinkId=204940)  
  
-   [Configurazione di una channel factory](http://go.microsoft.com/fwlink/?LinkId=204941)  
  
-   [Elemento endpoint standard](http://go.microsoft.com/fwlink/?LinkId=204942)  
  
-   [Miglioramenti della configurazione dei servizi in .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=204943)  
  
-   [Errore comune dell'utente in .NET 4: errata digitazione del nome della configurazione di un servizio WF\/WCF](http://go.microsoft.com/fwlink/?LinkId=204944)  
  
### Scenari di configurazione semplificati  
  
-   Un sviluppatore ASMX esperto desidera cominciare a utilizzare [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].Tuttavia, [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] sembra essere molto complicato.In particolare per tutte le informazioni da scrivere in un file di configurazione.In .NET 4, è anche possibile decidere di non avere un file di configurazione.  
  
-   È molto difficile configurare e gestire un set di servizi WCF già esistente.Il file di configurazione è composto da migliaia di righe di codice XML ed è molto pericoloso modificarle.È necessario aiutare gli utenti a ridurre la quantità di codice per renderlo più maneggevole.  
  
## Resolver del contratto dati  
 In .NET 3.5, esistevano alcune limitazioni nella progettazione di tipi noti:  
  
-   Non era possibile aggiungere in modo dinamico tipi noti durante la serializzazione o la deserializzazione.  
  
-   I serializzatori non erano in grado di gestire le informazioni sconosciute su xsi:type.  
  
-   Gli utenti non potevano specificare quale xsi:type visualizzare sulla rete per ridurre, ad esempio, le dimensioni di un'istanza di serializzazione.  
  
 Il [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md) risolve questi problemi in .NET 4.5.  
  
### Introduzione  
  
-   [Documentazione sull'API del resolver del contratto dati](http://go.microsoft.com/fwlink/?LinkId=204946)  
  
-   [Introduzione al resolver del contratto dati](http://go.microsoft.com/fwlink/?LinkId=204947)  
  
-   Esempi:  
  
    -   [DataContractResolver](../../../docs/framework/wcf/samples/datacontractresolver.md)  
  
    -   [KnownAssemblyAttribute](../../../docs/framework/wcf/samples/knownassemblyattribute.md)  
  
### Scenari relativi al resolver del contratto dati  
  
-   Evitare di dichiarare decine di oggetti <xref:System.Runtime.Serialization.KnownTypeAttribute> in un servizio.  
  
-   Ridurre la dimensione del blob XML.  
  
## Diagramma di flusso  
 Il diagramma di flusso è uno noto paradigma per rappresentare visivamente i problemi di un dominio.In .NET 4 è stato introdotto un nuovo stile del flusso di controllo.Una delle caratteristiche principali del diagramma di flusso è quella di eseguire solo un'attività alla volta.I diagrammi di flusso possono rappresentare cicli e risultati alternativi, ma non possono rappresentare a livello nativo l'esecuzione simultanea di più nodi.  
  
### Introduzione  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un'applicazione console flusso di lavoro.Aggiungere un diagramma di flusso nella finestra di progettazione.  
  
-   La funzionalità diagramma di flusso utilizza le classi seguenti:  
  
    -   <xref:System.Activities.Statements.Flowchart>  
  
    -   <xref:System.Activities.Statements.FlowNode>  
  
    -   <xref:System.Activities.Statements.FlowDecision>  
  
    -   <xref:System.Activities.Statements.FlowStep>  
  
    -   <xref:System.Activities.Statements.FlowSwitch%601>  
  
-   Esempi:  
  
    -   [Gestione errori in un'attività Flowchart utilizzando TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    -   [Scenario StateMachine utilizzando una combinazione attività FlowChart e Pick](../../../docs/framework/windows-workflow-foundation/samples/statemachine-scenario-using-a-combination-of-flowchart-and-pick.md)  
  
    -   [Processo di assunzione](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
-   Documentazione della finestra di progettazione:  
  
    -   [ActivityDesigner Diagramma di flusso](../Topic/Flowchart%20Activity%20Designers.md)  
  
### Scenari relativi al diagramma di flusso  
 Un'attività del diagramma di flusso può essere utilizzata per implementare un gioco per indovinare un numero.Il gioco è molto semplice: il computer seleziona un numero casuale e il giocatore deve indovinare il numero.Ogni volta che il giocatore invia un'ipotesi, il computer mostra un suggerimento, ad esempio,"prova con un numero inferiore"\).Se il giocatore indovina il numero in meno di 7 tentativi, viene visualizzato un messaggio di congratulazioni speciali.È possibile implementare questo gioco con una combinazione delle attività procedurali seguenti:  
  
-   <xref:System.Activities.Statements.Sequence>  
  
-   <xref:System.Activities.Statements.While>  
  
-   <xref:System.Activities.Statements.Switch%601>  
  
-   <xref:System.Activities.Statements.TryCatch>  
  
-   <xref:System.Activities.Statements.Assign%601>  
  
-   <xref:System.Activities.Statements.If>  
  
## Attività procedurali \(Sequence, If, ForEach, Switch, Assign, DoWhile, While\)  
 Le attività procedurali forniscono un meccanismo per modellare il flusso di controllo sequenziale utilizzando concetti noti ai programmatori.Queste attività abilitano i costrutti del linguaggio di programmazione strutturati in modo tradizionale e, se opportuno, forniscono la parità di linguaggio con linguaggi procedurali comuni, ad esempio C\#\/VB.  
  
### Introduzione  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un'applicazione console flusso di lavoro.Aggiungere le attività procedurali nella finestra di progettazione del flusso di lavoro.  
  
-   Esempi:  
  
    -   [Processo di assunzione](../../../docs/framework/windows-workflow-foundation/samples/hiring-process.md)  
  
    -   [Processo di acquisto aziendale](../../../docs/framework/windows-workflow-foundation/samples/corporate-purchase-process.md)  
  
-   Documentazione della finestra di progettazione:  
  
    -   [ActivityDesigner Parallel](../Topic/Parallel%20Activity%20Designer.md)  
  
    -   [ActivityDesigner ParallelForEach\<T\>](../Topic/ParallelForEach%3CT%3E%20Activity%20Designer.md)  
  
### Scenari relativi alle attività procedurali  
  
-   <xref:System.Activities.Statements.Parallel>Parallelo: un sistema di gestione documenti in una rete Intranet dispone di un flusso di lavoro di approvazione dei documenti.Prima di poter essere pubblicati nella rete Intranet, i documenti devono essere approvati dai responsabili dei diversi reparti.Non esiste un ordine prestabilito per le approvazioni; quando un documento si trova nella fase "in attesa di approvazione", può essere approvato in un qualsiasi momento.Quando un utente manda in revisione un documento, deve essere approvato dal suo responsabile diretto, dall'amministratore della rete Intranet e dal responsabile delle comunicazioni interne.  
  
-   <xref:System.Activities.Statements.ParallelForEach%601>: Un'applicazione WF gestisce gli acquisti di una grande società.In base a quanto definito nei regolamenti aziendali, prima di pianificare qualsiasi operazione di acquisto è necessario valutare tre fornitori diversi.Un dipendente dell'ufficio acquisti seleziona tre fornitori dall'elenco fornitori della società.Una volta selezionati e informati i fornitori, la società attenderà le proposte economiche.Le proposte possono pervenire in qualsiasi ordine.Per implementare questo scenario in WF, viene utilizzato <xref:System.Activities.Statements.ParallelForEach%601> per scorrere l'elenco dei fornitori e richiedere le proposte economiche.Una volta raccolte tutte le offerte, viene scelta e visualizzata la migliore.  
  
## InvokeMethod  
 L'attività <xref:System.Activities.Statements.InvokeMethod> consente di richiamare metodi pubblici in oggetti o tipi nell'ambito.Supporta il richiamo di metodi di istanza e statici con o senza parametri \(incluse le matrici di parametri\) e metodi generici.Consente inoltre l'esecuzione del metodo in modo sincrono e asincrono.  
  
### Introduzione  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un'applicazione console flusso di lavoro.Aggiungere un'attività <xref:System.Activities.Statements.InvokeMethod> nella finestra di progettazione del flusso di lavoro e configurare i metodi di istanza e statici.  
  
-   Esempi:  
  
    -   [InvokeMethod](../../../docs/framework/windows-workflow-foundation/samples/invokemethod.md)  
  
-   Documentazione della finestra di progettazione: [ActivityDesigner InvokeMethod](../Topic/InvokeMethod%20Activity%20Designer.md)  
  
### Scenari relativi a InvokeMethod  
  
-   È necessario richiamare un metodo in un oggetto nell'ambito.Ad esempio, è necessario aggiungere un valore a un dizionario.Viene richiamato il metodo Add dell'istanza del dizionario e vengono forniti la chiave e il valore.  
  
-   È necessario richiamare un metodo su un oggetto CLR legacy.Anziché creare un'attività personalizzata per eseguire il wrapping della chiamata a quella classe legacy, è possibile utilizzare <xref:System.Activities.Statements.InvokeMethod>, se rientra nell'ambito durante l'esecuzione del flusso di lavoro.  
  
## Attività di gestione degli errori  
 L'attività <xref:System.Activities.Statements.TryCatch> fornisce un meccanismo per il rilevamento delle eccezioni che si verificano durante l'esecuzione di un set di attività contenute \(simile al costrutto Try\/Catch in C\#\/VB\).<xref:System.Activities.Statements.TryCatch> fornisce la gestione delle eccezioni a livello di flusso di lavoro.Quando viene generata un'eccezione non gestita, il flusso di lavoro viene interrotto e non viene eseguito il blocco Finally.Questo comportamento è coerente con C\#.  
  
### Introduzione  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un'applicazione console flusso di lavoro.Aggiungere un'attività <xref:System.Activities.Statements.TryCatch> nella finestra di progettazione del flusso di lavoro.  
  
-   Esempi:  
  
    1.  [Gestione errori in un'attività Flowchart utilizzando TryCatch](../../../docs/framework/windows-workflow-foundation/samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)  
  
    2.  [Utilizzo di attività procedurali](../../../docs/framework/windows-workflow-foundation/samples/using-procedural-activities.md)  
  
-   Documentazione della finestra di progettazione: [ActivityDesigner Gestione errori](../Topic/Error%20Handling%20Activity%20Designers.md)  
  
### Scenari relativi alla gestione degli errori  
 È necessario eseguire un set di attività e, quando si verifica un errore, è necessario eseguire una logica specifica.Se durante l'esecuzione della logica di gestione degli errori si scopre che l'errore non è risolvibile, viene rigenerata l'eccezione e il problema viene gestito dall'attività padre \(o dall'host\).  
  
## Attività Pick  
 L'attività <xref:System.Activities.Statements.Pick> fornisce il modello di flusso di controllo basato sugli eventi in WF.L'attività <xref:System.Activities.Statements.Pick> contiene molti branch, la cui esecuzione è condizionata dal verificarsi di un particolare evento.In questa impostazione, <xref:System.Activities.Statements.Pick> si comporta in modo analogo a <xref:System.Activities.Statements.Switch%601>, ovvero l'attività esegue solo uno dei set di eventi in ascolto.Ogni ramo è basato sugli eventi e l'evento che si verifica per primo determina l'esecuzione del ramo corrispondente.Tutti gli altri rami vengono annullati e interrompono l'ascolto di altri eventi.  
  
### Introduzione  
  
-   In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un'applicazione console flusso di lavoro.Aggiungere un'attività <xref:System.Activities.Statements.Pick> nella finestra di progettazione del flusso di lavoro.  
  
-   Esempio: [Utilizzo dell'attività Pick](../../../docs/framework/windows-workflow-foundation/samples/using-the-pick-activity.md)  
  
-   Documentazione della finestra di progettazione: [ActivityDesigner Pick](../Topic/Pick%20Activity%20Designer.md)  
  
### Scenario relativo all'attività Pick  
 È necessario richiedere l'input di un utente.In circostanze normali, lo sviluppatore utilizzerebbe una chiamata al metodo come <xref:System.Console.ReadLine%2A> per richiedere l'input di un utente.Il problema di questa impostazione è che il programma attende fino a quando l'utente non immette un valore.In questo scenario, è necessario un timeout per sbloccare un'attività di blocco.Un scenario comune è quello in cui è necessario completare un'attività entro un periodo di tempo specificato.Il timeout di un'attività di blocco è uno scenario in cui l'attività Pick rappresenta un valore aggiunto.  
  
## Servizio di routing di WCF  
 Il servizio di routing è progettato per essere un router software generico che consente di controllare il flusso dei messaggi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] tra client e servizi. Il servizio di routing consente di separare i client dai servizi e di conseguenza offre una maggiore libertà in termini di configurazioni supportate e una maggiore flessibilità in termini di hosting dei servizi. In .NET 3.5, i client e i servizi erano strettamente collegati; un client doveva conoscere tutti i servizi con cui doveva comunicare e la loro posizione.WCF in .NET Framework 3.5 aveva inoltre le limitazioni seguenti:  
  
-   La gestione degli errori era complessa, in quanto la logica doveva essere impostata come hardcoded nel client.  
  
-   I client e i servizi dovevano utilizzare sempre le stesse associazioni.  
  
-   I servizi venivano adeguatamente diversificati molto raramente: è più facile far comunicare il client con un servizio che implementa tutto piuttosto che dover scegliere tra più servizi.  
  
 Il servizio di routing in .NET 4 è progettato per semplificare la risoluzione di questi problemi.Il nuovo servizio di routing offre le funzionalità seguenti:  
  
1.  Routing basato sul contenuto \(gli oggetti<xref:System.ServiceModel.Dispatcher.MessageFilter> esaminano un messaggio per stabilire dove deve essere inviato\).  
  
2.  Bridging del protocollo \(trasporto & messaggio\)  
  
3.  Gestione degli errori \(il router intercetta le eccezioni di comunicazione ed esegue il failover sugli endpoint di backup\)  
  
4.  Aggiornamento dinamico \(in memoria\) di <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> e configurazione del routing.  
  
### Introduzione  
  
1.  Documentazione: [Routing](../../../docs/framework/wcf/feature-details/routing.md)  
  
2.  Esempi: [Servizi di routing &#91;esempi WCF&#93;](../../../docs/framework/wcf/samples/routing-services.md)  
  
3.  Blog: [Le regole del routing](http://go.microsoft.com/fwlink/?LinkId=204956)  
  
### Scenari di routing  
 Il servizio di routing è utile negli scenari seguenti:  
  
-   I client possono comunicare con più servizi senza doverli indirizzare tutti direttamente.  
  
-   I client possono eseguire una logica aggiuntiva su una richiesta del client per determinare dove indirizzarlo.  
  
-   È possibile decomporre le operazioni eseguite da un client in più implementazioni del servizio senza eseguire il refactoring del client.  
  
-   I client e i servizi possono supportare associazioni diverse con impostazioni di sicurezza diverse.  
  
-   È possibile rendere i client più affidabili in caso di guasto o indisponibilità dei servizi.  
  
## WCF Discovery  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] Discovery è una tecnologia del framework che consente di integrare un meccanismo di individuazione nell'infrastruttura dell'applicazione.È possibile utilizzarlo per rendere individuabile il servizio e configura i client per la ricerca dei servizi.Non è più necessario impostare i clienti come hardcoded con gli endpoint, pertanto l'applicazione è più affidabile e garantisce una maggiore tolleranza agli errori.Discovery è la piattaforma ideale per integrare funzionalità di configurazione automatica nell'applicazione.  
  
 Il prodotto si basa sullo standard WS\-Discoveryed è progettato per essere interoperativo, estendibile e generico.Il prodotto supporta due modalità di funzionamento:  
  
1.  Gestito: se sulla rete esiste un'entità informata sui servizi esistenti, i client eseguono direttamente una query per ottenere le informazioni.È analogo ad Active Directory.  
  
2.  Ad hoc: in questa modalità i client utilizzano messaggi multicast per individuare i servizi.  
  
 Inoltre, i messaggi di individuazione non riconoscono il protocollo di rete; è possibile utilizzarli in aggiunta a qualsiasi protocollo che supporta i requisiti della modalità.Ad esempio, è possibile inviare messaggi multicast di individuazione sul canale UDP o su qualsiasi altra rete che supporta la messaggistica multicast. Grazie a questi punti di progettazione e alla flessibilità della funzionalità, è possibili adattare l'individuazione in modo specifico alla soluzione.  
  
### Introduzione  
  
-   Documentazione: [WCF Discovery](../../../docs/framework/wcf/feature-details/wcf-discovery.md)  
  
-   Esempi: [Individuazione \(esempi\)](../../../docs/framework/wcf/samples/discovery-samples.md)  
  
### Scenari relativi all'individuazione  
 Un sviluppatore non desidera impostare gli endpoint come hardcoded, in quanto non è possibile sapere quando sarà disponibile il servizio.Al contrario, lo sviluppatore desidera scegliere un servizio in fase di runtime.I componenti dell'applicazione devono essere più separabili, più affidabili e autoconfigurabili.  
  
## Rilevamento  
 Il rilevamento del flusso di lavoro consente di analizzare in dettaglio l'esecuzione di un'istanza del flusso di lavoro. Gli eventi di rilevamento vengono generati da un flusso di lavoro a livello dell'istanza del flusso di lavoro e durante l'esecuzione delle attività nel flusso di lavoro.Per sottoscrivere i record di rilevamento, è necessario aggiungere all'host del flusso di lavoro un partecipante del rilevamento del flusso di lavoro.I record di rilevamento vengono filtrati utilizzando un profilo di rilevamento..NET Framework fornisce un partecipante del rilevamento ETW \(Event Tracing for Windows\) e nel file machine.config. viene installato un profilo di base.  
  
### Introduzione  
  
1.  In [!INCLUDE[vs2010](../../../includes/vs2010-md.md)], creare un progetto Applicazione di servizi flusso di lavoro WCF.Inizialmente, nel canvas verrà posizionata la coppia <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply>.  
  
2.  Aprire web.config e aggiungere un comportamento di rilevamento ETW senza profilo.  
  
    1.  Viene utilizzato il profilo predefinito.  
  
    2.  Aprire il visualizzatore eventi e attivare il canale analitico nel nodo seguente: **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Attiva registro**.  
  
    3.  Eseguire il servizio del flusso di lavoro.  
  
    4.  Osservare gli eventi di rilevamento del flusso di lavoro nel visualizzatore eventi.  
  
3.  Esempi: [Rilevamento](../../../docs/framework/windows-workflow-foundation/samples/tracking.md)  
  
4.  Documentazione concettuale: [Rilevamento e traccia del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)  
  
## Archivio di istanze del flusso di lavoro SQL  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> è un'implementazione basata su server SQL di un archivio di istanze.In un archivio di istanze è memorizzato lo stato di un'istanza in esecuzione nonché tutti i dati necessari per caricare e riprendere l'esecuzione di quell'istanza.L'host del servizio indica all'archivio di istanze di salvare lo stato dell'istanza se il flusso di lavoro è persistente e di caricare lo stato dell'istanza all'arrivo di un messaggio per quell'istanza o alla scadenza di un'attività di ritardo.  
  
### Introduzione  
  
1.  In [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], creare un flusso di lavoro che contiene un'attività <xref:System.Activities.Statements.Persist> implicita o esplicita.Aggiungere il comportamento <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> all'host del servizio del flusso di lavoro.Questa operazione può essere eseguita nel codice o nel file di configurazione dell'applicazione.  
  
2.  Esempi: [Persistenza](../../../docs/framework/windows-workflow-foundation/samples/persistence.md)  
  
3.  Documentazione concettuale: [Archivio di istanze del flusso di lavoro SQL](../../../docs/framework/windows-workflow-foundation//sql-workflow-instance-store.md).