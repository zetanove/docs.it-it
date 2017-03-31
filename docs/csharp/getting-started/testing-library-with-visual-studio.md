---
title: Test di una libreria di classi con .NET Core in Visual Studio 2017
description: Informazioni su come testare una libreria di classi scritta in C# usando Visual Studio 2017
keywords: ".NET Core, libreria di classi .NET Standard, Visual Studio 2017 testing unità"
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 069ad711-3eaa-45c6-94d7-b40249cc8b99
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ee21799706b971f0ec13285b0771b32b4367f570
ms.lasthandoff: 03/13/2017

---

# <a name="testing-a-class-library-with-net-core-in-visual-studio-2017"></a>Test di una libreria di classi con .NET Core in Visual Studio 2017 #

Nell'argomento [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](library-with-visual-studio-2017.md) è stato illustrato come creare una semplice libreria di classi che aggiunge un metodo di estensione alla classe @System.String. Viene ora creato uno unit test per verificare che tale libreria funzioni nel modo previsto. Alla soluzione verrà aggiunto il progetto unit test creato nell'argomento precedente.

## <a name="creating-a-unit-test-project"></a>Creazione di un progetto unit test ##

Per creare un progetto unit test, seguire questa procedura:

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo della soluzione **ClassLibraryProject** e scegliere **Aggiungi**, **Nuovo progetto**.

   <!-- Need a VS 2017 version  [!NOTE] In addition to a Unit Test project, you can also use Visual Studio to create an XUnit test project for .NET Core. For a walkthrough that includes an XUnit test project, see [Getting started with .NET Core on Windows, using Visual Studio 2015](../../core/tutorials/using-on-windows.md). --> 

1. Nella finestra di dialogo **Aggiungi nuovo progetto** espandere i nodi **Visual C#** e **.NET Core**, quindi scegliere il modello di progetto **Unit Test Project (.NET Core)** e denominarlo `StringLibraryTest`, come mostrato nella figura seguente.

   ![Immagine](./media/testproject.jpg)

1. Scegliere il pulsante **OK** per creare il progetto. Visual Studio crea il progetto e apre il file `UnitTest1.cs` nella finestra del codice, come mostrato nella figura seguente.

   ![Immagine](./media/unit_test_code_window.jpg)

   Il codice sorgente creato dal modello di unit test esegue le operazioni seguenti:

   - Importa lo spazio dei nomi [Microsoft.VisualStudio.TestTools.UnitTesting](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.aspx), contenente i tipi usati per il testing unità.

   - Applica l'attributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx) alla classe `UnitTest1`. Ogni metodo di test presente in una classe di test contrassegnata con l'attributo \[TestMethod\] verrà eseguito automaticamente durante l'esecuzione dello unit test.

   - Applica l'attributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) per definire `TestMethod1` come metodo di test da eseguire automaticamente durante l'esecuzione dello unit test.

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Dipendenze** del progetto **StringLibraryTest** e scegliere **Aggiungi riferimento**. Verrà aggiunto un riferimento al progetto di libreria di classi `StringLibrary`. 

1. Nella finestra di dialogo **Gestione riferimenti** espandere il nodo **Progetti**, scegliere **Soluzione** e quindi fare clic sulla casella accanto a **StringLibrary**, come mostrato nella figura seguente. L'aggiunta di un riferimento all'assembly `StringLibrary` consente al compilatore di risolvere le chiamate ai metodi **StringLibrary**.

   ![Immagine](./media/add_reference.jpg)

1. Scegliere il pulsante **OK** per chiudere la finestra di dialogo **Gestione riferimenti**.

## <a name="adding-and-running-unit-test-methods"></a>Aggiunta ed esecuzione di metodi unit test ##

