---
title: "Procedura: creare un&#39;attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c09b1e99-21b5-4d96-9c04-ec31db3f4436
caps.latest.revision: 39
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 39
---
# Procedura: creare un&#39;attivit&#224;
Le attività sono l'unità principale del comportamento in [!INCLUDE[wf1](../../../includes/wf1-md.md)].La logica di esecuzione di un'attività può essere implementata nel codice gestito oppure tramite altre attività.In questo argomento viene illustrato come creare due attività.La prima è un'attività semplice che utilizza il codice per implementare la propria logica di esecuzione.L'implementazione della seconda attività viene definita tramite altre attività.Queste attività vengono utilizzate nei seguenti passaggi dell'esercitazione.  
  
> [!NOTE]
>  Per scaricare una versione completa dell'esercitazione, vedere [Windows Workflow Foundation \(WF45\) \- esercitazione introduttiva](http://go.microsoft.com/fwlink/?LinkID=248976).  
  
### Per creare il progetto di libreria di attività  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] e scegliere **Nuovo**, **Progetto** dal menu **File**.  
  
2.  Espandere il nodo **Altri tipi di progetto** nell'elenco **Installato**, **Modelli** e selezionare **Soluzioni di Visual Studio**.  
  
3.  Selezionare **Soluzione vuota** dall'elenco **Soluzioni di Visual Studio**.Assicurarsi che nell'elenco a discesa della versione di .NET Framework sia selezionata l'opzione **.NET Framework 4.5**.Digitare `WF45GettingStartedTutorial` nella casella **Nome**, quindi fare clic su **OK**.  
  
4.  Fare clic con il pulsante destro del mouse su **WF45GettingStartedTutorial** in **Esplora soluzioni** e scegliere **Aggiungi**, **Nuovo progetto**.  
  
    > [!TIP]
    >  Se la finestra **Esplora soluzioni** non è visualizzata, scegliere **Esplora soluzioni** dal menu **Visualizza**.  
  
5.  Nel nodo **Modelli installati** selezionare **Visual C\#**, **Flusso di lavoro** \(oppure **Visual Basic**, **Flusso di lavoro**\).Assicurarsi che nell'elenco a discesa della versione di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sia selezionata l'opzione **.NET Framework 4.5**.Selezionare **Libreria attività** dall'elenco **Flusso di lavoro**.Digitare `NumberGuessWorkflowActivities` nella casella **Nome**, quindi fare clic su **OK**.  
  
    > [!NOTE]
    >  A seconda del linguaggio di programmazione configurato come linguaggio principale in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], il nodo **Visual C\#** o **Visual Basic** può trovarsi sotto il nodo **Altri linguaggi** nel nodo **Installato**.  
  
6.  Fare clic con il pulsante destro del mouse su **Activity1.xaml** in **Esplora soluzioni** e scegliere **Elimina**.Per confermare scegliere **OK**.  
  
### Per creare l'attività ReadInt  
  
1.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
2.  Nel nodo **Installato**, **Elementi comuni**, selezionare **Flusso di lavoro**.Selezionare **Attività codice** dall'elenco **Flusso di lavoro**.  
  
3.  Digitare `ReadInt` nella casella **Nome**, quindi fare clic su **Aggiungi**.  
  
