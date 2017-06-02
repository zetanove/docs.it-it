---
title: 'Procedura dettagliata: accesso al Web con Async e Await (C#) | Documentazione Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: get-started-article
dev_langs:
- CSharp
ms.assetid: c95d8d71-5a98-4bf0-aaf4-45fed2ebbacd
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 0832ee88bba58579eea001335be9cb8c2130834d
ms.openlocfilehash: 2874eaadd23fdfdc1baf9337169ad5a52c05905f
ms.contentlocale: it-it
ms.lasthandoff: 03/28/2017

---
# <a name="walkthrough-accessing-the-web-by-using-async-and-await-c"></a>Procedura dettagliata: accesso al Web con Async e Await (C#)
È possibile scrivere programmi asincroni in modo più semplice e intuitivo usando le funzionalità async/await. È possibile scrivere codice asincrono simile al codice sincrono e consentire al compilatore di gestire le complesse funzioni di callback e continuazione tipiche del codice asincrono.  
  
 Per altre informazioni sulla funzionalità Async, vedere [Programmazione asincrona con Async e Await (C#)](../../../../csharp/programming-guide/concepts/async/index.md).  
  
 Questa procedura dettagliata inizia con l'esecuzione di un'applicazione Windows Presentation Foundation (WPF) sincrona che somma il numero di byte in un elenco di siti Web. La procedura dettagliata converte quindi l'applicazione in una soluzione asincrona usando le nuove funzionalità.  
  
 Se non si desidera compilare manualmente le applicazioni, è possibile scaricare "Esempio asincrono: accesso alla procedura dettagliata Web (C# e Visual Basic)" da [esempi di codice per sviluppatori](http://go.microsoft.com/fwlink/?LinkId=255191).  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   [Per creare un'applicazione WPF](#CreateWPFApp)  
  
-   [Per progettare una finestra WPF MainWindow semplice](#MainWindow)  
  
-   [Per aggiungere un riferimento](#AddRef)  
  
-   [Per aggiungere le direttive using necessarie](#usingDir)  
  
-   [Per creare un'applicazione sincrona](#synchronous)  
  
-   [Per eseguire il test della soluzione sincrona](#testSynch)  
  
-   [Per convertire GetURLContents in un metodo asincrono](#GetURLContents)  
  
-   [Per Convertire SumPageSizes in un metodo asincrono](#SumPageSizes)  
  
-   [Per convertire startButton_Click in un metodo asincrono](#startButton)  
  
-   [Per eseguire il test della soluzione asincrona](#testAsynch)  
  
-   [Per sostituire GetURLContentsAsync con un metodo .NET Framework](#GetURLContentsAsync)  
  
-   [Esempio](#BKMK_CompleteCodeExamples)  
  
## <a name="prerequisites"></a>Prerequisiti  
 È necessario che sia installato nel computer Visual Studio 2012 o versione successiva. Per altre informazioni, vedere il [sito Web di Microsoft](http://go.microsoft.com/fwlink/?LinkId=235233).  
  
###  <a name="CreateWPFApp"></a> Per creare un'applicazione WPF  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel riquadro **Modelli installati**, scegliere Visual C# e quindi scegliere **Applicazione WPF** nell'elenco dei tipi di progetto.  
  
4.  Nella casella di testo **Nome** immettere `AsyncExampleWPF` e quindi scegliere il pulsante **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
##  <a name="BKMK_DesignWPFMainWin"></a>   
###  <a name="MainWindow"></a> Per progettare una finestra WPF MainWindow semplice  
  
1.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
2.  Se la finestra **Casella degli strumenti** non è visibile, aprire il menu **Visualizza** e quindi scegliere **Casella degli strumenti**.  
  
3.  Aggiungere un controllo **Button** e un controllo **TextBox** alla finestra **MainWindow**.  
  
4.  Evidenziare il controllo **TextBox** e nella finestra **Proprietà** impostare i valori seguenti:  
  
    -   Impostare la proprietà **Nome** su `resultsTextBox`.  
  
    -   Impostare la proprietà **Height** su 250.  
  
    -   Impostare la proprietà **Width** su 500.  
  
    -   Nel scheda **Testo** specificare un tipo di carattere a spaziatura fissa, ad esempio Lucida Console o Global Monospace.  
  
5.  Evidenziare il controllo **Button** e nella finestra **Proprietà** impostare i valori seguenti:  
  
    -   Impostare la proprietà **Nome** su `startButton`.  
  
    -   Modificare il valore della proprietà **Content** da **Button** in **Start**.  
  
6.  Posizionare la casella di testo e il pulsante in modo che entrambi siano visualizzati nella finestra **MainWindow**.  
  
     Per altre informazioni su WPF XAML Designer, vedere [Creazione di un'interfaccia utente tramite XAML Designer](https://docs.microsoft.com/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio).  
  
##  <a name="BKMK_AddReference"></a>   
###  <a name="AddRef"></a> Per aggiungere un riferimento  
  
1.  In **Esplora soluzioni** evidenziare il nome del progetto.  
  
2.  Nella barra dei menu scegliere **Progetto**, **Aggiungi riferimento**.  
  
     Verrà visualizzata la finestra di dialogo **Gestione riferimenti**.  
  
3.  Nella parte superiore della finestra di dialogo verificare che il progetto sia destinato a .NET Framework 4.5 o versione successiva.  
  
4.  Nell'area **Assembly** scegliere **Framework** se non è già selezionato.  
  
5.  Nell'elenco dei nomi selezionare la casella di controllo **System.Net.Http**.  
  
6.  Scegliere il pulsante **OK** per chiudere la finestra di dialogo.  
  
##  <a name="BKMK_AddStatesandDirs"></a>   
###  <a name="usingDir"></a> Per aggiungere le direttive using necessarie  
  
1.  In **Esplora soluzioni** aprire il menu di scelta rapida per MainWindow.xaml.cs e scegliere **Visualizza codice**.  
  
2.  Aggiungere le seguenti direttive `using` all'inizio del file di codice, se non sono già presenti.  
  
    ```csharp  
    using System.Net.Http;  
    using System.Net;  
    using System.IO;  
    ```  
  
##  <a name="BKMK_CreatSynchApp"></a>   
###  <a name="synchronous"></a> Per creare un'applicazione sincrona  
  
1.  Nella finestra di progettazione MainWindow.xaml fare doppio clic sul pulsante **Start** per creare il gestore eventi `startButton_Click` in MainWindow.xaml.cs.  
  
2.  In MainWindow.xaml.cs copiare il codice seguente nel corpo di `startButton_Click`:  
  
    ```csharp  
    resultsTextBox.Clear();  
    SumPageSizes();  
    resultsTextBox.Text += "\r\nControl returned to startButton_Click.";  
    ```  
  
     Il codice chiama il metodo che controlla l'applicazione `SumPageSizes` e visualizza un messaggio quando il controllo torna a `startButton_Click`.  
  
3.  Il codice per la soluzione sincrona contiene i quattro metodi seguenti:  
  
    -   `SumPageSizes`, che ottiene un elenco di URL delle pagine Web da `SetUpURLList` e quindi chiama `GetURLContents` e `DisplayResults` per elaborare ogni URL.  
  
    -   `SetUpURLList`, che crea e restituisce un elenco di indirizzi web.  
  
    -   `GetURLContents`, che scarica il contenuto di ogni sito Web e restituisce il contenuto come matrice di byte.  
  
    -   `DisplayResults`, che visualizza il numero di byte nella matrice di byte per ogni URL.  
  
     Copiare i quattro metodi seguenti e incollarli nel gestore eventi `startButton_Click` in MainWindow.xaml.cs:  
  
    ```csharp  
    private void SumPageSizes()  
    {  
        // Make a list of web addresses.  
        List<string> urlList = SetUpURLList();   
  
        var total = 0;  
        foreach (var url in urlList)  
        {  
            // GetURLContents returns the contents of url as a byte array.  
            byte[] urlContents = GetURLContents(url);  
  
            DisplayResults(url, urlContents);  
  
            // Update the total.  
            total += urlContents.Length;  
        }  
  
        // Display the total count for all of the web addresses.  
        resultsTextBox.Text +=   
            string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
    }  
  
    private List<string> SetUpURLList()  
    {  
        var urls = new List<string>   
        {   
            "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
            "http://msdn.microsoft.com",  
            "http://msdn.microsoft.com/library/hh290136.aspx",  
            "http://msdn.microsoft.com/library/ee256749.aspx",  
            "http://msdn.microsoft.com/library/hh290138.aspx",  
            "http://msdn.microsoft.com/library/hh290140.aspx",  
            "http://msdn.microsoft.com/library/dd470362.aspx",  
            "http://msdn.microsoft.com/library/aa578028.aspx",  
            "http://msdn.microsoft.com/library/ms404677.aspx",  
            "http://msdn.microsoft.com/library/ff730837.aspx"  
        };  
        return urls;  
    }  
  
    private byte[] GetURLContents(string url)  
    {  
        // The downloaded resource ends up in the variable named content.  
        var content = new MemoryStream();  
  
        // Initialize an HttpWebRequest for the current URL.  
        var webReq = (HttpWebRequest)WebRequest.Create(url);  
  
        // Send the request to the Internet resource and wait for  
        // the response.  
        // Note: you can't use HttpWebRequest.GetResponse in a Windows Store app.  
        using (WebResponse response = webReq.GetResponse())  
        {  
            // Get the data stream that is associated with the specified URL.  
            using (Stream responseStream = response.GetResponseStream())  
            {  
                // Read the bytes in responseStream and copy them to content.    
                responseStream.CopyTo(content);  
            }  
        }  
  
        // Return the result as a byte array.  
        return content.ToArray();  
    }  
  
    private void DisplayResults(string url, byte[] content)  
    {  
        // Display the length of each website. The string format   
        // is designed to be used with a monospaced font, such as  
        // Lucida Console or Global Monospace.  
        var bytes = content.Length;  
        // Strip off the "http://".  
        var displayURL = url.Replace("http://", "");  
        resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
    }  
    ```  
  
##  <a name="BKMK_TestSynchSol"></a>   
###  <a name="testSynch"></a> Per eseguire il test della soluzione sincrona  
  
1.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Verrà visualizzato un output simile all'elenco seguente.  
  
    ```  
    msdn.microsoft.com/library/windows/apps/br211380.aspx        383832  
    msdn.microsoft.com                                            33964  
    msdn.microsoft.com/library/hh290136.aspx               225793  
    msdn.microsoft.com/library/ee256749.aspx               143577  
    msdn.microsoft.com/library/hh290138.aspx               237372  
    msdn.microsoft.com/library/hh290140.aspx               128279  
    msdn.microsoft.com/library/dd470362.aspx               157649  
    msdn.microsoft.com/library/aa578028.aspx               204457  
    msdn.microsoft.com/library/ms404677.aspx               176405  
    msdn.microsoft.com/library/ff730837.aspx               143474  
  
    Total bytes returned:  1834802  
  
    Control returned to startButton_Click.  
    ```  
  
     Si noti che sono necessari alcuni secondi per visualizzare i conteggi. Durante tale periodo, il thread dell'interfaccia utente viene bloccato mentre attende il download delle risorse richieste. Di conseguenza, è possibile spostare, ingrandire, ridurre o chiudere la finestra di visualizzazione dopo aver scelto il  pulsante **Start**. Queste operazioni hanno esito negativo finché non vengono visualizzati i conteggi dei byte. Se un sito Web non risponde, non si ha alcuna indicazione relativa al sito con esito negativo. È inoltre difficile interrompere l'attesa e chiudere il programma.  
  
##  <a name="BKMK_ConvertGtBtArr"></a>   
###  <a name="GetURLContents"></a> Per convertire GetURLContents in un metodo asincrono  
  
1.  Per convertire la soluzione sincrona in una soluzione asincrona, il luogo migliore dove iniziare è `GetURLContents` in quanto le chiamate del metodo di <xref:System.Net.HttpWebRequest> <xref:System.Net.HttpWebRequest.GetResponse%2A> e del metodo di <xref:System.IO.Stream> <xref:System.IO.Stream.CopyTo%2A> sono quelle in cui l'applicazione accede al Web. .NET Framework semplifica la conversione fornendo versioni asincrone di entrambi i metodi.  
  
     Per altre informazioni sui metodi utilizzati in `GetURLContents`, vedere <xref:System.Net.WebRequest>.  
  
    > [!NOTE]
    >  Mentre si esegue la procedura descritta in questa procedura dettagliata, vengono visualizzati diversi errori del compilatore. È possibile ignorarli e continuare con la procedura dettagliata.  
  
     Cambiare il metodo chiamato nella terza riga di `GetURLContents` da `GetResponse` al metodo asincrono <xref:System.Net.WebRequest.GetResponseAsync%2A> basato su attività.  
  
    ```csharp  
    using (WebResponse response = webReq.GetResponseAsync())  
    ```  
  
2.  `GetResponseAsync` restituisce un <xref:System.Threading.Tasks.Task%601>. In questo caso la *variabile di ritorno dell'attività*, `TResult`, è di tipo <xref:System.Net.WebResponse>. L'attività rappresenta una promessa di creazione di un oggetto `WebResponse` effettivo dopo il download dei dati richiesti e il completamento dell'esecuzione dell'attività.  
  
     Per recuperare il valore `WebResponse` dall'attività, applicare un operatore [await](../../../../csharp/language-reference/keywords/await.md) alla chiamata di `GetResponseAsync`, come mostrato nel codice riportato di seguito.  
  
    ```csharp  
    using (WebResponse response = await webReq.GetResponseAsync())  
    ```  
  
     L'operatore `GetURLContents` sospende l'esecuzione del metodo corrente `await` fino al completamento dell'attività attesa. Nel frattempo il controllo viene restituito al chiamante del metodo asincrono. In questo esempio, il metodo corrente è `GetURLContents` e il chiamante è `SumPageSizes`. Quando l'attività è terminata, l'oggetto promesso `WebResponse` viene generato come valore dell'attività attesa e assegnato alla variabile `response`.  
  
     L'istruzione precedente può essere suddivisa nelle due istruzioni seguenti per chiarire cosa accade.  
  
    ```csharp  
    //Task<WebResponse> responseTask = webReq.GetResponseAsync();  
    //using (WebResponse response = await responseTask)  
    ```  
  
     La chiamata a `webReq.GetResponseAsync` restituisce `Task(Of WebResponse)` o `Task<WebResponse>`. Viene quindi applicato un operatore await all'attività per recuperare il valore `WebResponse`.  
  
     Se il metodo asincrono ha operazioni da eseguire che non dipendono dal completamento dell'attività, il metodo può continuare l'esecuzione tra queste due istruzioni, dopo la chiamata al metodo asincrono e prima che venga applicato l'operatore `await`. Per esempi, vedere [Procedura: Eseguire più richieste Web in parallelo tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md) e [Procedura: Estendere la procedura dettagliata asincrona usando Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
3.  Poiché è stato aggiunto l'operatore `await` nel passaggio precedente, verrà generato un errore del compilatore. L'operatore può essere usato solo nei metodi contrassegnati con il modificatore [async](../../../../csharp/language-reference/keywords/async.md). Ignorare l'errore mentre vengono ripetuti i passaggi di conversione per sostituire la chiamata a `CopyTo` con una chiamata a `CopyToAsync`.  
  
    -   Cambiare il nome del metodo che viene chiamato in <xref:System.IO.Stream.CopyToAsync%2A>.  
  
    -   Il metodo `CopyTo` o `CopyToAsync` copia i byte nel relativo argomento `content` e non restituisce un valore significativo. Nella versione sincrona, la chiamata a `CopyTo` è un'istruzione semplice che non restituisce un valore. La versione asincrona, `CopyToAsync`, restituisce un <xref:System.Threading.Tasks.Task>. L'attività è analoga a "Task(void)" e consente l'attesa del metodo. Applicare `Await` o `await` alla chiamata a `CopyToAsync`, come mostrato nel codice riportato di seguito.  
  
        ```csharp  
        await responseStream.CopyToAsync(content);  
        ```  
  
         L'istruzione precedente abbrevia le due righe di codice riportate di seguito.  
  
        ```csharp  
        // CopyToAsync returns a Task, not a Task<T>.  
        //Task copyTask = responseStream.CopyToAsync(content);  
  
        // When copyTask is completed, content contains a copy of  
        // responseStream.  
        //await copyTask;  
        ```  
  
4.  A questo punto, non rimane che modificare la firma del metodo in `GetURLContents`. È possibile usare l'operatore `await` solo nei metodi contrassegnati con il modificatore [async](../../../../csharp/language-reference/keywords/async.md). Aggiungere il modificatore per contrassegnare il metodo come *metodo async*, come mostrato nel codice riportato di seguito.  
  
    ```csharp  
    private async byte[] GetURLContents(string url)  
    ```  
  
5.  Il tipo restituito di un metodo asincrono può essere solo <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601> o `void` in C#. In genere il tipo restituito `void` si usa solo in un gestore eventi asincrono, dove `void` è obbligatorio. In altri casi è possibile usare `Task(T)` se il metodo completato include un'istruzione [return](../../../../csharp/language-reference/keywords/return.md) che restituisce un valore di tipo T e si usa `Task` se il metodo completato non restituisce un valore significativo. È possibile considerare il tipo restituito `Task` come avente lo stesso significato di "Task(void)".  
  
     Per altre informazioni, vedere [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md).  
  
     Il metodo `GetURLContents` dispone di un'istruzione return che restituisce una matrice di byte. Pertanto, il tipo restituito della versione asincrona è Task(T), dove T è una matrice di byte. Apportare le modifiche seguenti nella firma del metodo:  
  
    -   Cambiare il tipo restituito in `Task<byte[]>`.  
  
    -   Per convenzione, i metodi asincroni presentano nomi che terminano in "Async". Rinominare pertanto il metodo `GetURLContentsAsync`.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```csharp  
    private async Task<byte[]> GetURLContentsAsync(string url)  
    ```  
  
     Dopo aver apportato queste modifiche, la conversione di `GetURLContents` in un metodo asincrono è completa.  
  
##  <a name="BKMK_ConvertSumPagSzs"></a>   
###  <a name="SumPageSizes"></a> Per Convertire SumPageSizes in un metodo asincrono  
  
1.  Ripetere i passaggi della procedura precedente per `SumPageSizes`. In primo luogo, modificare la chiamata a `GetURLContents` in una chiamata asincrona.  
  
    -   Modificare il nome del metodo chiamato da `GetURLContents` in `GetURLContentsAsync`, se non è ancora stato fatto.  
  
    -   Applicare `await` all'attività restituita da `GetURLContentsAsync` per ottenere il valore della matrice di byte.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```csharp  
    byte[] urlContents = await GetURLContentsAsync(url);  
    ```  
  
     L'assegnazione precedente abbrevia le due righe di codice riportate di seguito.  
  
    ```csharp  
    // GetURLContentsAsync returns a Task<T>. At completion, the task  
    // produces a byte array.  
    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
    //byte[] urlContents = await getContentsTask;  
    ```  
  
2.  Apportare le modifiche seguenti nella firma del metodo:  
  
    -   Contrassegnare il metodo con il modificatore `async`.  
  
    -   Aggiungere "Async" al nome del metodo.  
  
    -   In questo caso non esiste alcuna variabile di restituzione dell'attività, T, perché `SumPageSizesAsync` non restituisce un valore per T. Il metodo non ha alcuna istruzione `return`. Tuttavia, il metodo deve restituire `Task` per poter essere un metodo di tipo awaitable. Cambiare quindi il tipo restituito del metodo da `void` in `Task`.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```csharp  
    private async Task SumPageSizesAsync()  
    ```  
  
     La conversione di `SumPageSizes` in `SumPageSizesAsync` è completa.  
  
##  <a name="BKMK_Cnvrtbttn1"></a>   
###  <a name="startButton"></a> Per convertire startButton_Click in un metodo asincrono  
  
1.  Nel gestore eventi modificare il nome del metodo chiamato da `SumPageSizes` in `SumPageSizesAsync`, se non è ancora stato fatto.  
  
2.  Poiché `SumPageSizesAsync` è un metodo asincrono, modificare il codice nel gestore eventi in modo che attenda il risultato.  
  
     La chiamata a `SumPageSizesAsync` rispecchia la chiamata a `CopyToAsync` in `GetURLContentsAsync`. La chiamata restituisce `Task` e non `Task(T)`.  
  
     Come nelle procedure precedenti, è possibile convertire la chiamata tramite una o due istruzioni. Nel codice seguente sono illustrate queste modifiche.  
  
    ```csharp  
    // One-step async call.  
    await SumPageSizesAsync();  
  
    // Two-step async call.  
    //Task sumTask = SumPageSizesAsync();  
    //await sumTask;  
    ```  
  
3.  Per impedire la reentrancy accidentale dell'operazione, aggiungere l'istruzione seguente all'inizio di `startButton_Click` per disabilitare il pulsante **Start**.  
  
    ```csharp  
    // Disable the button until the operation is complete.  
    startButton.IsEnabled = false;  
    ```  
  
     È possibile riabilitare il pulsante alla fine del gestore eventi.  
  
    ```csharp  
    // Reenable the button in case you want to run the operation again.  
    startButton.IsEnabled = true;  
    ```  
  
     Per altre informazioni sulla reentrancy, vedere [Gestione della reentrancy nelle applicazioni asincrone (C#)](../../../../csharp/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md).  
  
4.  Aggiungere infine il modificatore `async` alla dichiarazione, in modo che il gestore eventi possa attendere `SumPagSizesAsync`.  
  
    ```csharp  
    private async void startButton_Click(object sender, RoutedEventArgs e)  
    ```  
  
     In genere, i nomi dei gestori eventi non vengono modificati. Il tipo restituito non viene modificato in `Task` perché i gestori evento devono restituire `void`.  
  
     La conversione del progetto dall'elaborazione sincrona a quella asincrona è completa.  
  
##  <a name="BKMK_testAsynchSolution"></a>   
###  <a name="testAsynch"></a> Per eseguire il test della soluzione asincrona  
  
1.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
2.  Viene visualizzato un output simile all'output della soluzione sincrona. Esistono tuttavia le differenze seguenti:  
  
    -   I risultati non vengono restituiti contemporaneamente, al termine dell'elaborazione. Ad esempio, entrambi i programmi contengono una riga in `startButton_Click` che consente di cancellare la casella di testo. Lo scopo è quello di cancellare il contenuto della casella di testo tra le esecuzioni se si sceglie il pulsante **Start** per la seconda volta, dopo la visualizzazione di un set di risultati. Nella versione sincrona la casella di testo viene cancellata prima della seconda visualizzazione dei conteggi, ovvero quando vengono completati i download e il thread dell'interfaccia utente è libero di eseguire altre operazioni. Nella versione asincrona, la casella di testo viene cancellata subito dopo aver scelto il pulsante **Start**.  
  
    -   È importante notare che il thread dell'interfaccia utente non è bloccato durante il download. È possibile spostare o ridimensionare la finestra durante il download, il conteggio e la visualizzazione delle risorse Web. Se uno dei siti Web è lento o non risponde, è possibile annullare l'operazione scegliendo il pulsante **Chiudi** (il simbolo x su sfondo rosso nell'angolo superiore destro).  
  
##  <a name="BKMK_ReplaceGetByteArrayAsync"></a>   
###  <a name="GetURLContentsAsync"></a> Per sostituire GetURLContentsAsync con un metodo .NET Framework  
  
1.  .NET Framework 4.5 fornisce molti metodi asincroni che è possibile usare. Uno di essi, il metodo di <xref:System.Net.Http.HttpClient> <xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29>, fa esattamente ciò che serve in questa procedura dettagliata. È possibile usarlo al posto del metodo `GetURLContentsAsync` creato in una procedura precedente.  
  
     Il primo passaggio consiste nel creare un oggetto `HttpClient` nel metodo `SumPageSizesAsync`. Aggiungere la dichiarazione seguente all'inizio del metodo.  
  
    ```csharp  
    // Declare an HttpClient object and increase the buffer size. The  
    // default buffer size is 65,536.  
    HttpClient client =  
        new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
    ```  
  
2.  In `SumPageSizesAsync,` sostituire la chiamata al metodo `GetURLContentsAsync` con una chiamata al metodo `HttpClient`.  
  
    ```csharp  
    byte[] urlContents = await client.GetByteArrayAsync(url);  
    ```  
  
3.  Rimuovere o impostare come commento il metodo `GetURLContentsAsync` precedentemente scritto.  
  
4.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Il comportamento di questa versione del progetto deve corrispondere al comportamento descritto nella procedura "Per eseguire il test della soluzione asincrona" ma con un intervento ridotto da parte dell'utente.  
  
##  <a name="BKMK_CompleteCodeExamples"></a> Esempio  
 Il codice seguente contiene l'esempio completo della conversione da soluzione sincrona a soluzione asincrona usando il metodo `GetURLContentsAsync` asincrono precedentemente scritto. Si noti che è molto simile alla soluzione sincrona originale.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            // Disable the button until the operation is complete.  
            startButton.IsEnabled = false;  
  
            resultsTextBox.Clear();  
  
            // One-step async call.  
            await SumPageSizesAsync();  
  
            // Two-step async call.  
            //Task sumTask = SumPageSizesAsync();  
            //await sumTask;  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
  
            // Reenable the button in case you want to run the operation again.  
            startButton.IsEnabled = true;  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            var total = 0;  
  
            foreach (var url in urlList)  
            {  
                byte[] urlContents = await GetURLContentsAsync(url);  
  
                // The previous line abbreviates the following two assignment statements.  
  
                // GetURLContentsAsync returns a Task<T>. At completion, the task  
                // produces a byte array.  
                //Task<byte[]> getContentsTask = GetURLContentsAsync(url);  
                //byte[] urlContents = await getContentsTask;  
  
                DisplayResults(url, urlContents);  
  
                // Update the total.            
                total += urlContents.Length;  
            }  
            // Display the total count for all of the websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        private async Task<byte[]> GetURLContentsAsync(string url)  
        {  
            // The downloaded resource ends up in the variable named content.  
            var content = new MemoryStream();  
  
            // Initialize an HttpWebRequest for the current URL.  
            var webReq = (HttpWebRequest)WebRequest.Create(url);  
  
            // Send the request to the Internet resource and wait for  
            // the response.                  
            using (WebResponse response = await webReq.GetResponseAsync())  
  
            // The previous statement abbreviates the following two statements.  
  
            //Task<WebResponse> responseTask = webReq.GetResponseAsync();  
            //using (WebResponse response = await responseTask)  
            {  
                // Get the data stream that is associated with the specified url.  
                using (Stream responseStream = response.GetResponseStream())  
                {  
                    // Read the bytes in responseStream and copy them to content.   
                    await responseStream.CopyToAsync(content);  
  
                    // The previous statement abbreviates the following two statements.  
  
                    // CopyToAsync returns a Task, not a Task<T>.  
                    //Task copyTask = responseStream.CopyToAsync(content);  
  
                    // When copyTask is completed, content contains a copy of  
                    // responseStream.  
                    //await copyTask;  
                }  
            }  
            // Return the result as a byte array.  
            return content.ToArray();  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
 Il codice seguente contiene l'esempio completo della soluzione che usa il metodo `HttpClient`, `GetByteArrayAsync`.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
  
// Add the following using directives, and add a reference for System.Net.Http.  
using System.Net.Http;  
using System.IO;  
using System.Net;  
  
namespace AsyncExampleWPF  
{  
    public partial class MainWindow : Window  
    {  
        public MainWindow()  
        {  
            InitializeComponent();  
        }  
  
        private async void startButton_Click(object sender, RoutedEventArgs e)  
        {  
            resultsTextBox.Clear();  
  
            // Disable the button until the operation is complete.  
            startButton.IsEnabled = false;  
  
            // One-step async call.  
            await SumPageSizesAsync();  
  
            //// Two-step async call.  
            //Task sumTask = SumPageSizesAsync();  
            //await sumTask;  
  
            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";  
  
            // Reenable the button in case you want to run the operation again.  
            startButton.IsEnabled = true;  
        }  
  
        private async Task SumPageSizesAsync()  
        {  
            // Declare an HttpClient object and increase the buffer size. The  
            // default buffer size is 65,536.  
            HttpClient client =  
                new HttpClient() { MaxResponseContentBufferSize = 1000000 };  
  
            // Make a list of web addresses.  
            List<string> urlList = SetUpURLList();  
  
            var total = 0;  
  
            foreach (var url in urlList)  
            {  
                // GetByteArrayAsync returns a task. At completion, the task  
                // produces a byte array.  
                byte[] urlContents = await client.GetByteArrayAsync(url);                 
  
                // The following two lines can replace the previous assignment statement.  
                //Task<byte[]> getContentsTask = client.GetByteArrayAsync(url);  
                //byte[] urlContents = await getContentsTask;  
  
                DisplayResults(url, urlContents);  
  
                // Update the total.  
                total += urlContents.Length;  
            }  
  
            // Display the total count for all of the websites.  
            resultsTextBox.Text +=  
                string.Format("\r\n\r\nTotal bytes returned:  {0}\r\n", total);  
        }  
  
        private List<string> SetUpURLList()  
        {  
            List<string> urls = new List<string>   
            {   
                "http://msdn.microsoft.com/library/windows/apps/br211380.aspx",  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290136.aspx",  
                "http://msdn.microsoft.com/library/ee256749.aspx",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            };  
            return urls;  
        }  
  
        private void DisplayResults(string url, byte[] content)  
        {  
            // Display the length of each website. The string format   
            // is designed to be used with a monospaced font, such as  
            // Lucida Console or Global Monospace.  
            var bytes = content.Length;  
            // Strip off the "http://".  
            var displayURL = url.Replace("http://", "");  
            resultsTextBox.Text += string.Format("\n{0,-58} {1,8}", displayURL, bytes);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio asincrono: accesso alla procedura dettagliata Web (C# e Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255191)   
 [async](../../../../csharp/language-reference/keywords/async.md)   
 [await](../../../../csharp/language-reference/keywords/await.md)   
 [Programmazione asincrona con Async e Await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [Tipi restituiti di async (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)   
 [Programmazione asincrona basata su attività (TAP)](http://go.microsoft.com/fwlink/?LinkId=204847)   
 [Procedura: estendere la procedura dettagliata asincrona usando Task.WhenAll (C#)](../../../../csharp/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)   
 [Procedura: effettuare più richieste Web in parallelo usando async e await (C#)](../../../../csharp/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)

