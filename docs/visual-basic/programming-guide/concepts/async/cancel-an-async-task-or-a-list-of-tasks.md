---
title: "Annullare un&quot;attività asincrona o un elenco di attività (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: a9ee1b71-5bec-4736-a1e9-448042dd7215
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
ms.openlocfilehash: fe2df73aaf49f1b61dafcad9a6c6e0f3d014f8ec
ms.lasthandoff: 03/13/2017

---
# <a name="cancel-an-async-task-or-a-list-of-tasks-visual-basic"></a>Annullare un'attività asincrona o un elenco di attività (Visual Basic)
È possibile impostare un pulsante che consente di annullare un'applicazione async se non si desidera attendere il completamento. Seguendo gli esempi in questo argomento, è possibile aggiungere un pulsante di annullamento di un'applicazione che consente di scaricare il contenuto di un sito Web o un elenco di siti Web.  
  
 Negli esempi viene utilizzato l'interfaccia utente che [ottimizzazione Async applicazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md) descrive.  
  
> [!NOTE]
>  Per eseguire gli esempi, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
##  <a name="BKMK_CancelaTask"></a>Annullare un'attività  
 Nel primo esempio associa il **Annulla** pulsante con un'attività di solo download. Se si sceglie il pulsante mentre l'applicazione sta scaricando il contenuto, il download viene annullato.  
  
### <a name="downloading-the-example"></a>Download dell'esempio  
 È possibile scaricare il progetto completo di Windows Presentation Foundation (WPF) da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046) e attenersi alla seguente procedura.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Nel **Apri progetto** la finestra di dialogo, aprire la cartella che contiene il codice di esempio che è stato decompresso e quindi aprire il file di soluzione (sln) per AsyncFineTuningVB.  
  
4.  In **Esplora**, aprire il menu di scelta rapida per il **CancelATask** del progetto, quindi fare clic **imposta come progetto di avvio**.  
  
5.  Premere il tasto F5 per eseguire il progetto.  
  
     Premere i tasti Ctrl + F5 per eseguire il progetto senza eseguirne il debug.  
  
 Se non si desidera scaricare il progetto, è possibile esaminare i file MainWindow.xaml.vb alla fine di questo argomento.  
  
### <a name="building-the-example"></a>Compilazione dell'esempio  
 Aggiungono le seguenti modifiche un **Annulla** pulsante a un'applicazione che esegue il download di un sito Web. Se non si desidera scaricare o compilare l'esempio, è possibile esaminare il prodotto finale nella sezione "Esempi completi" alla fine di questo argomento. Gli asterischi contrassegnare le modifiche nel codice.  
  
 Per compilare l'esempio è l'utente passo passo, seguire le istruzioni nella sezione "Download di esempio", ma scegliere **StarterCode** come il **progetto di avvio** invece di **CancelATask**.  
  
 Aggiungere quindi le modifiche seguenti al file MainWindow.xaml.vb del progetto.  
  
1.  Dichiarare un `CancellationTokenSource` variabile, `cts`, nell'ambito per tutti i metodi che vi accedono.  
  
    ```vb  
    Class MainWindow  
  
        ' ***Declare a System.Threading.CancellationTokenSource.  
        Dim cts As CancellationTokenSource  
    ```  
  
2.  Aggiungere il seguente gestore eventi per il **Annulla** pulsante. Il gestore eventi utilizza il <xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>metodo per notificare `cts` quando l'utente richiede l'annullamento.</xref:System.Threading.CancellationTokenSource.Cancel%2A?displayProperty=fullName>  
  
    ```vb  
    ' ***Add an event handler for the Cancel button.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
    ```  
  
3.  Apportare le modifiche seguenti nel gestore per il **avviare** pulsante `startButton_Click`.  
  
    -   Creare un'istanza di `CancellationTokenSource`, `cts`.  
  
        ```vb  
        ' ***Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
        ```  
  
    -   Nella chiamata a `AccessTheWebAsync`, che consente di scaricare il contenuto di un sito Web specificato, invia la <xref:System.Threading.CancellationTokenSource.Token%2A?displayProperty=fullName>proprietà di `cts` come argomento.</xref:System.Threading.CancellationTokenSource.Token%2A?displayProperty=fullName> Il `Token` proprietà propaga il messaggio se viene richiesto l'annullamento. Aggiungere un blocco catch che visualizza un messaggio se l'utente sceglie di annullare l'operazione di download. Il codice seguente mostra le modifiche.  
  
        ```vb  
        Try  
            ' ***Send a token to carry the message if cancellation is requested.  
            Dim contentLength As Integer = Await AccessTheWebAsync(cts.Token)  
  
            resultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
  
            ' *** If cancellation is requested, an OperationCanceledException results.  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf  
        End Try  
        ```  
  
