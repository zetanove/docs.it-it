---
title: 'Procedura: estendere la procedura dettagliata asincrona tramite Task. whenall (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: c06d386d-e996-4da9-bf3d-05a3b6c0a258
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
ms.openlocfilehash: 46c5cb9328f2fa1a4ffc5116d318bc3286419e13
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-visual-basic"></a>Procedura: estendere la procedura dettagliata asincrona tramite Task. whenall (Visual Basic)
È possibile migliorare le prestazioni della soluzione async in [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) utilizzando il <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>(metodo).</xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName> Questo metodo attende in modo asincrono di più operazioni asincrone vengono rappresentate come una raccolta di attività.  
  
 È possibile osservare nella procedura dettagliata che i siti Web di download a velocità diverse. A volte uno dei siti Web è molto lento, che ritarda tutti i download rimanenti. Quando si eseguono le soluzioni asincrone compilati nella procedura dettagliata, è possibile terminare il programma con facilità se non si desidera attendere, ma sarebbe un'opzione migliore per avviare tutti i download contemporaneamente e consentire più velocemente download continuare senza attendere che quello che viene ritardata.  
  
 Si applica il `Task.WhenAll` (metodo) a una raccolta di attività. L'applicazione di `WhenAll` restituisce una singola attività che non è completezza fino al completamento di tutte le attività nella raccolta. Vengono visualizzate le attività eseguite in parallelo, ma non gli altri thread vengono creati. Completare le attività in qualsiasi ordine.  
  
> [!IMPORTANT]
>  Le procedure seguenti descrivono le estensioni per le applicazioni asincrone che sono state sviluppate [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). È possibile sviluppare le applicazioni completato la procedura dettagliata o del download del codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191).  
>   
>  Per eseguire l'esempio, è necessario Visual Studio 2012 o versioni successive installato nel computer in uso.  
  
### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a>Per aggiungere alla soluzione di GetURLContentsAsync Task. whenall  
  
1.  Aggiungere il `ProcessURLAsync` metodo per la prima applicazione che è stata sviluppata in [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Se è stato scaricato il codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191), aprire il progetto AsyncWalkthrough e quindi aggiungere `ProcessURLAsync` al file MainWindow.xaml.vb.  
  
    -   Se il codice è stato creato completando la procedura dettagliata, aggiungere `ProcessURLAsync` all'applicazione che include il `GetURLContentsAsync` metodo. Il file MainWindow.xaml.vb per questa applicazione è il primo esempio nella sezione "Codice esempi dalla procedura dettagliata completa".  
  
     Il `ProcessURLAsync` metodo consente di consolidare le azioni nel corpo del `For Each` ciclo `SumPageSizesAsync` nella procedura dettagliata originale. Il metodo in modo asincrono Scarica il contenuto di un sito Web specificato come matrice di byte e quindi Visualizza e restituisce la lunghezza della matrice di byte.  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String) As Task(Of Integer)  
  
        Dim byteArray = Await GetURLContentsAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
    ```  
  
2.  Impostare come commento o eliminare il `For Each` ciclo `SumPageSizesAsync`, come mostrato nel codice seguente.  
  
    ```vb  
    'Dim total = 0  
    'For Each url In urlList  
  
    '    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
    '    ' The previous line abbreviates the following two assignment statements.  
  
    '    ' GetURLContentsAsync returns a task. At completion, the task  
    '    ' produces a byte array.  
    '    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
    '    'Dim urlContents As Byte() = Await getContentsTask  
  
    '    DisplayResults(url, urlContents)  
  
    '    ' Update the total.  
    '    total += urlContents.Length  
    'Next  
    ```  
  
3.  Creare una raccolta di attività. Il codice seguente definisce una [query](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) che, quando eseguita dal <xref:System.Linq.Enumerable.ToArray%2A>(metodo), crea una raccolta di attività che scaricare il contenuto di ogni sito Web.</xref:System.Linq.Enumerable.ToArray%2A> Le attività vengono avviate quando viene valutata la query.  
  
     Aggiungere il codice seguente al metodo `SumPageSizesAsync` dopo la dichiarazione di `urlList`.  
  
    ```vb  
    ' Create a query.   
    Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
        From url In urlList Select ProcessURLAsync(url)  
  
    ' Use ToArray to execute the query and start the download tasks.  
    Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
    ```  
  
4.  Applicare `Task.WhenAll` alla raccolta di attività, `downloadTasks`. `Task.WhenAll`Restituisce una singola attività che termina al completamento di tutte le attività nella raccolta di attività.  
  
     Nell'esempio seguente, il `Await` espressione attenderà il completamento dell'unico attività `WhenAll` restituisce. L'espressione restituisce una matrice di interi, dove ogni valore integer è la lunghezza di un sito Web scaricato. Aggiungere il codice seguente a `SumPageSizesAsync`, solo dopo il codice aggiunto nel passaggio precedente.  
  
    ```vb  
    ' Await the completion of all the running tasks.  
    Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
    '' The previous line is equivalent to the following two statements.  
    'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
    'Dim lengths As Integer() = Await whenAllTask  
    ```  
  
5.  Infine, utilizzare il <xref:System.Linq.Enumerable.Sum%2A>metodo per calcolare la somma delle lunghezze di tutti i siti Web.</xref:System.Linq.Enumerable.Sum%2A> Aggiungere la riga seguente a `SumPageSizesAsync`.  
  
    ```vb  
    Dim total = lengths.Sum()  
    ```  
  
### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a>Per aggiungere la soluzione HttpClient.GetByteArrayAsync Task. whenall  
  
1.  Aggiungere la seguente versione di `ProcessURLAsync` per la seconda applicazione che è stata sviluppata in [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Se è stato scaricato il codice da [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=255191), aprire il progetto AsyncWalkthrough_HttpClient e quindi aggiungere `ProcessURLAsync` al file MainWindow.xaml.vb.  
  
    -   Se il codice è stato creato completando la procedura dettagliata, aggiungere `ProcessURLAsync` all'applicazione che utilizza il `HttpClient.GetByteArrayAsync` metodo. Il file MainWindow.xaml.vb per questa applicazione è il secondo esempio nella sezione "Codice esempi dalla procedura dettagliata completa".  
  
     Il `ProcessURLAsync` metodo consente di consolidare le azioni nel corpo del `For Each` ciclo `SumPageSizesAsync` nella procedura dettagliata originale. Il metodo in modo asincrono Scarica il contenuto di un sito Web specificato come matrice di byte e quindi Visualizza e restituisce la lunghezza della matrice di byte.  
  
     L'unica differenza rispetto di `ProcessURLAsync` metodo nella procedura precedente consiste nell'utilizzare il <xref:System.Net.Http.HttpClient>istanza, `client`.</xref:System.Net.Http.HttpClient>  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
    ```  
  
