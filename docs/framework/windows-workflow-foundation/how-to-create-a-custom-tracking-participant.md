---
title: "Procedura: creare un partecipante del rilevamento personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b612c7e-2381-4a7c-b07a-77030415f2a3
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: creare un partecipante del rilevamento personalizzato
Il rilevamento del flusso di lavoro fornisce la visibilità nello stato dell'esecuzione del flusso di lavoro.Il runtime del flusso di lavoro genera i record di rilevamento che descrivono gli eventi del ciclo di vita di flusso del lavoro, gli eventi del ciclo di vita delle attività, le riprese dei segnalibri e gli errori.Tali record di rilevamento vengono utilizzati dai partecipanti del rilevamento.In [!INCLUDE[wf](../../../includes/wf-md.md)] viene fornito un partecipante del rilevamento standard che scrive record di rilevamento come eventi ETW \(Event Tracing for Windows\).Se tale partecipante non soddisfa i propri requisiti, è anche possibile scrivere un partecipante del rilevamento personalizzato.In questo passaggio dell'esercitazione viene illustrato come creare un profilo di rilevamento e un partecipante di rilevamento personalizzati che acquisiscono l'output delle attività di `WriteLine` per renderlo visibile all'utente.  
  
> [!NOTE]
>  Ogni argomento nell'Esercitazione introduttiva dipende dagli argomenti precedenti.Per completare questo argomento, è necessario completare prima gli argomenti precedenti.Per scaricare una versione completa o visualizzare una procedura dettagliata dell'esercitazione in un video, vedere la pagina relativa all'[esercitazione introduttiva di Windows Workflow Foundation \(WF45\)](http://go.microsoft.com/fwlink/?LinkID=248976).  
  
## In questo argomento  
  
