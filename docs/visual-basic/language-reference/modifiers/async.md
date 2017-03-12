---
title: "Async (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Async"
helpviewer_keywords: 
  - "Async [Visual Basic]"
  - "Async keyword [Visual Basic]"
ms.assetid: 1be8b4b5-9689-41b5-bd33-b906bfd53bc5
caps.latest.revision: 37
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 37
---
# Async (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il modificatore `Async` indica che il metodo o l'[espressione lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md) che l'ha modificato è asincrono.  Tali metodi vengono definiti *metodi async*.  
  
 Un metodo async consente di eseguire senza problemi le operazioni potenzialmente di lunga durata senza bloccare il thread del chiamante.  Il chiamante di un metodo async può riprendere un'operazione senza attendere la fine del metodo async.  
  
> [!NOTE]
>  Le parole chiave `Await` e `Async` introdotte in Visual Studio 2012.  Per un'introduzione alla programmazione asincrona, vedere [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Nell'esempio seguente viene mostrata la struttura di un metodo async.  Per convenzione, i nomi dei metodi async terminano con "Async".  
  
```vb  
  
Public Async Function ExampleMethodAsync() As Task(Of Integer)  
    ' . . .  
  
    ' At the Await expression, execution in this method is suspended and,  
    ' if AwaitedProcessAsync has not already finished, control returns  
    ' to the caller of ExampleMethodAsync. When the awaited task is   
    ' completed, this method resumes execution.   
    Dim exampleInt As Integer = Await AwaitedProcessAsync()  
  
    ' . . .  
  
    ' The return statement completes the task. Any method that is   
    ' awaiting ExampleMethodAsync can now get the integer result.  
    Return exampleInt  
End Function  
```  
  
 In genere, un metodo modificato dalla parola chiave `Async` contiene almeno un'espressione o un'istruzione [Await](../../../visual-basic/language-reference/modifiers/async.md).  Il metodo funziona in modo sincrono fino al primo `Await`, in quel punto si sospende finché l'attività attesa non viene completata.  Nel frattempo, il controllo viene ritornato al chiamante del metodo.  Se il metodo non contiene un'espressione o un'istruzione `Await`, il metodo non viene sospeso e viene eseguito come un metodo sincrono.  Avviso del compilatore che segnala di eventuali metodi async che non contengono `Await` perché questa situazione potrebbe indicare un errore.  Per ulteriori informazioni, vedere gli [errori di compilazione](../../../visual-basic/language-reference/error-messages/because-this-call-is-not-awaited-the-current-method-continues-to-run.md).  
  
 La parola chiave `Async` è una parola chiave non riservata.  È una parola chiave quando si modifica un metodo o un'espressione lambda.  In tutti gli altri contesti, viene interpretata come identificatore.  
  
## Tipi restituiti  
 Un metodo async è una routine [Sub](../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md), o una routine [Function](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md) che ha un tipo di ritorno <xref:System.Threading.Tasks.Task> oppure <xref:System.Threading.Tasks.Task%601>.  Il metodo non può dichiarare nessun parametro [ByRef](../../../visual-basic/language-reference/modifiers/byref.md).  
  
 Specificare `Task(Of TResult)` come tipo restituito del metodo async se l'istruzione [Return](../../../visual-basic/language-reference/statements/return-statement.md) del metodo ha un operando di tipo TResult.  Utilizzare `Task` se non viene restituito alcun valore significativo quando il metodo termina.  Ovvero una chiamata al metodo restituisce `Task`, ma quando il `Task` viene completato, ogni istruzione `Await` in attesa di `Task` non produce un valore risultato.  
  
 Le subroutine async vengono utilizzate principalmente per definire i gestori eventi in cui una routine `Sub` è necessaria.  Il chiamante di una subroutine async non può attendere il metodo e non può intercettare le eccezioni generate dal metodo.  
  
 Per ulteriori informazioni ed esempi, vedere [Tipi restituiti asincroni](../Topic/Async%20Return%20Types%20\(C%23%20and%20Visual%20Basic\).md).  
  
## Esempio  
 Negli esempi seguenti viene illustrato un gestore eventi async, un'espressione lambda async e un metodo async.  Per un esempio completo che utilizza questi elementi, vedere [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md).  È possibile scaricare il codice della procedura dettagliata dalla pagina degli [esempi di codice per gli sviluppatori](http://go.microsoft.com/fwlink/?LinkId=255191).  
  
```vb  
  
' An event handler must be a Sub procedure.  
Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
    textBox1.Clear()  
    ' SumPageSizesAsync is a method that returns a Task.  
    Await SumPageSizesAsync()  
    textBox1.Text = vbCrLf & "Control returned to button1_Click."  
End Sub  
  
' The following async lambda expression creates an equivalent anonymous  
' event handler.  
AddHandler button1.Click, Async Sub(sender, e)  
                              textBox1.Clear()  
                              ' SumPageSizesAsync is a method that returns a Task.  
                              Await SumPageSizesAsync()  
                              textBox1.Text = vbCrLf & "Control returned to button1_Click."  
                          End Sub  
  
' The following async method returns a Task(Of T).  
' A typical call awaits the Byte array result:  
'      Dim result As Byte() = Await GetURLContents("http://msdn.com")  
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
  
```  
  
## Vedere anche  
 <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>   
 [Await Operator](../../../visual-basic/language-reference/operators/await-operator.md)   
 [Programmazione asincrona con Async e Await](../Topic/Asynchronous%20Programming%20with%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura dettagliata: accesso al Web tramite Async e Await](../Topic/Walkthrough:%20Accessing%20the%20Web%20by%20Using%20Async%20and%20Await%20\(C%23%20and%20Visual%20Basic\).md)