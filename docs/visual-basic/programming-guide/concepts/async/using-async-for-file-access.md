---
title: "Utilizzo della funzionalità Async per l&quot;accesso ai File (Visual Basic) | Documenti di Microsoft"
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
ms.assetid: c989305f-08e3-4687-95c3-948465cda202
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
ms.openlocfilehash: e0e548989b1d2c32b9faf5ce0dd90ae371dfc028
ms.lasthandoff: 03/13/2017

---
# <a name="using-async-for-file-access-visual-basic"></a>Uso della funzionalità Async per l'accesso ai file (Visual Basic)
È possibile utilizzare la funzionalità Async per accedere ai file. Tramite la funzionalità Async, è possibile chiamare i metodi asincroni senza utilizzare callback o suddividere il codice in più metodi o espressioni lambda. Per rendere il codice sincrono asincrono, sufficiente chiamare un metodo asincrono anziché un metodo sincrono e aggiungere alcune parole chiave per il codice.  
  
 È opportuno considerare i seguenti motivi per l'aggiunta di asincronia per chiamate di accesso ai file:  
  
-   Modalità asincrona rende più reattive applicazioni dell'interfaccia utente perché il thread dell'interfaccia utente che avvia l'operazione può eseguire altre operazioni. Se il thread dell'interfaccia utente deve essere eseguito codice che richiede molto tempo (ad esempio, più di 50 millisecondi), l'interfaccia utente potrebbe bloccare fino a quando il / o è stata completata e il thread dell'interfaccia utente può elaborare tastiera nuovamente e inpui e di altri eventi del mouse.  
  
-   Modalità asincrona migliora la scalabilità di ASP.NET e altre applicazioni basate su server, riducendo la necessità di thread. Se l'applicazione utilizza un thread dedicato per ogni risposta e mille richieste vengono gestite contemporaneamente, sono necessari i thread delle migliaia. Operazioni asincrone non spesso necessitano usare un thread durante l'attesa. Essi usare brevemente il thread di completamento i/o esistente alla fine.  
  
-   La latenza di un'operazione di accesso ai file potrebbe essere molto bassa in condizioni correnti, ma la latenza può aumentare notevolmente in futuro. Ad esempio, è possibile spostare un file a un server in tutto il mondo.  
  
-   L'ulteriore overhead di utilizzo della funzionalità Async è ridotto.  
  
-   Attività asincrone può facilmente essere eseguita in parallelo.  
  
## <a name="running-the-examples"></a>Esecuzione degli esempi  
 Per eseguire gli esempi in questo argomento, è possibile creare un **applicazione WPF** o **applicazione Windows Form** e quindi aggiungere un **pulsante**. Il pulsante `Click` evento, aggiungere una chiamata al primo metodo in ogni esempio.  
  
 Negli esempi seguenti, incluse le seguenti `Imports` istruzioni.  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.Diagnostics  
Imports System.IO  
Imports System.Text  
Imports System.Threading.Tasks  
```  
  
## <a name="use-of-the-filestream-class"></a>Utilizzare la classe FileStream  
 Negli esempi inclusi in questo argomento viene utilizzato il <xref:System.IO.FileStream>classe, che dispone di un'opzione che causa i/o asincrone a livello di sistema operativo.</xref:System.IO.FileStream> Utilizzando questa opzione, è possibile evitare di bloccare un thread ThreadPool in molti casi. Per abilitare questa opzione, specificare il `useAsync=true` o `options=FileOptions.Asynchronous` argomento nella chiamata al costruttore.  
  
 È possibile utilizzare questa opzione con <xref:System.IO.StreamReader>e <xref:System.IO.StreamWriter>Se vengono aperti direttamente specificando un percorso del file.</xref:System.IO.StreamWriter> </xref:System.IO.StreamReader> Tuttavia, è possibile utilizzare questa opzione se si fornisce loro un <xref:System.IO.Stream>che la <xref:System.IO.FileStream>classe aperto.</xref:System.IO.FileStream> </xref:System.IO.Stream> Si noti che le chiamate asincrone sono più veloci in App dell'interfaccia utente anche se un thread di pool di thread è bloccato, poiché il thread dell'interfaccia utente non è bloccato durante l'attesa.  
  
## <a name="writing-text"></a>Scrittura di testo  
 Nell'esempio seguente scrive il testo in un file. In ogni istruzione await, il metodo termina immediatamente. Una volta completato il / o di file, il metodo riprende in corrispondenza dell'istruzione che segue l'istruzione await. Si noti che il modificatore async nella definizione di metodi che utilizzano l'istruzione await.  
  
```vb  
Public Async Sub ProcessWrite()  
    Dim filePath = "temp2.txt"  
    Dim text = "Hello World" & ControlChars.CrLf  
  
    Await WriteTextAsync(filePath, text)  
End Sub  
  
Private Async Function WriteTextAsync(filePath As String, text As String) As Task  
    Dim encodedText As Byte() = Encoding.Unicode.GetBytes(text)  
  
    Using sourceStream As New FileStream(filePath,  
        FileMode.Append, FileAccess.Write, FileShare.None,  
        bufferSize:=4096, useAsync:=True)  
  
        Await sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
    End Using  
