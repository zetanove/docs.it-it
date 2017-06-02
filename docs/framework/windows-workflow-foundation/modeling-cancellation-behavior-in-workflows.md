---
title: "Modellazione del comportamento di annullamento nei flussi di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d48f6cf3-cdde-4dd3-8265-a665acf32a03
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Modellazione del comportamento di annullamento nei flussi di lavoro
Le attività possono essere annullate all'interno di un flusso di lavoro, ad esempio da un'attività <xref:System.Activities.Statements.Parallel> che annulla i rami incompleti quando la proprietà <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> restituisce `true` oppure all'esterno del flusso di lavoro, se l'host chiama il metodo <xref:System.Activities.WorkflowApplication.Cancel%2A>.Per assicurare la gestione dell'annullamento, gli autori del flusso di lavoro possono utilizzare le attività <xref:System.Activities.Statements.CancellationScope> e <xref:System.Activities.Statements.CompensableActivity> o creare attività personalizzate che forniscono la logica di annullamento.In questo argomento viene fornita una panoramica sull'annullamento nei flussi di lavoro.  
  
## Annullamento, compensazione e transazioni  
 Le transazioni consentono all'applicazione di interrompere, ovvero eseguire il rollback, tutte le modifiche eseguite all'interno della transazione se si verificano errori durante qualsiasi parte del processo di transazione.Tuttavia, non tutte le operazioni che potrebbero dover essere annullate sono appropriate per le transazioni, ad esempio operazioni con esecuzione prolungata o che non implicano risorse transazionali.La compensazione fornisce un modello per annullare operazioni non transazionali completate precedentemente se, in seguito, si verifica un errore nel flusso di lavoro.L'annullamento fornisce agli autori di flussi di lavoro e attività un modello per gestire le operazioni non transazionali che non sono state completate.Se l'attività viene annullata poiché non ne è stata completata l'esecuzione, sarà richiamata la relativa logica di annullamento, se disponibile.  
  
