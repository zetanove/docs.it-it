---
title: 'Procedura dettagliata: Multithreading con il componente BackgroundWorker (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: ff670fbf-a0ac-40c1-ab08-9ed53768f880
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1a27591c62e55295b3cf2b9716776b25d984865a
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-multithreading-with-the-backgroundworker-component-c"></a>Procedura dettagliata: Multithreading con il componente BackgroundWorker (C#)
Questa procedura dettagliata spiega come creare un'applicazione Windows Form multithreading che cerca le occorrenze di una parola in un file di testo. Illustra quanto segue:  
  
-   Definizione di una classe con un metodo che può essere chiamato dal componente <xref:System.ComponentModel.BackgroundWorker>.  
  
-   Gestione degli eventi generati dal componente <xref:System.ComponentModel.BackgroundWorker>.  
  
-   Avvio di un componente <xref:System.ComponentModel.BackgroundWorker> per l'esecuzione di un metodo.  
  
-   Implementazione di un pulsante `Cancel` che arresta il componente <xref:System.ComponentModel.BackgroundWorker>.  
  
### <a name="to-create-the-user-interface"></a>Per creare l'interfaccia utente  
  
1.  Aprire un nuovo progetto a Windows Forms Application in C# e creare un form denominato `Form1`.  
  
2.  Aggiungere due pulsanti e quattro caselle di testo a `Form1`.  
  
3.  Assegnare i nomi agli oggetti come illustrato nella tabella seguente.  
  
    |Oggetto|Proprietà|Impostazione|  
    |------------|--------------|-------------|  
    |Primo pulsante|`Name`, `Text`|Start, Start|  
    |Secondo pulsante|`Name`, `Text`|Cancel, Cancel|  
    |Prima casella di testo|`Name`, `Text`|SourceFile, ""|  
    |Seconda casella di testo|`Name`, `Text`|CompareString, ""|  
    |Terza casella di testo|`Name`, `Text`|WordsCounted, "0"|  
    |Quarta casella di testo|`Name`, `Text`|LinesCounted, "0"|  
  
4.  Aggiungere un'etichetta accanto a ogni casella di testo. Impostare la proprietà `Text` per ogni etichetta come illustrato nella tabella seguente.  
  
    |Oggetto|Proprietà|Impostazione|  
    |------------|--------------|-------------|  
    |Prima etichetta|`Text`|File di origine|  
    |Seconda etichetta|`Text`|Stringa di confronto|  
    |Terza etichetta|`Text`|Parole corrispondenti|  
    |Quarta etichetta|`Text`|Righe conteggiate|  
  
### <a name="to-create-a-backgroundworker-component-and-subscribe-to-its-events"></a>Per creare un componente BackgroundWorker e sottoscrivere i relativi eventi  
  
1.  Aggiungere al form un componente <xref:System.ComponentModel.BackgroundWorker> della sezione **Componenti** della **Casella degli strumenti**. Verrà visualizzato nella barra dei componenti del form.  
  
2.  Impostare le proprietà seguenti per l'oggetto backgroundWorker1.  
  
    |Proprietà|Impostazione|  
    |--------------|-------------|  
    |`WorkerReportsProgress`|True|  
    |`WorkerSupportsCancellation`|True|  
  
3.  Sottoscrivere gli eventi dell'oggetto backgroundWorker1. Nella parte superiore della finestra **Proprietà** fare clic sull'icona **Eventi**. Fare doppio clic sull'evento `RunWorkerCompleted` per creare un metodo del gestore eventi. Eseguire la stessa operazione per gli eventi `ProgressChanged` e `DoWork`.  
  
### <a name="to-define-the-method-that-will-run-on-a-separate-thread"></a>Per definire il metodo che verrà eseguito in un thread separato  
  
1.  Scegliere **Aggiungi classe** dal menu **Progetto** per aggiungere una classe al progetto. Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento**.  
  
2.  Selezionare **Classe** nella finestra dei modelli e immettere `Words.cs` nel campo del nome.  
  
