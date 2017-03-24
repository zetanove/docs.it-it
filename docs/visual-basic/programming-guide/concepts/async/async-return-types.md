---
title: Tipi restituiti asincroni (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 07890291-ee72-42d3-932a-fa4d312f2c60
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
ms.openlocfilehash: 703d3fc3f503017edf38521d77f9b15a92d0ebf3
ms.lasthandoff: 03/13/2017

---
# <a name="async-return-types-visual-basic"></a>Tipi restituiti asincroni (Visual Basic)
I metodi asincroni sono tre possibili tipi restituiti: <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task>e void.</xref:System.Threading.Tasks.Task> </xref:System.Threading.Tasks.Task%601> In Visual Basic, il tipo restituito void viene scritto come un [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) procedura. Per ulteriori informazioni sui metodi asincroni, vedere [la programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md).  
  
 Ogni tipo restituito viene esaminato in una delle sezioni seguenti e alla fine dell'argomento è disponibile un esempio completo che usa tutti i tre tipi.  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
##  <a name="BKMK_TaskTReturnType"></a>Tipo restituito Task(T)  
 Il <xref:System.Threading.Tasks.Task%601>tipo restituito viene utilizzato per un metodo asincrono che contiene un [restituire](../../../../visual-basic/language-reference/statements/return-statement.md) istruzione in cui l'operando è di tipo `TResult`.</xref:System.Threading.Tasks.Task%601>  
  
 Nell'esempio seguente, il `TaskOfT_MethodAsync` metodo asincrono contiene un'istruzione return che restituisce un valore integer. Pertanto, la dichiarazione del metodo deve specificare un tipo restituito di `Task(Of Integer)`.  
  
```vb  
' TASK(OF T) EXAMPLE  
Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.FromResult is a placeholder for actual work that returns a string.  
    Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
    ' The method then can process the result in some way.  
    Dim leisureHours As Integer  
    If today.First() = "S" Then  
        leisureHours = 16  
    Else  
        leisureHours = 5  
    End If  
  
    ' Because the return statement specifies an operand of type Integer, the   
    ' method must have a return type of Task(Of Integer).   
    Return leisureHours  
End Function  
```  
  
 Quando `TaskOfT_MethodAsync` viene chiamato dall'interno di un'espressione await, l'espressione await recupera il valore integer (il valore di `leisureHours`) che viene archiviato nell'attività restituito da `TaskOfT_MethodAsync`. Per ulteriori informazioni sulle espressioni await, vedere [operatore Await](../../../../visual-basic/language-reference/operators/await-operator.md).  
  
 Il codice seguente chiama e attende metodo `TaskOfT_MethodAsync`. Il risultato viene assegnato per il `result1` variabile.  
  
```vb  
' Call and await the Task(Of T)-returning async method in the same statement.  
Dim result1 As Integer = Await TaskOfT_MethodAsync()  
```  
  
 È possibile comprendere meglio come ciò separando la chiamata a `TaskOfT_MethodAsync` dall'applicazione di `Await`, come mostrato nel codice seguente. Una chiamata al metodo `TaskOfT_MethodAsync` che non restituisce immediatamente atteso un `Task(Of Integer)`, come previsto dalla dichiarazione del metodo. L'attività viene assegnata per il `integerTask` variabile nell'esempio. Poiché `integerTask` è un <xref:System.Threading.Tasks.Task%601>, contiene un <xref:System.Threading.Tasks.Task%601.Result>proprietà di tipo `TResult`.</xref:System.Threading.Tasks.Task%601.Result> </xref:System.Threading.Tasks.Task%601> In questo caso, TResult rappresenta un tipo Integer. Quando `Await` viene applicato a `integerTask`, l'espressione await restituisce il contenuto della <xref:System.Threading.Tasks.Task%601.Result%2A>proprietà di `integerTask`.</xref:System.Threading.Tasks.Task%601.Result%2A> Il valore viene assegnato per il `result2` variabile.  
  
> [!WARNING]
>  Il <xref:System.Threading.Tasks.Task%601.Result%2A>è una proprietà di blocco.</xref:System.Threading.Tasks.Task%601.Result%2A> Se si prova ad accedervi prima del completamento dell'attività, il thread attualmente attivo viene bloccato fino a quando l'attività non viene completata e il valore non è disponibile. Nella maggior parte dei casi, è necessario accedere al valore utilizzando `Await` anziché accedere direttamente alla proprietà.  
  
```vb  
' Call and await in separate statements.  
Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
' You can do other work that does not rely on resultTask before awaiting.  
textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
Dim result2 As Integer = Await integerTask  
```  
  
 Le istruzioni di visualizzazione nel codice seguente verificare che i valori di `result1` variabile, il `result2` variabile e `Result` proprietà sono uguali. Tenere presente che la `Result` proprietà è una proprietà di blocco e non deve avvenire prima che l'attività è stata attesa.  
  
```vb  
' Display the values of the result1 variable, the result2 variable, and  
' the resultTask.Result property.  
textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
```  
  
##  <a name="BKMK_TaskReturnType"></a>Tipo restituito dell'attività  
 I metodi asincroni che non contengono un'istruzione return o che contiene un'istruzione return che non restituisce un operando in genere con un tipo restituito di <xref:System.Threading.Tasks.Task>.</xref:System.Threading.Tasks.Task> Tali metodi sarebbero [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) procedure se sono stati scritti per eseguire in modo sincrono. Se si utilizza un `Task` tipo restituito per un metodo asincrono, è possibile utilizzare un metodo chiamante un `Await` operatore di sospendere il completamento del chiamante fino al termine il metodo asincrono chiamato.  
  
 Nell'esempio seguente, il metodo asincrono `Task_MethodAsync` non contiene un'istruzione return. È pertanto necessario specificare un tipo restituito di `Task` per il metodo, che consente di `Task_MethodAsync` per essere atteso. La definizione di `Task` tipo non include un `Result` proprietà per archiviare un valore restituito.  
  
```vb  
' TASK EXAMPLE  
Async Function Task_MethodAsync() As Task  
  
    ' The body of an async method is expected to contain an awaited   
    ' asynchronous call.  
    ' Task.Delay is a placeholder for actual work.  
    Await Task.Delay(2000)  
    textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
    ' This method has no return statement, so its return type is Task.   
End Function  
```  
  
 `Task_MethodAsync`viene chiamato e atteso utilizzando un'istruzione await anziché un'espressione await, simile all'istruzione di chiamata per sincrona `Sub` o un metodo che restituisce void. L'applicazione di un `Await` operatore in questo caso, non genera un valore.  
  
 Il codice seguente chiama e attende metodo `Task_MethodAsync`.  
  
```vb  
' Call and await the Task-returning async method in the same statement.  
Await Task_MethodAsync()  
```  
  
 Come il precedente <xref:System.Threading.Tasks.Task%601>esempio, è possibile separare la chiamata a `Task_MethodAsync` dall'applicazione di un `Await` operatore, come illustrato nel codice seguente.</xref:System.Threading.Tasks.Task%601> Tuttavia, tenere presente che un `Task` non dispone di un `Result` , proprietà e che nessun valore viene generato quando un operatore await viene applicato a un `Task`.  
  
 Il codice seguente separa chiamata `Task_MethodAsync` da attendere l'attività che `Task_MethodAsync` restituisce.  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
##  <a name="BKMK_VoidReturnType"></a>Tipo restituito void  
 L'utilizzo principale di `Sub` procedure sia nei gestori eventi, in cui è presente alcun tipo restituito (definito per un tipo restituito void in altri linguaggi). Un tipo restituito void può essere usato anche per eseguire l'override di metodi che restituiscono void o per metodi che eseguono attività che possono essere categorizzate come "Fire and Forget". Tuttavia, è necessario restituire un `Task` laddove possibile, perché un metodo asincrono che restituisce void non può essere atteso. Qualsiasi chiamante di questo metodo deve poter continuare fino al completamento senza attendere il completamento del metodo asincrono chiamato e il chiamante deve essere indipendente da qualsiasi eccezione o valore generato dal metodo asincrono.  
  
 Il chiamante di un metodo asincrono che restituisce void non può intercettare le eccezioni generate dal metodo ed è probabile che queste eccezioni non gestite provochino un errore dell'applicazione. Se si verifica un'eccezione in un metodo asincrono che restituisce un <xref:System.Threading.Tasks.Task>o <xref:System.Threading.Tasks.Task%601>, l'eccezione viene archiviata nell'attività restituita e nuovamente generata quando l'attività è atteso.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> Pertanto, assicurarsi che qualsiasi metodo asincrono che può generare un'eccezione con un tipo restituito della <xref:System.Threading.Tasks.Task>o <xref:System.Threading.Tasks.Task%601>e che le chiamate al metodo sono atteso.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task>  
  
 Per ulteriori informazioni su come rilevare le eccezioni nei metodi asincroni, vedere [Try... Catch... Istruzione finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
 Il codice seguente definisce un gestore eventi asincroni.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
##  <a name="BKMK_Example"></a>Esempio completo  
 Il progetto Windows Presentation Foundation (WPF) seguente contiene gli esempi di codice di questo argomento.  
  
 Per eseguire il progetto, effettuare i passaggi seguenti:  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel **installato**, **modelli** categoria, scegliere **Visual Basic**, quindi scegliere **Windows**. Scegliere **applicazione WPF** dall'elenco dei tipi di progetto.  
  
4.  Immettere `AsyncReturnTypes` come nome del progetto, quindi scegliere il **OK** pulsante.  
  
     Il nuovo progetto verrà visualizzato **Esplora**.  
  
5.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow. XAML in **Esplora**, quindi scegliere **aprire**.  
  
6.  Nel **XAML** finestra di MainWindow. XAML, sostituire il codice con il codice seguente.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>  
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     Viene visualizzata una finestra semplice che contiene una casella di testo e un pulsante nel **progettazione** finestra di MainWindow. Xaml.  
  
7.  In **Esplora**, aprire il menu di scelta rapida per MainWindow.xaml.vb e quindi scegliere **Visualizza codice**.  
  
8.  Sostituire il codice in MainWindow.xaml.vb con quello riportato di seguito.  
  
    ```vb  
    Class MainWindow  
  
        ' SUB EXAMPLE  
        Async Sub button1_Click(sender As Object, e As RoutedEventArgs) Handles button1.Click  
  
            textBox1.Clear()  
  
            ' Start the process and await its completion. DriverAsync is a   
            ' Task-returning async method.  
            Await DriverAsync()  
  
            ' Say goodbye.  
            textBox1.Text &= vbCrLf & "All done, exiting button-click event handler."  
        End Sub  
  
        Async Function DriverAsync() As Task  
  
            ' Task(Of T)   
            ' Call and await the Task(Of T)-returning async method in the same statement.  
            Dim result1 As Integer = Await TaskOfT_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim integerTask As Task(Of Integer) = TaskOfT_MethodAsync()  
  
            ' You can do other work that does not rely on resultTask before awaiting.  
            textBox1.Text &= String.Format("Application can continue working while the Task(Of T) runs. . . . " & vbCrLf)  
  
            Dim result2 As Integer = Await integerTask  
  
            ' Display the values of the result1 variable, the result2 variable, and  
            ' the resultTask.Result property.  
            textBox1.Text &= String.Format(vbCrLf & "Value of result1 variable:   {0}" & vbCrLf, result1)  
            textBox1.Text &= String.Format("Value of result2 variable:   {0}" & vbCrLf, result2)  
            textBox1.Text &= String.Format("Value of resultTask.Result:  {0}" & vbCrLf, integerTask.Result)  
  
            ' Task   
            ' Call and await the Task-returning async method in the same statement.  
            Await Task_MethodAsync()  
  
            ' Call and await in separate statements.  
            Dim simpleTask As Task = Task_MethodAsync()  
  
            ' You can do other work that does not rely on simpleTask before awaiting.  
            textBox1.Text &= String.Format(vbCrLf & "Application can continue working while the Task runs. . . ." & vbCrLf)  
  
            Await simpleTask  
        End Function  
  
        ' TASK(OF T) EXAMPLE  
        Async Function TaskOfT_MethodAsync() As Task(Of Integer)  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.FromResult is a placeholder for actual work that returns a string.  
            Dim today As String = Await Task.FromResult(Of String)(DateTime.Now.DayOfWeek.ToString())  
  
            ' The method then can process the result in some way.  
            Dim leisureHours As Integer  
            If today.First() = "S" Then  
                leisureHours = 16  
            Else  
                leisureHours = 5  
            End If  
  
            ' Because the return statement specifies an operand of type Integer, the   
            ' method must have a return type of Task(Of Integer).   
            Return leisureHours  
        End Function  
  
        ' TASK EXAMPLE  
        Async Function Task_MethodAsync() As Task  
  
            ' The body of an async method is expected to contain an awaited   
            ' asynchronous call.  
            ' Task.Delay is a placeholder for actual work.  
            Await Task.Delay(2000)  
            textBox1.Text &= String.Format(vbCrLf & "Sorry for the delay. . . ." & vbCrLf)  
  
            ' This method has no return statement, so its return type is Task.   
        End Function  
  
    End Class  
    ```  
  
9. Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Dovrebbe venire visualizzato l'output seguente.  
  
    ```  
    Application can continue working while the Task<T> runs. . . .   
  
    Value of result1 variable:   5  
    Value of result2 variable:   5  
    Value of integerTask.Result: 5  
  
    Sorry for the delay. . . .  
  
    Application can continue working while the Task runs. . . .  
  
    Sorry for the delay. . . .  
  
    All done, exiting button-click event handler.  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Threading.Tasks.Task.FromResult%2A></xref:System.Threading.Tasks.Task.FromResult%2A>   
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Flusso di controllo in programmi asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)   
 [Async](../../../../visual-basic/language-reference/modifiers/async.md)   
 [Operatore Await](../../../../visual-basic/language-reference/operators/await-operator.md)
