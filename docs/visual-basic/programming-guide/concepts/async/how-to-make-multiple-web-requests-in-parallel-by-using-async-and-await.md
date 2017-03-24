---
title: "Procedura: effettuare più richieste Web in parallelo tramite Async e Await (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: a894b99b-7cfd-4a38-adfb-20d24f986730
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
ms.openlocfilehash: e4c41cc3813a9f96d944d115c6aaa5c5842a629b
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-visual-basic"></a>Procedura: effettuare più richieste Web in parallelo tramite Async e Await (Visual Basic)
In un metodo asincrono, le attività vengono avviate quando vengono creati. Il [Await](../../../../visual-basic/language-reference/operators/await-operator.md) operatore viene applicato all'attività in corrispondenza del punto nel metodo in cui è Impossibile continuare l'elaborazione fino al termine dell'attività. Spesso un'attività è atteso appena creato, come illustrato nell'esempio seguente.  
  
```vb  
Dim result = Await someWebAccessMethodAsync(url)  
```  
  
 Tuttavia, è possibile separare la creazione dell'attività che non dipendono dal completamento dell'attività da attendere l'attività se il programma dispone di altre attività da eseguire.  
  
```vb  
' The following line creates and starts the task.  
Dim myTask = someWebAccessMethodAsync(url)  
  
' While the task is running, you can do other work that does not depend  
' on the results of the task.  
' . . . . .  
  
' The application of Await suspends the rest of this method until the task is   
' complete.  
Dim result = Await myTask  
  
```  
  
 Tra l'avvio di un'attività e, in attesa, è possibile avviare altre attività. Le attività aggiuntive eseguite in modo implicito in parallelo, ma non gli altri thread vengono creati.  
  
 Il seguente programma inizia tre download web asincrono e quindi li attende nell'ordine in cui vengono chiamati. Si noti che, quando si esegue il programma, che non sempre alla fine dell'attività nell'ordine in cui sono creati e atteso. Avviano l'esecuzione quando vengono creati e uno o più delle attività potrebbe terminare prima che il metodo raggiunga le espressioni await.  
  
> [!NOTE]
>  Per completare il progetto, è necessario Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer.  
  
 Ad esempio un altro che avvii più operazioni contemporaneamente, vedere [procedura: estendere la Async Walkthrough da tramite Task. whenall (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
 È possibile scaricare il codice per questo esempio dalla [Developer Code Samples](http://go.microsoft.com/fwlink/?LinkId=254906).  
  
### <a name="to-set-up-the-project"></a>Per impostare il progetto  
  
1.  Per configurare un'applicazione WPF, completare i passaggi seguenti. È possibile trovare istruzioni dettagliate per le operazioni in [procedura dettagliata: accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Creare un'applicazione WPF che contiene una casella di testo e un pulsante. Denominare il pulsante `startButton`e la casella di testo Nome `resultsTextBox`.  
  
    -   Aggiungere un riferimento per <xref:System.Net.Http>.</xref:System.Net.Http>  
  
    -   Nel file MainWindow.xaml.vb, aggiungere un `Imports` istruzione per `System.Net.Http`.  
  
### <a name="to-add-the-code"></a>Per aggiungere il codice  
  
1.  Nella finestra di progettazione, MainWindow. XAML, fare doppio clic sul pulsante per creare il `startButton_Click` gestore dell'evento nel file MainWindow.xaml.vb.  
  
2.  Copiare il codice seguente e incollarlo nel corpo di `startButton_Click` in MainWindow.xaml.vb.  
  
    ```vb  
    resultsTextBox.Clear()  
    Await CreateMultipleTasksAsync()  
    resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    ```  
  
     Il codice chiama un metodo asincrono, `CreateMultipleTasksAsync`, le unità di cui l'applicazione.  
  
3.  Aggiungere i seguenti metodi di supporto al progetto:  
  
    -   `ProcessURLAsync`utilizza un <xref:System.Net.Http.HttpClient>metodo per scaricare il contenuto di un sito Web come una matrice di byte.</xref:System.Net.Http.HttpClient> Il metodo di supporto, `ProcessURLAsync` quindi Visualizza e restituisce la lunghezza della matrice.  
  
    -   `DisplayResults`Visualizza il numero di byte nella matrice di byte per ogni URL. Questa visualizzazione mostra quando ogni attività ha terminato il download.  
  
     Copiare i metodi seguenti e incollarli dopo il `startButton_Click` gestore dell'evento nel file MainWindow.xaml.vb.  
  
    ```vb  
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
    ```  
  
4.  Infine, definire metodo `CreateMultipleTasksAsync`, che consente di eseguire la procedura seguente.  
  
    -   Il metodo dichiara un `HttpClient` oggetto, è necessario accedere al metodo <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>in `ProcessURLAsync`.</xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>  
  
    -   Il metodo crea e avvia le tre attività di tipo <xref:System.Threading.Tasks.Task%601>, dove `TResult` è un numero intero.</xref:System.Threading.Tasks.Task%601> Di al termine di ogni attività, `DisplayResults` Visualizza l'URL dell'attività e la lunghezza del contenuto scaricato. Poiché le attività sono in esecuzione in modo asincrono, l'ordine in cui vengono visualizzati i risultati potrebbero essere diversi da quello in cui sono stati dichiarati.  
  
    -   Il metodo attenderà il completamento di ogni attività. Ogni `Await` operatore sospende l'esecuzione di `CreateMultipleTasksAsync` finché non viene completata l'attività attesa. L'operatore recupera inoltre il valore restituito dalla chiamata a `ProcessURLAsync` da ogni attività completata.  
  
    -   Quando sono state completate le attività e sono stati recuperati i valori interi, il metodo somma le lunghezze dei siti Web e viene visualizzato il risultato.  
  
     Copiare il metodo seguente e incollarlo in una soluzione.  
  
    ```vb  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
    ```  
  
5.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Eseguire il programma più volte per verificare che le tre attività non completate sempre nello stesso ordine e che l'ordine in cui vengono completate non è necessariamente l'ordine in cui creazione e di attesa.  
  
## <a name="example"></a>Esempio  
 Il codice seguente contiene l'esempio completo.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
        resultsTextBox.Clear()  
        Await CreateMultipleTasksAsync()  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
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
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Procedura: estendere la procedura dettagliata asincrona tramite Task. whenall (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)
