---
title: "Annullare le attività asincrone rimanenti dopo che ne è completa (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: c928b5a1-622f-4441-8baf-adca1dde197f
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
ms.openlocfilehash: 1b70822edd972ac33614ab49faad6ff50b0e80b7
ms.lasthandoff: 03/13/2017

---
# <a name="cancel-remaining-async-tasks-after-one-is-complete-visual-basic"></a>Annullare le attività asincrone rimanenti dopo che ne è completa (Visual Basic)
Tramite il <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>metodo insieme a un <xref:System.Threading.CancellationToken>, è possibile annullare tutte le attività rimanenti quando un'attività è stata completata.</xref:System.Threading.CancellationToken> </xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName> Il `WhenAny` metodo accetta un argomento che rappresenta una raccolta di attività. Il metodo avvia tutte le attività e restituisce una singola attività. La singola operazione è completa quando un'attività nella raccolta è stata completata.  
  
 In questo esempio viene illustrato come utilizzare un token di annullamento in combinazione con `WhenAny` per detenere la prima attività per completare dalla raccolta di attività e per annullare le attività rimanenti. Ogni attività Scarica il contenuto di un sito Web. L'esempio visualizza la lunghezza del contenuto del download prima di completare e Annulla altri download.  
  
> [!NOTE]
>  Per eseguire gli esempi, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
## <a name="downloading-the-example"></a>Download dell'esempio  
 È possibile scaricare il progetto completo di Windows Presentation Foundation (WPF) da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046) e attenersi alla seguente procedura.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Nel **Apri progetto** la finestra di dialogo, aprire la cartella che contiene il codice di esempio che è stato decompresso e quindi aprire il file di soluzione (sln) per AsyncFineTuningVB.  
  
4.  In **Esplora**, aprire il menu di scelta rapida per il **CancelAfterOneTask** del progetto, quindi fare clic **imposta come progetto di avvio**.  
  
5.  Premere il tasto F5 per eseguire il progetto.  
  
     Premere i tasti Ctrl + F5 per eseguire il progetto senza eseguirne il debug.  
  
6.  Eseguire il programma più volte per verificare che il download diversi terminare prima.  
  
 Se non si desidera scaricare il progetto, è possibile esaminare il file MainWindow.xaml.vb alla fine di questo argomento.  
  
## <a name="building-the-example"></a>Compilazione dell'esempio  
 Nell'esempio riportato in questo argomento viene aggiunto al progetto che è stato sviluppato in [annullare un'attività asincrona o un elenco di attività](http://msdn.microsoft.com/library/d6e4e801-df64-4705-98fc-df725a577fb0) per annullare un elenco di attività. Nell'esempio viene utilizzata la stessa interfaccia utente, anche se il **Annulla** pulsante non viene utilizzato in modo esplicito.  
  
 Per compilare l'esempio è l'utente passo passo, seguire le istruzioni nella sezione "Download di esempio", ma scegliere **CancelAListOfTasks** come il **progetto di avvio**. A tale progetto, aggiungere le modifiche in questo argomento.  
  
 Nel file MainWindow.xaml.vb del **CancelAListOfTasks** del progetto, avviare la transizione spostando le fasi di elaborazione per ogni sito Web del ciclo in `AccessTheWebAsync` per il seguente metodo async.  
  
```vb  
' ***Bundle the processing steps for a website into one async method.  
Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
    ' GetAsync returns a Task(Of HttpResponseMessage).   
    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
    ' Retrieve the website contents from the HttpResponseMessage.  
    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
    Return urlContents.Length  
End Function  
```  
  
 In `AccessTheWebAsync`, in questo esempio viene utilizzata una query, il <xref:System.Linq.Enumerable.ToArray%2A>(metodo) e `WhenAny` per creare e avviare attività di una matrice.</xref:System.Linq.Enumerable.ToArray%2A> L'applicazione di `WhenAny` alla matrice viene restituita una singola attività che, quando atteso, restituisce la prima attività per raggiungere il completamento della matrice di attività.  
  
 Apportare le modifiche seguenti in `AccessTheWebAsync`. Gli asterischi contrassegnare le modifiche nel file di codice.  
  
1.  Impostare come commento o eliminare il ciclo.  
  
2.  Creare una query che, quando eseguita, produce un insieme di attività generiche. Ogni chiamata a `ProcessURLAsync` restituisce un <xref:System.Threading.Tasks.Task%601>dove `TResult` è un numero intero.</xref:System.Threading.Tasks.Task%601>  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
3.  Chiamare `ToArray` per eseguire la query e avviare le attività. L'applicazione di `WhenAny` metodo nel passaggio successivo si esegue la query e avviare le attività senza utilizzare `ToArray`, ma non altri metodi. La più sicura consiste nel forzare l'esecuzione della query in modo esplicito.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
4.  Chiamare `WhenAny` sulla raccolta di attività. `WhenAny`Restituisce un `Task(Of Task(Of Integer))` o `Task<Task<int>>`.  Vale a dire `WhenAny` restituisce un'attività che valuta in un unico `Task(Of Integer)` o `Task<int>` quando si è atteso. Singola attività è la prima attività da completare nella raccolta. Attività completata innanzitutto viene assegnato a `firstFinishedTask`. Il tipo di `firstFinishedTask` è <xref:System.Threading.Tasks.Task%601>dove `TResult` è un numero intero che corrisponde al tipo restituito di `ProcessURLAsync`.</xref:System.Threading.Tasks.Task%601>  
  
```vb  
' ***Call WhenAny and then await the result. The task that finishes   
' first is assigned to firstFinishedTask.  
Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
```  
  
5.  In questo esempio, si è interessati solo l'attività che termina per prima. Pertanto, utilizzare <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>per annullare le attività rimanenti.</xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>  
  
```vb  
' ***Cancel the rest of the downloads. You just want the first one.  
cts.Cancel()  
```  
  
6.  Infine, await `firstFinishedTask` per recuperare la lunghezza del contenuto scaricato.  
  
```vb  
Dim length = Await firstFinishedTask  
resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
```  
  
 Eseguire il programma più volte per verificare che il download diversi terminare prima.  
  
## <a name="complete-example"></a>Esempio completo  
 Il codice seguente è il file MainWindow.xaml.vb o MainWindow.xaml.cs completo per l'esempio. Gli asterischi contrassegnare gli elementi che sono stati aggiunti per questo esempio.  
  
 Si noti che è necessario aggiungere un riferimento per <xref:System.Net.Http>.</xref:System.Net.Http>  
  
 È possibile scaricare il progetto da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046).  
  
