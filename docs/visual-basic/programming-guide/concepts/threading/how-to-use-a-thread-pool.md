---
title: 'Procedura: utilizzare un Pool di Thread (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 90a0bb24-39f8-41f5-a217-b52a7d4fed0b
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
ms.openlocfilehash: d60bceea0ed956075233f5f045131ffb2eb37eef
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-a-thread-pool-visual-basic"></a>Procedura: utilizzare un Pool di Thread (Visual Basic)
*Pooling dei thread* è un tipo di multithreading nei quali attività vengono aggiunti a una coda e avviate automaticamente quando vengono creati dei thread. Per ulteriori informazioni, vedere [(Visual Basic) il pool di Thread](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md).  
  
 Nell'esempio seguente viene utilizzato il pool di thread .NET Framework per calcolare il `Fibonacci` risultato per dieci numeri compresi tra 20 e 40. Ogni `Fibonacci` risultato è rappresentato dal `Fibonacci` classe che fornisce un metodo denominato `ThreadPoolCallback` che esegue il calcolo. Oggetto che rappresenta ogni `Fibonacci` valore viene creato e `ThreadPoolCallback` viene passato a <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>, che assegna un thread disponibile nel pool per eseguire il metodo.</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>  
  
 Poiché ogni `Fibonacci` oggetto viene assegnato un valore semi-casuale da calcolare e poiché ogni thread sarà in competizione per il tempo processore, non è possibile sapere in anticipo il tempo necessario per tutti i dieci risultati deve essere calcolato. Per questo motivo ogni `Fibonacci` oggetto viene passato un'istanza di <xref:System.Threading.ManualResetEvent>classe durante la costruzione.</xref:System.Threading.ManualResetEvent> Ogni oggetto segnala all'oggetto evento fornito quando cui il calcolo viene completato, che consente al thread principale di bloccare l'esecuzione con <xref:System.Threading.WaitHandle.WaitAll%2A>fino a quando tutte e dieci `Fibonacci` oggetti calcolato un risultato.</xref:System.Threading.WaitHandle.WaitAll%2A> Il `Main` metodo visualizza quindi ogni `Fibonacci` risultato.  
  
## <a name="example"></a>Esempio  
  
```vb  
Imports System.Threading  
  
Module Module1  
  
    Public Class Fibonacci  
        Private _n As Integer  
        Private _fibOfN  
        Private _doneEvent As ManualResetEvent  
  
        Public ReadOnly Property N() As Integer  
            Get  
                Return _n  
            End Get  
        End Property  
  
        Public ReadOnly Property FibOfN() As Integer  
            Get  
                Return _fibOfN  
            End Get  
        End Property  
  
        Sub New(ByVal n As Integer, ByVal doneEvent As ManualResetEvent)  
            _n = n  
            _doneEvent = doneEvent  
        End Sub  
  
        ' Wrapper method for use with the thread pool.  
        Public Sub ThreadPoolCallBack(ByVal threadContext As Object)  
            Dim threadIndex As Integer = CType(threadContext, Integer)  
            Console.WriteLine("thread {0} started...", threadIndex)  
            _fibOfN = Calculate(_n)  
            Console.WriteLine("thread {0} result calculated...", threadIndex)  
            _doneEvent.Set()  
        End Sub  
  
        Public Function Calculate(ByVal n As Integer) As Integer  
            If n <= 1 Then  
                Return n  
            End If  
            Return Calculate(n - 1) + Calculate(n - 2)  
        End Function  
  
    End Class  
  
    <MTAThread()>   
    Sub Main()  
        Const FibonacciCalculations As Integer = 9 ' 0 to 9  
  
        ' One event is used for each Fibonacci object  
        Dim doneEvents(FibonacciCalculations) As ManualResetEvent  
        Dim fibArray(FibonacciCalculations) As Fibonacci  
        Dim r As New Random()  
  
        ' Configure and start threads using ThreadPool.  
        Console.WriteLine("launching {0} tasks...", FibonacciCalculations)  
  
        For i As Integer = 0 To FibonacciCalculations  
            doneEvents(i) = New ManualResetEvent(False)  
            Dim f = New Fibonacci(r.Next(20, 40), doneEvents(i))  
            fibArray(i) = f  
            ThreadPool.QueueUserWorkItem(AddressOf f.ThreadPoolCallBack, i)  
        Next  
  
        ' Wait for all threads in pool to calculate.  
        WaitHandle.WaitAll(doneEvents)  
        Console.WriteLine("All calculations are complete.")  
  
        ' Display the results.  
        For i As Integer = 0 To FibonacciCalculations  
            Dim f As Fibonacci = fibArray(i)  
            Console.WriteLine("Fibonacci({0}) = {1}", f.N, f.FibOfN)  
        Next  
    End Sub  
  
End Module  
```  
  
 Seguito è riportato un esempio di output.  
  
```  
launching 10 tasks...  
thread 0 started...  
thread 1 started...  
thread 1 result calculated...  
thread 2 started...  
thread 2 result calculated...  
thread 3 started...  
thread 3 result calculated...  
thread 4 started...  
thread 0 result calculated...  
thread 5 started...  
thread 5 result calculated...  
thread 6 started...  
thread 4 result calculated...  
thread 7 started...  
thread 6 result calculated...  
thread 8 started...  
thread 8 result calculated...  
thread 9 started...  
thread 9 result calculated...  
thread 7 result calculated...  
All calculations are complete.  
Fibonacci(38) = 39088169  
Fibonacci(29) = 514229  
Fibonacci(25) = 75025  
Fibonacci(22) = 17711  
Fibonacci(38) = 39088169  
Fibonacci(29) = 514229  
Fibonacci(29) = 514229  
Fibonacci(38) = 39088169  
Fibonacci(21) = 10946  
Fibonacci(27) = 196418  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Mutex></xref:System.Threading.Mutex>   
 <xref:System.Threading.WaitHandle.WaitAll%2A></xref:System.Threading.WaitHandle.WaitAll%2A>   
 <xref:System.Threading.ManualResetEvent></xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.EventWaitHandle.Set%2A></xref:System.Threading.EventWaitHandle.Set%2A>   
 <xref:System.Threading.ThreadPool></xref:System.Threading.ThreadPool>   
 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A></xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>   
 <xref:System.Threading.ManualResetEvent></xref:System.Threading.ManualResetEvent>   
 [(Visual Basic) di pooling dei thread](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)   
 [Threading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)   
 @System.Threading.Monitor   
 [Sicurezza](http://msdn.microsoft.com/library/9a9621d7-8883-4a4f-a874-65e8e09e20a6)