Quando Visual Studio esegue uno unit test, esegue ciascun metodo contrassegnato con l'attributo [\[TestMethod\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testmethodattribute.aspx) in una classe unit test, ovvero la classe a cui è applicato l'attributo [\[TestClass\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.testclassattribute.aspx). Un metodo di test termina quando viene rilevato il primo errore o quando tutti i test contenuti nel metodo stesso hanno avuto esito positivo.

I test più comuni chiamano i membri della classe [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx). Molti metodi assert includono almeno due parametri, uno dei quali corrisponde al risultato previsto del test, mentre l'altro corrisponde al risultato effettivo. Di seguito sono riportati alcuni dei metodi chiamati con maggiore frequenza:

- `Assert.AreEqual`: verifica che due oggetti o valori siano uguali. Il metodo ha esito negativo se gli oggetti o i valori non sono uguali.

- `Assert.AreSame`: verifica che due variabili oggetto facciano riferimento allo stesso oggetto. Il metodo ha esito negativo se le variabili fanno riferimento a oggetti diversi.

- `Assert.IsFalse`: verifica che una condizione sia False. Il metodo ha esito negativo se la condizione è True.

- `Assert.IsNotNull`: verifica che un oggetto non sia `null`. Il metodo ha esito negativo se l'oggetto è `null`.

È inoltre possibile usare l'attributo [\[ExpectedException\]](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.expectedexceptionattribute.aspx) per indicare il tipo di eccezione che si prevede verrà generata dal metodo di test. Questo attributo viene usato per testare le condizioni in grado di generare un'eccezione. Il test ha esito negativo se l'eccezione specificata non viene generata.

Durante il test del metodo `StringLibrary.StartsWithUpper`, si vogliono fornire alcune stringhe che iniziano con un carattere maiuscolo. Si prevede che in questi casi il metodo restituisca `True`. È pertanto possibile chiamare il metodo [Assert.IsTrue(Boolean, String)](https://msdn.microsoft.com/library/ms243754.aspx). Analogamente, si vogliono fornire alcune stringhe che iniziano con un valore diverso da un carattere maiuscolo. Si prevede che in questi casi il metodo restituisca False. È pertanto possibile chiamare il metodo [Assert.IsFalse(Boolean, String)](https://msdn.microsoft.com/library/ms243805.aspx).

Poiché il metodo della libreria gestisce le stringhe, si vuole anche verificare che gestisca in modo corretto una [stringa vuota](xref:System.String.Empty), ovvero una stringa senza caratteri e con @System.String.Length uguale a 0, e una stringa `null`, ovvero una stringa non inizializzata. Se `StartsWithUpper` è chiamato come metodo di estensione su un'istanza di @System.String, non può essere passato a una stringa `null`. È tuttavia possibile chiamarlo direttamente come metodo statico e passarlo a un singolo argomento @System.String.

Verranno definiti tre metodi, ciascuno dei quali chiama più volte il relativo metodo [Assert](https://msdn.microsoft.com/library/microsoft.visualstudio.testtools.unittesting.assert.aspx) per ciascun elemento di una matrice di stringhe. Poiché il metodo di test ha esito negativo quando incontra il primo errore, verrà chiamato un overload del metodo che consente di passare una stringa in cui è indicato il valore stringa usato nella chiamata al metodo.

Per creare i metodi di test, seguire questa procedura:

1. Sostituire il codice nella finestra con il codice seguente:

   [!CODE-csharp[Test#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/testlib1.cs#1)]

   Si noti che nel metodo `TestStartsWithUpper` il test dei caratteri maiuscoli include la lettera alfa maiuscola dell'alfabeto greco (U+0391) e la lettera EM maiuscola dell'alfabeto cirillico (U+041C). Si noti inoltre che nel metodo `TestDoesNotStartWithUpper` il test dei caratteri minuscoli include la lettera alfa minuscola dell'alfabeto greco (U+03B1) e la lettera Ghe minuscola dell'alfabeto cirillico (U+0433).

1. Nella barra dei menu scegliere **File**, **Salva UnitTest1.cs con nome**. Nella finestra di dialogo **Salva con nome** scegliere la freccia accanto al pulsante **Salva** e quindi scegliere **Salva con codifica***.

1. Nella finestra di dialogo Conferma salvataggio scegliere il pulsante **Sì** per salvare il file.

1. Dall'elenco a discesa **Codifica** disponibile nella finestra di dialogo **Opzioni di salvataggio avanzate** selezionare **Unicode (UTF-8 con firma digitale) - Tabella codici 65001** e quindi scegliere **OK**.

   Se il salvataggio del codice sorgente come file con codifica UTF8 ha esito negativo, Visual Studio può salvarlo come file ASCII. In questo caso, il runtime non decodificherà in modo accurato i caratteri non compresi nell'intervallo ASCII e i risultati del test non saranno precisi.

1. Nella barra dei menu scegliere **Test**, **Esegui**, **Tutti i test**. Verrà visualizzata la finestra **Esplora test** in cui è indicato che entrambi i test sono stati eseguiti correttamente, come mostrato nella figura seguente. Si noti che i tre test sono elencati nella sezione **Test superati** e che nella sezione **Riepilogo** è riportato il risultato dell'esecuzione dei test.

   ![Immagine](./media/first_test.jpg)

## <a name="handling-test-failures"></a>Gestione degli errori di test ##

L'esecuzione dei test non ha generato errori. È quindi necessario apportare qualche modifica in modo che uno dei metodi di test abbia esito negativo:

1. Modificare la matrice `words` del metodo `TestDoesNotStartWithUpper` in modo che includa la stringa "Error". L'istruzione è quindi simile a quanto riportato di seguito:

   ```csharp
   string[] words = { "alphabet", "Error", "zebra", "abc", "αυτοκινητοβιομηχανία", "государство",
                      "1234", ".", ";", " " };
   ```

1. Eseguire il test scegliendo **Test**, **Esegui**, **Tutti i test**. Nella finestra **Esplora test** viene ora indicato che due test sono stati superati e che uno ha avuto esito negativo, come mostrato nella figura seguente.

   ![Immagine](./media/failed_test.jpg)

1. Scegliere il test che ha avuto esito negativo, `TestDoesNotStartWith`, nella sezione **Test non superati**. Nel riquadro inferiore della finestra **Esplora test** viene visualizzato il messaggio generato dal metodo assert: "Assert.IsFalse failed. Expected for 'Error': false; actual: True", come mostrato nello snapshot di **Esplora test** riportato di seguito. A causa dell'errore, tutte le stringhe della matrice successive a "Error" non sono state testate.

   ![Immagine](./media/failed_test2.jpg)

1. Rimuovere il codice che è stato aggiunto (`"Error", `) e rieseguire il test. A questo punto il test avrà esito positivo.

## <a name="testing-the-release-version-of-the-library"></a>Test della versione di rilascio della libreria ##

I test sono stati eseguiti con la versione di debug della libreria. Dopo che tutti i test sono stati superati e la libreria è stata testata in modo adeguato, è necessario ripetere i test con la versione di rilascio della libreria stessa. Esistono infatti alcuni fattori, ad esempio le ottimizzazioni del compilatore, in grado di generare a volte comportamenti diversi tra la versione di debug e quella di rilascio.

Per testare la versione di rilascio, seguire questa procedura:

1. Nella barra degli strumenti di Visual Studio modificare la configurazione di compilazione da **Debug** a **Rilascio**. Nella figura seguente viene mostrata una parte della barra degli strumenti.

   ![Immagine](./media/lib_release.jpg)

1. In **Esplora soluzioni** aprire il menu di scelta rapida per il nodo del progetto **StringLibrary** e scegliere **Compila** per ricompilare la libreria.

1. Eseguire nuovamente gli unit test scegliendo **Test**, **Esegui**, **Tutti i test** dal menu di Visual Studio. I test avranno tutti esito positivo.

Dopo aver completato le operazioni di test della libreria, il passaggio successivo consiste nel rendere quest'ultima disponibile ai chiamanti. È possibile aggregarla a una o più applicazioni oppure è possibile distribuirla come pacchetto NuGet. Per informazioni su come eseguire questa operazione, vedere [Consuming a .NET Standard Class Library](./consuming-library-with-visual-studio-2017.md) (Utilizzo di una libreria di classi .NET Standard).

