---
title: Tipi restituiti async (C#) | Microsoft Docs
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
ms.assetid: ddb2539c-c898-48c1-ad92-245e4a996df8
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: d974e93c3c50a61889a9ed37ad5f68f7a131a538
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="async-return-types-c"></a>Tipi restituiti async (C#)
I metodi asincroni hanno tre possibili tipi restituiti: <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task> e void. In Visual Basic il tipo restituito void è scritto come routine [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md). Per altre informazioni sulla funzionalità dei metodi asincroni, vedere [Asynchronous Programming with async and await (C#)](../../../../csharp/programming-guide/concepts/async/index.md) (Programmazione asincrona con async e await (C#)).  
  
 Ogni tipo restituito viene esaminato in una delle sezioni seguenti e alla fine dell'argomento è disponibile un esempio completo che usa tutti i tre tipi.  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario avere installato Visual Studio 2012 o versioni successive e .NET Framework 4.5 o versioni successive nel computer.  
  
##  <a name="BKMK_TaskTReturnType"></a> Tipo restituito task(T)  
 Il tipo restituito <xref:System.Threading.Tasks.Task%601> viene usato per un metodo asincrono che include un'istruzione [return](../../../../csharp/language-reference/keywords/return.md) (C#) in cui l'operando è di tipo `TResult`.  
  
 Nell'esempio seguente il metodo asincrono `TaskOfT_MethodAsync` contiene un'istruzione return che restituisce un valore intero. La dichiarazione del metodo deve quindi specificare un tipo restituito di `Task<int>`.  
  
```csharp  
// TASK<T> EXAMPLE  
async Task<int> TaskOfT_MethodAsync()  
{  
    // The body of the method is expected to contain an awaited asynchronous  
    // call.  
    // Task.FromResult is a placeholder for actual work that returns a string.  
    var today = await Task.FromResult<string>(DateTime.Now.DayOfWeek.ToString());  
  
    // The method then can process the result in some way.  
    int leisureHours;  
    if (today.First() == 'S')  
        leisureHours = 16;  
    else  
        leisureHours = 5;  
  
    // Because the return statement specifies an operand of type int, the  
    // method must have a return type of Task<int>.  
    return leisureHours;  
}  
```  
  
 Quando `TaskOfT_MethodAsync` viene chiamato da un'espressione await, l'espressione recupera il valore intero (valore di `leisureHours`) archiviato nell'attività restituita da `TaskOfT_MethodAsync`. Per altre informazioni sulle espressioni await, vedere [await](../../../../csharp/language-reference/keywords/await.md).  
  
 Il codice seguente chiama e attende il metodo `TaskOfT_MethodAsync`. Il risultato viene assegnato alla variabile `result1`.  
  
```csharp  
// Call and await the Task<T>-returning async method in the same statement.  
int result1 = await TaskOfT_MethodAsync();  
```  
  
 È possibile capire meglio il modo in cui ciò avviene separando la chiamata a `TaskOfT_MethodAsync` dall'applicazione di `await`, come illustrato dal codice seguente. Una chiamata al metodo `TaskOfT_MethodAsync` che non viene immediatamente attesa restituisce un tipo `Task<int>`, come ci si aspetterebbe dalla dichiarazione del metodo. Nell'esempio, l'attività viene assegnata alla variabile `integerTask`. Poiché `integerTask` è <xref:System.Threading.Tasks.Task%601>, contiene una proprietà <xref:System.Threading.Tasks.Task%601.Result> di tipo `TResult`. In questo caso, TResult rappresenta un tipo Integer. Quando `await` viene applicato a `integerTask`, l'espressione await restituisce il contenuto della proprietà <xref:System.Threading.Tasks.Task%601.Result%2A> di `integerTask`. Il valore viene assegnato alla variabile `result2`.  
  
> [!WARNING]
>  La proprietà <xref:System.Threading.Tasks.Task%601.Result%2A> è una proprietà di blocco. Se si prova ad accedervi prima del completamento dell'attività, il thread attualmente attivo viene bloccato fino a quando l'attività non viene completata e il valore non è disponibile. Nella maggior parte dei casi, è consigliabile accedere al valore usando `await` invece di accedere direttamente alla proprietà.  
  
```csharp  
// Call and await in separate statements.  
Task<int> integerTask = TaskOfT_MethodAsync();  
  
// You can do other work that does not rely on integerTask before awaiting.  
textBox1.Text += String.Format("Application can continue working while the Task<T> runs. . . . \r\n");  
  
int result2 = await integerTask;  
```  
  
 Le istruzioni di visualizzazione nel codice seguente verificano che i valori della variabile `result1`, della variabile `result2` e della proprietà `Result` siano identici. Si noti che la proprietà `Result` è una proprietà di blocco e non ci si deve accedere prima che la sua attività sia stata completata.  
  
```csharp  
// Display the values of the result1 variable, the result2 variable, and  
// the integerTask.Result property.  
textBox1.Text += String.Format("\r\nValue of result1 variable:   {0}\r\n", result1);  
textBox1.Text += String.Format("Value of result2 variable:   {0}\r\n", result2);  
textBox1.Text += String.Format("Value of integerTask.Result: {0}\r\n", integerTask.Result);  
```  
  
##  <a name="BKMK_TaskReturnType"></a> Tipo restituito Task  
 I metodi asincroni che non contengono un'istruzione return o che contengono un'istruzione return che non restituisce un operando hanno in genere il tipo restituito <xref:System.Threading.Tasks.Task>. Questi sarebbero metodi che restituiscono un valore void se fossero scritti per l'esecuzione sincrona. Se si usa un tipo restituito `Task` per un metodo asincrono, un metodo di chiamata può usare un operatore await per sospendere il completamento del chiamante fino a quando il metodo asincrono non abbia terminato l'operazione.  
  
 Nell'esempio seguente il metodo asincrono `Task_MethodAsync` non contiene un'istruzione return. Di conseguenza, si specifica un tipo restituito `Task` per il metodo, che consente a `Task_MethodAsync` di essere atteso. La definizione del tipo `Task` non include una proprietà `Result` per archiviare un valore restituito.  
  
```csharp  
// TASK EXAMPLE  
async Task Task_MethodAsync()  
{  
    // The body of an async method is expected to contain an awaited   
    // asynchronous call.  
    // Task.Delay is a placeholder for actual work.  
    await Task.Delay(2000);  
    // Task.Delay delays the following line by two seconds.  
    textBox1.Text += String.Format("\r\nSorry for the delay. . . .\r\n");  
  
    // This method has no return statement, so its return type is Task.    
}  
```  
  
 `Task_MethodAsync` viene chiamato e atteso usando un'istruzione await invece di un'espressione await, simile all'istruzione di chiamata per un metodo sincrono che restituisce void. L'applicazione di un operatore await in questo caso non produce un valore.  
  
 Il codice seguente chiama e attende il metodo `Task_MethodAsync`.  
  
```csharp  
// Call and await the Task-returning async method in the same statement.  
await Task_MethodAsync();  
```  
  
 Analogamente all'esempio precedente di <xref:System.Threading.Tasks.Task%601>, è possibile separare la chiamata a `Task_MethodAsync` dall'applicazione di un operatore await, come illustrato nel codice seguente. Tuttavia, si noti che un tipo `Task` non ha una proprietà `Result` e che quando viene applicato un operatore await a un tipo `Task` non viene prodotto alcun valore.  
  
 Il codice seguente separa la chiamata di `Task_MethodAsync` dall'attesa dell'attività restituita da `Task_MethodAsync`.  
  
```csharp  
// Call and await in separate statements.  
Task simpleTask = Task_MethodAsync();  
  
// You can do other work that does not rely on simpleTask before awaiting.  
textBox1.Text += String.Format("\r\nApplication can continue working while the Task runs. . . .\r\n");  
  
await simpleTask;  
```  
  
##  <a name="BKMK_VoidReturnType"></a> Tipo restituito void  
 Il tipo restituito void viene usato principalmente nei gestori di eventi in cui è obbligatorio. Un tipo restituito void può essere usato anche per eseguire l'override di metodi che restituiscono void o per metodi che eseguono attività che possono essere categorizzate come "Fire and Forget". È consigliabile tuttavia restituire un tipo `Task` ogni volta che è possibile, perché un metodo asincrono che restituisce void non può essere atteso. Qualsiasi chiamante di questo metodo deve poter continuare fino al completamento senza attendere il completamento del metodo asincrono chiamato e il chiamante deve essere indipendente da qualsiasi eccezione o valore generato dal metodo asincrono.  
  
 Il chiamante di un metodo asincrono che restituisce void non può intercettare le eccezioni generate dal metodo ed è probabile che queste eccezioni non gestite provochino un errore dell'applicazione. Se si verifica un'eccezione in un metodo asincrono che restituisce <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>, l'eccezione viene archiviata nell'attività restituita e rigenerata durante l'attesa dell'attività. Di conseguenza, verificare che qualsiasi metodo asincrono in grado di produrre un'eccezione abbia un tipo restituito <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601> e che le chiamate al metodo vengano attese.  
  
 Per altre informazioni su come intercettare eccezioni nei metodi asincroni, vedere [try-catch](../../../../csharp/language-reference/keywords/try-catch.md) .  
  
 Il codice seguente definisce un gestore eventi asincroni.  
  
```csharp  
// VOID EXAMPLE  
private async void button1_Click(object sender, RoutedEventArgs e)  
{  
    textBox1.Clear();  
  
    // Start the process and await its completion. DriverAsync is a   
    // Task-returning async method.  
    await DriverAsync();  
  
    // Say goodbye.  
    textBox1.Text += "\r\nAll done, exiting button-click event handler.";  
}  
```  
  
##  <a name="BKMK_Example"></a> Esempio completo  
 Il progetto Windows Presentation Foundation (WPF) seguente contiene gli esempi di codice di questo argomento.  
  
 Per eseguire il progetto, effettuare i passaggi seguenti:  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nella categoria **Installati**, **Modelli** scegliere Visual C# e quindi scegliere **Windows**. Dall'elenco dei tipi di progetto scegliere **Applicazione WPF**.  
  
4.  Immettere `AsyncReturnTypes` come nome del progetto e scegliere **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
5.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow.xaml in **Esplora soluzioni** e quindi scegliere **Apri**.  
  
6.  Nella finestra **XAML** di MainWindow.xaml sostituire il codice con quello seguente.  
  
    ```csharp  
    <Window x:Class="AsyncReturnTypes.MainWindow"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            Title="MainWindow" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="button1" Content="Start" HorizontalAlignment="Left" Margin="214,28,0,0" VerticalAlignment="Top" Width="75" HorizontalContentAlignment="Center" FontWeight="Bold" FontFamily="Aharoni" Click="button1_Click"/>  
            <TextBox x:Name="textBox1" Margin="0,80,0,0" TextWrapping="Wrap" FontFamily="Lucida Console"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     Nella finestra di **progettazione**di MainWindow.xaml verrà visualizzata una finestra contenente una casella di testo e un pulsante.  
  
7.  In **Esplora soluzioni** aprire il menu di scelta rapida per MainWindow.xaml.cs e quindi scegliere **Visualizza codice**.  
  
8.  Sostituire il codice in MainWindow.xaml.cs con quello riportato di seguito.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    using System.Windows;  
    using System.Windows.Controls;  
    using System.Windows.Data;  
    using System.Windows.Documents;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    using System.Windows.Media.Imaging;  
    using System.Windows.Navigation;  
    using System.Windows.Shapes;  
  
    namespace AsyncReturnTypes  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            // VOID EXAMPLE  
            private async void button1_Click(object sender, RoutedEventArgs e)  
            {  
                textBox1.Clear();  
  
                // Start the process and await its completion. DriverAsync is a   
                // Task-returning async method.  
                await DriverAsync();  
  
                // Say goodbye.  
                textBox1.Text += "\r\nAll done, exiting button-click event handler.";  
            }  
  
            async Task DriverAsync()  
            {  
                // Task<T>   
                // Call and await the Task<T>-returning async method in the same statement.  
                int result1 = await TaskOfT_MethodAsync();  
  
                // Call and await in separate statements.  
                Task<int> integerTask = TaskOfT_MethodAsync();  
  
                // You can do other work that does not rely on integerTask before awaiting.  
                textBox1.Text += String.Format("Application can continue working while the Task<T> runs. . . . \r\n");  
  
                int result2 = await integerTask;  
  
                // Display the values of the result1 variable, the result2 variable, and  
                // the integerTask.Result property.  
                textBox1.Text += String.Format("\r\nValue of result1 variable:   {0}\r\n", result1);  
                textBox1.Text += String.Format("Value of result2 variable:   {0}\r\n", result2);  
                textBox1.Text += String.Format("Value of integerTask.Result: {0}\r\n", integerTask.Result);  
  
                // Task  
                // Call and await the Task-returning async method in the same statement.  
                await Task_MethodAsync();  
  
                // Call and await in separate statements.  
                Task simpleTask = Task_MethodAsync();  
  
                // You can do other work that does not rely on simpleTask before awaiting.  
                textBox1.Text += String.Format("\r\nApplication can continue working while the Task runs. . . .\r\n");  
  
                await simpleTask;  
            }  
  
            // TASK<T> EXAMPLE  
            async Task<int> TaskOfT_MethodAsync()  
            {  
                // The body of the method is expected to contain an awaited asynchronous  
                // call.  
                // Task.FromResult is a placeholder for actual work that returns a string.  
                var today = await Task.FromResult<string>(DateTime.Now.DayOfWeek.ToString());  
  
                // The method then can process the result in some way.  
                int leisureHours;  
                if (today.First() == 'S')  
                    leisureHours = 16;  
                else  
                    leisureHours = 5;  
  
                // Because the return statement specifies an operand of type int, the  
                // method must have a return type of Task<int>.  
                return leisureHours;  
            }  
  
            // TASK EXAMPLE  
            async Task Task_MethodAsync()  
            {  
                // The body of an async method is expected to contain an awaited   
                // asynchronous call.  
                // Task.Delay is a placeholder for actual work.  
                await Task.Delay(2000);  
                // Task.Delay delays the following line by two seconds.  
                textBox1.Text += String.Format("\r\nSorry for the delay. . . .\r\n");  
  
                // This method has no return statement, so its return type is Task.    
            }  
        }  
    }  
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
 <xref:System.Threading.Tasks.Task.FromResult%2A>   
 [Procedura dettagliata: accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Flusso di controllo in programmi asincroni (C#)](../../../../csharp/programming-guide/concepts/async/control-flow-in-async-programs.md)   
 [async](../../../../csharp/language-reference/keywords/async.md)   
 [await](../../../../csharp/language-reference/keywords/await.md)
