---
title: Test di una libreria di classi con .NET Core in Visual Studio 2017
description: Informazioni su come testare una libreria di classi scritta in C# usando Visual Studio 2017
keywords: ".NET Core, libreria di classi .NET Standard, Visual Studio 2017 testing unità"
author: BillWagner
ms.author: wiwagn
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 069ad711-3eaa-45c6-94d7-b40249cc8b99
ms.translationtype: Human Translation
ms.sourcegitcommit: 39e8e757a446b30ab18914465853138e1c239e40
ms.openlocfilehash: 629af913bb5172b890161bb82f45a65e6bb6498d
ms.contentlocale: it-it
ms.lasthandoff: 05/03/2017

---

# <a name="testing-a-class-library-with-net-core-in-visual-studio-2017"></a>Test di una libreria di classi con .NET Core in Visual Studio 2017

In [Creazione di una libreria di classi con #C e .NET Core in Visual Studio 2017](library-with-visual-studio.md) è stata creata una libreria di classi semplice che aggiunge un metodo di estensione alla classe @System.String. Ora verrà creato uno unit test per verificare che tale libreria funzioni nel modo previsto. Il progetto unit test verrà aggiunto alla soluzione creata nell'argomento precedente.

## <a name="creating-a-unit-test-project"></a>Creazione di un progetto unit test

Per creare un progetto unit test, seguire questa procedura:

1. In **Esplora soluzioni** aprire il menu di scelta rapida per il nodo della soluzione **ClassLibraryProject** e selezionare **Aggiungi** > **Nuovo progetto**.

   <!-- Need a VS 2017 version  [!NOTE] In addition to a Unit Test project, you can also use Visual Studio to create an xUnit test project for .NET Core. For a walkthrough that includes an xUnit test project, see [Getting started with .NET Core on Windows, using Visual Studio 2015](../../core/tutorials/using-on-windows.md). --> 

1. Nella finestra di dialogo **Aggiungi nuovo progetto** selezionare il nodo **.NET Core** seguito dal modello di progetto **Progetto unit test (.NET Core)**. Nella casella di testo **Nome** immettere "StringLibraryTest" come nome del progetto. Selezionare **OK** per creare il progetto unit test.

   ![Finestra di dialogo Aggiungi nuovo progetto](./media/testing-library-with-visual-studio/testproject.png)

1. Visual Studio crea il progetto e apre il file *UnitTest1.cs* nella finestra del codice.

   ![Finestra del codice di Visual Studio che visualizza la classe predefinita del progetto unit test UnitTest1 e il metodo TestMethod1](./media/testing-library-with-visual-studio/unittestwindow.png)

   Il codice sorgente creato dal modello di unit test esegue le operazioni seguenti:

   * Importa lo spazio dei nomi [Microsoft.VisualStudio.TestTools.UnitTesting](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.aspx), contenente i tipi usati per il testing unità.

   * Applica l'attributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) alla classe `UnitTest1`. Ogni metodo di test presente in una classe di test contrassegnata con l'attributo \[TestMethod\] viene eseguito automaticamente durante l'esecuzione dello unit test.

   * Applica l'attributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) per definire `TestMethod1` come metodo di test da eseguire automaticamente durante l'esecuzione dello unit test.

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Dipendenze** del progetto **StringLibraryTest** e selezionare **Aggiungi riferimento** dal menu di scelta rapida.

   ![Menu di scelta rapida delle dipendenze StringLibraryTest](./media/testing-library-with-visual-studio/addreference.png)

1. Nella finestra di dialogo **Gestione riferimenti** selezionare la casella accanto a **StringLibrary**. L'aggiunta di un riferimento all'assembly `StringLibrary` consente al compilatore di individuare i metodi **StringLibrary**. Selezionare il pulsante **OK**. Viene aggiunto un riferimento al progetto di libreria di classi `StringLibrary`.

   ![Gestione riferimenti](./media/testing-library-with-visual-studio/referencemanager.png)

## <a name="adding-and-running-unit-test-methods"></a>Aggiunta ed esecuzione di metodi unit test

Quando Visual Studio esegue uno unit test, esegue tutti i metodi contrassegnati con l'attributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) in una classe unit test, ovvero la classe a cui è applicato l'attributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx). Un metodo di test termina quando viene rilevato il primo errore o quando tutti i test contenuti nel metodo stesso hanno avuto esito positivo.

