---
title: Accesso al Web con Async e Await (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: 84fd047f-fab8-4d89-8ced-104fb7310a91
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 643fff648336c664961ad7956308acbaea262f61
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-accessing-the-web-by-using-async-and-await-visual-basic"></a>Procedura dettagliata: accesso al Web con Async e Await (Visual Basic)
È possibile scrivere programmi asincroni più semplice e intuitivo utilizzando le funzionalità introdotte in [!INCLUDE[vs_dev11_long](../../../../csharp/includes/vs_dev11_long_md.md)]. È possibile scrivere codice asincrono simile al codice sincrono e consentire al compilatore di gestire le complesse funzioni di callback e continuazione tipiche del codice asincrono.  
  
 Per ulteriori informazioni sulla funzionalità asincrone, vedere [la programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md).  
  
 Questa procedura dettagliata inizia con l'esecuzione di un'applicazione Windows Presentation Foundation (WPF) sincrona che somma il numero di byte in un elenco di siti Web. La procedura dettagliata converte quindi l'applicazione in una soluzione asincrona usando le nuove funzionalità.  
  
 Se non si desidera compilare le applicazioni autonomamente, è possibile scaricare "esempio asincrono: accesso la procedura dettagliata Web (c# e Visual Basic)" da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191).  
  
 Questa procedura dettagliata prevede l'esecuzione delle attività seguenti:  
  