4.  Sostituire la definizione dell'attività `ReadInt` esistente con la definizione seguente.  
  
     [!code-csharp[CFX_WF_GettingStarted#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/readint.cs#1)]
     [!code-vb[CFX_WF_GettingStarted#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/readint.vb#1)]  
  
    > [!NOTE]
    >  L'attività `ReadInt` deriva da <xref:System.Activities.NativeActivity%601> anziché <xref:System.Activities.CodeActivity>, che è l'attività predefinita per il modello di attività codice.L'oggetto <xref:System.Activities.CodeActivity%601> può essere utilizzato se l'attività fornisce un singolo risultato, che viene esposto tramite l'argomento <xref:System.Activities.Activity%601.Result%2A>, ma <xref:System.Activities.CodeActivity%601> non supporta l'utilizzo dei segnalibri, quindi viene utilizzato l'oggetto <xref:System.Activities.NativeActivity%601>.  
  
### Per creare l'attività Prompt  
  
1.  Premere CTRL\+MAIUSC\+B per compilare il progetto.Nella compilazione del progetto, l'attività `ReadInt` in questo progetto può essere utilizzata per compilare l'attività personalizzata tramite questo passaggio.  
  
2.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  
  
3.  Nel nodo **Installato**, **Elementi comuni**, selezionare **Flusso di lavoro**.Selezionare **Attività** dall'elenco **Flusso di lavoro**.  
  
4.  Digitare `Prompt` nella casella **Nome**, quindi fare clic su **Aggiungi**.  
  
5.  Fare doppio clic su **Prompt.xaml** in **Esplora soluzioni** per visualizzarlo nella finestra di progettazione nel caso non sia già visibile.  
  
6.  Fare clic su **Argomenti** nel lato sinistro inferiore dell'ActivityDesigner per visualizzare il riquadro **Argomenti**.  
  
7.  Fare clic su **Crea argomento**.  
  
8.  Digitare `BookmarkName` nella casella **Nome**, selezionare **Interno** dall'elenco a discesa **Direzione**, scegliere **String** dall'elenco a discesa **Tipo di argomento**, quindi premere INVIO per salvare l'argomento.  
  
9. Fare clic su **Crea argomento**.  
  
10. Digitare `Result` nella casella **Nome** che si trova sotto l'argomento `BookmarkName` appena aggiunto, selezionare **Esterno** dall'elenco a discesa **Direzione**, selezionare **Int32** dall'elenco a discesa **Tipo di argomento**, quindi premere INVIO.  
  
11. Fare clic su **Crea argomento**.  
  
12. Digitare `Text` nella casella **Nome**, selezionare **Interno** dall'elenco a discesa **Direzione**, scegliere **String** dall'elenco a discesa **Tipo di argomento**, quindi premere INVIO per salvare l'argomento.  
  
     Questi tre argomenti vengono associati agli argomenti corrispondenti delle attività <xref:System.Activities.Statements.WriteLine> e `ReadInt` aggiunte all'attività `Prompt` nei passaggi seguenti.  
  
13. Fare clic su **Argomenti** nel lato inferiore sinistro dell'ActivityDesigner per chiudere il riquadro **Argomenti**.  
  
14. Trascinare un'attività **Sequence** dalla sezione **Flusso di controllo** della **Casella degli strumenti** e rilasciarla sull'etichetta **Rilasciare l'attività** di ActivityDesigner dell'attività **Prompt**.  
  
    > [!TIP]
    >  Se la finestra **Casella degli strumenti** non è visualizzata, scegliere **Casella degli strumenti** dal menu **Visualizza**.  
  
15. Trascinare un'attività **WriteLine** dalla sezione **Primitive** della **Casella degli strumenti** e rilasciarla sull'etichetta **Rilasciare l'attività** dell'attività **Sequence**.  
  
16. Associare l'argomento **Text** dell'attività **WriteLine** all'argomento **Text** dell'attività **Prompt** digitando `Text` nella casella **Immettere un'espressione VB** o **Immettere un'espressione VB** nella **Finestra Proprietà**, quindi premere il tasto TAB due volte.Ciò consente di chiudere la finestra dei membri dell'elenco IntelliSense e salva il valore della proprietà spostando la selezione dalla proprietà.Questa proprietà può essere impostata anche digitando `Text` nella casella **Immettere un'espressione VB** o **Immettere un'espressione VB** nell'attività stessa.  
  
    > [!TIP]
    >  Se la **Finestra proprietà** non è visualizzata, scegliere **Finestra Proprietà** dal menu **Visualizza**.  
  
17. Trascinare un'attività **ReadInt** dalla sezione **NumberGuessWorkflowActivities** della **Casella degli strumenti** e rilasciarla nell'attività **Sequence** in modo che segua l'attività **WriteLine**.  
  
18. Associare l'argomento **BookmarkName** dell'attività **ReadInt** all'argomento **BookmarkName** dell'attività **Prompt** digitando `BookmarkName` nella casella **Immettere un'espressione VB** a destra dell'argomento **BookmarkName** in **Finestra Proprietà**, quindi premere il tasto TAB due volte per chiudere la finestra dei membri dell'elenco di IntelliSense e salvare la proprietà.  
  
19. Associare l'argomento **Result** dell'attività **ReadInt** all'argomento **Result** dell'attività **Prompt** digitando `Result` nella casella **Immettere un'espressione VB** a destra dell'argomento **Result** in **Finestra Proprietà**, quindi premere il tasto TAB due volte.  
  
20. Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
     Per istruzioni su come creare un flusso di lavoro tramite queste attività, vedere il passaggio successivo dell'esercitazione, [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md).  
  
## Vedere anche  
 <xref:System.Activities.CodeActivity>   
 <xref:System.Activities.NativeActivity%601>   
 [Progettazione e implementazione di attività personalizzate](../../../docs/framework/windows-workflow-foundation//designing-and-implementing-custom-activities.md)   
 [Esercitazione introduttiva](../../../docs/framework/windows-workflow-foundation//getting-started-tutorial.md)   
 [Procedura: creare un flusso di lavoro](../../../docs/framework/windows-workflow-foundation//how-to-create-a-workflow.md)   
 [Utilizzo di ExpressionTextBox in un ActivityDesigner personalizzato](../../../docs/framework/windows-workflow-foundation/samples/using-the-expressiontextbox-in-a-custom-activity-designer.md)