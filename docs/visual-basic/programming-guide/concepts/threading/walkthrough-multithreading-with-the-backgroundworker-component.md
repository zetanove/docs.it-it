---
title: Multithreading con il componente BackgroundWorker (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: e4cd9b2a-f924-470e-a16e-50274709b40e
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3686eb230349876f6cfffd2ad94ed1f547779ab1
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-multithreading-with-the-backgroundworker-component-visual-basic"></a>Procedura dettagliata: Multithreading con il componente BackgroundWorker (Visual Basic)
Questa procedura dettagliata viene illustrato come creare un'applicazione Windows Form con multithreading che cerca un file di testo per le occorrenze di una parola. Viene illustrato come:  
  
-   Definizione di una classe con un metodo che può essere chiamato dal <xref:System.ComponentModel.BackgroundWorker>component.</xref:System.ComponentModel.BackgroundWorker>  
  
-   Gestione degli eventi generati dal <xref:System.ComponentModel.BackgroundWorker>component.</xref:System.ComponentModel.BackgroundWorker>  
  
-   Avvio di un <xref:System.ComponentModel.BackgroundWorker>componente per l'esecuzione di un metodo.</xref:System.ComponentModel.BackgroundWorker>  
  
-   Implementazione di un `Cancel` pulsante che consente di arrestare il <xref:System.ComponentModel.BackgroundWorker>component.</xref:System.ComponentModel.BackgroundWorker>  
  
### <a name="to-create-the-user-interface"></a>Per creare l'interfaccia utente  
  
1.  Aprire un nuovo progetto applicazione Windows Form di Visual Basic e creare un form denominato `Form1`.  
  
2.  Aggiungere due pulsanti e quattro caselle di testo per `Form1`.  
  
3.  Denominare gli oggetti come illustrato nella tabella seguente.  
  
    |Oggetto|Proprietà|Impostazione|  
    |------------|--------------|-------------|  
    |Primo pulsante|`Name`, `Text`|Inizio, avvio|  
    |Secondo pulsante|`Name`, `Text`|Annulla, Annulla|  
    |Prima casella di testo|`Name`, `Text`|SourceFile, ""|  
    |Seconda casella di testo|`Name`, `Text`|CompareString, ""|  
    |Terza casella di testo|`Name`, `Text`|WordsCounted, "0"|  
    |Quarta casella di testo|`Name`, `Text`|LinesCounted, "0"|  
  
4.  Aggiungere un'etichetta accanto a ciascuna casella di testo. Impostare il `Text` proprietà per ogni etichetta, come illustrato nella tabella seguente.  
  
    |Oggetto|Proprietà|Impostazione|  
    |------------|--------------|-------------|  
    |Prima etichetta|`Text`|File di origine|  
    |Seconda etichetta|`Text`|Confronto di stringhe|  
    |Terza etichetta|`Text`|Numero di termini corrispondenti|  
    |Quarta etichetta|`Text`|Conteggiata righe|  
  
### <a name="to-create-a-backgroundworker-component-and-subscribe-to-its-events"></a>Per creare un componente BackgroundWorker e sottoscrivere gli eventi  
  
1.  Aggiungere un <xref:System.ComponentModel.BackgroundWorker>componente il **componenti** sezione il **della casella degli strumenti** al form.</xref:System.ComponentModel.BackgroundWorker> Verrà visualizzato nella barra dei componenti del form.  
  
2.  Impostare le proprietà seguenti per l'oggetto BackgroundWorker1.  
  
    |Proprietà|Impostazione|  
    |--------------|-------------|  
    |`WorkerReportsProgress`|True|  
    |`WorkerSupportsCancellation`|True|  
  
### <a name="to-define-the-method-that-will-run-on-a-separate-thread"></a>Per definire il metodo che verrà eseguito in un thread separato  
  
1.  Dal **progetto** menu, scegliere **Aggiungi classe** per aggiungere una classe al progetto. Il **Aggiungi nuovo elemento** viene visualizzata la finestra di dialogo.  
  
2.  Selezionare **classe** nella finestra dei modelli e immettere `Words.vb` nel campo nome.  
  
3.  Fare clic su **Aggiungi**. La `Words` classe viene visualizzata.  
  
4.  Aggiungere il codice seguente alla classe `Words` :  
  
    ```vb  
    Public Class Words  
        ' Object to store the current state, for passing to the caller.  
        Public Class CurrentState  
            Public LinesCounted As Integer  
            Public WordsMatched As Integer  
        End Class  
  
        Public SourceFile As String  
        Public CompareString As String  
        Private WordCount As Integer = 0  
        Private LinesCounted As Integer = 0  
  
        Public Sub CountWords(  
            ByVal worker As System.ComponentModel.BackgroundWorker,  
            ByVal e As System.ComponentModel.DoWorkEventArgs  
        )  
            ' Initialize the variables.  
            Dim state As New CurrentState  
            Dim line = ""  
            Dim elapsedTime = 20  
            Dim lastReportDateTime = Now  
  
            If CompareString Is Nothing OrElse  
               CompareString = System.String.Empty Then  
  
               Throw New Exception("CompareString not specified.")  
            End If  
  
            Using myStream As New System.IO.StreamReader(SourceFile)  
  
                ' Process lines while there are lines remaining in the file.  
                Do While Not myStream.EndOfStream  
                    If worker.CancellationPending Then  
                        e.Cancel = True  
                        Exit Do  
                    Else  
                        line = myStream.ReadLine  
                        WordCount += CountInString(line, CompareString)  
                        LinesCounted += 1  
  
                        ' Raise an event so the form can monitor progress.  
                        If Now > lastReportDateTime.AddMilliseconds(elapsedTime) Then  
                            state.LinesCounted = LinesCounted  
                            state.WordsMatched = WordCount  
                            worker.ReportProgress(0, state)  
                            lastReportDateTime = Now  
                        End If  
  
                        ' Uncomment for testing.  
                        'System.Threading.Thread.Sleep(5)  
                    End If  
                Loop  
  
                ' Report the final count values.  
                state.LinesCounted = LinesCounted  
                state.WordsMatched = WordCount  
                worker.ReportProgress(0, state)  
            End Using  
        End Sub  
  
        Private Function CountInString(  
            ByVal SourceString As String,  
            ByVal CompareString As String  
        ) As Integer  
            ' This function counts the number of times  
            ' a word is found in a line.  
            If SourceString Is Nothing Then  
                Return 0  
            End If  
  
            Dim EscapedCompareString =  
                System.Text.RegularExpressions.Regex.Escape(CompareString)  
  
            ' To count all occurrences of the string, even within words, remove  
            ' both instances of "\b".  
            Dim regex As New System.Text.RegularExpressions.Regex(  
                "\b" + EscapedCompareString + "\b",  
                System.Text.RegularExpressions.RegexOptions.IgnoreCase)  
  
            Dim matches As System.Text.RegularExpressions.MatchCollection  
            matches = regex.Matches(SourceString)  
            Return matches.Count  
        End Function  
    End Class  
    ```  
  
### <a name="to-handle-events-from-the-thread"></a>Per gestire gli eventi dal thread  
  
-   Aggiungere i gestori eventi seguenti al form principale:  
  
    ```vb  
    Private Sub BackgroundWorker1_RunWorkerCompleted(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.RunWorkerCompletedEventArgs  
      ) Handles BackgroundWorker1.RunWorkerCompleted  
  
        ' This event handler is called when the background thread finishes.  
        ' This method runs on the main thread.  
        If e.Error IsNot Nothing Then  
            MessageBox.Show("Error: " & e.Error.Message)  
        ElseIf e.Cancelled Then  
            MessageBox.Show("Word counting canceled.")  
        Else  
            MessageBox.Show("Finished counting words.")  
        End If  
    End Sub  
  
    Private Sub BackgroundWorker1_ProgressChanged(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.ProgressChangedEventArgs  
      ) Handles BackgroundWorker1.ProgressChanged  
  
        ' This method runs on the main thread.  
        Dim state As Words.CurrentState =   
            CType(e.UserState, Words.CurrentState)  
        Me.LinesCounted.Text = state.LinesCounted.ToString  
        Me.WordsCounted.Text = state.WordsMatched.ToString  
    End Sub  
    ```  
  
### <a name="to-start-and-call-a-new-thread-that-runs-the-wordcount-method"></a>Per avviare e chiamare un nuovo thread che esegue il metodo WordCount  
  
1.  Aggiungere le seguenti procedure per il programma:  
  
    ```vb  
    Private Sub BackgroundWorker1_DoWork(   
        ByVal sender As Object,   
        ByVal e As System.ComponentModel.DoWorkEventArgs  
      ) Handles BackgroundWorker1.DoWork  
  
        ' This event handler is where the actual work is done.  
        ' This method runs on the background thread.  
  
        ' Get the BackgroundWorker object that raised this event.  
        Dim worker As System.ComponentModel.BackgroundWorker  
        worker = CType(sender, System.ComponentModel.BackgroundWorker)  
  
        ' Get the Words object and call the main method.  
        Dim WC As Words = CType(e.Argument, Words)  
        WC.CountWords(worker, e)  
    End Sub  
  
    Sub StartThread()  
        ' This method runs on the main thread.  
        Me.WordsCounted.Text = "0"  
  
        ' Initialize the object that the background worker calls.  
        Dim WC As New Words  
        WC.CompareString = Me.CompareString.Text  
        WC.SourceFile = Me.SourceFile.Text  
  
        ' Start the asynchronous operation.  
        BackgroundWorker1.RunWorkerAsync(WC)  
    End Sub  
    ```  
  
2.  Chiamare il `StartThread` dal metodo di `Start` pulsante nel form:  
  
    ```vb  
    Private Sub Start_Click() Handles Start.Click  
        StartThread()  
    End Sub  
    ```  
  
### <a name="to-implement-a-cancel-button-that-stops-the-thread"></a>Per implementare un pulsante Annulla che interrompe il thread  
  
-   Chiamare il `StopThread` procedura il `Click` gestore eventi per il `Cancel` pulsante.  
  
    ```vb  
    Private Sub Cancel_Click() Handles Cancel.Click  
        ' Cancel the asynchronous operation.  
        Me.BackgroundWorker1.CancelAsync()  
    End Sub  
    ```  
  
## <a name="testing"></a>Test  
 È ora possibile testare l'applicazione per assicurarsi che funzioni correttamente.  
  
#### <a name="to-test-the-application"></a>Per eseguire il test dell'applicazione  
  
1.  Premere F5 per eseguire l'applicazione.  
  
2.  Quando viene visualizzato il modulo, immettere il percorso del file per il file che si desidera testare il `sourceFile` casella. Ad esempio, supponendo che il file di test è denominato test. txt, immettere c:\test.txt..  
  
3.  Nella seconda casella di testo, immettere una parola o frase per l'applicazione per la ricerca nel file di testo.  
  
4.  Fare clic sul pulsante `Start`. Il `LinesCounted` pulsante dovrebbe iniziare immediatamente. L'applicazione visualizza il messaggio "Terminata Counting" è terminato.  
  
#### <a name="to-test-the-cancel-button"></a>Per testare il pulsante Annulla  
  
1.  Premere F5 per avviare l'applicazione e immettere il file nome e la ricerca come descritto nella procedura precedente. Assicurarsi che il file che scelto è sufficientemente elevato da garantire che essere in grado di annullare la procedura prima del completamento.  
  
2.  Fare clic sul `Start` pulsante per avviare l'applicazione.  
  
3.  Fare clic sul pulsante `Cancel`. Il conteggio dovrebbe arrestarsi immediatamente.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questa applicazione contiene alcune gestione degli errori di base. Rileva le stringhe di ricerca vuoto. È possibile rendere più affidabile questo programma tramite la gestione di altri errori, ad esempio il superamento del numero massimo di parole o le righe che possono essere conteggiate.  
  
## <a name="see-also"></a>Vedere anche  
 [Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)   
 [Procedura dettagliata: Creazione di componenti multithreading semplici con Visual Basic](http://msdn.microsoft.com/library/05693b70-3566-4d91-9f2c-c9bc4ccb3001)   
 [Procedura: Eseguire e annullare la sottoscrizione a eventi](../../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)