2.  Impostare come commento o eliminare il `For Each` ciclo `SumPageSizesAsync`, come mostrato nel codice seguente.  
  
    ```vb  
    'Dim total = 0   
    'For Each url In urlList   
    '    ' GetByteArrayAsync returns a task. At completion, the task   
    '    ' produces a byte array.   
    '    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)   
  
    '    ' The following two lines can replace the previous assignment statement.   
    '    'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)   
    '    'Dim urlContents As Byte() = Await getContentsTask   
  
    '    DisplayResults(url, urlContents)   
  
    '    ' Update the total.   
    '    total += urlContents.Length   
    'Next  
  
    ```  
  
3.  Definire un [query](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) che, quando eseguita dal <xref:System.Linq.Enumerable.ToArray%2A>(metodo), crea una raccolta di attività che scaricare il contenuto di ogni sito Web.</xref:System.Linq.Enumerable.ToArray%2A> Le attività vengono avviate quando viene valutata la query.  
  
     Aggiungere il codice seguente al metodo `SumPageSizesAsync` dopo la dichiarazione di `client` e `urlList`.  
  
    ```vb  
    ' Create a query.  
    Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
        From url In urlList Select ProcessURLAsync(url, client)  
  
    ' Use ToArray to execute the query and start the download tasks.  
    Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
    ```  
  
4.  Successivamente, si applicano `Task.WhenAll` alla raccolta di attività, `downloadTasks`. `Task.WhenAll`Restituisce una singola attività che termina al completamento di tutte le attività nella raccolta di attività.  
  
     Nell'esempio seguente, il `Await` espressione attenderà il completamento dell'unico attività `WhenAll` restituisce. Al termine, il `Await` espressione restituisce una matrice di interi, dove ogni valore integer è la lunghezza di un sito Web scaricato. Aggiungere il codice seguente a `SumPageSizesAsync`, solo dopo il codice aggiunto nel passaggio precedente.  
  
    ```vb  
    ' Await the completion of all the running tasks.  
    Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
    '' The previous line is equivalent to the following two statements.  
    'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
    'Dim lengths As Integer() = Await whenAllTask  
    ```  
  
