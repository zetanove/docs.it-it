---
title: Controllare il flusso in programmi asincroni (Visual Basic) | Documenti di Microsoft
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
ms.assetid: b0443af7-c586-4cb0-b476-742ae4098a96
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
ms.openlocfilehash: 15e02fbc023db9ae2f3ee9f40598faa7c9c027a0
ms.lasthandoff: 03/13/2017

---
# <a name="control-flow-in-async-programs-visual-basic"></a>Flusso di controllo in programmi asincroni (Visual Basic)
È possibile scrivere e gestire più facilmente programmi asincroni utilizzando il `Async` e `Await` le parole chiave. Tuttavia, i risultati potrebbero sorprendere di comprendere il funzionamento del programma. Tracce in questo argomento il flusso di controllo tramite un programma asincrono semplice visualizzare quando il controllo si sposta da un metodo a un altro e quali informazioni verrà trasferito ogni volta.  
  
> [!NOTE]
>  Le parole chiave `Async` e `Await` sono state introdotte in Visual Studio 2012.  
  
 In generale, contrassegnare i metodi che contengono codice asincrono con il [Async](../../../../visual-basic/language-reference/modifiers/async.md) modificatore. In un metodo contrassegnato con un modificatore async, è possibile utilizzare un [Await (Visual Basic)](../../../../visual-basic/language-reference/operators/await-operator.md) per specificare un in cui il metodo viene sospesa in attesa di un processo asincrono chiamato al completamento. Per ulteriori informazioni, vedere [la programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md).  
  
 L'esempio seguente usa i metodi asincroni per scaricare il contenuto di un sito Web specificato come stringa e visualizzare la lunghezza della stringa. L'esempio contiene due metodi seguenti.  
  
-   `startButton_Click`, che chiama `AccessTheWebAsync` e visualizza il risultato.  
  
-   `AccessTheWebAsync`, che scarica il contenuto di un sito Web sotto forma di stringa e restituisce la lunghezza della stringa. `AccessTheWebAsync`utilizza asincrono <xref:System.Net.Http.HttpClient>metodo <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>, per scaricare il contenuto.</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> </xref:System.Net.Http.HttpClient>  
  
 Numerate Visualizza le righe vengono visualizzate in punti strategici in tutto il programma per comprendere come viene eseguito il programma e viene descritto cosa accade in ogni punto contrassegnato. Visualizza linee sono contrassegnate con "Uno"e "sei." Le etichette di rappresentano l'ordine in cui il programma raggiunge le righe di codice.  
  
 Il codice seguente illustra una struttura del programma.  
  
```vb  
Class MainWindow  
  
    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
        ' ONE  
        Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
        ' FOUR  
        Dim contentLength As Integer = Await getLengthTask  
  
        ' SIX  
        ResultsTextBox.Text &=  
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
  
    End Sub  
  
    Async Function AccessTheWebAsync() As Task(Of Integer)  
  
        ' TWO  
        Dim client As HttpClient = New HttpClient()   
        Dim getStringTask As Task(Of String) =   
            client.GetStringAsync("http://msdn.microsoft.com")  
  
        ' THREE  
        Dim urlContents As String = Await getStringTask  
  
        ' FIVE  
        Return urlContents.Length  
    End Function  
  
End Class  
  
```  
  
 Ognuna delle posizioni di etichetta, "Uno"e "6", vengono visualizzate informazioni sullo stato corrente del programma. Viene prodotto l'output seguente.  
  
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
 È possibile scaricare il codice utilizzato in questo argomento da MSDN o è possibile generarlo manualmente.  
  
> [!NOTE]
>  Per eseguire l'esempio, è necessario disporre di Visual Studio 2012 o versione successiva e .NET Framework 4.5 o versioni successive installato nel computer in uso.  
  
### <a name="download-the-program"></a>Scaricare il programma  
 È possibile scaricare l'applicazione di questo argomento da [esempio asincrono: flusso di controllo in programmi asincroni](http://go.microsoft.com/fwlink/?LinkId=255285). I passaggi seguenti aprono ed eseguire il programma.  
  
1.  Decomprimere il file scaricato e quindi avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Apri**, **Progetto/Soluzione**.  
  