> [!NOTE]
>  [!INCLUDE[crabout](../../../includes/crabout-md.md)] transazioni e compensazione, vedere [Transazioni](../../../docs/framework/windows-workflow-foundation//workflow-transactions.md) e [Compensazione](../../../docs/framework/windows-workflow-foundation//compensation.md).  
  
## Utilizzo dell'attività CancellationScope  
 L'attività <xref:System.Activities.Statements.CancellationScope> dispone di due sezioni che possono contenere le attività figlio <xref:System.Activities.Statements.CancellationScope.Body%2A> e <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>.Nella proprietà <xref:System.Activities.Statements.CancellationScope.Body%2A> vengono posizionate le attività che costituiscono la logica dell'attività e nella proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> vengono posizionate le attività che forniscono la logica di annullamento per l'attività.Un'attività può essere annullata solo se non è stata completata.Nel caso dell'attività <xref:System.Activities.Statements.CancellationScope>, con completamento si intende il completamento delle attività nella proprietà <xref:System.Activities.Statements.CancellationScope.Body%2A>.Se viene pianificata una richiesta di annullamento e le attività nella proprietà <xref:System.Activities.Statements.CancellationScope.Body%2A> non sono state completate, l'attività <xref:System.Activities.Statements.CancellationScope> sarà contrassegnata come <xref:System.Activities.ActivityInstanceState> e saranno eseguite le attività della proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>.  
  
### Annullamento di un flusso di lavoro dall'host  
 Un host può annullare un flusso di lavoro chiamando il metodo <xref:System.Activities.WorkflowApplication.Cancel%2A> dell'istanza <xref:System.Activities.WorkflowApplication> che sta ospitando il flusso di lavoro.Nell'esempio seguente, viene creato un flusso di lavoro che dispone di un'attività <xref:System.Activities.Statements.CancellationScope>.Una volta richiamato il flusso di lavoro, l'host effettua una chiamata al metodo <xref:System.Activities.WorkflowApplication.Cancel%2A>.L'esecuzione principale del flusso di lavoro viene interrotta, viene richiamata la proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> dell'attività <xref:System.Activities.Statements.CancellationScope>, quindi il flusso di lavoro viene completato con lo stato <xref:System.Activities.ActivityInstanceState>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#35](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#35)]  
  
 Quando questo flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console.  
  
 **Avvio del flusso di lavoro.**   
**Oggetto CancellationHandler richiamato.**   
**Flusso di lavoro b30ebb30\-df46\-4d90\-a211\-e31c38d8db3c annullato.**    
> [!NOTE]
>  Quando un'attività <xref:System.Activities.Statements.CancellationScope> viene annullata e viene richiamata la proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>, l'autore del flusso di lavoro deve determinare lo stato dell'attività prima del relativo annullamento al fine di fornire la logica di annullamento appropriata.La proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> non fornisce alcuna informazione sullo stato dell'attività annullata.  
  
 Un flusso di lavoro può essere annullato anche dall'host se un'eccezione non gestita viene propagata oltre la radice del flusso di lavoro e il gestore della proprietà <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A> restituisce <xref:System.Activities.UnhandledExceptionAction>.In questo esempio, viene avviato il flusso di lavoro che, successivamente, genera un'eccezione <xref:System.ApplicationException>.Questa eccezione non viene gestita dal flusso di lavoro, pertanto viene richiamato il gestore della proprietà <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>.Il gestore indica al runtime di annullare il flusso di lavoro e viene richiamata la proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> dell'attività <xref:System.Activities.Statements.CancellationScope> attualmente in corso di esecuzione.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#36](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#36)]  
  
 Quando questo flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console.  
  
 **Avvio del flusso di lavoro.**   
**OnUnhandledException nel flusso di lavoro 6bb2d5d6\-f49a\-4c6d\-a988\-478afb86dbe9**   
**È stata generata un'eccezione dell'applicazione.**   
**Oggetto CancellationHandler richiamato.**   
**Flusso di lavoro 6bb2d5d6\-f49a\-4c6d\-a988\-478afb86dbe9 annullato.**    
### Annullamento di un'attività dall'interno di un flusso di lavoro  
 Un'attività può essere annullata anche dal relativo elemento padre.Ad esempio, se un'attività <xref:System.Activities.Statements.Parallel> dispone di più rami in esecuzione e la relativa proprietà <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> restituisce `true`, i rami incompleti corrispondenti saranno annullati.In questo esempio viene creata un'attività <xref:System.Activities.Statements.Parallel> che dispone di due rami.La relativa proprietà <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> è impostata su `true`, pertanto l'oggetto <xref:System.Activities.Statements.Parallel> viene completato non appena si verifica la stessa condizione per uno dei relativi rami.In questo esempio viene completato il ramo 2, pertanto il ramo 1 viene annullato.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#37](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#37)]  
  
 Quando questo flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console.  
  
 **Avvio del ramo 1.**   
**Ramo 2 completato.**   
**Ramo 1 annullato.**   
**Flusso di lavoro e0685e24\-18ef\-4a47\-acf3\-5c638732f3be completato.**  Le attività vengono annullate anche se un'eccezione viene propagata oltre la radice dell'attività, ma viene gestita a un livello superiore nel flusso di lavoro.In questo esempio la logica principale del flusso di lavoro è costituita da un'attività <xref:System.Activities.Statements.Sequence>L'oggetto <xref:System.Activities.Statements.Sequence> è specificato come <xref:System.Activities.Statements.CancellationScope.Body%2A> di un'attività <xref:System.Activities.Statements.CancellationScope> contenuta da un'attività <xref:System.Activities.Statements.TryCatch>.Dal corpo dell'attività <xref:System.Activities.Statements.Sequence> viene generata un'eccezione che viene gestita dall'attività padre <xref:System.Activities.Statements.TryCatch>. L'attività <xref:System.Activities.Statements.Sequence> viene quindi annullata.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#39](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#39)]  
  
 Quando questo flusso di lavoro viene richiamato, l'output seguente viene visualizzato nella console.  
  
 **Avvio dell'attività Sequence.**   
**Attività Sequence annullata.**   
**Eccezione rilevata.**   
**Flusso di lavoro e3c18939\-121e\-4c43\-af1c\-ba1ce977ce55 completato.**   
### Generazione di eccezioni da un oggetto CancellationHandler  
 Qualsiasi eccezione generata dalla proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> di un'attività <xref:System.Activities.Statements.CancellationScope> è irreversibile per il flusso di lavoro.Se è possibile che le eccezioni escano da una proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>, utilizzare un oggetto <xref:System.Activities.Statements.TryCatch> nella proprietà <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> per rilevare e gestire tali eccezioni.  
  
### Annullamento tramite l'oggetto CompensableActivity  
 Analogamente all'attività <xref:System.Activities.Statements.CancellationScope>, l'oggetto <xref:System.Activities.Statements.CompensableActivity> dispone di una proprietà <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>.Se un oggetto <xref:System.Activities.Statements.CompensableActivity> viene annullato, viene richiamata qualsiasi attività nella relativa proprietà <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>.Tale operazione può essere utile per annullare operazioni compensabili completate parzialmente.Per informazioni su come utilizzare l'oggetto <xref:System.Activities.Statements.CompensableActivity> per la compensazione e l'annullamento, vedere [Compensazione](../../../docs/framework/windows-workflow-foundation//compensation.md).  
  
## Annullamento tramite attività personalizzate  
 Gli autori di attività personalizzate possono implementare la logica di annullamento nelle proprie attività personalizzate in molti modi diversi.Le attività personalizzate che derivano da <xref:System.Activities.Activity> possono implementare la logica di annullamento inserendo <xref:System.Activities.Statements.CancellationScope> o un'altra attività personalizzata che contiene la logica di annullamento nel corpo dell'attività.Le attività derivate <xref:System.Activities.AsyncCodeActivity> e <xref:System.Activities.NativeActivity> possono eseguire l'override del rispettivo metodo <xref:System.Activities.NativeActivity.Cancel%2A> e fornire qui la logica di annullamento.Le attività derivate <xref:System.Activities.CodeActivity> non forniscono alcuna misura per l'annullamento poiché tutto il lavoro viene eseguito in un unico picco di esecuzione quando il runtime chiama il metodo <xref:System.Activities.CodeActivity.Execute%2A>.Se il metodo Execute non è ancora stato chiamato e viene annullata un'attività basata sull'oggetto <xref:System.Activities.CodeActivity>, l'attività viene chiusa con lo stato <xref:System.Activities.ActivityInstanceState> e il metodo <xref:System.Activities.CodeActivity.Execute%2A> non viene chiamato.  
  
### Annullamento tramite l'oggetto NativeActivity  
 Le classi derivate <xref:System.Activities.NativeActivity> possono eseguire l'override del metodo <xref:System.Activities.NativeActivity.Cancel%2A> per fornire la logica di annullamento personalizzata.Se questo metodo non viene sottoposto a override, viene applicata la logica di annullamento del flusso di lavoro predefinita.L'annullamento predefinito è il processo che si verifica per un oggetto <xref:System.Activities.NativeActivity> che non esegue l'override del metodo <xref:System.Activities.NativeActivity.Cancel%2A> o il cui metodo <xref:System.Activities.NativeActivity.Cancel%2A> chiama il metodo <xref:System.Activities.NativeActivity.Cancel%2A> dell'oggetto <xref:System.Activities.NativeActivity> base.Quando un'attività viene annullata, il runtime contrassegna l'attività per l'annullamento e gestisce automaticamente la pulizia.Se l'attività dispone solo di segnalibri in attesa, questi ultimi saranno rimossi e l'attività sarà contrassegnata come <xref:System.Activities.ActivityInstanceState>.Qualsiasi attività figlio in attesa dell'attività annullata sarà annullata a sua volta.Qualsiasi tentativo di pianificare attività figlio aggiuntive verrà ignorato e l'attività sarà contrassegnata come <xref:System.Activities.ActivityInstanceState>.Se qualsiasi attività figlio in attesa viene completata nello stato <xref:System.Activities.ActivityInstanceState> o <xref:System.Activities.ActivityInstanceState>, l'attività sarà contrassegnata come <xref:System.Activities.ActivityInstanceState>.Si noti che è possibile ignorare una richiesta di annullamento.Se un'attività non dispone di segnalibri in attesa o di attività figlio in esecuzione e non pianifica alcun elemento di lavoro aggiuntivo dopo essere stata contrassegnata per l'annullamento, verrà completata correttamente.Questo annullamento predefinito è sufficiente per molti scenari, tuttavia se è necessaria un'ulteriore logica di annullamento, è possibile utilizzare le attività di annullamento incorporate o le attività personalizzate.  
  
 Nell'esempio seguente, viene definito l'override <xref:System.Activities.NativeActivity.Cancel%2A> di un'attività `ParallelForEach` personalizzata basata sull'oggetto <xref:System.Activities.NativeActivity>.Quando l'attività viene annullata, questo override gestisce la logica di annullamento per l'attività.Questo esempio fa parte dell'esempio [Attività ParallelForEach non generica](../../../docs/framework/windows-workflow-foundation/samples/non-generic-parallelforeach.md).  
  
 <!-- TODO: review snippet reference [!code-csharp[CFX_WorkflowApplicationExample#1010](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1010)]  -->  
  
 Le attività derivate da <xref:System.Activities.NativeActivity> possono determinare se l'annullamento è stato richiesto in seguito al controllo della proprietà <xref:System.Activities.NativeActivityContext.IsCancellationRequested%2A> e possono contrassegnarsi come annullate chiamando il metodo <xref:System.Activities.NativeActivityContext.MarkCanceled%2A>.La chiamata al metodo <xref:System.Activities.NativeActivityContext.MarkCanceled%2A> non completa immediatamente l'attività.Come al solito, il runtime completerà l'attività quando non dispone più di alcuna operazione in attesa, tuttavia se viene chiamato il metodo <xref:System.Activities.NativeActivityContext.MarkCanceled%2A>, lo stato finale sarà <xref:System.Activities.ActivityInstanceState> anziché <xref:System.Activities.ActivityInstanceState>.  
  
### Annullamento tramite l'oggetto AsyncCodeActivity  
 Anche le attività basate sull'oggetto <xref:System.Activities.AsyncCodeActivity> possono fornire la logica di annullamento personalizzata eseguendo l'override del metodo <xref:System.Activities.AsyncCodeActivity.Cancel%2A>.Se questo metodo non viene sottoposto a override, non viene eseguita alcuna gestione dell'annullamento se l'attività viene annullata.Nell'esempio seguente, viene definito l'override <xref:System.Activities.AsyncCodeActivity.Cancel%2A> di un'attività `ExecutePowerShell` personalizzata basata sull'oggetto <xref:System.Activities.AsyncCodeActivity>.Quando l'attività viene annullata, esegue il comportamento di annullamento desiderato.Questo esempio fa parte dell'esempio [Utilizzo dell'attività InvokePowerShell](../../../docs/framework/windows-workflow-foundation/samples/using-the-invokepowershell-activity.md).  
  
 [!code-csharp[CFX_WorkflowApplicationExample#1020](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#1020)]  
  
 Le attività derivate da <xref:System.Activities.AsyncCodeActivity> possono determinare se l'annullamento è stato richiesto in seguito al controllo della proprietà <xref:System.Activities.AsyncCodeActivityContext.IsCancellationRequested%2A> e possono contrassegnarsi come annullate chiamando il metodo <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A>.