```vb  
' Add an Imports directive and a reference for System.Net.Http.  
Imports System.Net.Http  
  
' Add the following Imports directive for System.Threading.  
Imports System.Threading  
  
Class MainWindow  
  
    ' Declare a System.Threading.CancellationTokenSource.  
    Dim cts As CancellationTokenSource  
  
    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
  
        ' Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
  
        resultsTextBox.Clear()  
  
        Try  
            Await AccessTheWebAsync(cts.Token)  
            resultsTextBox.Text &= vbCrLf & "Download complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf  
        End Try  
  
        ' Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' You can still include a Cancel button if you want to.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' Provide a parameter for the CancellationToken.  
    ' Change the return type to Task because the method has no return statement.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
        Dim client As HttpClient = New HttpClient()  
  
        ' Call SetUpURLList to make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        '' Comment out or delete the loop.  
        ''For Each url In urlList  
        ''    ' GetAsync returns a Task(Of HttpResponseMessage).   
        ''    ' Argument ct carries the message if the Cancel button is chosen.   
        ''    ' Note that the Cancel button can cancel all remaining downloads.  
        ''    Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ''    ' Retrieve the website contents from the HttpResponseMessage.  
        ''    Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ''    resultsTextBox.Text &=  
        ''        String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
        ''Next  
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToArray to execute the query and start the download tasks.   
        Dim downloadTasks As Task(Of Integer)() = downloadTasksQuery.ToArray()  
  
        ' ***Call WhenAny and then await the result. The task that finishes   
        ' first is assigned to firstFinishedTask.  
        Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
        ' ***Cancel the rest of the downloads. You just want the first one.  
        cts.Cancel()  
  
        ' ***Await the first completed task and display the results  
        ' Run the program several times to demonstrate that different  
        ' websites can finish first.  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
    End Function  
  
    ' ***Bundle the processing steps for a website into one async method.  
    Async Function ProcessURLAsync(url As String, client As HttpClient, ct As CancellationToken) As Task(Of Integer)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        Return urlContents.Length  
    End Function  
  
    ' Add a method that creates a list of web addresses.  
    Private Function SetUpURLList() As List(Of String)  
  
        Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/hh290138.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/dd470362.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
        Return urls  
    End Function  
  
End Class  
  
' Sample output:  
  
' Length of the downloaded website:  158856  
  
' Download complete.  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Tasks.Task.WhenAny%2A></xref:System.Threading.Tasks.Task.WhenAny%2A>   
 [Ottimizzazione dell'applicazione Async (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Esempio asincrono: Ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046)
