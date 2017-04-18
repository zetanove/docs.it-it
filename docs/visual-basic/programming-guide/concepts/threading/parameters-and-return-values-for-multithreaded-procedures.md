---
title: Parametri e valori restituiti per routine multithreading (Visual Basic) | Documenti di Microsoft
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
ms.assetid: cbdce172-7ff6-41a9-bb21-53a7c6f538a5
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d5d8adde531d31aa6bf353f53bd4cfecc084f515
ms.lasthandoff: 03/13/2017

---
# <a name="parameters-and-return-values-for-multithreaded-procedures-visual-basic"></a>Parametri e valori restituiti per routine multithreading (Visual Basic)
Invio e la restituzione di valori in un'applicazione multithreading è complesso perché il costruttore della classe di thread deve essere passato un riferimento a una routine che non accetta argomenti e non restituisce alcun valore. Le sezioni seguenti mostrano alcuni semplici metodi per fornire i parametri e valori restituiti da procedure su un thread separato.  
  
## <a name="supplying-parameters-for-multithreaded-procedures"></a>Fornendo i parametri per routine multithreading  
 Il modo migliore per fornire i parametri per una chiamata al metodo multithreading consiste nel racchiudere il metodo di destinazione in una classe e definire i campi per la classe che verrà utilizzato come parametri per il nuovo thread. Il vantaggio di questo approccio è che è possibile creare una nuova istanza della classe, con i propri parametri, ogni volta che si desidera avviare un nuovo thread. Ad esempio, si supponga di che avere una funzione che calcola l'area di un triangolo, come nel codice seguente:  
  
```vb  
Function CalcArea(ByVal Base As Double, ByVal Height As Double) As Double  
    CalcArea = 0.5 * Base * Height  
End Function  
```  
  
 È possibile scrivere una classe che esegue il wrapping di `CalcArea` funzione e crea i campi per archiviare i parametri di input, come indicato di seguito:  
  
```vb  
Class AreaClass  
    Public Base As Double  
    Public Height As Double  
    Public Area As Double  
    Sub CalcArea()  
        Area = 0.5 * Base * Height  
        MessageBox.Show("The area is: " & Area.ToString)  
    End Sub  
End Class  
```  
  
 Utilizzare il `AreaClass`, è possibile creare un `AreaClass` oggetto e impostare il `Base` e `Height` proprietà come illustrato nel codice seguente:  
  
```vb  
Protected Sub TestArea()  
    Dim AreaObject As New AreaClass  
    Dim Thread As New System.Threading.Thread(  
                        AddressOf AreaObject.CalcArea)  
    AreaObject.Base = 30  
    AreaObject.Height = 40  
    Thread.Start()  
End Sub  
```  
  
 Si noti che il `TestArea` routine non verifica il valore di `Area` campo dopo la chiamata di `CalcArea` (metodo). Poiché `CalcArea` viene eseguito in un thread separato, il `Area` campo non è necessariamente impostato se lo si controlla subito dopo aver chiamato `Thread.Start`. Nella sezione successiva viene illustrato un modo migliore per restituire valori dalle routine multithreading.  
  
## <a name="returning-values-from-multithreaded-procedures"></a>Restituzione di valori da routine multithreading  
 Restituzione di valori da routine eseguite su thread diversi è complicata dal fatto che le procedure non possono essere funzioni e non possono utilizzare `ByRef` argomenti. Il modo più semplice per restituire i valori è utilizzare il <xref:System.ComponentModel.BackgroundWorker>componente per gestire i thread e generare un evento quando viene eseguita l'attività ed elaborare i risultati a un gestore eventi.</xref:System.ComponentModel.BackgroundWorker>  
  
 Nell'esempio seguente restituisce un valore generando un evento da una routine in esecuzione su un thread separato:  
  
```vb  
Private Class AreaClass2  
    Public Base As Double  
    Public Height As Double  
    Function CalcArea() As Double  
        ' Calculate the area of a triangle.  
        Return 0.5 * Base * Height  
    End Function  
End Class  
  
Private WithEvents BackgroundWorker1 As New System.ComponentModel.BackgroundWorker  
  
Private Sub TestArea2()  
    Dim AreaObject2 As New AreaClass2  
    AreaObject2.Base = 30  
    AreaObject2.Height = 40  
  
    ' Start the asynchronous operation.  
    BackgroundWorker1.RunWorkerAsync(AreaObject2)  
End Sub  
  
' This method runs on the background thread when it starts.  
Private Sub BackgroundWorker1_DoWork(  
    ByVal sender As Object,   
    ByVal e As System.ComponentModel.DoWorkEventArgs  
    ) Handles BackgroundWorker1.DoWork  
  
    Dim AreaObject2 As AreaClass2 = CType(e.Argument, AreaClass2)  
    ' Return the value through the Result property.  
    e.Result = AreaObject2.CalcArea()  
End Sub  
  
' This method runs on the main thread when the background thread finishes.  
Private Sub BackgroundWorker1_RunWorkerCompleted(  
    ByVal sender As Object,  
    ByVal e As System.ComponentModel.RunWorkerCompletedEventArgs  
    ) Handles BackgroundWorker1.RunWorkerCompleted  
  
    ' Access the result through the Result property.  
    Dim Area As Double = CDbl(e.Result)  
    MessageBox.Show("The area is: " & Area.ToString)  
End Sub  
```  
  
 È possibile fornire parametri e restituire valori ai thread di pool di thread utilizzando l'opzione facoltativa `ByVal` variabile dello stato dell'oggetto del <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>(metodo).</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> Thread di timer di thread supporta anche un oggetto di stato per questo scopo. Per informazioni sui pool di thread e timer di thread, vedere [(Visual Basic) il pool di Thread](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)[il pool di Thread](http://msdn.microsoft.com/library/4b8bb2c8-8ca4-457c-9afd-d11bc9a05701) e [il timer di Thread (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-timers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Multithreading con il componente BackgroundWorker (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md)   
 [(Visual Basic) di pooling dei thread](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)   
 [Sincronizzazione dei thread (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [Applicazioni multithreading (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Multithreading nei componenti](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)