3.  Passare alla cartella che contiene il codice di esempio non compressi, aprire il file di soluzione (sln) e quindi premere il tasto F5 per compilare ed eseguire il progetto.  
  
### <a name="build-the-program-yourself"></a>Compilare il programma autonomamente  
 Il progetto Windows Presentation Foundation (WPF) seguente contiene l'esempio di codice per questo argomento.  
  
 Per eseguire il progetto, effettuare i passaggi seguenti:  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra dei menu scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel **modelli installati** riquadro, scegliere **Visual Basic**, quindi scegliere **applicazione WPF** dall'elenco dei tipi di progetto.  
  
4.  Immettere `AsyncTracer` come nome del progetto, quindi scegliere il **OK** pulsante.  
  
     Il nuovo progetto verrà visualizzato **Esplora**.  
  
5.  Nell'Editor di codice di Visual Studio scegliere la scheda **MainWindow.xaml** .  
  
     Se la scheda non è visibile, aprire il menu di scelta rapida per MainWindow. XAML in **Esplora**, quindi scegliere **Visualizza codice**.  
  
6.  Nel **XAML** visualizzazione di MainWindow. XAML, sostituire il codice con il codice seguente.  
  
    ```vb  
    <Window  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="MainWindow"  
        Title="Control Flow Trace" Height="350" Width="525">  
        <Grid>  
            <Button x:Name="StartButton" Content="Start" HorizontalAlignment="Left" Margin="221,10,0,0" VerticalAlignment="Top" Width="75"/>  
            <TextBox x:Name="ResultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="510" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" d:LayoutOverrides="HorizontalMargin"/>  
  
        </Grid>  
    </Window>  
  
    ```  
  
     Viene visualizzata una finestra semplice che contiene una casella di testo e un pulsante nel **progettazione** visualizzazione di MainWindow. Xaml.  
  
7.  Aggiungere un riferimento per <xref:System.Net.Http>.</xref:System.Net.Http>  
  
8.  In **Esplora**, aprire il menu di scelta rapida per MainWindow.xaml.vb e quindi scegliere **Visualizza codice**.  
  
