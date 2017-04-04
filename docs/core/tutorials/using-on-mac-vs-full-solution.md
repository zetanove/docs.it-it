---
title: Creazione di una soluzione .NET Core completa in macOS con Visual Studio per Mac | Microsoft Docs
description: Questo argomento descrive il processo di creazione di una soluzione .NET Core contenente una libreria riutilizzabile e unit test.
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 03/16/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 6945bedf-5bf3-4955-8588-83fb87511b79
translationtype: Human Translation
ms.sourcegitcommit: ff143583ba62fc1d82561e739a75107e50ebee88
ms.openlocfilehash: c76168d1c9ae65ef0d17c55aab156a4f16ecea52
ms.lasthandoff: 03/20/2017

---

# <a name="building-a-complete-net-core-solution-on-macos-using-visual-studio-for-mac"></a>Creazione di una soluzione .NET Core completa in macOS con Visual Studio per Mac

Visual Studio per Mac offre un ambiente di sviluppo integrato completo per lo sviluppo di applicazioni .NET Core. Questo argomento descrive il processo di creazione di una soluzione .NET Core contenente una libreria riutilizzabile e unit test.

In questa esercitazione viene illustrato come creare un'applicazione che accetta una parola di ricerca e una stringa di testo dall'utente, conta il numero di volte in cui la parola di ricerca appare nella stringa usando un metodo in una libreria di classi e restituisce il risultato all'utente. La soluzione include anche unit test per la libreria di classi come introduzione ai concetti relativi allo sviluppo basato su test. Se si preferisce continuare l'esercitazione con un esempio completo, scaricare la [soluzione di esempio](https://github.com/dotnet/docs/blob/master/samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter).

> [!NOTE]
> Visual Studio per Mac è un software di anteprima. Come per qualsiasi versione di anteprima di prodotti Microsoft, il feedback dei clienti è sempre tenuto in grande considerazione. Sono disponibili due modi per comunicare al team di sviluppatori la propria opinione su Visual Studio per Mac:
> * In Visual Studio per Mac scegliere **? > Segnala un problema** dal menu o **Segnala un problema** dalla schermata iniziale per visualizzare una finestra per l'archiviazione di un report di bug.
> * Per inviare un suggerimento, scegliere **? > Invia un suggerimento** dal menu o **Invia un suggerimento** dalla schermata iniziale per aprire la [pagina Web UserVoice di Visual Studio per Mac](https://visualstudio.uservoice.com/forums/563332-visual-studio-for-mac).

## <a name="prerequisites"></a>Prerequisiti

[.NET Core e OpenSSL](https://www.microsoft.com/net/core#macos)

Per altre informazioni sui prerequisiti, vedere [Prerequisiti per .NET Core in Mac](../../core/macos-prerequisites.md).

## <a name="getting-started"></a>Per iniziare

Se i prerequisiti e Visual Studio per Mac sono già installati, ignorare questa sezione e passare a [Creazione di una libreria](#building-a-library). Seguire questa procedura per installare i prerequisiti e Visual Studio per Mac:

1. Scaricare e installare [.NET Core e OpenSSL](https://www.microsoft.com/net/core#macos).

1. Scaricare il [programma di installazione di Visual Studio per Mac](https://www.visualstudio.com/vs/visual-studio-mac/). Eseguire il programma di installazione. Leggere e accettare il contratto di licenza. Durante l'installazione viene offerta la possibilità di installare Xamarin, una tecnologia per lo sviluppo di app per dispositivi mobili multipiattaforma. L'installazione di Xamarin e dei relativi componenti è facoltativa per lo sviluppo di .NET Core. Per una descrizione dettagliata del processo di installazione di Visual Studio per Mac, vedere [Presentazione di Visual Studio per Mac](https://developer.xamarin.com/guides/cross-platform/visual-studio-mac/). Al termine dell'installazione, avviare l'IDE di Visual Studio per Mac.

## <a name="building-a-library"></a>Creazione di una libreria

1. Nella schermata iniziale selezionare **Nuovo progetto**. Nella finestra di dialogo **Nuovo progetto**, nel nodo **Multiplatform** (Multipiattaforma), selezionare il modello **.NET Standard Library** (Libreria .NET Standard). Scegliere **Avanti**.

   ![Finestra di dialogo Nuovo progetto](./media/using-on-mac-vs-full-solution/vsmacfull01.png)

1. Assegnare al progetto il nome "TextUtils" (nome breve per "Text Utilities") e alla soluzione il nome "WordCounter". Lasciare selezionata la casella **Crea una directory del progetto nella directory della soluzione**. Scegliere **Crea**.

   ![Finestra di dialogo Nuovo progetto](./media/using-on-mac-vs-full-solution/vsmacfull02.png)

1. Nella barra laterale **Soluzione** espandere il nodo `TextUtils` per visualizzare il file di classe fornito dal modello: *Class1.cs*. Fare clic con il pulsante destro del mouse sul file, scegliere **Rinomina** dal menu di scelta rapida e rinominare il file in *WordCount.cs*. Aprire il file e sostituire il contenuto con il codice seguente:

   [!code-csharp[Principale](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/TextUtils/WordCount.cs)]

1. Salvare il file adottando uno di questi tre metodi: usare l'abbreviazione da tastiera <kbd>&#8984;</kbd>+<kbd>s</kbd>, scegliere **File > Salva** dal menu o fare clic con il pulsante destro del mouse sulla scheda del file e scegliere **Salva** dal menu di scelta rapida. Nell'immagine seguente viene visualizzata la finestra dell'IDE:

   ![Finestra dell'IDE con la libreria di classi TextUtils, il file di classe WordCount, la classe statica WordCount e il metodo GetWordCount](./media/using-on-mac-vs-full-solution/vsmacfull03.png)

1. Selezionare **Errori** nel margine inferiore della finestra dell'IDE per aprire il pannello **Errori**. Selezionare il pulsante **Output di compilazione**.

   ![Margine inferiore della finestra dell'IDE con il pulsante Errori](./media/using-on-mac-vs-full-solution/vsmacfull03b.png)

1. Scegliere **Compila > Compila tutto** dal menu.

   La soluzione viene compilata e il riquadro dell'output di compilazione indica che la compilazione ha avuto esito positivo.

   ![Riquadro dell'output di compilazione del pannello Errori con il messaggio di compilazione riuscita](./media/using-on-mac-vs-full-solution/vsmacfull04.png)

## <a name="creating-a-test-project"></a>Creazione di un progetto di test

Gli unit test forniscono test software automatici durante le fasi di sviluppo e pubblicazione. Il framework di test usato in questa esercitazione è [xUnit](https://xunit.github.io/).

1. Nella barra laterale **Soluzione** fare clic con il pulsante destro del mouse sulla soluzione `WordCounter` e scegliere **Aggiungi > Aggiungi nuovo progetto**.

1. Nella finestra di dialogo **Nuovo progetto** selezionare **Test** sotto il nodo **.NET Core**. Selezionare **xUnit Test Project** (Progetto di test xUnit) e quindi scegliere **Avanti**.

   ![Finestra di dialogo Nuovo progetto in cui si crea il progetto di test xUnit](./media/using-on-mac-vs-full-solution/vsmacfull05.png)

1. Assegnare al nuovo progetto il nome "TestLibrary" e scegliere **Crea**.

   ![Finestra di dialogo Nuovo progetto in cui si specifica il nome del progetto](./media/using-on-mac-vs-full-solution/vsmacfull06.png)

1. Aggiungere un riferimento al progetto `TextUtils` per consentire l'interazione tra la libreria di test e la classe `WordCount`. Nella barra laterale **Soluzione** fare clic con il pulsante destro del mouse su **Dipendenze** in **TestLibrary**. Scegliere **Modifica riferimenti** dal menu di scelta rapida.

1. Nella finestra di dialogo **Modifica riferimenti** selezionare il progetto **TextUtils** nella scheda **Progetti**. Scegliere **OK**.

   ![Finestra di dialogo Modifica riferimenti](./media/using-on-mac-vs-full-solution/vsmacfull07.png)

1. Nel progetto **TestLibrary** rinominare il file *UnitTest1.cs* in *TextUtilsTests.cs*.

1. Aprire il file e sostituire il codice con il seguente:

   ```csharp
   using Xunit;
   using TextUtils;
   using System.Diagnostics;

   namespace TestLibrary
   {
       public class TextUtils_GetWordCountShould
       {
           [Fact]
           public void IgnoreCasing()
           {
               var wordCount = WordCount.GetWordCount("Jack", "Jack jack");
   
               Assert.NotEqual(2, wordCount);
           }
       }
   }
   ```

   Nell'immagine seguente viene visualizzato l'IDE con il codice dell'unit test. Prestare attenzione all'istruzione `Assert.NotEquals`.

   ![Unit test iniziale per verificare GetWordCount nella finestra principale dell'IDE](./media/using-on-mac-vs-full-solution/vsmacfull08.png)

   Quando si usa lo sviluppo basato su test, è importante fare in modo che il nuovo test la prima volta abbia esito negativo per verificare che la logica di test sia corretta. Il metodo passa il nome "Jack" (lettere maiuscole) e una stringa con "Jack" e "jack" (lettere maiuscole e minuscole). Se il metodo `GetWordCount` funziona correttamente, viene restituito un conteggio di due istanze della parola di ricerca. Per fare in modo che il test non riesca, è necessario prima implementare il test asserendo che dal metodo `GetWordCount` non vengono restituite due istanze della parola di ricerca "Jack". Andare quindi al passaggio successivo per fare in modo che il test abbia esito negativo.

1. Attualmente, Visual Studio per Mac non integra test xUnit nel Test Runner predefinito e i test xUnit devono essere quindi eseguiti nella console. Fare clic con il pulsante destro del mouse sul progetto `TestLibrary` e scegliere **Strumenti > Apri nel terminale** dal menu di scelta rapida. Al prompt dei comandi eseguire `dotnet test`.
   
   Il test ha esito negativo, che è il risultato previsto. Il metodo di test indica che dalla stringa "Jack Jack" fornita al metodo `GetWordCount` non vengono restituite due istanze della stringa `inputString`, "Jack". Poiché nel metodo `GetWordCount` è stato escluso l'uso delle maiuscole/minuscole, vengono invece restituite due istanze. L'asserzione che 2 *non è uguale a* 2 ha esito negativo. Questo è il risultato previsto e la logica del test è corretta. Lasciare aperta la finestra della console mentre nel passaggio successivo si preparerà l'ambiente per modificare il test per la versione finale.

   ![Esito negativo del test nella finestra della console. Totale test: 1 Esito positivo: 0 Esito negativo: 1. Esecuzione dei test non riuscita.](./media/using-on-mac-vs-full-solution/vsmacfull09.png)

1. Modificare il metodo di test `IgnoreCasing` sostituendo `Assert.NotEqual` con `Assert.Equal`. Salvare il file usando l'abbreviazione da tastiera <kbd>&#8984;</kbd>+<kbd>s</kbd>, selezionando **File > Salva** dal menu o facendo clic con il pulsante destro del mouse sulla scheda del file e scegliendo **Salva** dal menu di scelta rapida.

   Si prevede che l'oggetto `searchWord` "Jack" restituisca due istanze con la stringa `inputString` "Jack jack" passata a `GetWordCount`. Nella finestra della console eseguire di nuovo `dotnet test`. Il test ha esito positivo. Nella stringa "Jack jack" (senza distinzione tra maiuscole e minuscole) sono presenti due istanze di "Jack" e l'asserzione del test è `true`.

   ![Esito positivo del test nella finestra della console. Totale test: 1 Esito positivo: 1 Esito negativo: 0. Esecuzione dei test completata.](./media/using-on-mac-vs-full-solution/vsmacfull10.png)

1. La restituzione di singoli valori di test con un oggetto `Fact` è solo una delle operazioni che è possibile eseguire con gli unit test. Grazie a un'altra tecnica molto efficace, è possibile eseguire il test di più valori contemporaneamente usando un oggetto `Theory`. Aggiungere il metodo seguente alla classe `TextUtils_GetWordCountShould`. Dopo aver aggiunto il metodo alla classe sono disponibili due metodi:

   ```csharp
   [Theory]
   [InlineData(0, "Ting", "Does not appear in the string.")]
   [InlineData(1, "Ting", "Ting appears once.")]
   [InlineData(2, "Ting", "Ting appears twice with Ting.")]
   public void CountInstancesCorrectly(int count, 
                                       string searchWord, 
                                       string inputString)
   {
       Assert.Equal(count, WordCount.GetWordCount(searchWord,
                                                  inputString));
   }
   ```

   `CountInstancesCorrectly` verifica che il metodo `GetWordCount` esegua il conteggio in modo corretto. L'oggetto `InlineData` fornisce un conteggio, una parola di ricerca e una stringa di input da verificare. Il metodo di test viene eseguito una volta per ogni riga di dati. Tenere presente che, ancora una volta, si sta asserendo prima un esito negativo tramite `Assert.NotEqual`, anche se si è certi che i conteggi dei dati siano corretti e che i valori corrispondano ai conteggi restituiti dal metodo `GetWordCount`. Anche se, in un primo momento, l'esecuzione del test con esito negativo sembra una perdita di tempo, la verifica della logica del test tramite la generazione di un esito negativo consente in realtà di attestarne la correttezza. Successivamente si potrà trovare un metodo di test che ha esito positivo quando invece dovrebbe avere esito negativo e si identificherà un errore nella logica del test. Vale quindi la pena eseguire questo passaggio ogni volta che si crea un metodo di test.
   
1. Salvare il file ed eseguire `dotnet test` nella finestra della console. Il test delle maiuscole/minuscole ha esito positivo, mentre i tre test del conteggio hanno esito negativo. Questo è esattamente il risultato previsto.

   ![Esito negativo del test nella finestra della console. Totale test: 4 Esito positivo: 1 Esito negativo: 3. Esecuzione dei test non riuscita.](./media/using-on-mac-vs-full-solution/vsmacfull11.png)

1. Modificare il metodo di test `CountInstancesCorrectly` sostituendo `Assert.NotEqual` con `Assert.Equal`. Salvare il file. Eseguire di nuovo `dotnet test` nella finestra della console. Tutti i test hanno esito positivo.

   ![Esito positivo del test nella finestra della console. Totale test: 4 Esito positivo: 4 Esito negativo: 0. Esecuzione dei test completata.](./media/using-on-mac-vs-full-solution/vsmacfull12.png)

## <a name="adding-a-console-app"></a>Aggiunta di un'app console

1. Nella barra laterale **Soluzione** fare clic con il pulsante destro del mouse sulla soluzione `WordCounter`. Aggiungere un nuovo progetto **Applicazione console** selezionando il modello corrispondente dai modelli **.NET Core > App**. Scegliere **Avanti**. Assegnare al progetto il nome **WordCounterApp**. Scegliere **Crea** per creare il progetto nella soluzione.

1. Nella barra laterale **Soluzioni** fare clic con il pulsante destro del mouse sul nodo **Dipendenze** del nuovo progetto **WordCounterApp**. Nella finestra di dialogo **Modifica riferimenti** selezionare **TextUtils** e scegliere **OK**.

1. Aprire il file *Program.cs*. Sostituire il codice con quello seguente:

   [!code-csharp[Principale](../../../samples/core/tutorials/using-on-mac-vs-full-solution/WordCounter/WordCounterApp/Program.cs)]

1. Per eseguire l'app in una finestra della console anziché nell'IDE, fare clic con il pulsante destro del mouse sul progetto `WordCounterApp`, scegliere **Opzioni** e aprire il nodo **Predefinito** in **Configurazioni**. Selezionare la casella di controllo **Esegui in console esterna**. Lasciare selezionata l'opzione **Sospendi output della console**. Con questa impostazione l'app viene generata in una finestra della console in cui è possibile digitare l'input per le istruzioni `Console.ReadLine`. Se invece si lascia che l'app venga generata nell'ambiente IDE, è possibile vedere solo l'output delle istruzioni `Console.WriteLine`. Le istruzioni `Console.ReadLine` non funzionano nel pannello **Output applicazione** dell'ambiente IDE.

   ![Finestra Opzioni di progetto](./media/using-on-mac-vs-full-solution/vsmacfull13.png)

1. Poiché con l'anteprima di Visual Studio per Mac non è possibile eseguire i test quando è in esecuzione la soluzione, si esegue direttamente l'app console. Fare clic con il pulsante destro del mouse sul progetto `WordCounterApp` e scegliere **Run item** (Esegui elemento) dal menu di scelta rapida. Se si prova a eseguire l'applicazione con il pulsante di riproduzione, l'esecuzione del Test Runner e dell'app avranno esito negativo. Per altre informazioni sullo stato del lavoro inerente a questo problema, vedere [xunit/xamarinstudio.xunit (#60)](https://github.com/xunit/xamarinstudio.xunit/issues/60). Con l'app in esecuzione, specificare i valori relativi alla parola di ricerca e alla stringa di input quando vengono richiesti nella finestra della console. L'app indica il numero di volte in cui la parola di ricerca appare nella stringa.

   ![Finestra della console in cui viene eseguita la ricerca della parola "olives" nella stringa "Iro ate olives by the lake, and the olives were wonderful". L'app risponde "The search word olives appears 2 times."](./media/using-on-mac-vs-full-solution/vsmacfull14.png)

1. Si esaminerà infine la funzionalità di debug con Visual Studio per Mac. Impostare un punto di interruzione nell'istruzione `Console.WriteLine` e selezionare il margine sinistro della riga 23. Verrà visualizzato un cerchio rosso accanto alla riga di codice. In alternativa, selezionare un punto qualsiasi nella riga di codice e scegliere **Esegui > Imposta/Rimuovi punto di interruzione** dal menu.

   ![Punto di interruzione impostato sulla riga 23, istruzione Console.WriteLine](./media/using-on-mac-vs-full-solution/vsmacfull15.png)

1. Fare clic con il pulsante destro del mouse sul progetto `WordCounterApp`. Scegliere l'elemento **Avvia debug** dal menu di scelta rapida. Quando si esegue l'app, immettere la parola di ricerca "cat" e "The dog chased the cat, but the cat escaped." come stringa in cui eseguire la ricerca. Quando viene raggiunta l'istruzione `Console.WriteLine`, l'esecuzione del programma si interrompe per consentire l'esecuzione dell'istruzione. Nella scheda **Variabili locali** sono presenti i valori `searchWord`, `inputString`, `wordCount` e `pluralChar`.

   ![Esecuzione del programma interrotta in corrispondenza dell'istruzione Console.WriteLine e finestra Variabili locali con i valori visualizzati immediatamente prima dell'esecuzione dell'istruzione Console.WriteLine.](./media/using-on-mac-vs-full-solution/vsmacfull16.png)

1. Nel riquadro **Immediato** digitare "wordCount = 999;" e premere INVIO. Alla variabile `wordCount` viene assegnato un valore senza senso di 999 per indicare che è possibile sostituire i valori della variabile durante il debug.

   ![Punto di interruzione raggiunto. Nella finestra Immediato il valore wordCount viene impostato su 999](./media/using-on-mac-vs-full-solution/vsmacfull17.png)

1. Sulla barra degli strumenti fare clic sulla freccia per *continuare*. Esaminare l'output nella finestra della console. Viene visualizzato il valore non corretto 999 impostato durante il debug dell'app.

   ![Pulsante della barra degli strumenti per continuare l'operazione](./media/using-on-mac-vs-full-solution/vsmacfull18.png)

   ![Il conteggio della parola di ricerca è ora impostato su 999 nell'output dell'applicazione](./media/using-on-mac-vs-full-solution/vsmacfull19.png)

## <a name="next-steps"></a>Passaggi successivi

* Funzionalità aggiuntive di Visual Studio per Mac sono disponibili in [Introducing Visual Studio for Mac](https://developer.xamarin.com/guides/cross-platform/visual-studio-mac/) (Introduzione a Visual Studio per Mac) sul sito Web di Xamarin Developer.
* Per un'analisi più approfondita delle funzionalità di Visual Studio per Mac, vedere la guida [Xamarin Studio Tour](https://developer.xamarin.com/guides/cross-platform/xamarin-studio/ide-tour/) (Tour di Xamarin Studio).

