---
title: "Procedura: eseguire un flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f814ff82-fe2b-4614-aebb-b768c3e61179
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# Procedura: eseguire un flusso di lavoro
Questo argomento è una continuazione dell'esercitazione introduttiva di Windows Workflow Foundation e illustra come creare un host di flusso di lavoro ed eseguire il flusso di lavoro definito nell'argomento [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md) precedente.  
  
> [!NOTE]
>  Ogni argomento nell'Esercitazione introduttiva dipende dagli argomenti precedenti. Per completare questo argomento, è necessario completare prima [Procedura: creare un'attività](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md) e [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md).  
  
> [!NOTE]
>  Per scaricare una versione completa dell'esercitazione, vedere [Windows Workflow Foundation \(WF45\) \- esercitazione introduttiva](http://go.microsoft.com/fwlink/?LinkID=248976).  
  
### Per creare il progetto host del flusso di lavoro  
  
1.  Aprire la soluzione dall'argomento [Procedura: creare un'attività](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md) precedente tramite [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sulla soluzione **WF45GettingStartedTutorial** in **Esplora soluzioni** e scegliere **Aggiungi**, **Nuovo progetto**.  
  
    > [!TIP]
    >  Se la finestra **Esplora soluzioni** non è visualizzata, scegliere **Esplora soluzioni** dal menu **Visualizza**.  
  
3.  Nel nodo **Modelli installati** selezionare **Visual C\#**, **Flusso di lavoro** \(oppure **Visual Basic**, **Flusso di lavoro**\).  
  
    > [!NOTE]
    >  A seconda del linguaggio di programmazione configurato come linguaggio principale in Visual Studio, sotto il nodo **Altri linguaggi** del nodo **Installato** viene visualizzato il nodo **Visual C\#** o **Visual Basic**.  
  
     Assicurarsi che nell'elenco a discesa della versione di .NET Framework sia selezionata l'opzione **.NET Framework 4.5**. Selezionare **Applicazione console flusso di lavoro** dall'elenco **Flusso di lavoro**. Digitare `NumberGuessWorkflowHost` nella casella **Nome**, quindi fare clic su **OK**. In questo modo verrà creata un'applicazione flusso di lavoro iniziale con supporto per l'hosting del flusso di lavoro di base. Il codice host di base viene modificato e usato per eseguire l'applicazione flusso di lavoro.  
  
4.  Fare clic con il pulsante destro del mouse sul progetto **NumberGuessWorkflowHost** appena aggiunto in **Esplora soluzioni** e selezionare **Aggiungi riferimento**. Scegliere **Soluzione** nell'elenco **Aggiungi riferimento**, selezionare la casella di controllo accanto a **NumberGuessWorkflowActivities**, quindi scegliere **OK**.  
  
5.  Fare clic con il pulsante destro del mouse su **Workflow1.xaml** in **Esplora soluzioni** e scegliere **Elimina**. Per confermare scegliere **OK**.  
  
### Per modificare il codice host del flusso di lavoro  
  
1.  Fare doppio clic su **Program.cs** o **Module1.vb** in **Esplora soluzioni** per visualizzare il codice.  
  
    > [!TIP]
    >  Se la finestra **Esplora soluzioni** non è visualizzata, scegliere **Esplora soluzioni** dal menu **Visualizza**.  
  
     Poiché questo progetto viene creato usando il modello  **Applicazione console flusso di lavoro**, **Program.cs** o **Module1.vb** contiene il seguente codice host del flusso di lavoro di base.  
  
    ```vb  
    ' Create and cache the workflow definition  
    Activity workflow1 = new Workflow1()  
    WorkflowInvoker.Invoke(workflow1)  
    ```  
  
    ```csharp  
    // Create and cache the workflow definition  
    Activity workflow1 = new Workflow1();  
    WorkflowInvoker.Invoke(workflow1);  
    ```  
  
     Questo codice host generato usa <xref:System.Activities.WorkflowInvoker>.<xref:System.Activities.WorkflowInvoker> offre un modo semplice per richiamare un flusso di lavoro come se fosse una chiamata a un metodo e può essere usato solo per i flussi di lavoro che non usano la persistenza.<xref:System.Activities.WorkflowApplication> fornisce un modello più dettagliato per l'esecuzione di flussi di lavoro che include la notifica degli eventi del ciclo di vita, il controllo di esecuzione, la ripresa del segnalibro e la persistenza. In questo esempio vengono usati i segnalibri e l'oggetto <xref:System.Activities.WorkflowApplication> viene usato per ospitare il flusso di lavoro. Aggiungere la seguente istruzione `using` o **Imports** all'inizio del file **Program.cs** o **Module1.vb** dopo le istruzioni **using** o **Imports** esistenti.  
  
    ```vb  
    Imports NumberGuessWorkflowActivities  
    Imports System.Threading  
    ```  
  
    ```csharp  
    using NumberGuessWorkflowActivities;  
    using System.Threading;  
    ```  
  
     Sostituire le righe di codice che usano l'oggetto <xref:System.Activities.WorkflowInvoker> con il seguente codice host <xref:System.Activities.WorkflowApplication> di base. In questo codice host di esempio vengono illustrati i passaggi di base per ospitare e richiamare un flusso di lavoro, ma non è contenuta ancora la funzionalità per eseguire correttamente il flusso di lavoro da questo argomento. Nei seguenti passaggi il codice di base viene modificato e vengono aggiunte funzionalità aggiuntive fino a quando l'applicazione non viene completata.  
  
    > [!NOTE]
    >  Sostituire `Workflow1` in questi esempi con `FlowchartNumberGuessWorkflow`, `SequentialNumberGuessWorkflow` o `StateMachineNumberGuessWorkflow`, a seconda del flusso di lavoro completato nel passaggio precedente [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md). Se non si sostituisce `Workflow1`, si verificheranno degli errori di compilazione quando si tenterà di compilare o eseguire il flusso di lavoro.  
  
     [!code-csharp[CFX_WF_GettingStarted#4](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/extrasnippets.cs#4)]
     [!code-vb[CFX_WF_GettingStarted#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/extrasnippets.vb#4)]  
  
     Questo codice crea un oggetto <xref:System.Activities.WorkflowApplication>, sottoscrive tre eventi del ciclo di vita del flusso di lavoro, avvia il flusso di lavoro con una chiamata al metodo <xref:System.Activities.WorkflowApplication.Run%2A>, quindi attende il completamento del flusso di lavoro. Quando il flusso di lavoro viene completato, l'oggetto <xref:System.Threading.AutoResetEvent> viene impostato e l'applicazione host viene completata.  
  
### Per impostare gli argomenti di input di un flusso di lavoro  
  
1.  Aggiungere la seguente istruzione all'inizio del file **Program.cs** o **Module1.vb** dopo le istruzioni `using` o `Imports` esistenti.  
  
     [!code-csharp[CFX_WF_GettingStarted#5](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#5)]
     [!code-vb[CFX_WF_GettingStarted#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#5)]  
  
2.  Sostituire la riga di codice che crea il nuovo oggetto <xref:System.Activities.WorkflowApplication> con il codice seguente che crea e passa un dizionario di parametri al flusso di lavoro quando viene creato.  
  
    > [!NOTE]
    >  Sostituire `Workflow1` in questi esempi con `FlowchartNumberGuessWorkflow`, `SequentialNumberGuessWorkflow` o `StateMachineNumberGuessWorkflow`, a seconda del flusso di lavoro completato nel passaggio precedente [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md). Se non si sostituisce `Workflow1`, si verificheranno degli errori di compilazione quando si tenterà di compilare o eseguire il flusso di lavoro.  
  
     [!code-csharp[CFX_WF_GettingStarted#6](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#6)]
     [!code-vb[CFX_WF_GettingStarted#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#6)]  
  
     Questo dizionario contiene un elemento con una chiave di `MaxNumber`. Le chiavi nel dizionario di input corrispondono agli argomenti di input sull'attività radice del flusso di lavoro.`MaxNumber` viene usato dal flusso di lavoro per determinare il limite superiore del numero generato casualmente.  
  
### Per recuperare gli argomenti di output di un flusso di lavoro  
  
1.  Modificare il gestore <xref:System.Activities.WorkflowApplication.Completed%2A> per recuperare e visualizzare il numero di turni usati dal flusso di lavoro.  
  
     [!code-csharp[CFX_WF_GettingStarted#7](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#7)]
     [!code-vb[CFX_WF_GettingStarted#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#7)]  
  
### Per riprendere un segnalibro  
  
1.  Aggiungere il seguente codice all'inizio del metodo `Main` subito dopo la dichiarazione <xref:System.Threading.AutoResetEvent> esistente.  
  
     [!code-csharp[CFX_WF_GettingStarted#8](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#8)]
     [!code-vb[CFX_WF_GettingStarted#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#8)]  
  
2.  Aggiungere il seguente gestore <xref:System.Activities.WorkflowApplication.Idle%2A> subito dopo i tre gestori del ciclo di vita del flusso di lavoro esistenti in `Main`.  
  
     [!code-csharp[CFX_WF_GettingStarted#9](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#9)]
     [!code-vb[CFX_WF_GettingStarted#9](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#9)]  
  
     Ogni volta che il flusso di lavoro diventa inattivo nell'attesa del successivo tentativo, questo gestore viene chiamato e l'oggetto `idleAction`<xref:System.Threading.AutoResetEvent> viene impostato. Il codice nel passaggio seguente usa `idleEvent` e `syncEvent` per determinare se il flusso di lavoro è in attesa della prossimo tentativo o viene completato.  
  
    > [!NOTE]
    >  In questo esempio l'applicazione host usa eventi di reimpostazione automatica nei gestori <xref:System.Activities.WorkflowApplication.Completed%2A> e <xref:System.Activities.WorkflowApplication.Idle%2A> per sincronizzare l'applicazione host con lo stato di avanzamento del flusso di lavoro. Non è necessario bloccare e attendere l'inattività del flusso di lavoro prima di riprendere un segnalibro, ma in questo esempio gli eventi di sincronizzazione sono obbligatori affinché l'host sappia se il flusso di lavoro viene completato o se è in attesa di più input dell'utente usando l'oggetto <xref:System.Activities.Bookmark>.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [Segnalibri](../../../docs/framework/windows-workflow-foundation//bookmarks.md).  
  
3.  Rimuovere la chiamata al metodo `WaitOne` e sostituirla con codice per raccogliere l'input dell'utente e riprendere l'oggetto <xref:System.Activities.Bookmark>.  
  
     Rimuovere la seguente riga di codice.  
  
     [!code-csharp[CFX_WF_GettingStarted#10](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/extrasnippets.cs#10)]
     [!code-vb[CFX_WF_GettingStarted#10](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/extrasnippets.vb#10)]  
  
     Sostituirla con l'esempio seguente.  
  
     [!code-csharp[CFX_WF_GettingStarted#11](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#11)]
     [!code-vb[CFX_WF_GettingStarted#11](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#11)]  
  
##  <a name="BKMK_ToRunTheApplication"></a> Per compilare ed eseguire l'applicazione  
  
1.  Fare clic con il pulsante destro del mouse su **NumberGuessWorkflowHost** in **Esplora soluzioni** e selezionare **Imposta come progetto di avvio**.  
  
2.  Premere CTRL\+F5 per compilare ed eseguire l'applicazione. Provare a determinare il numero con meno tentativi possibili.  
  
     Per provare l'applicazione con uno degli altri stili del flusso di lavoro, sostituire `Workflow1` nel codice che crea <xref:System.Activities.WorkflowApplication> con `FlowchartNumberGuessWorkflow`, `SequentialNumberGuessWorkflow` o `StateMachineNumberGuessWorkflow`, a seconda dello stile del flusso di lavoro desiderato.  
  
     [!code-csharp[CFX_WF_GettingStarted#6](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#6)]
     [!code-vb[CFX_WF_GettingStarted#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#6)]  
  
     Per istruzioni sull'aggiunta di persistenza a un'applicazione flusso di lavoro, vedere l'argomento successivo, [Procedura: creare ed eseguire un flusso di lavoro con esecuzione prolungata](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md).  
  
## Esempio  
 L'esempio seguente è l'elenco di codice per il metodo `Main`.  
  
> [!NOTE]
>  Sostituire `Workflow1` in questi esempi con `FlowchartNumberGuessWorkflow`, `SequentialNumberGuessWorkflow` o `StateMachineNumberGuessWorkflow`, a seconda del flusso di lavoro completato nel passaggio precedente [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md). Se non si sostituisce `Workflow1`, si verificheranno degli errori di compilazione quando si tenterà di compilare o eseguire il flusso di lavoro.  
  
 [!code-csharp[CFX_WF_GettingStarted#12](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#12)]
 [!code-vb[CFX_WF_GettingStarted#12](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#12)]  
  
## Vedere anche  
 <xref:System.Activities.WorkflowApplication>   
 <xref:System.Activities.Bookmark>   
 [Programmazione di Windows Workflow Foundation](../../../docs/framework/windows-workflow-foundation//programming.md)   
 [Esercitazione introduttiva](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)   
 [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)   
 [Procedura: creare ed eseguire un flusso di lavoro con esecuzione prolungata](../../../docs/framework/windows-workflow-foundation//how-to-create-and-run-a-long-running-workflow.md)   
 [Attesa per l'input in un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//waiting-for-input-in-a-workflow.md)   
 [Hosting dei flussi di lavoro](../../../docs/framework/windows-workflow-foundation//hosting-workflows.md)