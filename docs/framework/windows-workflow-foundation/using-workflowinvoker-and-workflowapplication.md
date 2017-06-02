---
title: "Utilizzo di WorkflowInvoker e WorkflowApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd0e583c-a3f9-4fa2-b247-c7b3368c48a7
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Utilizzo di WorkflowInvoker e WorkflowApplication
In [!INCLUDE[wf](../../../includes/wf-md.md)] sono disponibili diversi metodi per l'hosting dei flussi di lavoro.<xref:System.Activities.WorkflowInvoker> offre un modo semplice per richiamare un flusso di lavoro come se fosse una chiamata a un metodo e può essere utilizzato solo per i flussi di lavoro che non utilizzano la persistenza.<xref:System.Activities.WorkflowApplication> fornisce un modello più dettagliato per l'esecuzione di flussi di lavoro che include la notifica degli eventi del ciclo di vita, il controllo di esecuzione, la ripresa del segnalibro e la persistenza.<xref:System.ServiceModel.Activities.WorkflowServiceHost> fornisce il supporto per le attività di messaggistica e viene principalmente utilizzato con i servizi di flusso di lavoro.In questo argomento viene illustrato l'hosting del flusso di lavoro con <xref:System.Activities.WorkflowInvoker> e <xref:System.Activities.WorkflowApplication>.[!INCLUDE[crabout](../../../includes/crabout-md.md)]l'hosting dei flussi di lavoro con <xref:System.ServiceModel.Activities.WorkflowServiceHost>, vedere [Servizi flusso di lavoro](../../../docs/framework/wcf/feature-details/workflow-services.md) e [Panoramica dell'hosting dei servizi flusso di lavoro](../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md).  
  
## Utilizzo di WorkflowInvoker  
 L'oggetto <xref:System.Activities.WorkflowInvoker> fornisce un modello per l'esecuzione di un flusso di lavoro come se si trattasse di una chiamata al metodo.Per richiamare un flusso di lavoro tramite l'oggetto <xref:System.Activities.WorkflowInvoker>, chiamare il metodo <xref:System.Activities.WorkflowInvoker.Invoke%2A> e passare la definizione del flusso di lavoro da richiamare.In questo esempio viene richiamata un'attività <xref:System.Activities.Statements.WriteLine> tramite l'oggetto <xref:System.Activities.WorkflowInvoker>.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#1)]  
  
 Quando un flusso di lavoro viene richiamato utilizzando l'oggetto <xref:System.Activities.WorkflowInvoker>, tale flusso di lavoro viene eseguito sul thread chiamante e il metodo <xref:System.Activities.WorkflowInvoker.Invoke%2A> viene bloccato finché il flusso di lavoro non viene completato, incluso qualsiasi tempo di inattività.Per configurare un intervallo di timeout entro cui completare il flusso di lavoro, utilizzare uno degli overload <xref:System.Activities.WorkflowInvoker.Invoke%2A> che accetta un parametro <xref:System.TimeSpan>.In questo esempio un flusso di lavoro viene richiamato due volte con due intervalli di timeout diversi.Il primo flusso di lavoro viene completato, ma non il secondo.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#50](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#50)]  
  
> [!NOTE]
>  L'eccezione <xref:System.TimeoutException> viene generata solo se l'intervallo di timeout scade e il flusso di lavoro diventa inattivo durante l'esecuzione.Un flusso di lavoro il cui completamento richiede più tempo rispetto all'intervallo di timeout specificato viene completato correttamente se non diventa inattivo.  
  
 <xref:System.Activities.WorkflowInvoker> fornisce anche versioni asincrone del metodo di richiamo.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<xref:System.Activities.WorkflowInvoker.InvokeAsync%2A> e <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A>.  
  
### Impostazione degli argomenti di input di un flusso di lavoro  
 I dati possono essere passati in un flusso di lavoro tramite un dizionario di parametri di input, con chiavi in base al nome dell'argomento, che sono mappati agli argomenti di input del flusso di lavoro.In questo esempio viene richiamato un oggetto <xref:System.Activities.Statements.WriteLine> e il valore del relativo argomento <xref:System.Activities.Statements.WriteLine.Text%2A> viene specificato utilizzando il dizionario di parametri di input.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#3](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#3)]  
  
### Recupero degli argomenti di output di un flusso di lavoro  
 I parametri di output di un flusso di lavoro possono essere ottenuti tramite il dizionario di output restituito dalla chiamata all'overload <xref:System.Activities.WorkflowInvoker.Invoke%2A>.Nell'esempio seguente viene richiamato un flusso di lavoro composto da una singola attività `Divide` che dispone di due argomenti di input e due di output.Quando viene richiamato il flusso di lavoro, viene passato il dizionario `arguments` che contiene i valori per ogni argomento di input, con chiavi in base al nome dell'argomento.Quando la chiamata a `Invoke` restituisce un valore, ogni argomento di output viene restituito nel dizionario `outputs`, anche con chiavi in base al nome dell'argomento.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#120](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#120)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#20](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#20)]  
  
 Se il flusso di lavoro deriva da <xref:System.Activities.ActivityWithResult>, ad esempio `CodeActivity<TResult>` o `Activity<TResult>`, ed esistono altri argomenti di output oltre all'argomento di output <xref:System.Activities.Activity%601.Result%2A> definito correttamente, è necessario utilizzare un overload non generico di `Invoke` per recuperare gli argomenti aggiuntivi.A tale scopo, la definizione del flusso di lavoro passata in `Invoke` deve essere di tipo <xref:System.Activities.Activity>.In questo esempio l'attività `Divide` deriva da `CodeActivity<int>`, ma viene dichiarata come <xref:System.Activities.Activity> in modo che venga utilizzato un overload non generico di `Invoke` che restituisce un dizionario di argomenti anziché un solo valore restituito.  
  
 [!code-csharp[CFX_WorkflowInvokerExample#121](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#121)]  
  
 [!code-csharp[CFX_WorkflowInvokerExample#21](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowinvokerexample/cs/program.cs#21)]  
  
## Utilizzo di WorkflowApplication  
 <xref:System.Activities.WorkflowApplication> offre un'ampia gamma di funzionalità per la gestione delle istanze del flusso di lavoro.<xref:System.Activities.WorkflowApplication> agisce da proxy thread\-safe verso l'oggetto <xref:System.Activities.Hosting.WorkflowInstance> effettivo, che incapsula il runtime e fornisce i metodo per creare e caricare istanze del flusso di lavoro, sospendere e riprendere, chiudere e inviare notifiche di eventi del ciclo di vita.Per eseguire un flusso di lavoro tramite l'oggetto <xref:System.Activities.WorkflowApplication> è necessario creare l'oggetto <xref:System.Activities.WorkflowApplication>, sottoscrivere un qualsiasi evento del ciclo di vita desiderato, avviare il flusso di lavoro, quindi attendere il relativo completamento.In questo esempio viene creata una definizione del flusso di lavoro costituita da un'attività <xref:System.Activities.Statements.WriteLine>; con la definizione del flusso specificata viene creato poi un oggetto <xref:System.Activities.WorkflowApplication>.L'oggetto <xref:System.Activities.WorkflowApplication.Completed%2A> viene gestito in modo che all'host sia notificato quando il flusso di lavoro viene completato, il flusso di lavoro viene avviato con una chiamata a <xref:System.Activities.WorkflowApplication.Run%2A>, quindi l'host attende il completamento del flusso di lavoro.Quando il flusso di lavoro viene completato, l'oggetto <xref:System.Threading.AutoResetEvent> viene impostato e l'applicazione host può riprendere l'esecuzione, come mostrato nell'esempio seguente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#31](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#31)]  
  
### Eventi del ciclo di vita di WorkflowApplication  
 Oltre alla proprietà <xref:System.Activities.WorkflowApplication.Completed%2A>, gli autori di host possono ricevere una notifica quando un flusso di lavoro viene scaricato \(<xref:System.Activities.WorkflowApplication.Unloaded%2A>\), interrotto \(<xref:System.Activities.WorkflowApplication.Aborted%2A>\), diventa inattivo \(<xref:System.Activities.WorkflowApplication.Idle%2A> e <xref:System.Activities.WorkflowApplication.PersistableIdle%2A>\) o si verifica un'eccezione non gestita \(<xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>\).Gli sviluppatori di applicazioni del flusso di lavoro possono gestire queste notifiche e intraprendere le azioni appropriate, come mostrato nell'esempio seguente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#32](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#32)]  
  
### Impostazione degli argomenti di input di un flusso di lavoro  
 I dati possono essere passati in un flusso di lavoro come se avviati tramite un dizionario di parametri, ovvero in modo simile al passaggio dei dati tramite l'oggetto <xref:System.Activities.WorkflowInvoker>.Ogni elemento del dizionario viene mappato a un argomento di input del flusso di lavoro specificato.In questo esempio viene richiamato un flusso di lavoro costituito da un'attività <xref:System.Activities.Statements.WriteLine> e il relativo argomento <xref:System.Activities.Statements.WriteLine.Text%2A> viene specificato utilizzando il dizionario di parametri di input.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#30](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#30)]  
  
### Recupero degli argomenti di output di un flusso di lavoro  
 Quando un flusso di lavoro viene completato, qualsiasi argomento di output può essere recuperato nel gestore <xref:System.Activities.WorkflowApplication.Completed%2A> eseguendo l'accesso al dizionario <xref:System.Activities.WorkflowApplicationCompletedEventArgs.Outputs%2A?displayProperty=fullName>.Nell'esempio seguente viene ospitato un flusso di lavoro tramite <xref:System.Activities.WorkflowApplication>.Un'istanza <xref:System.Activities.WorkflowApplication> viene costruita utilizzando una definizione di flusso di lavoro composta da una singola attività `DiceRoll`.L'attività `DiceRoll` dispone di due argomenti di output che rappresentano i risultati dell'operazione di lancio dei dadi.Quando il flusso di lavoro viene completato, gli output vengono recuperati nel gestore <xref:System.Activities.WorkflowApplication.Completed%2A>.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#130](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#130)]  
  
 [!code-csharp[CFX_WorkflowApplicationExample#21](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#21)]  
  
> [!NOTE]
>  Gli oggetti <xref:System.Activities.WorkflowApplication> e <xref:System.Activities.WorkflowInvoker> accettano un dizionario di argomenti di input e restituiscono un dizionario di argomenti `out`.Questi parametri, proprietà e valori restituiti del dizionario sono di tipo `IDictionary<string, object>`.L'istanza effettiva della classe di dizionario passata può essere qualsiasi classe che implementa `IDictionary<string, object>`.In questi esempi, viene utilizzato `Dictionary<string, object>`.[!INCLUDE[crabout](../../../includes/crabout-md.md)]i dizionari, vedere <xref:System.Collections.Generic.IDictionary%602> e <xref:System.Collections.Generic.Dictionary%602>.  
  
### Passaggio di dati in un flusso di lavoro in esecuzione tramite i segnalibri  
 I segnalibri consentono a un'attività di attendere passivamente la relativa ripresa, nonché di passare i dati a un'istanza del flusso di lavoro in esecuzione.Se un'attività sta attendendo dei dati, può creare un oggetto <xref:System.Activities.Bookmark> e registrare un metodo callback da chiamare quando l'oggetto <xref:System.Activities.Bookmark> viene ripreso, come mostrato nell'esempio seguente.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
 In caso di esecuzione, l'attività `ReadLine` crea un oggetto <xref:System.Activities.Bookmark>, registra un callback, quindi attende la ripresa dell'oggetto <xref:System.Activities.Bookmark>.Una volta ripresa, l'attività `ReadLine` assegna i dati passati con l'oggetto <xref:System.Activities.Bookmark> al relativo argomento <xref:System.Activities.Activity%601.Result%2A>.In questo esempio viene creato un flusso di lavoro che utilizza l'attività `ReadLine` per rilevare il nome dell'utente e visualizzarlo nella finestra della console.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#22](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#22)]  
  
 Quando l'attività `ReadLine` viene eseguita, crea un oggetto <xref:System.Activities.Bookmark> denominato `UserName` e attende la ripresa del segnalibro.L'host raccoglie i dati desiderati, quindi riprende l'oggetto <xref:System.Activities.Bookmark>.Il flusso di lavoro viene ripreso, ne viene visualizzato il nome, quindi viene completato.  
  
 L'applicazione host può esaminare il flusso di lavoro per determinare se sono disponibili segnalibri attivi.Tale operazione può essere eseguita chiamando il metodo <xref:System.Activities.WorkflowApplication.GetBookmarks%2A> di un'istanza <xref:System.Activities.WorkflowApplication> o esaminando l'oggetto <xref:System.Activities.WorkflowApplicationIdleEventArgs> nel gestore <xref:System.Activities.WorkflowApplication.Idle%2A>.  
  
 L'esempio di codice seguente è simile al precedente, ad eccezione del fatto che i segnalibri attivi vengono enumerati prima che venga ripreso il segnalibro.Il flusso di lavoro viene avviato e, una volta creato l'oggetto <xref:System.Activities.Bookmark> e reso inattivo il flusso di lavoro, viene chiamato il metodo <xref:System.Activities.WorkflowApplication.GetBookmarks%2A>.Quando il flusso di lavoro viene completato, l'output seguente viene visualizzato nella console.  
  
 **Come ti chiami?**   
**BookmarkName: UserName \- OwnerDisplayName: ReadLine**   
**Steve**   
**Ciao, Steve**  [!code-csharp[CFX_WorkflowApplicationExample#14](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#14)]  
  
 Nell'esempio di codice seguente viene esaminato l'oggetto <xref:System.Activities.WorkflowApplicationIdleEventArgs> passato nel gestore <xref:System.Activities.WorkflowApplication.Idle%2A> di un'istanza <xref:System.Activities.WorkflowApplication>.In questo esempio il flusso di lavoro che diventa inattivo dispone di un oggetto <xref:System.Activities.Bookmark> denominato `EnterGuess`, di proprietà di un'attività denominata `ReadInt`.Questo esempio di codice è basato su [Procedura: eseguire un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-run-a-workflow.md) che fa parte dell'[Esercitazione introduttiva](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md).Se il gestore <xref:System.Activities.WorkflowApplication.Idle%2A> nel passaggio indicato viene modificato per contenere il codice da questo esempio, viene visualizzato l'output seguente.  
  
 **BookmarkName: EnterGuess \- OwnerDisplayName: ReadInt** [!code-csharp[CFX_WorkflowApplicationExample#2](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#2)]  
  
## Riepilogo  
 L'oggetto <xref:System.Activities.WorkflowInvoker> rappresenta un modo semplice per richiamare i flussi di lavoro e, sebbene fornisca i metodi per passare i dati all'inizio di un flusso di lavoro ed estrarli da un flusso di lavoro completato, non garantisce scenari più complessi in cui è possibile utilizzare l'oggetto <xref:System.Activities.WorkflowApplication>.