3.  Fare clic su **Aggiungi**. Viene visualizzata la classe `Words`.  
  
4.  Aggiungere il codice seguente alla classe `Words` :  
  
    ```csharp  
    public class Words  
    {  
        // Object to store the current state, for passing to the caller.  
        public class CurrentState  
        {  
            public int LinesCounted;  
            public int WordsMatched;  
        }  
  
        public string SourceFile;  
        public string CompareString;  
        private int WordCount;  
        private int LinesCounted;  
  
        public void CountWords(  
            System.ComponentModel.BackgroundWorker worker,  
            System.ComponentModel.DoWorkEventArgs e)  
        {  
            // Initialize the variables.  
            CurrentState state = new CurrentState();  
            string line = "";  
            int elapsedTime = 20;  
            DateTime lastReportDateTime = DateTime.Now;  
  
            if (CompareString == null ||  
                CompareString == System.String.Empty)  
            {  
                throw new Exception("CompareString not specified.");  
            }  
  
            // Open a new stream.  
            using (System.IO.StreamReader myStream = new System.IO.StreamReader(SourceFile))  
            {  
                // Process lines while there are lines remaining in the file.  
                while (!myStream.EndOfStream)  
                {  
                    if (worker.CancellationPending)  
                    {  
                        e.Cancel = true;  
                        break;  
                    }  
                    else  
                    {  
                        line = myStream.ReadLine();  
                        WordCount += CountInString(line, CompareString);  
                        LinesCounted += 1;  
  
                        // Raise an event so the form can monitor progress.  
                        int compare = DateTime.Compare(  
                            DateTime.Now, lastReportDateTime.AddMilliseconds(elapsedTime));  
                        if (compare > 0)  
                        {  
                            state.LinesCounted = LinesCounted;  
                            state.WordsMatched = WordCount;  
                            worker.ReportProgress(0, state);  
                            lastReportDateTime = DateTime.Now;  
                        }  
                    }  
                    // Uncomment for testing.  
                    //System.Threading.Thread.Sleep(5);  
                }  
  
                // Report the final count values.  
                state.LinesCounted = LinesCounted;  
                state.WordsMatched = WordCount;  
                worker.ReportProgress(0, state);  
            }  
        }  
  
        private int CountInString(  
            string SourceString,  
            string CompareString)  
        {  
            // This function counts the number of times  
            // a word is found in a line.  
            if (SourceString == null)  
            {  
                return 0;  
            }  
  
            string EscapedCompareString =  
                System.Text.RegularExpressions.Regex.Escape(CompareString);  
  
            System.Text.RegularExpressions.Regex regex;  
            regex = new System.Text.RegularExpressions.Regex(   
                // To count all occurrences of the string, even within words, remove  
                // both instances of @"\b" from the following line.  
                @"\b" + EscapedCompareString + @"\b",  
                System.Text.RegularExpressions.RegexOptions.IgnoreCase);  
  
            System.Text.RegularExpressions.MatchCollection matches;  
            matches = regex.Matches(SourceString);  
            return matches.Count;  
        }  
  
    }  
    ```  
  
### <a name="to-handle-events-from-the-thread"></a>Per gestire gli eventi dal thread  
  
-   Aggiungere i seguenti gestori eventi al form principale:  
  
    ```csharp  
    private void backgroundWorker1_RunWorkerCompleted(object sender, RunWorkerCompletedEventArgs e)  
    {  
    // This event handler is called when the background thread finishes.  
    // This method runs on the main thread.  
    if (e.Error != null)  
        MessageBox.Show("Error: " + e.Error.Message);  
    else if (e.Cancelled)  
        MessageBox.Show("Word counting canceled.");  
    else  
        MessageBox.Show("Finished counting words.");  
    }  
  
    private void backgroundWorker1_ProgressChanged(object sender, ProgressChangedEventArgs e)  
    {  
        // This method runs on the main thread.  
        Words.CurrentState state =  
            (Words.CurrentState)e.UserState;  
        this.LinesCounted.Text = state.LinesCounted.ToString();  
        this.WordsCounted.Text = state.WordsMatched.ToString();  
    }  
    ```  
  