I test più comuni chiamano i membri della classe [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx). Molti metodi assert includono almeno due parametri, uno dei quali corrisponde al risultato previsto del test, mentre l'altro corrisponde al risultato effettivo. La tabella seguente illustra alcuni dei metodi chiamati con maggiore frequenza.

Metodi Assert | Funzione
--- | ---
`Assert.AreEqual` | Verifica che due oggetti o valori siano uguali. Il metodo ha esito negativo se gli oggetti o i valori non sono uguali.
`Assert.AreSame` | Verifica che due variabili oggetto facciano riferimento allo stesso oggetto. Il metodo ha esito negativo se le variabili fanno riferimento a oggetti diversi.
`Assert.IsFalse` | Verifica che una condizione sia `false`. Il metodo ha esito negativo se la condizione è `true`.
`Assert.IsNotNull` | Verifica che un oggetto non sia `null`. Il metodo ha esito negativo se l'oggetto è `null`.
Attributo [\[ExpectedException\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.expectedexceptionattribute.aspx) | Indica il tipo di eccezione che un metodo di test dovrebbe generare. Il test ha esito negativo se l'eccezione specificata non viene generata.

Durante il test del metodo `StringLibrary.StartsWithUpper`, è possibile specificare alcune stringhe che iniziano con un carattere maiuscolo. In tal caso si prevede che il metodo restituisca `true`, quindi è possibile chiamare il metodo [Assert.IsTrue(Boolean, String)](https://msdn.microsoft.com/library/ms243754.aspx). Analogamente, è possibile specificare alcune stringhe che iniziano con un valore diverso da un carattere maiuscolo. In tal caso si prevede che il metodo restituisca `false`, quindi è possibile chiamare il metodo [Assert.IsFalse(Boolean, String)](https://msdn.microsoft.com/library/ms243805.aspx).

Poiché il metodo della libreria gestisce le stringhe, è anche possibile verificare che gestisca in modo corretto una [stringa vuota (`String.Empty`) ](xref:System.String.Empty), ovvero una stringa valida senza caratteri e con proprietà @System.String.Length uguale a 0, e una stringa `null` che non è stata inizializzata. Se `StartsWithUpper` è chiamato come metodo di estensione su un'istanza di @System.String, non può essere passato a una stringa `null`. È tuttavia possibile chiamarlo direttamente come metodo statico e passarlo a un singolo argomento @System.String.

Verranno definiti tre metodi, ognuno dei quali chiama più volte il relativo metodo [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx) per ogni elemento di una matrice di stringhe. Poiché il metodo di test ha esito negativo quando incontra il primo errore, verrà chiamato un overload del metodo che consente di passare una stringa in cui è indicato il valore stringa usato nella chiamata al metodo.

Per creare i metodi di test:

1. Nella finestra del codice *UnitTest1.cs* sostituire il codice con il seguente:

   [!CODE-csharp[Test#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs#1)]

   Si noti che nel metodo `TestStartsWithUpper` il test dei caratteri maiuscoli include la lettera alfa maiuscola dell'alfabeto greco (U+0391) e la lettera EM maiuscola dell'alfabeto cirillico (U+041C). Si noti anche che nel metodo `TestDoesNotStartWithUpper` il test dei caratteri minuscoli include la lettera alfa minuscola dell'alfabeto greco (U+03B1) e la lettera Ghe minuscola dell'alfabeto cirillico (U+0433).

1. Nella barra dei menu scegliere **File** > **Salva UnitTest1.cs con nome**. Nella finestra di dialogo **Salva file con nome** selezionare la freccia accanto al pulsante **Salva** e selezionare **Salva con codifica**.

   ![Finestra di dialogo Salva file con nome](./media/testing-library-with-visual-studio/savefileas.png)

1. Nella finestra di dialogo **Conferma Salva con nome** selezionare il pulsante **Sì** per salvare il file.

1. Nella finestra di dialogo **Opzioni di salvataggio avanzate** selezionare **Unicode (UTF-8 con firma digitale) - Tabella codici 65001** dall'elenco a discesa **Codifica** e selezionare **OK**.

   ![Finestra di dialogo Opzioni di salvataggio avanzate](./media/testing-library-with-visual-studio/advancedsaveoptions.png)

   Se il salvataggio del codice sorgente come file con codifica UTF8 ha esito negativo, Visual Studio può salvarlo come file ASCII. In questo caso il runtime non decodifica in modo accurato i caratteri UTF8 non compresi nell'intervallo ASCII e i risultati del test non sono precisi.

1. Nella barra dei menu selezionare **Test** > **Esegui** > **Tutti i test**. Viene aperta la finestra **Esplora test** che illustra che i test sono stati eseguiti correttamente. I tre test sono elencati nella sezione **Test superati** e nella sezione **Riepilogo** è riportato il risultato dell'esecuzione dei test.

   ![Finestra Esplora test](./media/testing-library-with-visual-studio/firsttest.png)

## <a name="handling-test-failures"></a>Gestione degli errori di test

L'esecuzione dei test non ha generato errori ma è opportuno apportare qualche modifica in modo che uno dei metodi di test abbia esito negativo:

1. Modificare la matrice `words` del metodo `TestDoesNotStartWithUpper` per includere la stringa "Error". Non è necessario salvare il file perché Visual Studio salva i file aperti automaticamente quando viene creata una soluzione per eseguire i test.

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. Eseguire il test selezionando **Test** > **Esegui** > **Tutti i test** dalla barra dei menu. La finestra **Esplora test** indica che due test hanno avuto esito positivo e uno esito negativo.

   ![Finestra Esplora test](./media/testing-library-with-visual-studio/failedtest.png)

1. Scegliere il test che ha avuto esito negativo, `TestDoesNotStartWith`, nella sezione **Test non superati**. Nella finestra **Esplora test** viene visualizzato il messaggio generato dal metodo Assert: "Assert.IsFalse failed. Expected for 'Error': false; actual: True". A causa dell'errore, tutte le stringhe della matrice successive a "Error" non sono state testate.

   ![Finestra di Esplora test con l'errore del metodo Assert Is False](./media/testing-library-with-visual-studio/failedtestdetail.png)

1. Rimuovere il codice che è stato aggiunto (`"Error", `) e rieseguire il test. I test verranno superati.

## <a name="testing-the-release-version-of-the-library"></a>Test della versione di rilascio della libreria

I test sono stati eseguiti con la versione di debug della libreria. Dopo che tutti i test sono stati superati e la libreria è stata testata in modo adeguato, è necessario ripetere i test con la versione di rilascio della libreria stessa. Esistono infatti alcuni fattori, ad esempio le ottimizzazioni del compilatore, in grado di generare a volte comportamenti diversi tra la versione di debug e quella di rilascio.

Per testare la versione di rilascio, seguire questa procedura:

1. Nella barra degli strumenti di Visual Studio modificare la configurazione di compilazione da **Debug** a **Rilascio**.

   ![Barra degli strumenti di Visual Studio](./media/testing-library-with-visual-studio/toolbar.png)

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **StringLibrary** e selezionare **Compila** dal menu di scelta rapida per ricompilare la libreria.

   ![Menu di scelta rapida StringLibrary](./media/testing-library-with-visual-studio/buildlibrary.png)

1. Eseguire gli unit test selezionando **Test** > **Esegui** > **Tutti i test** dalla barra dei menu. I test avranno esito positivo.

Dopo aver completato le operazioni di test della libreria, il passaggio successivo consiste nel rendere quest'ultima disponibile ai chiamanti. È possibile aggregarla a una o più applicazioni oppure è possibile distribuirla come pacchetto NuGet. Per altre informazioni, vedere [Consuming a .NET Standard Class Library](./consuming-library-with-visual-studio.md) (Utilizzo di una libreria di classi .NET Standard).