-   [Per creare un partecipante di rilevamento personalizzato](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md#BKMK_CustomTrackingParticipant)  
  
-   [Per creare il profilo di rilevamento e registrare il partecipante di rilevamento](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md#BKMK_TrackingProfile)  
  
-   [Per visualizzare le informazioni di rilevamento](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md#BKMK_DisplayTracking)  
  
-   [Per compilare ed eseguire l'applicazione](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md#BKMK_BuildAndRun)  
  
###  <a name="BKMK_CustomTrackingParticipant"></a> Per creare un partecipante di rilevamento personalizzato  
  
1.  Fare clic con il pulsante destro del mouse su **NumberGuessWorkflowHost** in **Esplora soluzioni** e scegliere **Aggiungi**, **Classe**.Digitare `StatusTrackingParticipant` nella casella **Nome**, quindi fare clic su **Aggiungi**.  
  
2.  Aggiungere le seguenti istruzioni `using` \(o `Imports`\) nella parte superiore del file con le altre istruzioni `using` \(o `Imports`\).  
  
    ```vb  
    Imports System.Activities.Tracking  
    Imports System.IO  
    ```  
  
    ```csharp  
    using System.Activities.Tracking;  
    using System.IO;  
    ```  
  
3.  Modificare la classe `StatusTrackingParticipant` per fare in modo che erediti da `TrackingParticipant`.  
  
    ```vb  
    Public Class StatusTrackingParticipant  
        Inherits TrackingParticipant  
  
    End Class  
    ```  
  
    ```csharp  
    class StatusTrackingParticipant : TrackingParticipant  
    {  
    }  
    ```  
  
4.  Aggiungere il seguente override del metodo `Track`.Esistono vari tipi di record di rilevamento.In questo caso, si utilizza l'output delle attività di `WriteLine` contenute nei record di rilevamento delle attività.Se `TrackingRecord` è un `ActivityTrackingRecord` di un'attività `WriteLine`, `Text` di `WriteLine` viene aggiunto a un file denominato dopo l'elemento `InstanceId` del flusso di lavoro.In questa esercitazione, il file viene salvato nella cartella corrente dell'applicazione host.  
  
    ```vb  
    Protected Overrides Sub Track(record As TrackingRecord, timeout As TimeSpan)  
        Dim asr As ActivityStateRecord = TryCast(record, ActivityStateRecord)  
  
        If Not asr Is Nothing Then  
            If asr.State = ActivityStates.Executing And _  
            asr.Activity.TypeName = "System.Activities.Statements.WriteLine" Then  
  
                'Append the WriteLine output to the tracking  
                'file for this instance.  
                Using writer As StreamWriter = File.AppendText(record.InstanceId.ToString())  
                    writer.WriteLine(asr.Arguments("Text"))  
                    writer.Close()  
                End Using  
            End If  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    protected override void Track(TrackingRecord record, TimeSpan timeout)  
    {  
        ActivityStateRecord asr = record as ActivityStateRecord;  
  
        if (asr != null)  
        {  
            if (asr.State == ActivityStates.Executing &&  
                asr.Activity.TypeName == "System.Activities.Statements.WriteLine")  
            {  
                // Append the WriteLine output to the tracking  
                // file for this instance  
                using (StreamWriter writer = File.AppendText(record.InstanceId.ToString()))  
                {  
                    writer.WriteLine(asr.Arguments["Text"]);  
                    writer.Close();  
                }  
            }  
        }  
    }  
    ```  
  
     Se non è specificato alcun profilo di rilevamento, viene utilizzato il profilo di rilevamento predefinito.Quando viene utilizzato il profilo di rilevamento predefinito, i record di rilevamento vengono generati per tutti gli elementi `ActivityStates`.Dal momento che è necessario acquisire il testo solo una volta durante il ciclo di vita dell'attività `WriteLine`, si estrae solo il testo dello stato `ActivityStates.Executing`.In [Per creare il profilo di rilevamento e registrare il partecipante di rilevamento](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-tracking-participant.md#BKMK_TrackingProfile), viene creato un profilo di rilevamento che specifica che vengono generati solo i record di rilevamento `ActivityStates.Executing` di `WriteLine`.  
  
###  <a name="BKMK_TrackingProfile"></a> Per creare il profilo di rilevamento e registrare il partecipante di rilevamento  
  
1.  Fare clic con il pulsante destro del mouse su **WorkflowHostForm** in **Esplora soluzioni**, quindi scegliere **Visualizza codice**.  
  
2.  Aggiungere la seguente istruzione `using` \(o `Imports`\) nella parte superiore del file con le altre istruzioni `using` \(o `Imports`\).  
  
    ```vb  
    Imports System.Activities.Tracking  
    ```  
  
    ```csharp  
    using System.Activities.Tracking;  
    ```  
  
3.  Aggiungere il codice seguente a `ConfigureWorkflowApplication` immediatamente dopo il codice che aggiunge `StringWriter` alle estensioni del flusso di lavoro e prima dei gestori del ciclo di vita del flusso di lavoro.  
  
    ```vb  
    'Add the custom tracking participant with a tracking profile  
    'that only emits tracking records for WriteLine activities.  
    Dim query As New ActivityStateQuery()  
    query.ActivityName = "WriteLine"  
    query.States.Add(ActivityStates.Executing)  
    query.Arguments.Add("Text")  
  
    Dim profile As New TrackingProfile()  
    profile.Queries.Add(query)  
  
    Dim stp As New StatusTrackingParticipant()  
    stp.TrackingProfile = profile  
  
    wfApp.Extensions.Add(stp)  
    ```  
  
    ```csharp  
    // Add the custom tracking participant with a tracking profile  
    // that only emits tracking records for WriteLine activities.  
    StatusTrackingParticipant stp = new StatusTrackingParticipant  
    {  
        TrackingProfile = new TrackingProfile  
        {  
            Queries =   
            {  
                new ActivityStateQuery  
                {  
                    ActivityName = "WriteLine",  
                    States = { ActivityStates.Executing },  
                    Arguments = { "Text" }  
                }  
            }  
        }  
    };  
  
    wfApp.Extensions.Add(stp);  
    ```  
  
     Questo profilo di rilevamento specifica che vengono generati solo i record di stato dell'attività per le attività `WriteLine` nello stato `Executing` per il partecipante di rilevamento personalizzato.  
  
     Dopo aver aggiunto il codice, l'inizio di `ConfigureWorkflowApplication` risulterà analogo al seguente esempio.  
  
    ```vb  
    Private Sub ConfigureWorkflowApplication(wfApp As WorkflowApplication)  
        'Configure the persistence store.  
        wfApp.InstanceStore = store  
  
        'Add a StringWriter to the extensions. This captures the output  
        'from the WriteLine activities so we can display it in the form.  
        Dim sw As New StringWriter()  
        wfApp.Extensions.Add(sw)  
  
        'Add the custom tracking participant with a tracking profile  
        'that only emits tracking records for WriteLine activities.  
        Dim query As New ActivityStateQuery()  
        query.ActivityName = "WriteLine"  
        query.States.Add(ActivityStates.Executing)  
        query.Arguments.Add("Text")  
  
        Dim profile As New TrackingProfile()  
        profile.Queries.Add(query)  
  
        Dim stp As New StatusTrackingParticipant()  
        stp.TrackingProfile = profile  
  
        wfApp.Extensions.Add(stp)  
  
        'Workflow lifecycle handlers...  
    ```  
  
    ```csharp  
    private void ConfigureWorkflowApplication(WorkflowApplication wfApp)  
    {  
        // Configure the persistence store.  
        wfApp.InstanceStore = store;  
  
        // Add a StringWriter to the extensions. This captures the output  
        // from the WriteLine activities so we can display it in the form.  
        StringWriter sw = new StringWriter();  
        wfApp.Extensions.Add(sw);  
  
        // Add the custom tracking participant with a tracking profile  
        // that only emits tracking records for WriteLine activities.  
        StatusTrackingParticipant stp = new StatusTrackingParticipant  
        {  
            TrackingProfile = new TrackingProfile  
            {  
                Queries =   
                {  
                    new ActivityStateQuery  
                    {  
                        ActivityName = "WriteLine",  
                        States = { ActivityStates.Executing },  
                        Arguments = { "Text" }  
                    }  
                }  
            }  
        };  
  
        wfApp.Extensions.Add(stp);  
  
        // Workflow lifecycle handlers...  
    ```  
  
###  <a name="BKMK_DisplayTracking"></a> Per visualizzare le informazioni di rilevamento  
  
1.  Fare clic con il pulsante destro del mouse su **WorkflowHostForm** in **Esplora soluzioni**, quindi scegliere **Visualizza codice**.  
  
2.  Nel gestore `InstanceId_SelectedIndexChanged`, aggiungere il codice seguente subito dopo il codice che cancella la finestra di stato.  
  
    ```vb  
    'If there is tracking data for this workflow, display it  
    'in the status window.  
    If File.Exists(WorkflowInstanceId.ToString()) Then  
        Dim status As String = File.ReadAllText(WorkflowInstanceId.ToString())  
        UpdateStatus(status)  
    End If  
    ```  
  
    ```csharp  
    // If there is tracking data for this workflow, display it  
    // in the status window.  
    if (File.Exists(WorkflowInstanceId.ToString()))  
    {  
        string status = File.ReadAllText(WorkflowInstanceId.ToString());  
        UpdateStatus(status);  
    }  
    ```  
  
     Quando viene selezionato un nuovo flusso di lavoro nell'elenco dei flusso di lavoro, i record di rilevamento del flusso di lavoro vengono caricati e visualizzati nella finestra di stato.Nell'esempio seguente viene mostrato il gestore `InstanceId_SelectedIndexChanged` completato.  
  
    ```vb  
    Private Sub InstanceId_SelectedIndexChanged(sender As Object, e As EventArgs) Handles InstanceId.SelectedIndexChanged  
        If InstanceId.SelectedIndex = -1 Then  
            Return  
        End If  
  
        'Clear the status window.  
        WorkflowStatus.Clear()  
  
        'If there is tracking data for this workflow, display it  
        'in the status window.  
        If File.Exists(WorkflowInstanceId.ToString()) Then  
            Dim status As String = File.ReadAllText(WorkflowInstanceId.ToString())  
            UpdateStatus(status)  
        End If  
  
        'Get the workflow version and display it.  
        'If the workflow is just starting then this info will not  
        'be available in the persistence store so do not try and retrieve it.  
        If Not WorkflowStarting Then  
            Dim instance As WorkflowApplicationInstance = _  
                WorkflowApplication.GetInstance(WorkflowInstanceId, store)  
  
            WorkflowVersion.Text = _  
                WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity)  
  
            'Unload the instance.  
            instance.Abandon()  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    private void InstanceId_SelectedIndexChanged(object sender, EventArgs e)  
    {  
        if (InstanceId.SelectedIndex == -1)  
        {  
            return;  
        }  
  
        // Clear the status window.  
        WorkflowStatus.Clear();  
  
        // If there is tracking data for this workflow, display it  
        // in the status window.  
        if (File.Exists(WorkflowInstanceId.ToString()))  
        {  
            string status = File.ReadAllText(WorkflowInstanceId.ToString());  
            UpdateStatus(status);  
        }  
  
        // Get the workflow version and display it.  
        // If the workflow is just starting then this info will not  
        // be available in the persistence store so do not try and retrieve it.  
        if (!WorkflowStarting)  
        {  
            WorkflowApplicationInstance instance =  
                WorkflowApplication.GetInstance(this.WorkflowInstanceId, store);  
  
            WorkflowVersion.Text =  
                WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity);  
  
            // Unload the instance.  
            instance.Abandon();  
        }  
    }  
  
    ```  
  
###  <a name="BKMK_BuildAndRun"></a> Per compilare ed eseguire l'applicazione  
  
1.  Premere CTRL\+MAIUSC\+B per compilare l'applicazione.  
  
2.  Premere CTRL\+F5 per avviare l'applicazione.  
  
3.  Selezionare un intervallo per il gioco per determinare un numero e il tipo di flusso di lavoro da avviare, quindi fare clic su **Nuova partita**.Immettere un tentativo nella casella **Guess**, quindi fare clic su **Go** per inviare il tentativo.Si noti che lo stato del flusso di lavoro viene visualizzato nella finestra di stato.Questo output viene acquisito dalle attività `WriteLine`.Passare a un altro flusso di lavoro selezionandone uno dalla casella combinata **ID istanza flusso di lavoro**. Lo stato del flusso di lavoro corrente viene rimosso.Passare di nuovo al flusso di lavoro precedente. Notare che lo stato viene ripristinato, in modo simile all'esempio seguente.  
  
    > [!NOTE]
    >  Se si passa a un flusso di lavoro che è stato avviato prima dell'abilitazione del rilevamento non viene visualizzato alcuno stato.Tuttavia se si creano tentativi aggiuntivi, lo stato viene salvato in quanto il rilevamento viene così abilitato.  
  
 **Please enter a number between 1 and 10**   
**Your guess is too high.**   
**Please enter a number between 1 and 10**    
    > [!NOTE]
    >  Queste informazioni sono utili per la scelta dell'intervallo del numero casuale, ma non contiene alcuna informazione sui tentativi effettuati in precedenza.Questa informazione è contenuta nel prossimo passaggio, [Procedura: ospitare più versioni di un flusso di lavoro side\-by\-side](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md).  
  
     Annotare l'ID istanza del flusso di lavoro e giocare fino al completamento.  
  
4.  Aprire Esplora risorse e passare alla cartella **NumberGuessWorkflowHost\\bin\\debug** \(o **bin\\release** a seconda delle impostazioni del progetto\).Si noti che oltre ai file eseguibili di progetto, sono presenti file con nomi file GUID.Identificare quello corrispondente all'ID istanza del flusso di lavoro dal flusso di lavoro completato nel passaggio precedente e aprirlo in Blocco Note.Le informazioni sul rilevamento contengono dati simili al seguente esempio.  
  
 **Please enter a number between 1 and 10**   
**Your guess is too high.**   
**Please enter a number between 1 and 10**   
**Your guess is too high.**   
**Please enter a number between 1 and 10**      Oltre all'assenza dei tentativi dell'utente, questi dati di rilevamento non contengono informazioni sul tentativo finale del flusso di lavoro.Ciò accade perché le informazioni di rilevamento sono costituite solo dall'output di `WriteLine` restituito dal flusso di lavoro e il messaggio finale visualizzato viene in tal modo creato dal gestore `Completed` dopo il completamento del flusso di lavoro.Il passaggio successivo dell'esercitazione, [Procedura: ospitare più versioni di un flusso di lavoro side\-by\-side](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md), le attività `WriteLine` esistenti vengono modificate per visualizzare i tentativi dell'utente e viene aggiunta un'altra attività `WriteLine` che visualizza i risultati finali.Una volta integrate tali modifiche, in [Procedura: ospitare più versioni di un flusso di lavoro side\-by\-side](../../../docs/framework/windows-workflow-foundation//how-to-host-multiple-versions-of-a-workflow-side-by-side.md) viene illustrato come ospitare più versioni di un flusso di lavoro contemporaneamente.