-   [Per creare un'applicazione WPF](#CreateWPFApp)  
  
-   [Per progettare una finestra principale semplice WPF](#MainWindow)  
  
-   [Per aggiungere un riferimento](#AddRef)  
  
-   [Per aggiungere istruzioni Imports necessarie](#ImportsState)  
  
-   [Per creare un'applicazione sincrona](#synchronous)  
  
-   [Per testare la soluzione sincrona](#testSynch)  
  
-   [Per convertire un metodo asincrono GetURLContents](#GetURLContents)  
  
-   [Per convertire un metodo asincrono SumPageSizes](#SumPageSizes)  
  
-   [Per convertire un metodo asincrono startButton_Click](#startButton)  
  
-   [Per testare la soluzione asincrona](#testAsynch)  
  
-   [Per sostituire il metodo GetURLContentsAsync con un metodo .NET Framework](#GetURLContentsAsync)  
  
-   [Esempio](#BKMK_CompleteCodeExamples)  
  
## <a name="prerequisites"></a>Prerequisiti  
 Visual Studio 2012 o versione successiva deve essere installato nel computer. Per ulteriori informazioni, vedere il [sito Web Microsoft](http://go.microsoft.com/fwlink/?LinkId=235233).  
  
###  <a name="CreateWPFApp"></a>Per creare un'applicazione WPF  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel **modelli installati** riquadro, scegliere Visual Basic, quindi **applicazione WPF** dall'elenco dei tipi di progetto.  
  
4.  Nel **nome** testo immettere `AsyncExampleWPF`, quindi scegliere il **OK** pulsante.  
  
     Il nuovo progetto verrà visualizzato **Esplora**.  
  
##  <a name="BKMK_DesignWPFMainWin"></a>   
###  <a name="MainWindow"></a>Per progettare una finestra principale semplice WPF  
  
1.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
2.  Se il **della casella degli strumenti** finestra non è visibile, aprire il **visualizzazione** dal menu e quindi scegliere **della casella degli strumenti**.  
  
3.  Aggiungere un **pulsante** controllo e un **TextBox** controllo il **MainWindow** finestra.  
  
4.  Evidenziare il **TextBox** controllo e, nel **proprietà** finestra, impostare i valori seguenti:  
  
    -   Impostare il **nome** proprietà `resultsTextBox`.  
  
    -   Impostare il **altezza** proprietà a 250.  
  
    -   Impostare il **larghezza** proprietà fino a 500.  
  
    -   Nel **testo** , specificare un carattere a spaziatura fissa, ad esempio Lucida Console o a spaziatura fissa globale.  
  
5.  Evidenziare il **pulsante** controllo e, nel **proprietà** finestra, impostare i valori seguenti:  
  
    -   Impostare il **nome** proprietà `startButton`.  
  
    -   Modificare il valore di **contenuto** proprietà **pulsante** a **avviare**.  
  
6.  Posizionare la casella di testo e il pulsante in modo che entrambi visualizzati nella finestra di **MainWindow** finestra.  
  
     Per ulteriori informazioni sulla finestra di progettazione XAML WPF, vedere [la creazione di un'interfaccia utente tramite XAML Designer](https://docs.microsoft.com/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio).  
  
##  <a name="BKMK_AddReference"></a>   
###  <a name="AddRef"></a>Per aggiungere un riferimento  
  
1.  In **Esplora**, evidenziare il nome del progetto.  
  
2.  Nella barra dei menu, scegliere **progetto**, **Aggiungi riferimento**.  
  
     Il **gestione riferimenti** viene visualizzata la finestra di dialogo.  
  
3.  Nella parte superiore della finestra di dialogo, verificare che il progetto è destinato a .NET Framework 4.5 o versioni successive.  
  
4.  Nel **assembly** area, scegliere **Framework** se non è già selezionato.  
  
5.  Nell'elenco di nomi, selezionare il **System.Net.Http** casella di controllo.  
  
6.  Scegliere il **OK** per chiudere la finestra di dialogo.  
  
##  <a name="BKMK_AddStatesandDirs"></a>   
###  <a name="ImportsState"></a>Per aggiungere istruzioni Imports necessarie  
  
1.  In **Esplora**, aprire il menu di scelta rapida per MainWindow.xaml.vb e quindi scegliere **Visualizza codice**.  
  
2.  Aggiungere il codice seguente `Imports` istruzioni all'inizio del file di codice, se non sono già presenti.  
  
    ```vb  
    Imports System.Net.Http  
    Imports System.Net  
    Imports System.IO  
    ```  
  
##  <a name="BKMK_CreatSynchApp"></a>   
###  <a name="synchronous"></a>Per creare un'applicazione sincrona  
  
1.  Nella finestra di progettazione, MainWindow. XAML, fare doppio clic su di **avviare** per creare il `startButton_Click` gestore dell'evento nel file MainWindow.xaml.vb.  
  
2.  In MainWindow.xaml.vb, copiare il codice seguente nel corpo di `startButton_Click`:  
  
    ```vb  
    resultsTextBox.Clear()  
    SumPageSizes()  
    resultsTextBox.Text &= vbCrLf & "Control returned to startButton_Click."  
    ```  
  
     Il codice chiama il metodo che controlla l'applicazione `SumPageSizes` e visualizza un messaggio quando il controllo torna a `startButton_Click`.  
  
3.  Il codice per la soluzione sincrona contiene i quattro metodi seguenti:  
  
    -   `SumPageSizes`, che ottiene un elenco di URL delle pagine Web da `SetUpURLList` e quindi chiama `GetURLContents` e `DisplayResults` per elaborare ogni URL.  
  
    -   `SetUpURLList`, che crea e restituisce un elenco di indirizzi web.  
  
    -   `GetURLContents`, che scarica il contenuto di ogni sito Web e restituisce il contenuto come matrice di byte.  
  
    -   `DisplayResults`, che visualizza il numero di byte nella matrice di byte per ogni URL.  
  
     Copiare i quattro metodi seguenti e incollarli nel `startButton_Click` gestore dell'evento nel file MainWindow.xaml.vb:  
  
    ```vb  
    Private Sub SumPageSizes()  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            ' GetURLContents returns the contents of url as a byte array.  
            Dim urlContents As Byte() = GetURLContents(url)  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "Total bytes returned:  {0}" & vbCrLf, total)  
    End Sub  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
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
            }  
        Return urls  
    End Function  
  
    Private Function GetURLContents(url As String) As Byte()  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        ' Note: you can't use HttpWebRequest.GetResponse in a Windows Store app.  
        Using response As WebResponse = webReq.GetResponse()  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                responseStream.CopyTo(content)  
            End Using  
        End Using  
  
        ' Return the result as a byte array.  
        Return content.ToArray()  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
    ```  
  
##  <a name="BKMK_TestSynchSol"></a>   
###  <a name="testSynch"></a>Per testare la soluzione sincrona  
  
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
  
     Si noti che sono necessari alcuni secondi per visualizzare i conteggi. Durante tale periodo, il thread dell'interfaccia utente viene bloccato mentre attende il download delle risorse richieste. Di conseguenza, è possibile spostare, ingrandire, ridurre al minimo o perfino chiudere la finestra di visualizzazione dopo aver scelto il **avviare** pulsante. Queste operazioni hanno esito negativo finché non vengono visualizzati i conteggi dei byte. Se un sito Web non risponde, non si ha alcuna indicazione relativa al sito con esito negativo. È inoltre difficile interrompere l'attesa e chiudere il programma.  
  
##  <a name="BKMK_ConvertGtBtArr"></a>   
###  <a name="GetURLContents"></a>Per convertire un metodo asincrono GetURLContents  
  
1.  Per convertire la soluzione sincrona in una soluzione asincrona, è consigliabile iniziare in `GetURLContents` perché le chiamate al <xref:System.Net.HttpWebRequest>metodo <xref:System.Net.HttpWebRequest.GetResponse%2A>e il <xref:System.IO.Stream>metodo <xref:System.IO.Stream.CopyTo%2A>sono in cui l'applicazione accede al web.</xref:System.IO.Stream.CopyTo%2A> </xref:System.IO.Stream> </xref:System.Net.HttpWebRequest.GetResponse%2A> </xref:System.Net.HttpWebRequest> .NET Framework semplifica la conversione fornendo versioni asincrone di entrambi i metodi.  
  
     Per ulteriori informazioni sui metodi utilizzati in `GetURLContents`, vedere <xref:System.Net.WebRequest>.</xref:System.Net.WebRequest>  
  
    > [!NOTE]
    >  Mentre si esegue la procedura descritta in questa procedura dettagliata, vengono visualizzati diversi errori del compilatore. È possibile ignorarli e continuare con la procedura dettagliata.  
  
     Modifica del metodo viene chiamato nella terza riga del `GetURLContents` da `GetResponse` asincrono, basato su attività <xref:System.Net.WebRequest.GetResponseAsync%2A>(metodo).</xref:System.Net.WebRequest.GetResponseAsync%2A>  
  
    ```vb  
    Using response As WebResponse = webReq.GetResponseAsync()  
    ```  
  
2.  `GetResponseAsync`Restituisce un <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> In questo caso, il *variabile restituita attività*, `TResult`, è di tipo <xref:System.Net.WebResponse>.</xref:System.Net.WebResponse> L'attività rappresenta una promessa di creazione di un oggetto `WebResponse` effettivo dopo il download dei dati richiesti e il completamento dell'esecuzione dell'attività.  
  
     Per recuperare il `WebResponse` valore dall'attività, applicare un [Await](../../../../visual-basic/language-reference/operators/await-operator.md) operatore per la chiamata a `GetResponseAsync`, come mostrato nel codice seguente.  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
     Il `Await` operatore sospende l'esecuzione del metodo corrente, `GetURLContents`, fino a quando l'attività attesa è stata completata. Nel frattempo il controllo viene restituito al chiamante del metodo asincrono. In questo esempio, il metodo corrente è `GetURLContents` e il chiamante è `SumPageSizes`. Quando l'attività è terminata, l'oggetto promesso `WebResponse` viene generato come valore dell'attività attesa e assegnato alla variabile `response`.  
  
     The previous statement can be separated into the following two statements to clarify what happens.  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
     La chiamata a `webReq.GetResponseAsync` restituisce `Task(Of WebResponse)` o `Task<WebResponse>`. Un oggetto `Await` operatore viene applicato all'attività per recuperare il `WebResponse` valore.  
  
     If your async method has work to do that doesn’t depend on the completion of the task, the method can continue with that work between these two statements, after the call to the async method and before the await operator is applied. For examples, see [How to: Make Multiple Web Requests in Parallel by Using Async and Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md) and [How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
3.  Poiché è stato aggiunto il `Await` operatore nel passaggio precedente, verrà generato un errore del compilatore. L'operatore può essere utilizzato solo nei metodi contrassegnati con il [Async](../../../../visual-basic/language-reference/modifiers/async.md) modificatore. Ignorare l'errore mentre vengono ripetuti i passaggi di conversione per sostituire la chiamata a `CopyTo` con una chiamata a `CopyToAsync`.  
  
    -   Modificare il nome del metodo che viene chiamato per <xref:System.IO.Stream.CopyToAsync%2A>.</xref:System.IO.Stream.CopyToAsync%2A>  
  
    -   Il metodo `CopyTo` o `CopyToAsync` copia i byte nel relativo argomento `content` e non restituisce un valore significativo. Nella versione sincrona, la chiamata a `CopyTo` è un'istruzione semplice che non restituisce un valore. La versione asincrona `CopyToAsync`, restituisce un <xref:System.Threading.Tasks.Task>.</xref:System.Threading.Tasks.Task> L'attività è analoga a "Task(void)" e consente l'attesa del metodo. Applicare `Await` o `await` alla chiamata a `CopyToAsync`, come mostrato nel codice riportato di seguito.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
         L'istruzione precedente abbrevia le due righe di codice riportate di seguito.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
4.  A questo punto, non rimane che modificare la firma del metodo in `GetURLContents`. È possibile utilizzare il `Await` operatore solo nei metodi contrassegnati con il [Async](../../../../visual-basic/language-reference/modifiers/async.md) modificatore. Aggiungere il modificatore per contrassegnare il metodo come un *metodo asincrono*, come mostrato nel codice seguente.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
5.  Il tipo restituito di un metodo asincrono può essere solo <xref:System.Threading.Tasks.Task> <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> ,</xref:System.Threading.Tasks.Task> In Visual Basic, il metodo deve essere `Function` che restituisce `Task` o `Task(Of T)` oppure il metodo deve essere `Sub`. In genere, un `Sub` metodo viene utilizzato solo in un gestore eventi asincrono, in cui `Sub` è obbligatorio. In altri casi, utilizzare `Task(T)` se il metodo completato ha un [restituire](../../../../visual-basic/language-reference/statements/return-statement.md) istruzione che restituisce un valore di tipo T e si utilizza `Task` se il metodo completato non restituisce alcun valore significativo.  
  
     Per ulteriori informazioni, vedere [Async restituire tipi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md).  
  
     Il metodo `GetURLContents` dispone di un'istruzione return che restituisce una matrice di byte. Pertanto, il tipo restituito della versione asincrona è Task(T), dove T è una matrice di byte. Apportare le modifiche seguenti nella firma del metodo:  
  
    -   Modificare il tipo restituito per `Task(Of Byte())`.  
  
    -   Per convenzione, i metodi asincroni presentano nomi che terminano in "Async". Rinominare pertanto il metodo `GetURLContentsAsync`.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```vb  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
    ```  
  
     Dopo aver apportato queste modifiche, la conversione di `GetURLContents` in un metodo asincrono è completa.  
  
##  <a name="BKMK_ConvertSumPagSzs"></a>   
###  <a name="SumPageSizes"></a>Per convertire un metodo asincrono SumPageSizes  
  
1.  Ripetere i passaggi della procedura precedente per `SumPageSizes`. In primo luogo, modificare la chiamata a `GetURLContents` in una chiamata asincrona.  
  
    -   Modificare il nome del metodo chiamato da `GetURLContents` in `GetURLContentsAsync`, se non è ancora stato fatto.  
  
    -   Applicare `Await` all'attività che `GetURLContentsAsync` valore restituisce per ottenere il byte della matrice.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```vb  
    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
    ```  
  
     L'assegnazione precedente abbrevia le due righe di codice riportate di seguito.  
  
    ```vb  
    ' GetURLContentsAsync returns a task. At completion, the task   
    ' produces a byte array.   
    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)   
    'Dim urlContents As Byte() = Await getContentsTask  
  
    ```  
  
2.  Apportare le modifiche seguenti nella firma del metodo:  
  
    -   Contrassegnare il metodo con il `Async` modificatore.  
  
    -   Aggiungere "Async" al nome del metodo.  
  
    -   In questo caso non esiste alcuna variabile di restituzione dell'attività, T, perché `SumPageSizesAsync` non restituisce un valore per T. (Il metodo non ha `Return` istruzione.) Tuttavia, il metodo deve restituire `Task` per poter essere un metodo di tipo awaitable. Pertanto, modificare il tipo di metodo da `Sub` a `Function`. Il tipo restituito della funzione è `Task`.  
  
     Nel codice seguente sono illustrate queste modifiche.  
  
    ```vb  
    Private Async Function SumPageSizesAsync() As Task  
    ```  
  
     La conversione di `SumPageSizes` in `SumPageSizesAsync` è completa.  
  
##  <a name="BKMK_Cnvrtbttn1"></a>   
###  <a name="startButton"></a>Per convertire un metodo asincrono startButton_Click  
  
1.  Nel gestore eventi modificare il nome del metodo chiamato da `SumPageSizes` in `SumPageSizesAsync`, se non è ancora stato fatto.  
  
2.  Poiché `SumPageSizesAsync` è un metodo asincrono, modificare il codice nel gestore eventi in modo che attenda il risultato.  
  
     La chiamata a `SumPageSizesAsync` rispecchia la chiamata a `CopyToAsync` in `GetURLContentsAsync`. La chiamata restituisce `Task` e non `Task(T)`.  
  
     Come nelle procedure precedenti, è possibile convertire la chiamata tramite una o due istruzioni. Nel codice seguente sono illustrate queste modifiche.  
  
    ```vb  
    '' One-step async call.  
    Await SumPageSizesAsync()  
  
    ' Two-step async call.  
    'Dim sumTask As Task = SumPageSizesAsync()  
    'Await sumTask  
    ```  
  
3.  Per evitare accidentalmente immettere di nuovo l'operazione, aggiungere l'istruzione seguente all'inizio del `startButton_Click` per disabilitare il **avviare** pulsante.  
  
    ```vb  
    ' Disable the button until the operation is complete.  
    startButton.IsEnabled = False  
    ```  
  
     È possibile riabilitare il pulsante alla fine del gestore eventi.  
  
    ```vb  
    ' Reenable the button in case you want to run the operation again.  
    startButton.IsEnabled = True  
    ```  
  
     Per ulteriori informazioni su reentrancy, vedere [la gestione della Reentrancy nelle applicazioni asincrone (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md).  
  
4.  Infine, aggiungere il `Async` modificatore per la dichiarazione in modo che il gestore eventi può await `SumPagSizesAsync`.  
  
    ```vb  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
    ```  
  
     In genere, i nomi dei gestori eventi non vengono modificati. Il tipo restituito non è cambiato in `Task` perché i gestori eventi devono essere `Sub` routine in Visual Basic.  
  
     La conversione del progetto dall'elaborazione sincrona a quella asincrona è completa.  
  
##  <a name="BKMK_testAsynchSolution"></a>   
###  <a name="testAsynch"></a>Per testare la soluzione asincrona  
  
1.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
2.  Viene visualizzato un output simile all'output della soluzione sincrona. Esistono tuttavia le differenze seguenti:  
  
    -   I risultati non vengono restituiti contemporaneamente, al termine dell'elaborazione. Ad esempio, entrambi i programmi contengono una riga in `startButton_Click` che consente di cancellare la casella di testo. Lo scopo consiste nel deselezionare la casella di testo tra le esecuzioni, se si sceglie il **avviare** pulsante per la seconda volta, dopo è apparsa un set di risultati. Nella versione sincrona la casella di testo viene cancellata prima della seconda visualizzazione dei conteggi, ovvero quando vengono completati i download e il thread dell'interfaccia utente è libero di eseguire altre operazioni. Poiché la versione asincrona, la casella di testo Cancella immediatamente dopo aver scelto il **avviare** pulsante.  
  
    -   È importante notare che il thread dell'interfaccia utente non è bloccato durante il download. È possibile spostare o ridimensionare la finestra durante il download, il conteggio e la visualizzazione delle risorse Web. Se uno dei siti Web è lento o non risponde, è possibile annullare l'operazione scegliendo il **Chiudi** pulsante (la x nella casella rossa nell'angolo superiore destro).  
  
##  <a name="BKMK_ReplaceGetByteArrayAsync"></a>   
###  <a name="GetURLContentsAsync"></a>Per sostituire il metodo GetURLContentsAsync con un metodo .NET Framework  
  
1.  .NET Framework 4.5 fornisce molti metodi asincroni che è possibile usare. Uno di essi, il <xref:System.Net.Http.HttpClient>metodo <xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29>, viene solo ciò che è necessario per questa procedura dettagliata.</xref:System.Net.Http.HttpClient.GetByteArrayAsync%28System.String%29> </xref:System.Net.Http.HttpClient> È possibile usarlo al posto del metodo `GetURLContentsAsync` creato in una procedura precedente.  
  
     Il primo passaggio consiste nel creare un oggetto `HttpClient` nel metodo `SumPageSizesAsync`. Aggiungere la dichiarazione seguente all'inizio del metodo.  
  
    ```vb  
    ' Declare an HttpClient object and increase the buffer size. The  
    ' default buffer size is 65,536.  
    Dim client As HttpClient =  
        New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
    ```  
  
2.  In `SumPageSizesAsync,` sostituire la chiamata al metodo `GetURLContentsAsync` con una chiamata al metodo `HttpClient`.  
  
    ```vb  
    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
    ```  
  
3.  Rimuovere o impostare come commento il metodo `GetURLContentsAsync` precedentemente scritto.  
  
4.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Il comportamento di questa versione del progetto deve corrispondere al comportamento descritto nella procedura "Per eseguire il test della soluzione asincrona" ma con un intervento ridotto da parte dell'utente.  
  
##  <a name="BKMK_CompleteCodeExamples"></a>Esempio  
 Il codice seguente contiene l'esempio completo della conversione da soluzione sincrona a soluzione asincrona usando il metodo `GetURLContentsAsync` asincrono precedentemente scritto. Si noti che è molto simile alla soluzione sincrona originale.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        ' Disable the button until the operation is complete.  
        startButton.IsEnabled = False  
  
        resultsTextBox.Clear()  
  
        '' One-step async call.  
        Await SumPageSizesAsync()  
  
        ' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
  
        ' Reenable the button in case you want to run the operation again.  
        startButton.IsEnabled = True  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
            ' The previous line abbreviates the following two assignment statements.  
  
            '//<snippet21>  
            ' GetURLContentsAsync returns a task. At completion, the task  
            ' produces a byte array.  
            'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
            'Dim urlContents As Byte() = Await getContentsTask  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
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
            }  
        Return urls  
    End Function  
  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        Using response As WebResponse = Await webReq.GetResponseAsync()  
  
            ' The previous statement abbreviates the following two statements.  
  
            'Dim responseTask As Task(Of WebResponse) = webReq.GetResponseAsync()  
            'Using response As WebResponse = Await responseTask  
  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                Await responseStream.CopyToAsync(content)  
  
                ' The previous statement abbreviates the following two statements.  
  
                ' CopyToAsync returns a Task, not a Task<T>.  
                'Dim copyTask As Task = responseStream.CopyToAsync(content)  
  
                ' When copyTask is completed, content contains a copy of  
                ' responseStream.  
                'Await copyTask  
            End Using  
        End Using  
  
        ' Return the result as a byte array.  
        Return content.ToArray()  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
  
End Class  
```  
  
 Il codice seguente contiene l'esempio completo della soluzione che usa il metodo `HttpClient`, `GetByteArrayAsync`.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        ' Disable the button until the operation is complete.  
        startButton.IsEnabled = False  
  
        ' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
  
        ' Reenable the button in case you want to run the operation again.  
        startButton.IsEnabled = True  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Declare an HttpClient object and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        Dim total = 0  
        For Each url In urlList  
            ' GetByteArrayAsync returns a task. At completion, the task  
            ' produces a byte array.  
            Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
  
            ' The following two lines can replace the previous assignment statement.  
            'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)  
            'Dim urlContents As Byte() = Await getContentsTask  
  
            DisplayResults(url, urlContents)  
  
            ' Update the total.  
            total += urlContents.Length  
        Next  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
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
            }  
        Return urls  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
  
End Class  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio asincrono: Accesso la procedura dettagliata Web (c# e Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255191)   
 [Await (operatore)](../../../../visual-basic/language-reference/operators/await-operator.md)   
 [Async](../../../../visual-basic/language-reference/modifiers/async.md)   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Tipi restituiti asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [Programmazione asincrona basato su attività (TAP)](http://go.microsoft.com/fwlink/?LinkId=204847)   
 [Procedura: estendere la procedura dettagliata asincrona tramite Task. whenall (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)   
 [Procedura: effettuare più richieste Web in parallelo tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)
