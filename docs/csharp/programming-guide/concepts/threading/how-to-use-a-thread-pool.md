---
title: 'Procedura: Usare un pool di thread (C#) | Microsoft Docs'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 210a9235-83a6-420b-af52-2d6a58e5133f
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 3814213389119f1fb6692fd57b0f5636a81025bb
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="how-to-use-a-thread-pool-c"></a>Procedura: Usare un pool di thread (C#)
La *creazione di un pool di thread* è una forma di multithreading che prevede l'aggiunta di attività a una coda e l'avvio automatico di tali attività nel corso della creazione dei thread. Per altre informazioni, vedere [Creazione di pool di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md).  
  
 Nell'esempio seguente viene usato il pool di thread di .NET Framework per calcolare il risultato della sequenza di `Fibonacci` relativa a 10 numeri compresi tra 20 e 40. Ogni risultato di `Fibonacci` viene rappresentato dalla classe `Fibonacci`, che fornisce un metodo denominato `ThreadPoolCallback` per l'esecuzione del calcolo. Viene creato un oggetto che rappresenta ogni valore `Fibonacci`, il metodo `ThreadPoolCallback` viene passato a <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>, che assegna un thread disponibile del pool per eseguire il metodo.  
  
 Poiché a ogni oggetto `Fibonacci` viene assegnato un valore semi-casuale da calcolare e poiché ogni thread è in competizione con gli altri per ottenere il tempo del processore, non è possibile prevedere quanto tempo richiederà il calcolo di tutti e 10 i risultati. Per questo motivo a ogni oggetto `Fibonacci` viene passata un'istanza della classe <xref:System.Threading.ManualResetEvent> durante la costruzione. Dopo aver completato il calcolo, ogni oggetto segnala l'oggetto evento specificato. In questo modo il thread primario può bloccare l'esecuzione con `Fibonacci` finché tutti e dieci gli oggetti <xref:System.Threading.WaitHandle.WaitAll%2A> non hanno calcolato un risultato. Il metodo `Main` visualizza quindi ogni risultato `Fibonacci`.  
  
## <a name="example"></a>Esempio  
  
```csharp  
using System;  
using System.Threading;  
  
public class Fibonacci  
{  
    private int _n;  
    private int _fibOfN;  
    private ManualResetEvent _doneEvent;  
  
    public int N { get { return _n; } }  
    public int FibOfN { get { return _fibOfN; } }  
  
    // Constructor.  
    public Fibonacci(int n, ManualResetEvent doneEvent)  
    {  
        _n = n;  
        _doneEvent = doneEvent;  
    }  
  
    // Wrapper method for use with thread pool.  
    public void ThreadPoolCallback(Object threadContext)  
    {  
        int threadIndex = (int)threadContext;  
        Console.WriteLine("thread {0} started...", threadIndex);  
        _fibOfN = Calculate(_n);  
        Console.WriteLine("thread {0} result calculated...", threadIndex);  
        _doneEvent.Set();  
    }  
  
    // Recursive method that calculates the Nth Fibonacci number.  
    public int Calculate(int n)  
    {  
        if (n <= 1)  
        {  
            return n;  
        }  
  
        return Calculate(n - 1) + Calculate(n - 2);  
    }  
}  
  
public class ThreadPoolExample  
{  
    static void Main()  
    {  
        const int FibonacciCalculations = 10;  
  
        // One event is used for each Fibonacci object.  
        ManualResetEvent[] doneEvents = new ManualResetEvent[FibonacciCalculations];  
        Fibonacci[] fibArray = new Fibonacci[FibonacciCalculations];  
        Random r = new Random();  
  
        // Configure and start threads using ThreadPool.  
        Console.WriteLine("launching {0} tasks...", FibonacciCalculations);  
        for (int i = 0; i < FibonacciCalculations; i++)  
        {  
            doneEvents[i] = new ManualResetEvent(false);  
            Fibonacci f = new Fibonacci(r.Next(20, 40), doneEvents[i]);  
            fibArray[i] = f;  
            ThreadPool.QueueUserWorkItem(f.ThreadPoolCallback, i);  
        }  
  
        // Wait for all threads in pool to calculate.  
        WaitHandle.WaitAll(doneEvents);  
        Console.WriteLine("All calculations are complete.");  
  
        // Display the results.  
        for (int i= 0; i<FibonacciCalculations; i++)  
        {  
            Fibonacci f = fibArray[i];  
            Console.WriteLine("Fibonacci({0}) = {1}", f.N, f.FibOfN);  
        }  
    }  
}  
```  
  
 Di seguito viene riportato un esempio dell'output.  
  
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
 <xref:System.Threading.Mutex>   
 <xref:System.Threading.WaitHandle.WaitAll%2A>   
 <xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.EventWaitHandle.Set%2A>   
 <xref:System.Threading.ThreadPool>   
 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>   
 <xref:System.Threading.ManualResetEvent>   
 [Creazione di pool di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md)   
 [Threading (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)   
 @System.Threading.Monitor   
 [Sicurezza](../../../../standard/security/index.md)