9. Nel file MainWindow.xaml.vb, sostituire il codice con il codice seguente.  
  
    ```vb  
    ' Add an Imports statement and a reference for System.Net.Http.  
    Imports System.Net.Http  
  
    Class MainWindow  
  
        Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs) Handles StartButton.Click  
  
            ' The display lines in the example lead you through the control shifts.  
            ResultsTextBox.Text &= "ONE:   Entering StartButton_Click." & vbCrLf &  
                "           Calling AccessTheWebAsync." & vbCrLf  
  
            Dim getLengthTask As Task(Of Integer) = AccessTheWebAsync()  
  
            ResultsTextBox.Text &= vbCrLf & "FOUR:  Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is started." & vbCrLf &  
                "           About to await getLengthTask -- no caller to return to." & vbCrLf  
  
            Dim contentLength As Integer = Await getLengthTask  
  
            ResultsTextBox.Text &= vbCrLf & "SIX:   Back in StartButton_Click." & vbCrLf &  
                "           Task getLengthTask is finished." & vbCrLf &  
                "           Result from AccessTheWebAsync is stored in contentLength." & vbCrLf &  
                "           About to display contentLength and exit." & vbCrLf  
  
            ResultsTextBox.Text &=  
                String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
        End Sub  
  
        Async Function AccessTheWebAsync() As Task(Of Integer)  
  
            ResultsTextBox.Text &= vbCrLf & "TWO:   Entering AccessTheWebAsync."  
  
            ' Declare an HttpClient object.  
            Dim client As HttpClient = New HttpClient()  
  
            ResultsTextBox.Text &= vbCrLf & "           Calling HttpClient.GetStringAsync." & vbCrLf  
  
            ' GetStringAsync returns a Task(Of String).   
            Dim getStringTask As Task(Of String) = client.GetStringAsync("http://msdn.microsoft.com")  
  
            ResultsTextBox.Text &= vbCrLf & "THREE: Back in AccessTheWebAsync." & vbCrLf &  
                "           Task getStringTask is started."  
  
            ' AccessTheWebAsync can continue to work until getStringTask is awaited.  
  
            ResultsTextBox.Text &=  
                vbCrLf & "           About to await getStringTask & return a Task(Of Integer) to StartButton_Click." & vbCrLf  
  
            ' Retrieve the website contents when task is complete.  
            Dim urlContents As String = Await getStringTask  
  
            ResultsTextBox.Text &= vbCrLf & "FIVE:  Back in AccessTheWebAsync." &  
                vbCrLf & "           Task getStringTask is complete." &  
                vbCrLf & "           Processing the return statement." &  
                vbCrLf & "           Exiting from AccessTheWebAsync." & vbCrLf  
  
            Return urlContents.Length  
        End Function  
  
    End Class  
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
  
## <a name="trace-the-program"></a>Il programma di analisi  
  
### <a name="steps-one-and-two"></a>Passaggi UNO e DUE  
 Visualizza prime due righe di traccia il percorso come `startButton_Click` chiamate `AccessTheWebAsync`, e `AccessTheWebAsync` chiama il <xref:System.Net.Http.HttpClient>metodo <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>.</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> </xref:System.Net.Http.HttpClient> asincrono Nell'immagine seguente vengono illustrate le chiamate da un metodo a.  
  
 ![Passaggi uno e due](../../../../csharp/programming-guide/concepts/async/media/asynctrace-onetwo.png "AsyncTrace ONETWO")  
  
 Il tipo restituito di `AccessTheWebAsync` e `client.GetStringAsync` è <xref:System.Threading.Tasks.Task%601>.</xref:System.Threading.Tasks.Task%601> Per `AccessTheWebAsync`, TResult è un numero intero. Per `GetStringAsync`, TResult è una stringa. Per ulteriori informazioni sui tipi restituiti di metodi asincroni, vedere [Async restituire tipi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md).  
  
 Un metodo asincrono che restituisce task restituisce un'istanza dell'attività quando il controllo passa al chiamante. Controllo viene restituito da un metodo asincrono al chiamante quando un `Await` operatore viene rilevata nel metodo chiamato o quando termina il metodo chiamato. Visualizza linee che sono contrassegnate con "Tre"e "sei" tracciano questa parte del processo.  
  
### <a name="step-three"></a>Passaggio TRE  
 In `AccessTheWebAsync`, il metodo asincrono <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29>viene chiamato per scaricare il contenuto della pagina Web di destinazione.</xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> Controllo viene restituito da `client.GetStringAsync` a `AccessTheWebAsync` quando `client.GetStringAsync` restituisce.  
  
 Il `client.GetStringAsync` un'attività di stringa che viene assegnato a un metodo di `getStringTask` variabile in `AccessTheWebAsync`. La riga seguente nel programma di esempio illustra la chiamata a `client.GetStringAsync` e l'assegnazione.  
  
<CodeContentPlaceHolder>5</CodeContentPlaceHolder>  
 Può essere considerato dell'attività come una promessa da `client.GetStringAsync` per produrre una stringa effettiva alla fine. Nel frattempo, se `AccessTheWebAsync` dispone di lavoro che non dipende dalla stringa promessa di `client.GetStringAsync`, che possibile continuare a lavorare mentre `client.GetStringAsync` rimane in attesa. Nell'esempio, le seguenti righe di output, che sono contrassegnate con "Tre", rappresentano la possibilità di eseguire operazioni indipendenti  
  
<CodeContentPlaceHolder>6</CodeContentPlaceHolder>  
 L'istruzione seguente consente di sospendere lo stato di avanzamento in `AccessTheWebAsync` quando `getStringTask` è atteso.  
  
<CodeContentPlaceHolder>7</CodeContentPlaceHolder>  
 Di seguito viene illustrato il flusso di controllo da `client.GetStringAsync` per l'assegnazione al `getStringTask` e dalla creazione di `getStringTask` all'applicazione di un operatore Await.  
  
 ![Passaggio tre](../../../../csharp/programming-guide/concepts/async/media/asynctrace-three.png "AsyncTrace tre")  
  
 L'espressione await sospende `AccessTheWebAsync` fino a quando non `client.GetStringAsync` restituisce. Nel frattempo il controllo viene restituito al chiamante di `AccessTheWebAsync`, `startButton_Click`.  
  
> [!NOTE]
>  In genere, si attende immediatamente la chiamata a un metodo asincrono. Ad esempio, l'assegnazione seguente Impossibile sostituire il codice precedente che crea e quindi attende `getStringTask`:`Dim urlContents As String = Await client.GetStringAsync("http://msdn.microsoft.com")`  
>   
>  In questo argomento, l'operatore await viene applicato in un secondo momento per contenere le righe di output che indicano il flusso di controllo tramite il programma.  
  
### <a name="step-four"></a>Passaggio QUATTRO  
 Dichiarato il tipo restituito di `AccessTheWebAsync` è `Task(Of Integer)`. Pertanto, quando `AccessTheWebAsync` è sospeso, restituisce un'attività di intero a `startButton_Click`. È necessario comprendere che l'attività restituita non è `getStringTask`. L'attività restituita è una nuova attività di integer che rappresenta ciò che resta da eseguire nel metodo sospeso, `AccessTheWebAsync`. L'attività è una promessa da `AccessTheWebAsync` per produrre un numero intero quando l'attività è completata.  
  
 L'istruzione seguente assegna questa attività per il `getLengthTask` variabile.  
  
<CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
 Come in `AccessTheWebAsync`, `startButton_Click` possibile continuare con un lavoro che non dipenda dai risultati dell'attività asincrona (`getLengthTask`) fino a quando l'attività è atteso. Le seguenti righe di output rappresentano il lavoro.  
  
<CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
 Stato di avanzamento `startButton_Click` viene sospesa quando `getLengthTask` è atteso. Sospende la seguente istruzione di assegnazione `startButton_Click` fino a quando non `AccessTheWebAsync` è stata completata.  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
 Nella figura seguente, le frecce indicano il flusso di controllo dall'espressione await in `AccessTheWebAsync` per l'assegnazione di un valore a `getLengthTask`, seguito dall'elaborazione normale in `startButton_Click` fino a quando non `getLengthTask` è atteso.  
  
 ![Passaggio quattro](../../../../csharp/programming-guide/concepts/async/media/asynctrace-four.png "AsyncTrace quattro")  
  
### <a name="step-five"></a>Passaggio CINQUE  
 Quando `client.GetStringAsync` segnala che è completo, l'elaborazione `AccessTheWebAsync` viene rilasciato dalla sospensione e può continuare oltre l'istruzione await. Le seguenti righe di output rappresentano la ripresa dell'elaborazione.  
  
<CodeContentPlaceHolder>11</CodeContentPlaceHolder>  
 L'operando dell'istruzione return, `urlContents.Length`, viene archiviato nell'attività che `AccessTheWebAsync` restituisce. L'espressione await recupera il valore da `getLengthTask` in `startButton_Click`.  
  
 Di seguito viene illustrato il trasferimento del controllo dopo `client.GetStringAsync` (e `getStringTask`) sono state completate.  
  
 ![Passaggio cinque](../../../../csharp/programming-guide/concepts/async/media/asynctrace-five.png "cinque AsyncTrace")  
  
 `AccessTheWebAsync`Restituisce fino al completamento e il controllo `startButton_Click`, che è in attesa del completamento.  
  
### <a name="step-six"></a>Passaggio SEI  
 Quando `AccessTheWebAsync` segnala che è completo, l'elaborazione può continuare oltre all'istruzione await nel `startButton_Async`. Infatti, il programma è nulla da eseguire.  
  
 Le seguenti righe di output rappresentano la ripresa dell'elaborazione in `startButton_Async`:  
  
<CodeContentPlaceHolder>12</CodeContentPlaceHolder>  
 L'espressione await recupera da `getLengthTask` il valore intero che rappresenta l'operando dell'istruzione return in `AccessTheWebAsync`. L'istruzione seguente assegna tale valore per il `contentLength` variabile.  
  
<CodeContentPlaceHolder>13</CodeContentPlaceHolder>  
 La figura seguente mostra la restituzione del controllo da `AccessTheWebAsync` a `startButton_Click`.  
  
 ![Passaggio sei](../../../../csharp/programming-guide/concepts/async/media/asynctrace-six.png "AsyncTrace sei")  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione asincrona con Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)   
 [Tipi restituiti asincroni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md)   
 [Procedura dettagliata: Accesso al Web tramite Async e Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)   
 [Esempio asincrono: Flusso di controllo in programmi asincroni (c# e Visual Basic)](http://go.microsoft.com/fwlink/?LinkId=255285)