4.  In `AccessTheWebAsync`, utilizzare il <xref:System.Net.Http.HttpClient.GetAsync%28System.String%2CSystem.Threading.CancellationToken%29?displayProperty=fullName>Overload dei metodi di `GetAsync` metodo il <xref:System.Net.Http.HttpClient>tipo per scaricare il contenuto di un sito Web.</xref:System.Net.Http.HttpClient> </xref:System.Net.Http.HttpClient.GetAsync%28System.String%2CSystem.Threading.CancellationToken%29?displayProperty=fullName> Passare `ct`, <xref:System.Threading.CancellationToken>parametro di `AccessTheWebAsync`, come secondo argomento.</xref:System.Threading.CancellationToken> Il token contiene il messaggio se l'utente sceglie il **Annulla** pulsante.  
  
     Il codice seguente mostra le modifiche in `AccessTheWebAsync`.  
  
    ```vb  
    ' ***Provide a parameter for the CancellationToken.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task(Of Integer)  
  
        Dim client As HttpClient = New HttpClient()  
  
        resultsTextBox.Text &=  
            String.Format(vbCrLf & "Ready to download." & vbCrLf)  
  
        ' You might need to slow things down to have a chance to cancel.  
        Await Task.Delay(250)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        ' ***The ct argument carries the message if the Cancel button is chosen.  
        Dim response As HttpResponseMessage = Await client.GetAsync("http://msdn.microsoft.com/library/dd470362.aspx", ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ' The result of the method is the length of the downloaded website.  
        Return urlContents.Length  
    End Function  
    ```  
  
5.  Se non si annulla il programma, produce l'output seguente.  
  
    ```  
    Ready to download.  
    Length of the downloaded string: 158125.  
    ```  
  
     Se si sceglie il **Annulla** pulsante prima il programma termina il download del contenuto, il programma produce l'output seguente.  
  
    ```  
    Ready to download.  
    Download canceled.  
    ```  
  
##  <a name="BKMK_CancelaListofTasks"></a>Annullare un elenco di attività  
 È possibile estendere l'esempio precedente per annullare molte attività associando lo stesso `CancellationTokenSource` istanza con ogni attività. Se si sceglie il **Annulla** pulsante, si annulla tutte le attività che non sono ancora completate.  
  
### <a name="downloading-the-example"></a>Download dell'esempio  
 È possibile scaricare il progetto completo di Windows Presentation Foundation (WPF) da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046) e attenersi alla seguente procedura.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Nel **Apri progetto** la finestra di dialogo, aprire la cartella che contiene il codice di esempio che è stato decompresso e quindi aprire il file di soluzione (sln) per AsyncFineTuningVB.  
  
4.  In **Esplora**, aprire il menu di scelta rapida per il **CancelAListOfTasks** del progetto, quindi fare clic **imposta come progetto di avvio**.  
  
5.  Premere il tasto F5 per eseguire il progetto.  
  
     Premere i tasti Ctrl + F5 per eseguire il progetto senza eseguirne il debug.  
  
 Se non si desidera scaricare il progetto, è possibile esaminare i file MainWindow.xaml.vb alla fine di questo argomento.  
  
### <a name="building-the-example"></a>Compilazione dell'esempio  
 Per estendere l'esempio è l'utente passo passo, seguire le istruzioni nella sezione "Download di esempio", ma scegliere **CancelATask** come il **progetto di avvio**. Aggiungere le seguenti modifiche al progetto. Gli asterischi contrassegnare le modifiche nel programma.  
  
1.  Aggiungere un metodo per creare un elenco di indirizzi web.  
  
    ```vb  
    ' ***Add a method that creates a list of web addresses.  
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
    ```  
  
2.  Chiamare il metodo `AccessTheWebAsync`.  
  
    ```vb  
    ' ***Call SetUpURLList to make a list of web addresses.  
    Dim urlList As List(Of String) = SetUpURLList()  
    ```  
  
3.  Aggiungere il seguente ciclo in `AccessTheWebAsync` per elaborare gli indirizzi web nell'elenco.  
  
    ```vb  
    ' ***Add a loop to process the list of web addresses.  
    For Each url In urlList  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        ' Argument ct carries the message if the Cancel button is chosen.   
        ' ***Note that the Cancel button can cancel all remaining downloads.  
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        resultsTextBox.Text &=  
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
    Next  
    ```  
  
4.  Poiché `AccessTheWebAsync` Visualizza le lunghezze, il metodo non è necessario restituire un valore. Rimuovere l'istruzione return e modificare il tipo restituito del metodo per <xref:System.Threading.Tasks.Task>anziché <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task>  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
     Chiamare il metodo dal `startButton_Click` utilizzando un'istruzione anziché un'espressione.  
  
    ```vb  
    Await AccessTheWebAsync(cts.Token)  
    ```  
  
5.  Se non si annulla il programma, produce l'output seguente.  
  
    ```  
  
    Length of the downloaded string: 35939.  
  
    Length of the downloaded string: 237682.  
  
    Length of the downloaded string: 128607.  
  
    Length of the downloaded string: 158124.  
  
    Length of the downloaded string: 204890.  
  
    Length of the downloaded string: 175488.  
  
    Length of the downloaded string: 145790.  
  
    Downloads complete.  
  
    ```  
  
     Se si sceglie il **Annulla** pulsante prima di aver completato il download, l'output contiene le lunghezze dei download completato prima dell'annullamento.  
  
    ```  
    Length of the downloaded string: 35939.  
  
    Length of the downloaded string: 237682.  
  
    Length of the downloaded string: 128607.  
  
    Downloads canceled.  
  
    ```  
  
