---
title: "Eccezioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 065205cc-52dd-4f30-9578-b17d8d113136
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Eccezioni
I flussi di lavoro possono utilizzare l'attività <xref:System.Activities.Statements.TryCatch> per gestire le eccezioni generate durante l'esecuzione di un flusso di lavoro.Queste eccezioni possono essere gestite o generate una seconda volta utilizzando l'attività <xref:System.Activities.Statements.Rethrow>.Le attività della sezione <xref:System.Activities.Statements.TryCatch.Finally%2A> vengono eseguite quando viene completata la sezione <xref:System.Activities.Statements.TryCatch.Try%2A> o <xref:System.Activities.Statements.TryCatch.Catches%2A>.I flussi di lavoro ospitati da un'istanza <xref:System.Activities.WorkflowApplication> possono utilizzare anche il gestore dell'evento <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> per gestire le eccezioni che non sono gestite da un'attività <xref:System.Activities.Statements.TryCatch>.  
  
## Cause delle eccezioni  
 In un flusso di lavoro le eccezioni possono essere generate nei modi seguenti:  
  
-   Timeout delle transazioni nell'oggetto <xref:System.Activities.Statements.TransactionScope>.  
  
-   Eccezione esplicita generata dal flusso di lavoro utilizzando l'attività <xref:System.Activities.Statements.Throw>.  
  
-   Eccezione di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] generata da un'attività.  
  
-   Eccezione generata da codice esterno, ad esempio librerie, componenti o servizi utilizzati nel flusso di lavoro.  
  
## Gestione delle eccezioni  
 Se un'eccezione viene generata da un'attività ma non viene gestita, il comportamento predefinito prevede l'interruzione dell'istanza del flusso di lavoro.Se presente, un gestore personalizzato <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> può eseguire l'override di questo comportamento predefinito.Questo gestore consente all'autore dell'host del flusso di lavoro di fornire la gestione appropriata, ad esempio la registrazione personalizzata, l'interruzione, l'annullamento o la chiusura del flusso di lavoro.Se un flusso di lavoro genera un'eccezione che non viene gestita, viene chiamato il gestore <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>.Esistono tre azioni possibili restituite da <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> che determinano il risultato finale del flusso di lavoro.  
  
-   **Annullamento**: un'istanza del flusso di lavoro annullata è una valida uscita per l'esecuzione di un branch.È possibile modellare il comportamento di annullamento, ad esempio utilizzando un'attività CancellationScope.Il gestore Completed viene richiamato al completamento del processo di annullamento.Un flusso di lavoro annullato si trova nello stato di annullato.  
  
-   **Termine**: un'istanza di flusso di lavoro terminata non può essere ripresa o riavviata.Ciò attiva l'evento Completed in cui è possibile immettere un'eccezione come motivo del termine dell'istanza.Il gestore Terminated viene richiamato al completamento del processo di chiusura.Un flusso di lavoro terminato si trova nello stato di non riuscito.  
  
-   **Interruzione**: un'istanza del flusso di lavoro può essere ripresa solo se è stata configurata come persistente.Senza la persistenza, un flusso di lavoro non può essere ripreso.Nel momento in cui un flusso di lavoro viene interrotto, qualsiasi lavoro eseguito \(in memoria\) dall'ultimo di punto di persistenza verrà perso.Per un flusso di lavoro interrotto, viene richiamato il gestore Aborted utilizzando l'eccezione come motivo di quando è stato completato il processo di interruzione.Tuttavia, a differenza dei gestori Cancelled e Terminated, il gestore Completed non viene richiamato.Un flusso di lavoro interrotto si trova nello stato di interrotto.  
  
 Nell'esempio seguente viene richiamato un flusso di lavoro che genera un'eccezione.L'eccezione non viene gestita dal flusso di lavoro e viene richiamato il gestore <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>.Gli argomenti <xref:System.Activities.WorkflowApplicationUnhandledExceptionEventArgs> vengono controllati per fornire informazioni sull'eccezione e il flusso di lavoro viene terminato.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1)]  
  
