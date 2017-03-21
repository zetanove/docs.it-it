---
title: "Avviare più attività asincrone ed elaborarle quando vengono completate (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: 57ffb748-af40-4794-bedd-bdb7fea062de
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
ms.openlocfilehash: 6fbf4611ecd64abfd016963dff887d82aad333b7
ms.lasthandoff: 03/13/2017

---
# <a name="start-multiple-async-tasks-and-process-them-as-they-complete-visual-basic"></a>Avviare più attività asincrone ed elaborarle quando vengono completate (Visual Basic)
Utilizzando <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>, è possibile avviare più attività contemporaneamente ed elaborare uno alla volta, si è completati invece di elaborarle nell'ordine in cui è avviati.</xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=fullName>  
  
 Nell'esempio seguente viene utilizzata una query per creare una raccolta di attività. Ogni attività Scarica il contenuto di un sito Web specificato. In ogni iterazione di un periodo di tempo del ciclo, una chiamata a atteso `WhenAny` restituisce l'attività nella raccolta di attività che termina il download per prima. Tale attività viene rimossa dalla raccolta ed elaborato. Il ciclo viene ripetuto fino a quando la raccolta non contiene altre attività.  
  
> [!NOTE]
>  Per eseguire gli esempi, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
## <a name="downloading-the-example"></a>Download dell'esempio  
 È possibile scaricare il progetto completo di Windows Presentation Foundation (WPF) da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046) e attenersi alla seguente procedura.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Nel **Apri progetto** la finestra di dialogo, aprire la cartella che contiene il codice di esempio che è stato decompresso e quindi aprire il file di soluzione (sln) per AsyncFineTuningVB.  
  
4.  In **Esplora**, aprire il menu di scelta rapida per il **ProcessTasksAsTheyFinish** del progetto, quindi fare clic **imposta come progetto di avvio**.  
  
5.  Premere il tasto F5 per eseguire il progetto.  
  
     Premere i tasti Ctrl + F5 per eseguire il progetto senza eseguirne il debug.  
  
6.  Eseguire il progetto più volte per verificare che le lunghezze scaricate non siano sempre visualizzati nello stesso ordine.  
  
 Se non si desidera scaricare il progetto, è possibile esaminare il file MainWindow.xaml.vb alla fine di questo argomento.  
  
## <a name="building-the-example"></a>Compilazione dell'esempio  
 Questo esempio viene aggiunto al codice che è stato sviluppato in [annullare attività asincrone rimanenti dopo una completa (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md) e utilizza la stessa interfaccia utente.  
  
 Per compilare l'esempio è l'utente passo passo, seguire le istruzioni nella sezione "Download di esempio", ma scegliere **CancelAfterOneTask** come il **progetto di avvio**. Aggiungere le modifiche in questo argomento per il `AccessTheWebAsync` metodo nel progetto. Le modifiche sono contrassegnate con asterischi.  
  
 Il **CancelAfterOneTask** progetto include già una query che, quando eseguita, crea una raccolta di attività. Ogni chiamata a `ProcessURLAsync` nel codice seguente restituisce un <xref:System.Threading.Tasks.Task%601>dove `TResult` è un numero intero.</xref:System.Threading.Tasks.Task%601>  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Nel file MainWindow.xaml.vb del progetto, apportare le modifiche seguenti per il `AccessTheWebAsync` metodo.  
  
-   Eseguire la query applicando <xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>anziché <xref:System.Linq.Enumerable.ToArray%2A>.</xref:System.Linq.Enumerable.ToArray%2A> </xref:System.Linq.Enumerable.ToList%2A?displayProperty=fullName>  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
-   Aggiungere un po' di tempo ciclo che esegue i passaggi seguenti per ogni attività nella raccolta.  
  
    1.  Attende una chiamata a `WhenAny` per identificare la prima attività da completare il download nella raccolta.  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
    2.  Rimuove l'attività dalla raccolta.  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
    3.  Attende `firstFinishedTask`, che viene restituito da una chiamata a `ProcessURLAsync`. Il `firstFinishedTask` variabile è un <xref:System.Threading.Tasks.Task%601>dove `TReturn` è un numero intero.</xref:System.Threading.Tasks.Task%601> L'attività è già completa, ma si è in attesa per recuperare la lunghezza del sito Web scaricato, come illustrato nell'esempio seguente.  
  
        ```vb  
        Dim length = Await firstFinishedTask  
        resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        ```  
  
 È necessario eseguire il progetto più volte per verificare che le lunghezze scaricate non siano sempre visualizzati nello stesso ordine.  
  
> [!CAUTION]
>  È possibile utilizzare `WhenAny` in un ciclo, come descritto nell'esempio, per risolvere i problemi che coinvolgono un numero limitato di attività. Tuttavia, se ci sono molte attività da elaborare, altri approcci sono più efficienti. Per ulteriori informazioni ed esempi, vedere [man mano che completa le attività di elaborazione](http://go.microsoft.com/fwlink/?LinkId=260810).  
  
## <a name="complete-example"></a>Esempio completo  
 Il codice seguente è il testo completo del file MainWindow.xaml.vb per l'esempio. Gli asterischi contrassegnare gli elementi che sono stati aggiunti per questo esempio.  
  
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
            resultsTextBox.Text &= vbCrLf & "Downloads complete."  
  
        Catch ex As OperationCanceledException  
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf  
  
        Catch ex As Exception  
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf  
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
  
        ' ***Create a query that, when executed, returns a collection of tasks.  
        Dim downloadTasksQuery As IEnumerable(Of Task(Of Integer)) =  
            From url In urlList Select ProcessURLAsync(url, client, ct)  
  
        ' ***Use ToList to execute the query and start the download tasks.   
        Dim downloadTasks As List(Of Task(Of Integer)) = downloadTasksQuery.ToList()  
  
        ' ***Add a loop to process the tasks one at a time until none remain.  
        While downloadTasks.Count > 0  
            ' ***Identify the first task that completes.  
            Dim firstFinishedTask As Task(Of Integer) = Await Task.WhenAny(downloadTasks)  
  
            ' ***Remove the selected task from the list so that you don't  
            ' process it more than once.  
            downloadTasks.Remove(firstFinishedTask)  
  
            ' ***Await the first completed task and display the results.  
            Dim length = Await firstFinishedTask  
            resultsTextBox.Text &= String.Format(vbCrLf & "Length of the downloaded website:  {0}" & vbCrLf, length)  
        End While  
  
    End Function  
  
    ' Bundle the processing steps for a website into one async method.  
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
  
' Length of the download:  226093  
' Length of the download:  412588  
' Length of the download:  175490  
' Length of the download:  204890  
' Length of the download:  158855  
' Length of the download:  145790  
' Length of the download:  44908  
' Downloads complete.  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Tasks.Task.WhenAny%2A></xref:System.Threading.Tasks.Task.WhenAny%2A>   
 [Ottimizzazione dell'applicazione Async (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Esempio asincrono: Ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046)
