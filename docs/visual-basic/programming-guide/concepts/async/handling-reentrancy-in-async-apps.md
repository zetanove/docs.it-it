---
title: Gestione della Reentrancy nelle applicazioni asincrone (Visual Basic) | Documenti di Microsoft
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
ms.assetid: ef3dc73d-13fb-4c5f-a686-6b84148bbffe
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 64a708e3b88f48ad30d3f3ad25141a31f3d8f73d
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="handling-reentrancy-in-async-apps-visual-basic"></a>Gestione della Reentrancy nelle applicazioni asincrone (Visual Basic)
Quando si include codice asincrono nell'applicazione, è consigliabile prevedere ed evitare la reentrancy, ovvero il reinserimento di un'operazione asincrona prima del suo completamento. Se non vengono identificate e gestite le possibilità di reentrancy, esse possono causare risultati imprevisti.  
  
 **Contenuto dell'argomento**  
  
-   [Riconoscimento della Reentrancy](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Gestione della Reentrancy](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Disabilitare il pulsante Start](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Annullare e riavviare l'operazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
    -   [Eseguire più operazioni e mettere in coda di Output](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
-   [Esame ed esecuzione dell'applicazione di esempio](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
##  <a name="BKMK_RecognizingReentrancy"></a>Riconoscimento della Reentrancy  
 Nell'esempio in questo argomento, gli utenti scegliere un **avviare** pulsante per avviare un'applicazione asincrona che scarica una serie di siti Web e calcola il numero totale di byte che sono stati scaricati. Una versione sincrona dell'esempio avrebbe risposto allo stesso modo indipendentemente dal numero di volte che un utente sceglie il pulsante perché, dopo la prima volta, il thread dell'interfaccia utente ignora tali eventi fino al termine dell'esecuzione dell'applicazione. In un'applicazione asincrona, tuttavia, il thread dell'interfaccia utente continua a rispondere e potrebbe essere possibile riattivare l'operazione asincrona prima del suo completamento.  
  
 Nell'esempio seguente viene previsto output se l'utente sceglie il **avviare** solo una volta. Viene visualizzato un elenco dei siti Web scaricati con la dimensione, espressa in byte, di ogni sito. Il numero totale di byte viene visualizzato alla fine.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Tuttavia, se l'utente sceglie il pulsante più volte, il gestore eventi viene chiamato più volte e il processo di download viene riattivato ogni volta. Di conseguenza, diverse operazioni asincrone sono in esecuzione contemporaneamente, l'output si sovrappone ai risultati e il numero totale di byte è poco chiaro.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/en-us/library/jj155761.aspx                29019  
7. msdn.microsoft.com                                            42972  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
7. msdn.microsoft.com                                            42972  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 È possibile esaminare il codice che genera l'output andando alla fine di questo argomento. È possibile sperimentare il codice per scaricare la soluzione nel computer locale e quindi eseguire il progetto WebsiteDownload o utilizzando il codice alla fine di questo argomento per creare un progetto per ulteriori informazioni e istruzioni, vedere [esame ed esecuzione dell'applicazione di esempio](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645).  
  
##  <a name="BKMK_HandlingReentrancy"></a>Gestione della Reentrancy  
 È possibile gestire la reentrancy in diversi modi, a seconda delle operazioni che si desidera che l'applicazione esegua. In questo argomento vengono illustrati gli esempi seguenti:  
  
-   [Disabilitare il pulsante Start](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Disabilitare il **avviare** pulsante mentre l'operazione è in esecuzione in modo che l'utente non comporta l'interruzione.  
  
-   [Annullare e riavviare l'operazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Annullare qualsiasi operazione che è ancora in esecuzione quando l'utente sceglie il **avviare** nuovamente clic sul pulsante e quindi continuare con consentono l'operazione richiesta più recente.  
  
-   [Eseguire più operazioni e mettere in coda di Output](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645)  
  
     Consentire l'esecuzione asincrona di tutte le operazioni richieste, ma coordinare la visualizzazione dell'output in modo che vengano visualizzati i risultati di ogni operazione tutti insieme e ordinati.  
  
###  <a name="BKMK_DisableTheStartButton"></a>Disabilitare il pulsante Start  
 È possibile bloccare la **avviare** pulsante mentre è in esecuzione un'operazione disattivando il pulsante in cima il `StartButton_Click` gestore dell'evento. È possibile riabilitare il pulsante dall'interno un blocco `Finally` al termine dell'operazione in modo che gli utenti possano eseguire nuovamente l'applicazione.  
  
 Il codice seguente illustra queste modifiche, contrassegnate da asterischi. È possibile aggiungere le modifiche al codice alla fine di questo argomento, oppure è possibile scaricare l'applicazione finita da [Async esempi: della Reentrancy nelle applicazioni Desktop di .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Il nome del progetto è DisableStartButton.  
  
```vb  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
    ' This line is commented out to make the results clearer in the output.  
    'ResultsTextBox.Text = ""  
  
    ' ***Disable the Start button until the downloads are complete.   
    StartButton.IsEnabled = False  
  
    Try  
        Await AccessTheWebAsync()  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
    ' ***Enable the Start button in case you want to run the program again.   
    Finally  
        StartButton.IsEnabled = True  
  
    End Try  
End Sub  
```  
  
 In seguito alle modifiche, il pulsante non risponde mentre `AccessTheWebAsync` sta scaricando i siti Web. Pertanto, il processo non potrà essere riattivato.  
  
###  <a name="BKMK_CancelAndRestart"></a>Annullare e riavviare l'operazione  
 Anziché la disabilitazione di **avviare** pulsante, è possibile mantenere attivo il pulsante ma, se l'utente sceglie il pulsante nuovo, annullare l'operazione che è già in esecuzione e consente di continuare l'operazione avviata più di recente.  
  
 Per ulteriori informazioni sull'annullamento, vedere [ottimizzazione Async applicazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md).  
  
 Per configurare questo scenario, apportare le modifiche seguenti al codice di base fornita in [esame ed esecuzione dell'applicazione di esempio](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645). È inoltre possibile scaricare l'applicazione finita da [Async esempi: della Reentrancy nelle applicazioni Desktop di .NET](http://go.microsoft.com/fwlink/?LinkId=266571). Il nome di questo progetto è CancelAndRestart.  
  
1.  Dichiarare un <xref:System.Threading.CancellationTokenSource>variabile, `cts`, nell'ambito per tutti i metodi.</xref:System.Threading.CancellationTokenSource>  
  
    ```vb  
    Class MainWindow // Or Class MainPage  
  
        ' *** Declare a System.Threading.CancellationTokenSource.  
        Dim cts As CancellationTokenSource  
    ```  
  
2.  In `StartButton_Click` determinare se un'operazione è già in corso. Se il valore di `cts` è `Nothing`, nessuna operazione è già attiva. Se il valore non è `Nothing`, l'operazione che è già in esecuzione viene annullata.  
  
    ```vb  
    ' *** If a download process is already underway, cancel it.  
    If cts IsNot Nothing Then  
        cts.Cancel()  
    End If  
    ```  
  
3.  Impostare `cts` su un valore diverso che rappresenti il processo corrente.  
  
    ```vb  
    ' *** Now set cts to cancel the current process if the button is chosen again.  
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()  
    cts = newCTS  
    ```  
  
4.  Alla fine di `StartButton_Click`, il processo corrente è stato completato, quindi impostare il valore di `cts` al `Nothing`.  
  
    ```vb  
    ' *** When the process completes, signal that another process can proceed.  
    If cts Is newCTS Then  
        cts = Nothing  
    End If  
    ```  
  
 Il codice seguente illustra tutte le modifiche in `StartButton_Click`. Le aggiunte sono contrassegnate con asterischi.  
  
```vb  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
    ' This line is commented out to make the results clearer.   
    'ResultsTextBox.Text = ""  
  
    ' *** If a download process is underway, cancel it.  
    If cts IsNot Nothing Then  
        cts.Cancel()  
    End If  
  
    ' *** Now set cts to cancel the current process if the button is chosen again.  
    Dim newCTS As CancellationTokenSource = New CancellationTokenSource()  
    cts = newCTS  
  
    Try  
        ' *** Send a token to carry the message if the operation is canceled.  
        Await AccessTheWebAsync(cts.Token)  
  
    Catch ex As OperationCanceledException  
        ResultsTextBox.Text &= vbCrLf & "Download canceled." & vbCrLf  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
    End Try  
  
    ' *** When the process is complete, signal that another process can proceed.  
    If cts Is newCTS Then  
        cts = Nothing  
    End If  
End Sub  
```  
  
 In `AccessTheWebAsync`, apportare le seguenti modifiche.  
  
-   Aggiungere un parametro per accettare il token di annullamento da `StartButton_Click`.  
  
-   Utilizzare il <xref:System.Net.Http.HttpClient.GetAsync%2A>metodo per scaricare i siti Web perché `GetAsync` accetta un <xref:System.Threading.CancellationToken>argomento.</xref:System.Threading.CancellationToken> </xref:System.Net.Http.HttpClient.GetAsync%2A>  
  
-   Prima di chiamare `DisplayResults` per visualizzare i risultati per ogni sito Web scaricato, controllare `ct` per verificare che l'operazione corrente non sia stata annullata.  
  
 Il codice seguente illustra queste modifiche, contrassegnate da asterischi.  
  
```vb  
' *** Provide a parameter for the CancellationToken from StartButton_Click.  
Private Async Function AccessTheWebAsync(ct As CancellationToken) As Task  
  
    ' Declare an HttpClient object.  
    Dim client = New HttpClient()  
  
    ' Make a list of web addresses.  
    Dim urlList As List(Of String) = SetUpURLList()  
  
    Dim total = 0  
    Dim position = 0  
  
    For Each url In urlList  
        ' *** Use the HttpClient.GetAsync method because it accepts a   
        ' cancellation token.  
        Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)  
  
        ' *** Retrieve the website contents from the HttpResponseMessage.  
        Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()  
  
        ' *** Check for cancellations before displaying information about the   
        ' latest site.   
        ct.ThrowIfCancellationRequested()  
  
        position += 1  
        DisplayResults(url, urlContents, position)  
  
        ' Update the total.  
        total += urlContents.Length  
    Next  
  
    ' Display the total count for all of the websites.  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
End Function  
```  
  
 Se si sceglie il **avviare** diverse volte durante l'esecuzione di questa app deve produrre risultati simili all'output seguente.  
  
```  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               122505  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
Download canceled.  
  
1. msdn.microsoft.com/library/hh191443.aspx                83732  
2. msdn.microsoft.com/library/aa578028.aspx               205273  
3. msdn.microsoft.com/library/jj155761.aspx                29019  
4. msdn.microsoft.com/library/hh290140.aspx               117152  
5. msdn.microsoft.com/library/hh524395.aspx                68959  
6. msdn.microsoft.com/library/ms404677.aspx               197325  
7. msdn.microsoft.com                                            42972  
8. msdn.microsoft.com/library/ff730837.aspx               146159  
  
TOTAL bytes returned:  890591  
```  
  
 Per eliminare gli elenchi parziali, rimuovere la prima riga di codice in `StartButton_Click` per cancellare la casella di testo ogni volta che l'utente riavvia l'operazione.  
  
###  <a name="BKMK_RunMultipleOperations"></a>Eseguire più operazioni e mettere in coda di Output  
 Il terzo esempio è la più complicata in quanto l'app viene avviata un'altra operazione asincrona ogni volta che l'utente sceglie il **avviare** pulsante e tutte le operazioni eseguite fino al completamento. Tutte le operazioni richieste scaricano i siti Web dall'elenco in modo asincrono, ma l'output delle operazioni viene visualizzato in sequenza. Vale a dire l'effettiva attività di download viene interfacciato, come output in [il riconoscimento della Reentrancy](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) illustrato, ma l'elenco dei risultati per ogni gruppo viene presentato separatamente.  
  
 Le operazioni di condividono globale <xref:System.Threading.Tasks.Task>, `pendingWork`, che funge da gatekeeper per il processo di visualizzazione.</xref:System.Threading.Tasks.Task>  
  
 È possibile eseguire questo esempio incollando le modifiche nel codice [compilazione dell'applicazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), oppure è possibile seguire le istruzioni in [download dell'applicazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) per scaricare l'esempio e quindi eseguire il progetto QueueResults.  
  
 L'output seguente viene illustrato il risultato se l'utente sceglie il **avviare** solo una volta. L'etichetta, lettera A, indica che il risultato è dalla prima volta il **avviare** pulsante viene scelto. I numeri indicano l'ordine degli URL nell'elenco delle destinazioni di download.  
  
```  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               209858  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
A-7. msdn.microsoft.com                                            53266  
A-8. msdn.microsoft.com/library/ff730837.aspx               148020  
  
TOTAL bytes returned:  918876  
  
#Group A is complete.  
```  
  
 Se l'utente sceglie il **avviare** pulsante tre volte, l'applicazione produce un output simile le righe seguenti. Le righe di informazioni che iniziano con un cancelletto (#) tengono traccia dello stato di avanzamento dell'applicazione.  
  
```  
#Starting group A.  
#Task assigned for group A.  
  
A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
A-4. msdn.microsoft.com/library/hh290140.aspx               119027  
A-5. msdn.microsoft.com/library/hh524395.aspx                71259  
A-6. msdn.microsoft.com/library/ms404677.aspx               199185  
  
#Starting group B.  
#Task assigned for group B.  
  
A-7. msdn.microsoft.com                                            53266  
  
#Starting group C.  
#Task assigned for group C.  
  
A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916095  
  
B-1. msdn.microsoft.com/library/hh191443.aspx                87389  
B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
  
#Group A is complete.  
  
B-7. msdn.microsoft.com                                            53266  
B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  916097  
  
C-1. msdn.microsoft.com/library/hh191443.aspx                87389  
C-2. msdn.microsoft.com/library/aa578028.aspx               207089  
  
#Group B is complete.  
  
C-3. msdn.microsoft.com/library/jj155761.aspx                30870  
C-4. msdn.microsoft.com/library/hh290140.aspx               119027  
C-5. msdn.microsoft.com/library/hh524395.aspx                72765  
C-6. msdn.microsoft.com/library/ms404677.aspx               199186  
C-7. msdn.microsoft.com                                            56190  
C-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
TOTAL bytes returned:  920526  
  
#Group C is complete.  
```  
  
 I gruppi B e C vengono avviati prima del completamento del gruppo A, ma l'output per ogni gruppo viene visualizzato separatamente. Tutto l'output per il gruppo viene visualizzata per prima, seguita da tutto l'output per il gruppo B e quindi tutto l'output per il gruppo C. L'applicazione sempre vengono visualizzati i gruppi in ordine e, per ogni gruppo, viene visualizzato sempre le informazioni sui singoli siti Web nell'ordine in cui gli URL vengono visualizzati nell'elenco di URL.  
  
 Tuttavia, è possibile prevedere l'ordine in cui vengono eseguiti i download. Dopo l'avvio di più gruppi, tutte le attività di download generate sono attive. Non è possibile presupporre che A-1 venga scaricato prima di B-1 e che A-1 venga scaricato prima A&2;.  
  
#### <a name="global-definitions"></a>Definizioni globali  
 Il codice di esempio contiene le seguenti dichiarazioni globali visibili da tutti i metodi.  
  
```vb  
Class MainWindow    ' Class MainPage in Windows Store app.  
  
    ' ***Declare the following variables where all methods can access them.   
    Private pendingWork As Task = Nothing  
    Private group As Char = ChrW(AscW("A") - 1)  
```  
  
 La variabile `Task`, `pendingWork`, controlla il processo di visualizzazione e impedisce a qualsiasi gruppo di interrompere l'operazione di visualizzazione di un altro gruppo. La variabile di tipo carattere, `group`, etichetta l'output dei vari gruppi per far sì che i risultati vengano visualizzati nell'ordine previsto.  
  
#### <a name="the-click-event-handler"></a>Il gestore eventi Click  
 Il gestore dell'evento, `StartButton_Click`, la lettera di gruppo viene incrementato ogni volta che l'utente sceglie il **avviare** pulsante. Il gestore chiama quindi `AccessTheWebAsync` per eseguire l'operazione di download.  
  
```vb  
Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
    ' ***Verify that each group's results are displayed together, and that  
    ' the groups display in order, by marking each group with a letter.  
    group = ChrW(AscW(group) + 1)  
    ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Starting group {0}.", group)  
  
    Try  
        ' *** Pass the group value to AccessTheWebAsync.  
        Dim finishedGroup As Char = Await AccessTheWebAsync(group)  
  
        ' The following line verifies a successful return from the download and   
        ' display procedures.   
        ResultsTextBox.Text &= String.Format(vbCrLf & vbCrLf & "#Group {0} is complete." & vbCrLf, finishedGroup)  
  
    Catch ex As Exception  
        ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
  
    End Try  
End Sub  
```  
  
#### <a name="the-accessthewebasync-method"></a>Il metodo AccessTheWebAsync  
 Questo esempio suddivide `AccessTheWebAsync` in due metodi. Il primo metodo, `AccessTheWebAsync`, avvia tutte le attività di download per un gruppo e configura `pendingWork` per il controllo del processo di visualizzazione. Il metodo utilizza una Language Integrated Query (LINQ) e <xref:System.Linq.Enumerable.ToArray%2A>per avviare tutte le attività di download nello stesso momento.</xref:System.Linq.Enumerable.ToArray%2A>  
  
 `AccessTheWebAsync` quindi chiama `FinishOneGroupAsync` per attendere il completamento di ogni download e visualizzare la relativa lunghezza.  
  
 `FinishOneGroupAsync` restituisce un'attività assegnata a `pendingWork` in `AccessTheWebAsync`. Tale valore impedisce l'interruzione da parte di un'altra operazione prima del completamento dell'attività.  
  
```vb  
Private Async Function AccessTheWebAsync(grp As Char) As Task(Of Char)  
  
    Dim client = New HttpClient()  
  
    ' Make a list of the web addresses to download.  
    Dim urlList As List(Of String) = SetUpURLList()  
  
    ' ***Kick off the downloads. The application of ToArray activates all the download tasks.  
    Dim getContentTasks As Task(Of Byte())() =  
        urlList.Select(Function(addr) client.GetByteArrayAsync(addr)).ToArray()  
  
    ' ***Call the method that awaits the downloads and displays the results.  
    ' Assign the Task that FinishOneGroupAsync returns to the gatekeeper task, pendingWork.  
    pendingWork = FinishOneGroupAsync(urlList, getContentTasks, grp)  
  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & "#Task assigned for group {0}. Download tasks are active." & vbCrLf, grp)  
  
    ' ***This task is complete when a group has finished downloading and displaying.  
    Await pendingWork  
  
    ' You can do other work here or just return.  
    Return grp  
End Function  
```  
  
#### <a name="the-finishonegroupasync-method"></a>Il metodo FinishOneGroupAsync  
 Questo metodo consente di scorrere le attività di download in reciproca attesa in un gruppo, nonché visualizza la lunghezza del sito Web scaricato e aggiunge la lunghezza al totale.  
  
 La prima istruzione in `FinishOneGroupAsync` utilizza `pendingWork` per assicurarsi che il metodo non interferisca con un'operazione che è già in corso la visualizzazione o che è già in attesa. Se tale operazione è in corso, l'operazione di attivazione deve attendere il suo turno.  
  
```vb  
Private Async Function FinishOneGroupAsync(urls As List(Of String), contentTasks As Task(Of Byte())(), grp As Char) As Task  
  
    ' Wait for the previous group to finish displaying results.  
    If pendingWork IsNot Nothing Then  
        Await pendingWork  
    End If  
  
    Dim total = 0  
  
    ' contentTasks is the array of Tasks that was created in AccessTheWebAsync.  
    For i As Integer = 0 To contentTasks.Length - 1  
        ' Await the download of a particular URL, and then display the URL and  
        ' its length.  
        Dim content As Byte() = Await contentTasks(i)  
        DisplayResults(urls(i), content, i, grp)  
        total += content.Length  
    Next  
  
    ' Display the total count for all of the websites.  
    ResultsTextBox.Text &=  
        String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
End Function  
```  
  
 È possibile eseguire questo esempio incollando le modifiche nel codice [compilazione dell'applicazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), oppure è possibile seguire le istruzioni in [download dell'applicazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) per scaricare l'esempio e quindi eseguire il progetto QueueResults.  
  
#### <a name="points-of-interest"></a>Punti di interesse  
 Le righe di informazioni che iniziano con un segno di cancelletto (#) nell'output descrivono il funzionamento dell'esempio.  
  
 L'output mostra i modelli seguenti.  
  
-   Un gruppo può essere avviato anche se un gruppo precedente è visualizzato nel relativo output, ma la visualizzazione dell'output del gruppo precedente non viene interrotta.  
  
    ```  
    #Starting group A.  
    #Task assigned for group A. Download tasks are active.  
  
    A-1. msdn.microsoft.com/library/hh191443.aspx                87389  
    A-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    A-3. msdn.microsoft.com/library/jj155761.aspx                30870  
    A-4. msdn.microsoft.com/library/hh290140.aspx               119037  
    A-5. msdn.microsoft.com/library/hh524395.aspx                71260  
  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
  
    A-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    A-7. msdn.microsoft.com                                            53078  
    A-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915919  
  
    B-1. msdn.microsoft.com/library/hh191443.aspx                87388  
    B-2. msdn.microsoft.com/library/aa578028.aspx               207089  
    B-3. msdn.microsoft.com/library/jj155761.aspx                30870  
  
    #Group A is complete.  
  
    B-4. msdn.microsoft.com/library/hh290140.aspx               119027  
    B-5. msdn.microsoft.com/library/hh524395.aspx                71260  
    B-6. msdn.microsoft.com/library/ms404677.aspx               199186  
    B-7. msdn.microsoft.com                                            53078  
    B-8. msdn.microsoft.com/library/ff730837.aspx               148010  
  
    TOTAL bytes returned:  915908  
    ```  
  
-   Il `pendingWork` attività `Nothing` all'inizio di `FinishOneGroupAsync` solo per il gruppo, quale avviato per primo. Il gruppo A non ha ancora completato un'espressione await quando raggiunge `FinishOneGroupAsync`. Pertanto, il controllo non è stato restituito a `AccessTheWebAsync` e non è stata eseguita la prima assegnazione a `pendingWork`.  
  
-   Le due righe seguenti sono sempre visualizzate insieme nell'output. Il codice non viene mai interrotto tra l'avvio dell'operazione di un gruppo in `StartButton_Click` e l'assegnazione di un'attività per il gruppo a `pendingWork`.  
  
    ```  
    #Starting group B.  
    #Task assigned for group B. Download tasks are active.  
    ```  
  
     Dopo che un gruppo entra in `StartButton_Click`, l'operazione non completa un'espressione await fino a quando l'operazione non entra in `FinishOneGroupAsync`. Pertanto, nessuna operazione può assumere il controllo durante l'esecuzione di tale segmento di codice.  
  
##  <a name="BKMD_SettingUpTheExample"></a>Esame ed esecuzione dell'applicazione di esempio  
 Per comprendere meglio l'applicazione di esempio, è possibile scaricarla, compilarla manualmente o esaminare il codice alla fine di questo argomento senza implementare l'applicazione.  
  
> [!NOTE]
>  Per eseguire l'esempio come un'applicazione desktop di Windows Presentation Foundation (WPF), è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
###  <a name="BKMK_DownloadingTheApp"></a>Download dell'applicazione  
  
1.  Scaricare il file compresso da [Async esempi: della Reentrancy nelle applicazioni Desktop di .NET](http://go.microsoft.com/fwlink/?LinkId=266571).  
  
2.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
3.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
4.  Passare alla cartella che contiene il codice di esempio decompresso e quindi aprire il file di soluzione (sln).  
  
5.  In **Esplora**, aprire il menu di scelta rapida per il progetto che si desidera eseguire, quindi scegliere **impostato come StartUpProject**.  
  
6.  Premere CTRL+F5 per compilare ed eseguire il progetto.  
  
###  <a name="BKMK_BuildingTheApp"></a>Compilazione dell'applicazione  
 Nella sezione seguente fornisce il codice per compilare l'esempio come un'applicazione WPF.  
  
##### <a name="to-build-a-wpf-app"></a>Per compilare un'applicazione WPF  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel **modelli installati** riquadro, espandere **Visual Basic**, quindi espandere **Windows**.  
  
4.  Nell'elenco dei tipi di progetto, scegliere **applicazione WPF**.  
  
5.  Denominare il progetto `WebsiteDownloadWPF`, quindi scegliere il **OK** pulsante.  
  
     Il nuovo progetto verrà visualizzato **Esplora**.  
  
6.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow. XAML in **Esplora**, quindi scegliere **Visualizza codice**.  
  
7.  Nel **XAML** visualizzazione di MainWindow. XAML, sostituire il codice con il codice seguente.  
  
    ```vb  
    <Window x:Class="MainWindow"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:local="using:WebsiteDownloadWPF"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"  
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
        mc:Ignorable="d">  
  
        <Grid Width="517" Height="360">  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="-1,0,0,0" VerticalAlignment="Top" Click="StartButton_Click" Height="53" Background="#FFA89B9B" FontSize="36" Width="518"  />  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" Margin="-1,53,0,-36" TextWrapping="Wrap" VerticalAlignment="Top" Height="343" FontSize="10" ScrollViewer.VerticalScrollBarVisibility="Visible" Width="518" FontFamily="Lucida Console" />  
        </Grid>  
    </Window>  
    ```  
  
     Viene visualizzata una finestra semplice che contiene una casella di testo e un pulsante nel **progettazione** visualizzazione di MainWindow. Xaml.  
  
8.  Aggiungere un riferimento per <xref:System.Net.Http>.</xref:System.Net.Http>  
  
9. In **Esplora**, aprire il menu di scelta rapida per MainWindow.xaml.vb e quindi scegliere **Visualizza codice**.  
  
10. Nel file MainWindow.xaml.vb, sostituire il codice con il codice seguente.  
  
    ```vb  
    ' Add the following Imports statements, and add a reference for System.Net.Http.  
    Imports System.Net.Http  
    Imports System.Threading  
  
    Class MainWindow  
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
            ' This line is commented out to make the results clearer in the output.  
            'ResultsTextBox.Text = ""  
  
            Try  
                Await AccessTheWebAsync()  
  
            Catch ex As Exception  
                ResultsTextBox.Text &= vbCrLf & "Downloads failed."  
  
            End Try  
        End Sub  
  
        Private Async Function AccessTheWebAsync() As Task  
  
            ' Declare an HttpClient object.  
            Dim client = New HttpClient()  
  
            ' Make a list of web addresses.  
            Dim urlList As List(Of String) = SetUpURLList()  
  
            Dim total = 0  
            Dim position = 0  
  
            For Each url In urlList  
                ' GetByteArrayAsync returns a task. At completion, the task  
                ' produces a byte array.  
                Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)  
  
                position += 1  
                DisplayResults(url, urlContents, position)  
  
                ' Update the total.  
                total += urlContents.Length  
            Next  
  
            ' Display the total count for all of the websites.  
            ResultsTextBox.Text &=  
                String.Format(vbCrLf & vbCrLf & "TOTAL bytes returned:  " & total & vbCrLf)  
        End Function  
  
        Private Function SetUpURLList() As List(Of String)  
            Dim urls = New List(Of String) From  
            {  
                "http://msdn.microsoft.com/library/hh191443.aspx",  
                "http://msdn.microsoft.com/library/aa578028.aspx",  
                "http://msdn.microsoft.com/library/jj155761.aspx",  
                "http://msdn.microsoft.com/library/hh290140.aspx",  
                "http://msdn.microsoft.com/library/hh524395.aspx",  
                "http://msdn.microsoft.com/library/ms404677.aspx",  
                "http://msdn.microsoft.com",  
                "http://msdn.microsoft.com/library/ff730837.aspx"  
            }  
            Return urls  
        End Function  
  
        Private Sub DisplayResults(url As String, content As Byte(), pos As Integer)  
            ' Display the length of each website. The string format is designed  
            ' to be used with a monospaced font, such as Lucida Console or  
            ' Global Monospace.  
  
            ' Strip off the "http:'".  
            Dim displayURL = url.Replace("http://", "")  
            ' Display position in the URL list, the URL, and the number of bytes.  
            ResultsTextBox.Text &= String.Format(vbCrLf & "{0}. {1,-58} {2,8}", pos, displayURL, content.Length)  
        End Sub  
    End Class  
    ```  
  
11. Premere i tasti CTRL + F5 per eseguire il programma, quindi scegliere il **avviare** più volte.  
  
12. Apportare le modifiche da [disabilitare il pulsante Start](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), [annullare e riavviare l'operazione](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645), o [eseguire più operazioni e coda di Output](http://msdn.microsoft.com/library/5b54de66-6be3-459e-b869-65070b020645) per gestire la reentrancy.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)

