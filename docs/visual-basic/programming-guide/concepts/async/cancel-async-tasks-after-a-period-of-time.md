---
title: "Annullare attività asincrone dopo un periodo di tempo (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: a48045a3-6a99-42af-b824-af340f0b9a5d
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
ms.openlocfilehash: 6708bd92d8dc2455b9dcb8e02dcc0a4455e00cda
ms.lasthandoff: 03/13/2017

---
# <a name="cancel-async-tasks-after-a-period-of-time-visual-basic"></a>Annullare attività asincrone dopo un periodo di tempo (Visual Basic)
È possibile annullare un'operazione asincrona dopo un periodo di tempo utilizzando il <xref:System.Threading.CancellationTokenSource.CancelAfter%2A?displayProperty=fullName>metodo se non si desidera attendere il completamento dell'operazione.</xref:System.Threading.CancellationTokenSource.CancelAfter%2A?displayProperty=fullName> Questo metodo pianifica l'annullamento di eventuali attività associate che non completata entro il periodo di tempo definito dal `CancelAfter` espressione.  
  
 Questo esempio viene aggiunto al codice che è stato sviluppato in [annullare un'attività asincrona o un elenco di attività (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md) per scaricare un elenco di siti Web e per visualizzare la lunghezza del contenuto di ciascuna di esse.  
  
> [!NOTE]
>  Per eseguire gli esempi, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
## <a name="downloading-the-example"></a>Download dell'esempio  
 È possibile scaricare il progetto completo di Windows Presentation Foundation (WPF) da [esempio asincrono: Fine ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046) e attenersi alla seguente procedura.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Nel **Apri progetto** la finestra di dialogo, aprire la cartella che contiene il codice di esempio che è stato decompresso e quindi aprire il file di soluzione (sln) per AsyncFineTuningVB.  
  
4.  In **Esplora**, aprire il menu di scelta rapida per il **CancelAfterTime** del progetto, quindi fare clic **imposta come progetto di avvio**.  
  
5.  Premere il tasto F5 per eseguire il progetto.  
  
     Premere i tasti Ctrl + F5 per eseguire il progetto senza eseguirne il debug.  
  
6.  Eseguire il programma più volte per verificare che l'output potrebbe essere visualizzato l'output per tutti i siti Web, nessun sito Web o alcuni siti web.  
  
 Se non si desidera scaricare il progetto, è possibile esaminare il file MainWindow.xaml.vb alla fine di questo argomento.  
  
## <a name="building-the-example"></a>Compilazione dell'esempio  
 Nell'esempio riportato in questo argomento viene aggiunto al progetto che è stato sviluppato in [annullare un'attività asincrona o un elenco di attività (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md) per annullare un elenco di attività. Nell'esempio viene utilizzata la stessa interfaccia utente, anche se il **Annulla** pulsante non viene utilizzato in modo esplicito.  
  
 Per compilare l'esempio è l'utente passo passo, seguire le istruzioni nella sezione "Download di esempio", ma scegliere **CancelAListOfTasks** come il **progetto di avvio**. A tale progetto, aggiungere le modifiche in questo argomento.  
  
 Per specificare un tempo massimo prima che l'attività viene contrassegnata come annullata, aggiungere una chiamata a `CancelAfter` a `startButton_Click`, come illustrato nell'esempio seguente. L'aggiunta è contrassegnato con un asterisco.  
  
```vb  
Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)  
  
    ' Instantiate the CancellationTokenSource.  
    cts = New CancellationTokenSource()  
  
    resultsTextBox.Clear()  
  
    Try  
        ' ***Set up the CancellationTokenSource to cancel after 2.5 seconds. (You   
        ' can adjust the time.)  
        cts.CancelAfter(2500)  
  
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
```  
  
 Eseguire il programma più volte per verificare che l'output potrebbe essere visualizzato l'output per tutti i siti Web, nessun sito Web o alcuni siti web. L'output seguente è riportato un esempio.  
  
```  
Length of the downloaded string: 35990.  
  
Length of the downloaded string: 407399.  
  
Length of the downloaded string: 226091.  
  
Downloads canceled.  
```  
  
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
            ' ***Set up the CancellationTokenSource to cancel after 2.5 seconds. (You   
            ' can adjust the time.)  
            cts.CancelAfter(2500)  
  
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
  
        ' Process each element in the list of web addresses.  
        For Each url In urlList  
            ' GetAsync returns a Task(Of HttpResponseMessage).   
            ' Argument ct carries the message if the Cancel button is chosen.   
            ' Note that the Cancel button can cancel all remaining downloads.  
            Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
            ' Retrieve the website contents from the HttpResponseMessage.  
            Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
            resultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, urlContents.Length)  
        Next  
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
  
' Length of the downloaded string: 35990.  
  
' Length of the downloaded string: 407399.  
  
' Length of the downloaded string: 226091.  
  
' Downloads canceled.  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Annullare un'attività asincrona o un elenco di attività (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md)   
 [Ottimizzazione dell'applicazione Async (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md)   
 [Esempio asincrono: Ottimizzazione dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=255046)
