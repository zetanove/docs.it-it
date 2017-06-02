---
title: "Host ReadLine di WorkflowApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7b362be-cb42-40d7-b9ef-cfc4aed2455b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Host ReadLine di WorkflowApplication
Questo esempio è un host ReadLine generico.È possibile caricare ed eseguire qualsiasi flusso di lavoro utilizzando l'attività `ReadLine` inclusa \(o altre attività quali quelle che ottengono dati dai segnalibri ripresi con le stringhe\).L'output dell'attività `WriteLine` o qualsiasi elemento che scrive nell'estensione della proprietà <xref:System.Activities.Statements.WriteLine.TextWriter%2A> è diretto alla finestra host.Quando un'istanza è inattiva, i segnalibri disponibili per tale istanza vengono visualizzati in una casella combinata.Selezionando un segnalibro, inserendo un testo e premendo il pulsante di ripresa del segnalibro viene continuata l'esecuzione del flusso di lavoro.Inoltre, è possibile annullare, interrompere o terminare un flusso di lavoro selezionato.La persistenza è attiva per impostazione predefinita; è possibile arrestare l'host e ripristinarlo in modo che l'elenco di istanze venga popolato con le istanze archiviate nel database.Il rilevamento viene utilizzato per restituire gli eventi a livello dell'oggetto <xref:System.Activities.WorkflowApplication> all'host con la possibilità di aggiungere il rilevamento dettagliato a livello di attività.  
  
## Dettagli dell'esempio  
 In questo host sono disponibili due livelli: la visualizzazione e la gestione di istanze.La visualizzazione è costituita dalle classi `HostView` e `WorkflowApplicationInfo`.Il modello generale di questo host prevede che nella classe `HostView` siano visualizzate le opzioni disponibili all'utente in base agli oggetti `WorkflowApplicationInfo` mantenuti ragionevolmente in sincronizzazione con le istanze che rappresentano.Il livello della gestione di istanze è costituito dalla classe `WorkflowApplicationManager` che rappresenta il nucleo centrale di tutte le comunicazioni dell'host e dalla classe `WorkflowDefinitionExtension` che rende persistente la relazione tra un'istanza e la definizione del programma con cui è stata avviata, nonché alcune altre classi.Le chiamate `HostView` controllano le operazioni nell'oggetto `WorkflowApplicationManager`.Queste chiamate sono generalmente asincrone per gestire un'interfaccia utente in grado di rispondere.Al termine delle chiamate asincrone, l'oggetto `WorkflowApplicationManager` effettua di nuovo delle chiamate nel livello di visualizzazione tramite un'interfaccia ben definita \(`IHostView`\).Solitamente, la classe `HostView` invia queste chiamate dalla classe `WorkflowApplicationManager` al thread dell'interfaccia utente.La scrittura di testo viene effettuata negli oggetti <xref:System.Activities.Statements.WriteLine.TextWriter%2A> thread\-safe forniti dalla classe `HostView`.L'interfaccia utente non è l'unico elemento che genera eventi.Anche gli oggetti <xref:System.Activities.WorkflowApplication> segnalano l'oggetto `WorkflowApplicationManager` quando, ad esempio, diventano `Idle`, `Complete` o quando sono `Aborted`.La classe `WorkflowApplicationManager` esce dal thread eventi inviando operazioni di pulizia o aggiornamento all'host.  
  
 La registrazione del file utilizzato per avviare un oggetto <xref:System.Activities.WorkflowApplication> è resa più semplice dalla classe `WorkflowDefinitionExtension`che implementa l'interfaccia <xref:System.Activities.Persistence.PersistenceIOParticipant> per partecipare alla persistenza e rendere persistente il percorso nella definizione di flusso di lavoro.  
  
 Il metodo `WorkflowApplicationManager.Load` utilizza il percorso archiviato per creare un'istanza dei programmi del flusso di lavoro richiesti per il caricamento di oggetti <xref:System.Activities.WorkflowApplication> non terminati.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Per questo esempio è necessario aver installato SQL Express.SQL Express viene fornito con [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Aprire il prompt dei comandi di Visual Studio 2010.  
  
3.  Passare alla directory di esempio \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\) ed eseguire CreateInstanceStore.cmd.  
  
4.  Lo script CreateInstanceStore.cmd tenta di creare il database nell'istanza predefinita di SQL Server 2008 Express.Se si desidera installare il database in un'istanza diversa, modificare lo script.  
  
5.  Compilare il progetto WorkflowApplicationReadLineHost ed eseguirlo dalla riga di comando.  
  
6.  Una volta in esecuzione, è possibile disattivare o attivare la persistenza.Inoltre, è possibile attivare o disattivare il rilevamento dettagliato di attività.  
  
7.  Premere il pulsante con i puntini di sospensione accanto al pulsante **Esegui** per cercare un flusso di lavoro definito in un file XAML  
  
     Nella cartella SampleWorkflows sono disponibili due esempi.L'esempio parallel1.xaml diventa inattivo.  
  
8.  Una volta selezionato un esempio, premere il pulsante **Esegui**.  
  
9. Se o quando il flusso di lavoro diventa inattivo, la casella combinata **Segnalibri** viene popolata con i segnalibri disponibili.  
  
10. Le opzioni di questa fase servono per riprendere un segnalibro oppure per annullare, interrompere o terminare il flusso di lavoro.Inoltre, è possibile arrestare l'host e riavviarlo.Se la persistenza viene mantenuta attiva, le istanze vengono scaricate all'arresto e ricaricate al riavvio.  
  
     Per riprendere un segnalibro, selezionare quello desiderato, digitare un valore nella casella di testo accanto alla casella combinata e premere **Riprendi segnalibro**.  
  
#### Per rimuovere il database dell'archivio di istanze  
  
1.  Aprire il prompt dei comandi di Visual Studio 2010.  
  
2.  Passare alla directory di esempio \(\\WF\\Basic\\Execution\\ControllingWorkflowApplications\) ed eseguire RemoveInstanceStore.cmd.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Execution\ControllingWorkflowApplications`  
  
## Vedere anche