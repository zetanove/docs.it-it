---
title: Flusso di controllo in programmi asincroni (C#) | Microsoft Docs
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
ms.assetid: fc92b08b-fe1d-4d07-84ab-5192fafe06bb
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: be7974018ce3195dc7344192d647fe64fb2ebcc4
ms.openlocfilehash: 4d73428cd2a896309f90af45fef682186c470417
ms.contentlocale: it-it
ms.lasthandoff: 05/14/2017

---
# <a name="control-flow-in-async-programs-c"></a>Flusso di controllo in programmi asincroni (C#)
Le parole chiave `async` e `await` consentono di scrivere e gestire più facilmente i programmi asincroni. Tuttavia, i risultati potrebbero creare perplessità se non si conosce il funzionamento del programma. Questo argomento descrive il flusso di controllo attraverso un programma asincrono semplice per indicare quando il controllo si sposta da un metodo a un altro e quali informazioni vengono trasferite ogni volta.  
  
> [!NOTE]
>  Le parole chiave `async` e `await` sono state introdotte in Visual Studio 2012.  
  
 In generale, si contrassegnano i metodi che contengono codice asincrono con il modificatore [async (C#)](../../../../csharp/language-reference/keywords/async.md). In un metodo contrassegnato con un modificatore async è possibile usare un operatore [await (C#)](../../../../csharp/language-reference/keywords/await.md) per specificare dove il metodo viene sospeso in attesa del completamento di un processo asincrono chiamato. Per altre informazioni, vedere [Programmazione asincrona con async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md).  
  
 L'esempio seguente usa i metodi asincroni per scaricare come stringa il contenuto di un sito Web specificato e per visualizzare la lunghezza della stringa. L'esempio contiene i due metodi seguenti.  
  
-   `startButton_Click`, che chiama `AccessTheWebAsync` e visualizza il risultato.  
  
-   `AccessTheWebAsync`, che scarica il contenuto di un sito Web come stringa e restituisce la lunghezza della stringa. `AccessTheWebAsync` usa un metodo <xref:System.Net.Http.HttpClient> asincrono, ovvero <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>, per scaricare il contenuto.  
  
 In corrispondenza dei punti strategici del programma sono visualizzate righe numerate che consentono di comprendere come viene eseguito il programma e spiegano che cosa accade in ogni punto contrassegnato. Le righe sono evidenziate con etichette numerate da "ONE" a "SIX." Le etichette rappresentano l'ordine in cui il programma raggiunge queste righe di codice.  
  
 Il codice seguente rappresenta una struttura del programma.  
  
```csharp  
public partial class MainWindow : Window  
{  
    // . . .  
    private async void startButton_Click(object sender, RoutedEventArgs e)  
    {  
        // ONE  
        Task<int> getLengthTask = AccessTheWebAsync();  
  
        // FOUR  
        int contentLength = await getLengthTask;  
  
        // SIX  
        resultsTextBox.Text +=  
            String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
    }  
  
    async Task<int> AccessTheWebAsync()  
    {  
        // TWO  
        HttpClient client = new HttpClient();  
        Task<string> getStringTask =  
            client.GetStringAsync("http://msdn.microsoft.com");  
  
        // THREE                   
        string urlContents = await getStringTask;  
  
        // FIVE  
        return urlContents.Length;  
    }  
}  
```  
  
 Ognuna delle posizioni con etichetta da "ONE" a "SIX" visualizza informazioni sullo stato corrente del programma. Viene visualizzato l'output seguente.  
  
```  
ONE:   Entering startButton_Click.  
           Calling AccessTheWebAsync.  
  
TWO:   Entering AccessTheWebAsync.  
           Calling HttpClient.GetStringAsync.  
  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
  
Length of the downloaded string: 33946.  
```  
  
## <a name="set-up-the-program"></a>Impostare il programma  
 È possibile scaricare il codice usato in questo argomento da MSDN oppure crearlo manualmente.  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario che Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versione successiva siano installati nel computer.  
  
### <a name="download-the-program"></a>Scaricare il programma  
 È possibile scaricare l'applicazione di questo argomento da [Async Sample: Control Flow in Async Programs](http://go.microsoft.com/fwlink/?LinkId=255285) (Esempio di attività asincrona: flusso di controllo in programmi asincroni). I passaggi seguenti consentono di aprire ed eseguire il programma.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Passare alla cartella che contiene il codice di esempio decompresso, aprire il file della soluzione (SLN) e quindi scegliere il tasto F5 per compilare ed eseguire il progetto.  
  
### <a name="build-the-program-yourself"></a>Compilare il programma autonomamente  
 Il seguente progetto Windows Presentation Foundation (WPF) contiene gli esempi di codice per questo argomento.  
  
 Per eseguire il progetto, effettuare i passaggi seguenti:  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel riquadro **Modelli installati** scegliere **Visual C#** e quindi **Applicazione WPF** nell'elenco dei tipi di progetto.  
  
4.  Immettere `AsyncTracer` come nome del progetto, quindi scegliere il pulsante **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
5.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow.xaml in **Esplora soluzioni** e scegliere **Visualizza codice**.  
  
6.  Nella visualizzazione **XAML** di MainWindow.xaml sostituire il codice con quello riportato di seguito.  
  
    ```csharp  
    <Window  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="AsyncTracer.MainWindow"  
            Title="Control Flow Trace" Height="350" Width="592">  
        <Grid>  
            <Button x:Name="startButton" Content="Start  
    " HorizontalAlignment="Left" Margin="250,10,0,0" VerticalAlignment="Top" Width="75" Height="24"  Click="startButton_Click" d:LayoutOverrides="GridBox"/>  
            <TextBox x:Name="resultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="576" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" Grid.ColumnSpan="3"/>  
        </Grid>  
    </Window>  
    ```  
  
     Nella visualizzazione **Progettazione** di MainWindow.xaml viene visualizzata una finestra semplice contenente una casella di testo e un pulsante.  
  
7.  Aggiunge un riferimento a <xref:System.Net.Http>.  
  
8.  In **Esplora soluzioni** aprire il menu di scelta rapida per MainWindow.xaml.cs e scegliere **Visualizza codice**.  
  
9. Sostituire il codice in MainWindow.xaml.cs con quello riportato di seguito.  
  
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
  
    // Add a using directive and a reference for System.Net.Http;  
    using System.Net.Http;  
  
    namespace AsyncTracer  
    {  
        public partial class MainWindow : Window  
        {  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            private async void startButton_Click(object sender, RoutedEventArgs e)  
            {  
                // The display lines in the example lead you through the control shifts.  
                resultsTextBox.Text += "ONE:   Entering startButton_Click.\r\n" +  
                    "           Calling AccessTheWebAsync.\r\n";  
  
                Task<int> getLengthTask = AccessTheWebAsync();  
  
                resultsTextBox.Text += "\r\nFOUR:  Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is started.\r\n" +  
                    "           About to await getLengthTask -- no caller to return to.\r\n";  
  
                int contentLength = await getLengthTask;  
  
                resultsTextBox.Text += "\r\nSIX:   Back in startButton_Click.\r\n" +  
                    "           Task getLengthTask is finished.\r\n" +  
                    "           Result from AccessTheWebAsync is stored in contentLength.\r\n" +  
                    "           About to display contentLength and exit.\r\n";  
  
                resultsTextBox.Text +=  
                    String.Format("\r\nLength of the downloaded string: {0}.\r\n", contentLength);  
            }  
  
            async Task<int> AccessTheWebAsync()  
            {  
                resultsTextBox.Text += "\r\nTWO:   Entering AccessTheWebAsync.";  
  
                // Declare an HttpClient object.  
                HttpClient client = new HttpClient();  
  
                resultsTextBox.Text += "\r\n           Calling HttpClient.GetStringAsync.\r\n";  
  
                // GetStringAsync returns a Task<string>.   
                Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
  
                resultsTextBox.Text += "\r\nTHREE: Back in AccessTheWebAsync.\r\n" +  
                    "           Task getStringTask is started.";  
  
                // AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
                resultsTextBox.Text +=  
                    "\r\n           About to await getStringTask and return a Task<int> to startButton_Click.\r\n";  
  
                // Retrieve the website contents when task is complete.  
                string urlContents = await getStringTask;  
  
                resultsTextBox.Text += "\r\nFIVE:  Back in AccessTheWebAsync." +  
                    "\r\n           Task getStringTask is complete." +  
                    "\r\n           Processing the return statement." +  
                    "\r\n           Exiting from AccessTheWebAsync.\r\n";  
  
                return urlContents.Length;  
            }  
        }  
    }  
    ```  
  
10. Premere il tasto F5 per eseguire il programma e quindi scegliere il pulsante **Start** .  
  
     Dovrebbe venire visualizzato l'output seguente.  
  
    ```  
    ONE:   Entering startButton_Click.  
               Calling AccessTheWebAsync.  
  
    TWO:   Entering AccessTheWebAsync.  
               Calling HttpClient.GetStringAsync.  
  
    THREE: Back in AccessTheWebAsync.  
               Task getStringTask is started.  
               About to await getStringTask & return a Task<int> to startButton_Click.  
  
    FOUR:  Back in startButton_Click.  
               Task getLengthTask is started.  
               About to await getLengthTask -- no caller to return to.  
  
    FIVE:  Back in AccessTheWebAsync.  
               Task getStringTask is complete.  
               Processing the return statement.  
               Exiting from AccessTheWebAsync.  
  
    SIX:   Back in startButton_Click.  
               Task getLengthTask is finished.  
               Result from AccessTheWebAsync is stored in contentLength.  
               About to display contentLength and exit.  
  
    Length of the downloaded string: 33946.  
    ```  
  
## <a name="trace-the-program"></a>Analizzare il programma  
  
### <a name="steps-one-and-two"></a>Passaggi UNO e DUE  
 Le prime due righe di visualizzazione tracciano il percorso poiché `startButton_Click` chiama `AccessTheWebAsync` e `AccessTheWebAsync` chiama il metodo asincrono <xref:System.Net.Http.HttpClient>, ovvero <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>. Nell'immagine seguente vengono illustrate le chiamate metodo a metodo.  
  
 ![Passaggi UNO e DUE](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace-ONETWO")  
  
 Il tipo restituito di `AccessTheWebAsync` e `client.GetStringAsync` è <xref:System.Threading.Tasks.Task%601>. Per `AccessTheWebAsync` TResult è un numero intero. Per `GetStringAsync` TResult è una stringa. Per altre informazioni sui tipi restituiti dei metodi asincroni, vedere [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md).  
  
 Un metodo asincrono che restituisce un'attività restituisce un'istanza dell'attività quando il controllo torna al chiamante. Il controllo viene restituito da un metodo asincrono al relativo chiamante quando viene rilevato un operatore `await` nel metodo chiamato o quando termina il metodo chiamato. Le righe evidenziate con le etichette da "THREE" a "SIX" analizzano questa parte del processo.  
  
### <a name="step-three"></a>Passaggio TRE  
 In `AccessTheWebAsync`, il metodo asincrono <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> viene chiamato per scaricare il contenuto della pagina Web di destinazione. Il controllo viene restituito da `client.GetStringAsync` a `AccessTheWebAsync` quando viene restituito `client.GetStringAsync`.  
  
 Il metodo `client.GetStringAsync` restituisce un'attività di stringa che viene assegnata alla variabile `getStringTask` in `AccessTheWebAsync`. La riga seguente nel programma di esempio indica la chiamata a `client.GetStringAsync` e l'assegnazione.  
  
```csharp  
Task<string> getStringTask = client.GetStringAsync("http://msdn.microsoft.com");  
```  
  
 Si può pensare all'attività come a una promessa fatta da `client.GetStringAsync` di produrre una stringa reale alla fine. Nel frattempo, se `AccessTheWebAsync` ha del lavoro da svolgere che non dipende dalla stringa promessa da `client.GetStringAsync`, il lavoro può continuare mentre `client.GetStringAsync` rimane in attesa. Nell'esempio, le righe di output seguenti, che sono contrassegnate con "THREE", rappresentano la possibilità di eseguire operazioni indipendenti  
  
```  
THREE: Back in AccessTheWebAsync.  
           Task getStringTask is started.  
           About to await getStringTask & return a Task<int> to startButton_Click.  
```  
  
 L'istruzione seguente sospende lo stato di avanzamento in `AccessTheWebAsync` quando si attende `getStringTask`.  
  
```csharp  
string urlContents = await getStringTask;  
```  
  
 L'immagine che segue illustra il flusso di controllo da `client.GetStringAsync` all'assegnazione a `getStringTask` e dalla creazione di `getStringTask` all'applicazione di un operatore await.  
  
 ![Passaggio TRE](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace tre")  
  
 L'espressione await sospende `AccessTheWebAsync` finché non viene restituito `client.GetStringAsync`. Nel frattempo il controllo viene restituito al chiamante di `AccessTheWebAsync`, `startButton_Click`.  
  
> [!NOTE]
>  In genere, la chiamata a un metodo asincrono si attende immediatamente. Ad esempio, l'assegnazione seguente potrebbe sostituire il codice precedente che crea e quindi attende `getStringTask`:`string urlContents = await client.GetStringAsync("http://msdn.microsoft.com");`  
>   
>  In questo argomento l'operatore await viene applicato in un secondo tempo per contenere le righe di output che indicano il flusso di controllo attraverso il programma.  
  
### <a name="step-four"></a>Passaggio QUATTRO  
 Il tipo restituito dichiarato di `AccessTheWebAsync` è `Task<int>`. Di conseguenza, quando `AccessTheWebAsync` è sospeso, restituisce un'attività di valori integer a `startButton_Click`. È necessario comprendere che l'attività restituita non è `getStringTask`. L'attività restituita è una nuova attività di valori integer che rappresenta ciò che resta da eseguire nel metodo sospeso, `AccessTheWebAsync`. L'attività è una promessa da parte di `AccessTheWebAsync` di produrre un numero intero al termine dell'attività.  
  
 L'istruzione seguente assegna questa attività alla variabile `getLengthTask`.  
  
```csharp  
Task<int> getLengthTask = AccessTheWebAsync();  
```  
  
 Come in `AccessTheWebAsync`, `startButton_Click` può continuare a eseguire operazioni che non dipendono dai risultati dell'attività asincrona (`getLengthTask`) finché si è in attesa dell'attività. Le seguenti righe di output rappresentano tali operazioni.  
  
```  
FOUR:  Back in startButton_Click.  
           Task getLengthTask is started.  
           About to await getLengthTask -- no caller to return to.  
```  
  
 Lo stato di avanzamento in `startButton_Click` viene sospeso quando si attende `getLengthTask`. La seguente istruzione di assegnazione sospende `startButton_Click` finché non si completa `AccessTheWebAsync`.  
  
```csharp  
int contentLength = await getLengthTask;  
```  
  
 Nella figura seguente le frecce indicano il flusso di controllo dall'espressione await in `AccessTheWebAsync` all'assegnazione di un valore a `getLengthTask`, seguita dall'elaborazione normale in `startButton_Click` finché si è in attesa di `getLengthTask`.  
  
 ![Passaggio QUATTRO](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace-FOUR")  
  
### <a name="step-five"></a>Passaggio CINQUE  
 Quando l'attività `client.GetStringAsync` segnala il proprio completamento, l'elaborazione in `AccessTheWebAsync` viene rilasciata dalla sospensione e può continuare oltre l'istruzione await. Le seguenti righe di output rappresentano la ripresa dell'elaborazione.  
  
```  
FIVE:  Back in AccessTheWebAsync.  
           Task getStringTask is complete.  
           Processing the return statement.  
           Exiting from AccessTheWebAsync.  
```  
  
 L'operando dell'istruzione return, `urlContents.Length`, viene archiviato nell'attività restituita da `AccessTheWebAsync`. L'espressione await recupera tale valore da `getLengthTask` in `startButton_Click`.  
  
 L'immagine seguente illustra il trasferimento del controllo dopo il completamento di `client.GetStringAsync` (e `getStringTask`).  
  
 ![Passaggio CINQUE](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "AsyncTrace-FIVE")  
  
 `AccessTheWebAsync` viene eseguita fino al completamento e il controllo viene restituito a `startButton_Click`, che è in attesa del completamento.  
  
### <a name="step-six"></a>Passaggio SEI  
 Quando l'attività `AccessTheWebAsync` segnala il proprio completamento, l'elaborazione può continuare oltre l'istruzione await in `startButton_Async`. Di fatto il programma non ha altre operazioni da eseguire.  
  
 Le seguenti righe di output rappresentano la ripresa dell'elaborazione in `startButton_Async`:  
  
```  
SIX:   Back in startButton_Click.  
           Task getLengthTask is finished.  
           Result from AccessTheWebAsync is stored in contentLength.  
           About to display contentLength and exit.  
```  
  
 L'espressione await recupera da `getLengthTask` il valore integer che rappresenta l'operando dell'istruzione return in `AccessTheWebAsync`. L'istruzione seguente assegna tale valore alla variabile `contentLength`.  
  
```csharp  
int contentLength = await getLengthTask;  
```  
  
 La figura seguente illustra la restituzione del controllo da `AccessTheWebAsync` a `startButton_Click`.  
  
 ![Passaggio SEI](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace-SIX")  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con async e await (C#)](../../../../csharp/programming-guide/concepts/async/index.md)   
 [Tipi restituiti asincroni (C#)](../../../../csharp/programming-guide/concepts/async/async-return-types.md)   
 [Procedura dettagliata: Accesso al Web tramite async e await (C#)](../../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Async Sample: Control Flow in Async Programs (C# and Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255285) (Esempio di attività asincrona: Flusso di controllo in programmi asincroni (C# e Visual Basic))