### Gestione delle eccezioni con l'attività TryCatch  
 La gestione delle eccezioni in un flusso di lavoro viene eseguita con l'attività <xref:System.Activities.Statements.TryCatch>.L'attività <xref:System.Activities.Statements.TryCatch> dispone di una raccolta <xref:System.Activities.Statements.TryCatch.Catches%2A> di attività <xref:System.Activities.Statements.Catch>, ognuna delle quali è associata a un tipo <xref:System.Exception> specifico.Se l'eccezione generata da un'attività contenuta nella sezione <xref:System.Activities.Statements.TryCatch.Try%2A> di un'attività <xref:System.Activities.Statements.TryCatch> corrisponde all'eccezione di un'attività <xref:System.Activities.Statements.Catch%601> nella raccolta <xref:System.Activities.Statements.TryCatch.Catches%2A>, l'eccezione viene gestita.Se l'eccezione viene generata in modo esplicito una seconda volta oppure viene generata una nuova eccezione, quest'ultima passa fino all'attività padre.Nell'esempio di codice seguente viene mostrata un'attività <xref:System.Activities.Statements.TryCatch> che gestisce un oggetto <xref:System.ApplicationException> generato nella sezione <xref:System.Activities.Statements.TryCatch.Try%2A> da un'attività <xref:System.Activities.Statements.Throw>.Il messaggio dell'eccezione viene scritto nella console dall'attività <xref:System.Activities.Statements.Catch%601>, quindi viene scritto un messaggio nella console nella sezione <xref:System.Activities.Statements.TryCatch.Finally%2A>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#33](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#33)]  
  
 Le attività della sezione <xref:System.Activities.Statements.TryCatch.Finally%2A> vengono eseguite quando viene completata correttamente la sezione <xref:System.Activities.Statements.TryCatch.Try%2A> o <xref:System.Activities.Statements.TryCatch.Catches%2A>.La sezione <xref:System.Activities.Statements.TryCatch.Try%2A> viene completata correttamente se non vengono generate eccezioni dal suo interno e la sezione <xref:System.Activities.Statements.TryCatch.Catches%2A> viene completata correttamente se non viene generata o rigenerata alcuna eccezione dal suo interno.Se un'eccezione viene generata nella sezione <xref:System.Activities.Statements.TryCatch.Try%2A> section di <xref:System.Activities.Statements.TryCatch> e o non è gestita da un oggetto <xref:System.Activities.Statements.Catch%601> nella sezione <xref:System.Activities.Statements.TryCatch.Catches%2A> o è rigenerata dall'oggetto <xref:System.Activities.Statements.TryCatch.Catches%2A>, le attività in <xref:System.Activities.Statements.TryCatch.Finally%2A> non verranno eseguite a meno che non si verifichi una delle situazioni indicate di seguito.  
  
-   L'eccezione è intercettata da un'attività <xref:System.Activities.Statements.TryCatch> di livello superiore nel flusso di lavoro, indipendentemente che sia rigenerata da quell'attività <xref:System.Activities.Statements.TryCatch> di livello superiore.  
  
-   L'eccezione non è gestita da un'attività <xref:System.Activities.Statements.TryCatch> di livello superiore, ignora la radice del flusso di lavoro e il flusso di lavoro è configurato per l'annullamento anziché per la chiusura o l'interruzione.I flussi di lavoro ospitati utilizzando <xref:System.Activities.WorkflowApplication> possono configurare queste operazioni gestendo <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> e restituendo <xref:System.Activities.UnhandledExceptionAction>.Un esempio di gestione di <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> è stato fornito in precedenza in questo argomento.I servizi di flusso di lavoro possono configurare queste operazioni utilizzando <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> e specificando <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction>.Per un esempio di configurazione di <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>, vedere [Estensibilità host del servizio flusso di lavoro](../../../docs/framework/wcf/feature-details/workflow-service-host-extensibility.md).  
  
## Gestione delle eccezioni e compensazione  
 La gestione delle eccezioni si verifica durante l'esecuzione di un'attività,mentre la compensazione si verifica dopo il corretto completamento di un'attività.La gestione delle eccezioni consente di eseguire una pulizia dopo che l'attività genera l'eccezione, mentre la compensazione permette di annullare il lavoro correttamente completato di un'attività portata a termine in precedenza.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Compensazione](../../../docs/framework/windows-workflow-foundation//compensation.md).  
  
## Vedere anche  
 <xref:System.Activities.Statements.TryCatch>   
 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>   
 <xref:System.Activities.Statements.CompensableActivity>