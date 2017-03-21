---
title: "Poiché questa chiamata non può essere attesa, il metodo corrente continua prima del completamento della chiamata di | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42358
- vbc42358
helpviewer_keywords:
- BC42358
ms.assetid: 43342515-c3c8-4155-9263-c302afabcbc2
caps.latest.revision: 8
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a9165414bc08b62aab20410e7af187fa4b45c162
ms.lasthandoff: 03/13/2017

---
# <a name="because-this-call-is-not-awaited-the-current-method-continues-to-run-before-the-call-is-completed"></a>Poiché la chiamata non può essere attesa, l'esecuzione del metodo corrente continua prima del completamento della chiamata
Non è possibile attendere la chiamata, pertanto l'esecuzione del metodo corrente continuerà prima del completamento della chiamata. È possibile applicare l'operatore "Await" al risultato della chiamata.  
  
 Il metodo corrente viene chiamato un metodo asincrono che restituisce un <xref:System.Threading.Tasks.Task>o <xref:System.Threading.Tasks.Task%601>e non si applica il [Await](../../../visual-basic/language-reference/operators/await-operator.md) nel risultato.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> Con la chiamata al metodo asincrono viene avviata un'attività asincrona. Tuttavia, poiché non viene applicato alcun operatore `Await` , l'esecuzione del programma continua senza attendere il completamento dell'attività. Nella maggior parte dei casi questo comportamento non è quello previsto. Di solito altri aspetti del metodo chiamante dipendono dai risultati della chiamata o, come minimo, si prevede che il metodo chiamato venga completato prima della restituzione da parte del metodo contenente la chiamata.  
  
 Un problema ugualmente importante riguarda cosa accade con le eccezioni generate nel metodo asincrono richiamato. Un'eccezione generata in un metodo che restituisce un <xref:System.Threading.Tasks.Task>o <xref:System.Threading.Tasks.Task%601>viene archiviato nell'attività restituita.</xref:System.Threading.Tasks.Task%601> </xref:System.Threading.Tasks.Task> Se non si attende l'attività o si controllano in modo esplicito le eccezioni, l'eccezione viene persa. Se si attende l'attività, la relativa eccezione viene generata di nuovo.  
  
 Come procedura consigliata, attendere sempre la chiamata.  
  
 Per impostazione predefinita, si tratta di un messaggio di avviso. Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [configurazione degli avvisi in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC42358  
  
### <a name="to-address-this-warning"></a>Per risolvere questo avviso  
  
-   Si consideri la possibilità di eliminare l'avviso solo se si è certi che non si desidera attendere il completamento della chiamata asincrona e che il metodo chiamato non generi alcuna eccezione. In tal caso, è possibile eliminare l'avviso assegnando il risultato dell'attività della chiamata a una variabile.  
  
     Nell'esempio seguente viene illustrato come generare l'avviso, come eliminarlo e come attendere la chiamata.  
  
    ```vb  
    Async Function CallingMethodAsync() As Task  
  
        ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
        ' Variable delay is used to slow down the called method so that you  
        ' can distinguish between awaiting and not awaiting in the program's output.   
        ' You can adjust the value to produce the output that this topic shows   
        ' after the code.  
        Dim delay = 5000  
  
        ' Call #1.  
        ' Call an async method. Because you don't await it, its completion isn't   
        ' coordinated with the current method, CallingMethodAsync.  
        ' The following line causes the warning.  
        CalledMethodAsync(delay)  
  
        ' Call #2.  
        ' To suppress the warning without awaiting, you can assign the   
        ' returned task to a variable. The assignment doesn't change how  
        ' the program runs. However, the recommended practice is always to  
        ' await a call to an async method.  
        ' Replace Call #1 with the following line.  
        'Task delayTask = CalledMethodAsync(delay)  
  
        ' Call #3  
        ' To contrast with an awaited call, replace the unawaited call   
        ' (Call #1 or Call #2) with the following awaited call. The best   
        ' practice is to await the call.  
  
        'Await CalledMethodAsync(delay)  
  
        ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
        ' continues to run and, in this example, finishes its work and returns  
        ' to its caller.  
        ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
    End Function  
  
    Async Function CalledMethodAsync(howLong As Integer) As Task  
  
        ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
        ' Slow the process down a little so you can distinguish between awaiting  
        ' and not awaiting. Adjust the value for howLong if necessary.  
        Await Task.Delay(howLong)  
        ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
    End Function  
  
    ```  
  
     Nell'esempio, se si sceglie Call #1 o Call #2, il metodo asincrono senza attesa (`CalledMethodAsync`) termina dopo che il relativo chiamante (`CallingMethodAsync`) e il chiamante del chiamante (`StartButton_Click`) sono completati. Nell'ultima riga nell'output seguente viene mostrato quando viene completato il metodo chiamato. L'entrata e l'uscita dal gestore eventi tramite cui viene chiamato `CallingMethodAsync` nell'esempio completo sono contrassegnate nell'output.  
  
    ```  
  
    Entering the Click event handler.  
      Entering calling method.  
        Entering called method, starting and awaiting Task.Delay.  
      Returning from calling method.  
    Exiting the Click event handler.  
        Task.Delay is finished--returning from called method.  
    ```  
  
## <a name="example"></a>Esempio  
 Nell'applicazione Windows Presentation Foundation (WPF) seguente sono inclusi i metodi dell'esempio precedente. L'applicazione viene configurata con i passaggi riportati di seguito.  
  
1.  Creare un'applicazione WPF e denominarla `AsyncWarning`.  
  
2.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow.xaml in **Esplora soluzioni**, quindi scegliere **Visualizza codice**.  
  
3.  Sostituire il codice nella visualizzazione **XAML** di MainWindow.xaml con quello riportato di seguito.  
  
    ```vb  
    <Window x:Class="MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="StartButton_Click" />  
            <TextBox x:Name="ResultsTextBox" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
        </Grid>  
    </Window>  
  
    ```  
  
     Una finestra semplice con un pulsante e una casella di testo viene visualizzata nella visualizzazione **Progettazione** di MainWindow.xaml.  
  
     Per ulteriori informazioni sulla finestra di progettazione XAML, vedere [la creazione di un'interfaccia utente tramite XAML Designer](https://docs.microsoft.com/visualstudio/designers/creating-a-ui-by-using-xaml-designer-in-visual-studio). Per informazioni su come compilare una semplice interfaccia utente, vedere la "per creare un'applicazione WPF" e "per progettare una finestra principale semplice WPF" sezioni di [procedura dettagliata: accesso al Web tramite Async e Await](http://msdn.microsoft.com/library/25879a6d-fdee-4a38-bc98-bb8c24d16042).  
  
4.  Sostituire il codice in MainWindow.xaml.vb con quello riportato di seguito.  
  
    ```vb  
  
    Class MainWindow   
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
            ResultsTextBox.Text &= vbCrLf & "Entering the Click event handler."  
            Await CallingMethodAsync()  
            ResultsTextBox.Text &= vbCrLf & "Exiting the Click event handler."  
        End Sub  
  
        Async Function CallingMethodAsync() As Task  
  
            ResultsTextBox.Text &= vbCrLf & "  Entering calling method."  
  
            ' Variable delay is used to slow down the called method so that you  
            ' can distinguish between awaiting and not awaiting in the program's output.   
            ' You can adjust the value to produce the output that this topic shows   
            ' after the code.  
            Dim delay = 5000  
  
            ' Call #1.  
            ' Call an async method. Because you don't await it, its completion isn't   
            ' coordinated with the current method, CallingMethodAsync.  
            ' The following line causes the warning.  
            CalledMethodAsync(delay)  
  
            ' Call #2.  
            ' To suppress the warning without awaiting, you can assign the   
            ' returned task to a variable. The assignment doesn't change how  
            ' the program runs. However, the recommended practice is always to  
            ' await a call to an async method.  
  
            ' Replace Call #1 with the following line.  
            'Task delayTask = CalledMethodAsync(delay)  
  
            ' Call #3  
            ' To contrast with an awaited call, replace the unawaited call   
            ' (Call #1 or Call #2) with the following awaited call. The best   
            ' practice is to await the call.  
  
            'Await CalledMethodAsync(delay)  
  
            ' If the call to CalledMethodAsync isn't awaited, CallingMethodAsync  
            ' continues to run and, in this example, finishes its work and returns  
            ' to its caller.  
            ResultsTextBox.Text &= vbCrLf & "  Returning from calling method."  
        End Function  
  
        Async Function CalledMethodAsync(howLong As Integer) As Task  
  
            ResultsTextBox.Text &= vbCrLf & "    Entering called method, starting and awaiting Task.Delay."  
            ' Slow the process down a little so you can distinguish between awaiting  
            ' and not awaiting. Adjust the value for howLong if necessary.  
            Await Task.Delay(howLong)  
            ResultsTextBox.Text &= vbCrLf & "    Task.Delay is finished--returning from called method."  
        End Function  
  
    End Class  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    '     Task.Delay is finished--returning from called method.  
  
    ' Output  
  
    ' Entering the Click event handler.  
    '   Entering calling method.  
    '     Entering called method, starting and awaiting Task.Delay.  
    '     Task.Delay is finished--returning from called method.  
    '   Returning from calling method.  
    ' Exiting the Click event handler.  
    ```  
  
5.  Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     L'output previsto viene visualizzato alla fine del codice.  
  
## <a name="see-also"></a>Vedere anche  
 [Await (operatore)](../../../visual-basic/language-reference/operators/await-operator.md)   
 [Programmazione asincrona con Async e Await](../../../visual-basic/programming-guide/concepts/async/index.md)