##  <a name="BKMK_CompleteExamples"></a>Esempi completi  
 Nelle sezioni seguenti contengono il codice per ognuno degli esempi precedenti. Si noti che è necessario aggiungere un riferimento per <xref:System.Net.Http>.</xref:System.Net.Http>  
  
 È possibile scaricare i progetti da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046).  
  
### <a name="cancel-a-task-example"></a>Annullare un'attività di esempio  
 Il codice seguente è il file MainWindow.xaml.vb completo per l'esempio che consente di annullare una singola attività.  
  
```vb  
' Add an Imports directive and a reference for System.Net.Http.  
Imports System.Net.Http  
  
' Add the following Imports directive for System.Threading.  
Imports System.Threading  
  
Class MainWindow  
  
    ' ***Declare a System.Threading.CancellationTokenSource.  
    Dim cts As CancellationTokenSource  
  
    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
        ' ***Instantiate the CancellationTokenSource.  
        cts = New CancellationTokenSource()  
  
        resultsTextBox.Clear()  
  
        Try  
            ' ***Send a token to carry the message if cancellation is requested.  
            Dim contentLength As Integer = Await AccessTheWebAsync(cts.Token)  
  
            resultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
  
            ' *** If cancellation is requested, an OperationCanceledException results.  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Download failed." & vbCrLf  
        End Try  
  
        ' ***Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' ***Add an event handler for the Cancel button.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' ***Provide a parameter for the CancellationToken.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task(Of Integer)  
  
        Dim client As HttpClient = New HttpClient()  
  
        resultsTextBox.Text &=  
            String.Format(vbCrLf & "Ready to download." & vbCrLf)  
  
        ' You might need to slow things down to have a chance to cancel.  
        Await Task.Delay(250)  
  
        ' GetAsync returns a Task(Of HttpResponseMessage).   
        ' ***The ct argument carries the message if the Cancel button is chosen.  
        Dim response As HttpResponseMessage = Await client.GetAsync("http://msdn.microsoft.com/library/dd470362.aspx", ct)  
  
        ' Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ' The result of the method is the length of the downloaded website.  
        Return urlContents.Length  
    End Function  
End Class  
  
' Output for a successful download:  
  
' Ready to download.  
  
' Length of the downloaded string: 158125.  
  
' Or, if you cancel:  
  
' Ready to download.  
  
' Download canceled.  
```  
  
### <a name="cancel-a-list-of-tasks-example"></a>Annullare un elenco di esempio di attività  
 Il codice seguente è il file MainWindow.xaml.vb completo per l'esempio che consente di annullare un elenco di attività.  
  
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
            ' ***AccessTheWebAsync returns a Task, not a Task(Of Integer).  
            Await AccessTheWebAsync(cts.Token)  
            '  ***Small change in the display lines.  
            resultsTextBox.Text &= vbCrLf & "Downloads complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf  
        End Try  
  
        ' Set the CancellationTokenSource to Nothing when the download is complete.  
        cts = Nothing  
    End Sub  
  
    ' Add an event handler for the Cancel button.  
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)  
  
        If cts IsNot Nothing Then  
            cts.Cancel()  
        End If  
    End Sub  
  
    ' Provide a parameter for the CancellationToken.  
    ' ***Change the return type to Task because the method has no return statement.  
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
        Dim client As HttpClient = New HttpClient()  
  
        ' ***Call SetUpURLList to make a list of web addresses.  
        Dim urlList As List(Of String) = SetUpURLList()  
  
        ' ***Add a loop to process the list of web addresses.  
        For Each url In urlList  
            ' GetAsync returns a Task(Of HttpResponseMessage).   
            ' Argument ct carries the message if the Cancel button is chosen.   
            ' ***Note that the Cancel button can cancel all remaining downloads.  
            Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
            ' Retrieve the website contents from the HttpResponseMessage.  
            Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
            resultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
        Next  
    End Function  
  
    ' ***Add a method that creates a list of web addresses.  
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
  
' Output if you do not choose to cancel:  
  
' Length of the downloaded string: 35939.  
  
' Length of the downloaded string: 237682.  
  
' Length of the downloaded string: 128607.  
  
' Length of the downloaded string: 158124.  
  
' Length of the downloaded string: 204890.  
  
' Length of the downloaded string: 175488.  
  
' Length of the downloaded string: 145790.  
  
' Downloads complete.  
  
'  Sample output if you choose to cancel:  
  
' Length of the downloaded string: 35939.  
  
' Length of the downloaded string: 237682.  
  
' Length of the downloaded string: 128607.  
  
' Downloads canceled.  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.CancellationTokenSource></xref:System.Threading.CancellationTokenSource>   
 <xref:System.Threading.CancellationToken></xref:System.Threading.CancellationToken>   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Ottimizzazione dell'applicazione Async (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [Esempio asincrono: Ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046)