End Function  
```  
  
 L'esempio originale include l'istruzione `Await sourceStream.WriteAsync(encodedText, 0, encodedText.Length)`, che è una contrazione delle due istruzioni seguenti:  
  
```vb  
Dim theTask As Task = sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
Await theTask  
```  
  
 La prima istruzione restituisce un'attività e determina l'elaborazione di file avviare. La seconda istruzione con await induce il metodo chiudere immediatamente e restituire un'attività diversa. Al termine dell'elaborazione in un secondo momento il file, esecuzione torna all'istruzione successiva ad await. Per ulteriori informazioni, vedere [flusso di controllo in programmi asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md).  
  
## <a name="reading-text"></a>Lettura di testo  
 Nell'esempio seguente legge il testo da un file. Il testo viene memorizzato nel buffer e, in questo caso, inserito in un <xref:System.Text.StringBuilder>.</xref:System.Text.StringBuilder> A differenza nell'esempio precedente, la valutazione dell'attesa produce un valore. Il <xref:System.IO.Stream.ReadAsync%2A>metodo restituisce un <xref:System.Threading.Tasks.Task> \< <xref:System.Int32>>, pertanto la valutazione dell'attesa produce un `Int32` valore (`numRead`) dopo il completamento dell'operazione.</xref:System.Int32> </xref:System.Threading.Tasks.Task> </xref:System.IO.Stream.ReadAsync%2A> Per ulteriori informazioni, vedere [Async restituire tipi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md).  
  
```vb  
Public Async Sub ProcessRead()  
    Dim filePath = "temp2.txt"  
  
    If File.Exists(filePath) = False Then  
        Debug.WriteLine("file not found: " & filePath)  
    Else  
        Try  
            Dim text As String = Await ReadTextAsync(filePath)  
            Debug.WriteLine(text)  
        Catch ex As Exception  
            Debug.WriteLine(ex.Message)  
        End Try  
    End If  
End Sub  
  
Private Async Function ReadTextAsync(filePath As String) As Task(Of String)  
  
    Using sourceStream As New FileStream(filePath,  
        FileMode.Open, FileAccess.Read, FileShare.Read,  
        bufferSize:=4096, useAsync:=True)  
  
        Dim sb As New StringBuilder  
  
        Dim buffer As Byte() = New Byte(&H1000) {}  
        Dim numRead As Integer  
        numRead = Await sourceStream.ReadAsync(buffer, 0, buffer.Length)  
        While numRead <> 0  
            Dim text As String = Encoding.Unicode.GetString(buffer, 0, numRead)  
            sb.Append(text)  
  
            numRead = Await sourceStream.ReadAsync(buffer, 0, buffer.Length)  
        End While  
  
        Return sb.ToString  
    End Using  
End Function  
```  
  
## <a name="parallel-asynchronous-io"></a>/ O asincrone parallela  
 Nell'esempio seguente viene illustrato l'elaborazione parallela scrivendo 10 file di testo. Per ogni file, il <xref:System.IO.Stream.WriteAsync%2A>metodo restituisce un'attività che viene quindi aggiunto a un elenco di attività.</xref:System.IO.Stream.WriteAsync%2A> Il `Await Task.WhenAll(tasks)` istruzione termina il metodo e riprende all'interno del metodo dell'elaborazione di file completate per tutte le attività.  
  
 Nell'esempio vengono chiuse tutte <xref:System.IO.FileStream>le istanze in un `Finally` blocchi dopo le attività vengono completate.</xref:System.IO.FileStream> Se ogni `FileStream` invece è stato creato in un `Imports` istruzione, il `FileStream` potrebbero essere eliminati prima del completamento dell'attività.  
  
 Si noti che qualsiasi miglioramento delle prestazioni è quasi interamente dall'elaborazione in parallelo e non l'elaborazione asincrona. I vantaggi dell'asincronia sono che non impegnare più thread e che non bloccare il thread dell'interfaccia utente.  
  
```vb  
Public Async Sub ProcessWriteMult()  
    Dim folder = "tempfolder\"  
    Dim tasks As New List(Of Task)  
    Dim sourceStreams As New List(Of FileStream)  
  
    Try  
        For index = 1 To 10  
            Dim text = "In file " & index.ToString & ControlChars.CrLf  
  
            Dim fileName = "thefile" & index.ToString("00") & ".txt"  
            Dim filePath = folder & fileName  
  
            Dim encodedText As Byte() = Encoding.Unicode.GetBytes(text)  
  
            Dim sourceStream As New FileStream(filePath,  
                FileMode.Append, FileAccess.Write, FileShare.None,  
                bufferSize:=4096, useAsync:=True)  
  
            Dim theTask As Task = sourceStream.WriteAsync(encodedText, 0, encodedText.Length)  
            sourceStreams.Add(sourceStream)  
  
            tasks.Add(theTask)  
        Next  
  
        Await Task.WhenAll(tasks)  
    Finally  
        For Each sourceStream As FileStream In sourceStreams  
            sourceStream.Close()  
        Next  
    End Try  
End Sub  
```  
  
 Quando si utilizza il <xref:System.IO.Stream.WriteAsync%2A>e <xref:System.IO.Stream.ReadAsync%2A>metodi, è possibile specificare un <xref:System.Threading.CancellationToken>, che consente di annullare il flusso intermedio di operazione.</xref:System.Threading.CancellationToken> </xref:System.IO.Stream.ReadAsync%2A> </xref:System.IO.Stream.WriteAsync%2A> Per ulteriori informazioni, vedere [ottimizzazione Async applicazione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md) e [annullamento in thread gestiti](http://msdn.microsoft.com/library/eea11fe5-d8b0-4314-bb5d-8a58166fb1c3).  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Tipi restituiti asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [Flusso di controllo in programmi asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)