5.  Infine, utilizzare il <xref:System.Linq.Enumerable.Sum%2A>metodo per ottenere la somma delle lunghezze di tutti i siti Web.</xref:System.Linq.Enumerable.Sum%2A> Aggiungere la riga seguente a `SumPageSizesAsync`.  
  
    ```vb  
    Dim total = lengths.Sum()  
    ```  
  
### <a name="to-test-the-taskwhenall-solutions"></a>Per testare le soluzioni di Task. whenall  
  
-   Per entrambe le soluzioni, scegliere il tasto F5 per eseguire il programma, quindi il **avviare** pulsante. L'output dovrebbe essere simile l'output dalle soluzioni async in [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md). Tuttavia, si noti che i siti Web vengono visualizzati in un ordine diverso ogni volta.  
  
## <a name="example"></a>Esempio  
 Il codice seguente mostra le estensioni per il progetto che utilizza il `GetURLContentsAsync` metodo per scaricare il contenuto dal web.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        ' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' Create a query.   
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url)  
  
        ' Use ToArray to execute the query and start the download tasks.  
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' You can do other work here before awaiting.  
  
        ' Await the completion of all the running tasks.  
        Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
        '' The previous line is equivalent to the following two statements.  
        'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
        'Dim lengths As Integer() = Await whenAllTask  
  
        Dim total = lengths.Sum()  
  
        'Dim total = 0  
        'For Each url In urlList  
  
        '    Dim urlContents As Byte() = Await GetURLContentsAsync(url)  
  
        '    ' The previous line abbreviates the following two assignment statements.  
  
        '    ' GetURLContentsAsync returns a task. At completion, the task  
        '    ' produces a byte array.  
        '    'Dim getContentsTask As Task(Of Byte()) = GetURLContentsAsync(url)  
        '    'Dim urlContents As Byte() = Await getContentsTask  
  
        '    DisplayResults(url, urlContents)  
  
        '    ' Update the total.  
        '    total += urlContents.Length  
        'NextNext  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
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
  
    ' The actions from the foreach loop are moved to this async method.  
    Private Async Function ProcessURLAsync(url As String) As Task(Of Integer)  
  
        Dim byteArray = Await GetURLContentsAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Async Function GetURLContentsAsync(url As String) As Task(Of Byte())  
  
        ' The downloaded resource ends up in the variable named content.  
        Dim content = New MemoryStream()  
  
        ' Initialize an HttpWebRequest for the current URL.  
        Dim webReq = CType(WebRequest.Create(url), HttpWebRequest)  
  
        ' Send the request to the Internet resource and wait for  
        ' the response.  
        Using response As WebResponse = Await webReq.GetResponseAsync()  
            ' Get the data stream that is associated with the specified URL.  
            Using responseStream As Stream = response.GetResponseStream()  
                ' Read the bytes in responseStream and copy them to content.    
                ' CopyToAsync returns a Task, not a Task<T>.  
                Await responseStream.CopyToAsync(content)  
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
  
## <a name="example"></a>Esempio  
 Il codice seguente mostra le estensioni per il progetto che usa metodo `HttpClient.GetByteArrayAsync` per scaricare il contenuto dal web.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
Imports System.Net  
Imports System.IO  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
  
        resultsTextBox.Clear()  
  
        '' One-step async call.  
        Await SumPageSizesAsync()  
  
        '' Two-step async call.  
        'Dim sumTask As Task = SumPageSizesAsync()  
        'Await sumTask  
  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function SumPageSizesAsync() As Task  
  
        ' Declare an HttpClient object and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' Create a query.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client)  
  
        ' Use ToArray to execute the query and start the download tasks.  
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' You can do other work here before awaiting.  
  
        ' Await the completion of all the running tasks.  
        Dim lengths As Integer() = Await Task.WhenAll(downloadTasks)  
  
        '' The previous line is equivalent to the following two statements.  
        'Dim whenAllTask As Task(Of Integer()) = Task.WhenAll(downloadTasks)  
        'Dim lengths As Integer() = Await whenAllTask  
  
        Dim total = lengths.Sum()  
  
        ''<snippet7>  
        'Dim total = 0  
        'For Each url In urlList  
        '    ' GetByteArrayAsync returns a task. At completion, the task  
        '    ' produces a byte array.  
        '    '<snippet31>  
        '    Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
        '    '</snippet31>  
  
        '    ' The following two lines can replace the previous assignment statement.  
        '    'Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)  
        '    'Dim urlContents As Byte() = Await getContentsTask  
  
        '    DisplayResults(url, urlContents)  
  
        '    ' Update the total.  
        '    total += urlContents.Length  
        'NextNext  
  
        ' Display the total count for all of the web addresses.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://www.msdn.com",  
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
  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
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
 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName></xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>   
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