### <a name="to-start-and-call-a-new-thread-that-runs-the-wordcount-method"></a>Per avviare e chiamare un nuovo thread che esegue il metodo WordCount  
  
1.  Aggiungere le procedure seguenti al programma:  
  
    ```csharp  
    private void backgroundWorker1_DoWork(object sender, DoWorkEventArgs e)  
    {  
        // This event handler is where the actual work is done.  
        // This method runs on the background thread.  
  
        // Get the BackgroundWorker object that raised this event.  
        System.ComponentModel.BackgroundWorker worker;  
        worker = (System.ComponentModel.BackgroundWorker)sender;  
  
        // Get the Words object and call the main method.  
        Words WC = (Words)e.Argument;  
        WC.CountWords(worker, e);  
    }  
  
    private void StartThread()  
    {  
        // This method runs on the main thread.  
        this.WordsCounted.Text = "0";  
  
        // Initialize the object that the background worker calls.  
        Words WC = new Words();  
        WC.CompareString = this.CompareString.Text;  
        WC.SourceFile = this.SourceFile.Text;  
  
        // Start the asynchronous operation.  
        backgroundWorker1.RunWorkerAsync(WC);  
    }  
    ```  
  
2.  Chiamare il metodo `StartThread` dal pulsante `Start` nel form:  
  
    ```csharp  
    private void Start_Click(object sender, EventArgs e)  
    {  
        StartThread();  
    }  
    ```  
  
    ##### <a name="to-implement-a-cancel-button-that-stops-the-thread"></a>Per implementare un pulsante Annulla che interrompe il thread  
  
    -   Chiamare la procedura`StopThread` dal gestore eventi `Click` per il pulsante `Cancel`.  
  
        ```csharp  
        private void Cancel_Click(object sender, EventArgs e)  
        {  
            // Cancel the asynchronous operation.  
            this.backgroundWorker1.CancelAsync();  
        }  
        ```  
  
## <a name="testing"></a>Test  
 È ora possibile testare l'applicazione per verificare che funzioni correttamente.  
  
#### <a name="to-test-the-application"></a>Per eseguire il test dell'applicazione  
  
1.  Premere F5 per eseguire l'applicazione.  
  
2.  Quando viene visualizzato il form immettere il percorso del file da testare nella casella `sourceFile`. Ad esempio, se il file di test è denominato Test.txt, immettere C:\Test.txt.  
  
3.  Nella seconda casella di testo immettere una parola o frase per l'applicazione da cercare nel file di testo.  
  
4.  Fare clic sul pulsante `Start`. Il pulsante `LinesCounted` dovrebbe iniziare immediatamente ad aumentare. Al termine l'applicazione visualizza un messaggio che indica che il conteggio è terminato.  
  
#### <a name="to-test-the-cancel-button"></a>Per testare il pulsante Annulla  
  
1.  Premere F5 per avviare l'applicazione e immettere il nome del file e la parola di ricerca come descritto nella procedura precedente. Verificare che il file che scelto sia abbastanza grande da garantire di avere tempo a sufficienza per annullare la procedura prima che venga completata.  
  
2.  Fare clic sul pulsante `Start` per avviare l'applicazione.  
  
3.  Fare clic sul pulsante `Cancel`. L'applicazione deve interrompere immediatamente il conteggio.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questa applicazione contiene alcune operazioni di base per la gestione degli errori. Rileva le stringhe di ricerca vuote. È possibile rendere più efficace questo aggiungendo la gestione di altri errori, ad esempio il superamento del numero massimo di parole o righe che possono essere conteggiate.  
  
## <a name="see-also"></a>Vedere anche  
 [Threading (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)   
 [Procedura: Eseguire e annullare la sottoscrizione a eventi](../../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)
