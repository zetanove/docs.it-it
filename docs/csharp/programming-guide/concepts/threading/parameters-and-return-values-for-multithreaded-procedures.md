---
title: Parametri e valori restituiti per routine multithreading (C#) | Microsoft Docs
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
ms.assetid: ba63c30c-d9f0-4962-b5c7-9d83ba851e6a
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 95fdc0f74c1f2c35a4f3b5c0a8f40f5d4fe9457c
ms.lasthandoff: 03/13/2017

---
# <a name="parameters-and-return-values-for-multithreaded-procedures-c"></a>Parametri e valori restituiti per routine multithreading (C#)
L'invio e la restituzione di valori in un'applicazione multithreading è un processo complesso poiché è necessario che il costruttore della classe di thread riceva un riferimento a una routine che non accetta alcun argomento e non restituisce alcun valore. Le sezioni seguenti descrivono alcuni metodi semplici per l'inserimento di parametri e la restituzione di valori da routine su thread diversi.  
  
## <a name="supplying-parameters-for-multithreaded-procedures"></a>Inserimento di parametri per routine multithreading  
 Il modo migliore per inserire i parametri per una chiamata di metodo multithreading consiste nel racchiudere il metodo di destinazione in una classe e definire per la classe campi che verranno usati come parametri per il nuovo thread. Il vantaggio di questo approccio consiste nella possibilità di creare una nuova istanza della classe con parametri propri ogni volta che si vuole iniziare un nuovo thread. Ad esempio, si supponga di avere una funzione che calcola l'area di un triangolo come nel codice seguente:  
  
```csharp  
double CalcArea(double Base, double Height)  
{  
    return 0.5 * Base * Height;  
}  
```  
  
 È possibile scrivere una classe che racchiuda la funzione `CalcArea` e crei i campi in cui memorizzare i parametri di input come segue:  
  
```csharp  
class AreaClass  
{  
    public double Base;  
    public double Height;  
    public double Area;  
    public void CalcArea()  
    {  
        Area = 0.5 * Base * Height;  
        MessageBox.Show("The area is: " + Area.ToString());  
    }  
}  
```  
  
 Per usare `AreaClass`, è possibile creare un oggetto `AreaClass` e impostare le proprietà `Base` e `Height` come illustrato nel codice seguente:  
  
```csharp  
protected void TestArea()  
{  
    AreaClass AreaObject = new AreaClass();  
  
    System.Threading.Thread Thread =  
        new System.Threading.Thread(AreaObject.CalcArea);  
    AreaObject.Base = 30;  
    AreaObject.Height = 40;  
    Thread.Start();  
}  
```  
  
 Si noti che la routine `TestArea` non verifica il valore del campo `Area` dopo che è stato chiamato il metodo `CalcArea`. Poiché `CalcArea` viene eseguita su un thread separato, il campo `Area` non sarà necessariamente impostato se lo si controlla subito dopo avere chiamato `Thread.Start`. La sezione seguente illustra un metodo più efficace per la restituzione di valori dalle routine multithreading.  
  
## <a name="returning-values-from-multithreaded-procedures"></a>Restituzione di valori da routine multithreading  
 La restituzione di valori da routine eseguite su thread diversi è resa complessa dal fatto che le routine non possono essere funzioni e non possono usare argomenti `ByRef`. Il modo più semplice per restituire i valori consiste nell'usare il componente <xref:System.ComponentModel.BackgroundWorker> per gestire i thread e generare un evento dopo aver completato l'attività, quindi elaborare i risultati con un gestore eventi.  
  
 L'esempio seguente restituisce un valore generando un evento da una routine eseguita su un thread separato:  
  
```csharp  
class AreaClass2  
{  
    public double Base;  
    public double Height;  
    public double CalcArea()  
    {  
        // Calculate the area of a triangle.  
        return 0.5 * Base * Height;  
    }  
}  
  
private System.ComponentModel.BackgroundWorker BackgroundWorker1  
    = new System.ComponentModel.BackgroundWorker();  
  
private void TestArea2()  
{  
    InitializeBackgroundWorker();  
  
    AreaClass2 AreaObject2 = new AreaClass2();  
    AreaObject2.Base = 30;  
    AreaObject2.Height = 40;  
  
    // Start the asynchronous operation.  
    BackgroundWorker1.RunWorkerAsync(AreaObject2);  
}  
  
private void InitializeBackgroundWorker()  
{  
    // Attach event handlers to the BackgroundWorker object.  
    BackgroundWorker1.DoWork +=  
        new System.ComponentModel.DoWorkEventHandler(BackgroundWorker1_DoWork);  
    BackgroundWorker1.RunWorkerCompleted +=  
        new System.ComponentModel.RunWorkerCompletedEventHandler(BackgroundWorker1_RunWorkerCompleted);  
}  
  
private void BackgroundWorker1_DoWork(  
    object sender,  
    System.ComponentModel.DoWorkEventArgs e)  
{  
    AreaClass2 AreaObject2 = (AreaClass2)e.Argument;  
    // Return the value through the Result property.  
    e.Result = AreaObject2.CalcArea();  
}  
  
private void BackgroundWorker1_RunWorkerCompleted(  
    object sender,  
    System.ComponentModel.RunWorkerCompletedEventArgs e)  
{  
    // Access the result through the Result property.  
    double Area = (double)e.Result;  
    MessageBox.Show("The area is: " + Area.ToString());  
}  
```  
  
 La variabile facoltativa dell'oggetto di stato `ByVal` del metodo <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> consente di inserire parametri e restituire valori ai thread del pool di thread. Un oggetto di stato è supportato a questo scopo anche dai thread dei timer di thread. Per informazioni sul pooling dei thread e i timer di thread, vedere [Creazione di pool di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md) e [Timer di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-timers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: multithreading con il componente BackgroundWorker (C#)](../../../../csharp/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md)   
 [Creazione di pool di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md)   
 [Sincronizzazione di thread (C#)](../../../../csharp/programming-guide/concepts/threading/thread-synchronization.md)   
 [Eventi](../../../../csharp/programming-guide/events/index.md)   
 [Applicazioni multithreading (C#)](../../../../csharp/programming-guide/concepts/threading/multithreaded-applications.md)   
 [Delegati](../../../../csharp/programming-guide/delegates/index.md)   
 [Multithreading nei componenti](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)
