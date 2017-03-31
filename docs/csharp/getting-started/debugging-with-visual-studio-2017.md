---
title: Debug dell&quot;applicazione C# Hello World con Visual Studio 2017
description: Informazioni su come eseguire il debug di un&quot;applicazione Hello World scritta in C# con Visual Studio 2017
keywords: .NET Core, applicazione console .NET Core, debug .NET
author: stevehoag
ms.author: shoag
ms.date: 10/24/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: cb213625-cc60-438b-9b9e-49aed0e4a974
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6a6a461984c140d180cf70cd7a1a33818a40b451
ms.lasthandoff: 03/13/2017

---

# <a name="debugging-your-c-hello-world-application-with-visual-studio-2017"></a>Debug dell'applicazione C# Hello World con Visual Studio 2017 #

Finora è stata seguita la procedura descritta in [Creazione di un'applicazione C# Hello World con .NET Core in Visual Studio 2017](.\with-visual-studio-2017.md) per creare ed eseguire una semplice applicazione console. Dopo aver scritto e compilato un'applicazione, è possibile iniziare a testarla. Visual Studio include un set completo di strumenti di debug che è possibile usare durante il test e la risoluzione dei problemi dell'applicazione. Nel corso del debug dell'applicazione verranno presi in esame alcuni di questi strumenti.

## <a name="debugging-in-debug-mode"></a>Debug in modalità di debug ##

La modalità di debug è una delle due configurazioni di compilazione predefinite di Visual Studio. L'altra è la modalità di rilascio. La configurazione di compilazione corrente viene visualizzata sulla barra degli strumenti. La figura seguente mostra che l'applicazione verrà compilata in modalità di debug.

   ![Immagine](./media/debugmode.jpg)

È necessario iniziare sempre eseguendo il test del programma in modalità di debug. La modalità di debug disattiva la maggior parte delle ottimizzazioni del compilatore e offre informazioni più dettagliate nel file di database dei simboli (con estensione pdb) restituito dal processo di compilazione.

## <a name="setting-a-breakpoint"></a>Impostazione di un punto di interruzione ##

Verrà eseguito un programma in modalità di debug e verranno provate alcune funzionalità di debug:

1. Impostare un punto di interruzione posizionando il cursore sulla riga `Console.WriteLine("\nHello, {0}, on {1:d} at {1:t}", name, date);` e facendo clic sul margine sinistro della finestra del codice. In alternativa, scegliere la voce di menu **Debug**, **Imposta/Rimuovi punto di interruzione**. Un punto di interruzione arresta temporaneamente l'esecuzione dell'applicazione *prima* che venga eseguita la riga con il punto di interruzione. Come mostrato nella figura seguente, Visual Studio indica la riga in cui è impostato il punto di interruzione evidenziando tale riga e visualizzando un cerchio rosso sul margine sinistro della finestra.

   ![Immagine](./media/setbreakpoint_2017.jpg)

1. Eseguire il programma in modalità di debug scegliendo il pulsante "HelloWorld" con la freccia verde sulla barra degli strumenti, premendo F5 o scegliendo **Debug**, **Avvia debug**.

1. Quando il programma chiede di specificare un nome, immettere una stringa nella finestra della console e premere INVIO.

1. L'esecuzione del programma si arresta quando raggiunge il punto di interruzione e prima che il metodo `Console.WriteLine` venga eseguito. La schermata di Visual Studio dovrebbe essere simile alla figura seguente. Si noti che nella finestra **Auto** vengono visualizzati i valori delle variabili usate nella riga corrente. Nella finestra **Variabili locali** vengono visualizzati i valori delle variabili definite nel metodo attualmente in esecuzione.

   ![Immagine](./media/breakpoint_2017.jpg)

1. Di seguito verranno modificati i valori delle variabili per vedere in che modo tale operazione influisce sul programma. Se la **finestra di controllo immediato** non è visibile, visualizzarla scegliendo la voce di menu **Debug**, **Finestre**, **Controllo immediato**. La **finestra di controllo immediato** consente di interagire con l'applicazione in fase di debug.

1. È possibile modificare in modo interattivo i valori delle variabili. Immettere `name = "Yuma"` nella finestra di controllo immediato e premere INVIO.

1. Immettere `date = new DateTime(2016,11,01,11,59,00)` nella finestra di controllo immediato e premere INVIO.

   Nella **finestra di controllo immediato** viene visualizzata l'immagine seguente:

   ![Immagine](./media/immediatewindow.jpg)

   Si noti che nella finestra vengono visualizzati il valore della variabile string e le proprietà del valore @System.DateTime. Inoltre, il valore delle variabili viene aggiornato nelle finestre **Auto** e **Variabili locali**.

1. Continuare l'esecuzione del programma scegliendo il pulsante **Continua** sulla barra degli strumenti oppure scegliendo la voce di menu **Debug**, **Continua**. La finestra della console risultante dovrebbe essere simile all'immagine seguente. Si noti che anche i valori visualizzati nella finestra della console corrispondono alle modifiche apportate nella **finestra di controllo immediato**.

   ![Immagine](./media/changed.jpg)

1. Premere un tasto qualsiasi per chiudere l'applicazione e uscire dalla modalità di debug.

## <a name="setting-a-conditional-breakpoint"></a>Impostazione di un punto di interruzione condizionale ##

A questo punto è stato verificato che il programma visualizzerà correttamente la stringa immessa dall'utente. Ma cosa succede se l'utente non immette alcuna stringa? È possibile testare questa eventualità e usare nel processo un'altra funzionalità di debug, ovvero la possibilità di impostare un punto di interruzione condizionale.

Per impostare un punto di interruzione condizionale e verificare cosa succede quando l'utente non immette una stringa, seguire questa procedura:

1. Fare clic con il pulsante destro del mouse sul punto rosso che rappresenta il punto di interruzione. Scegliere **Condizioni** dal menu di scelta rapida per aprire la finestra di dialogo **Impostazioni del punto di interruzione** mostrata nella figura seguente.

   ![Immagine](./media/breakpoint_settings.jpg)

1. Nella casella di testo contenente "e.g. x == 5" immettere quanto segue:

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   Viene qui verificata una condizione di codice. È anche possibile specificare un numero di passaggi in modo da interrompere l'esecuzione del programma prima che un'istruzione venga eseguita un numero specificato di volte. In alternativa, è possibile specificare una condizione di filtro, in modo da interrompere l'esecuzione del programma sulla base di attributi quali l'identificatore di thread, il nome del processo e il nome del thread.

1. Scegliere il pulsante **Chiudi** per chiudere la finestra di dialogo.

1. Eseguire il programma in modalità di debug.

1. Nella finestra della console premere INVIO quando viene chiesto di immettere il proprio nome.

1. Poiché la condizione specificata è stata soddisfatta (`name` è `null` o [String.Empty](xref:System.String.Empty)), l'esecuzione del programma si interrompe quando raggiunge il punto di interruzione e prima che venga eseguito il metodo `Console.WriteLine`.

1. Scegliere la finestra **Variabili locali**, dove vengono visualizzati i valori delle variabili che sono locali rispetto al metodo attualmente in esecuzione, in questo caso il `Main`.

1. Si noti che il valore della variabile `name` è "" o [String.Empty](xref:System.String.Empty). Eseguire questa verifica immettendo l'istruzione seguente nella **finestra di controllo immediato**:

   ```csharp
   ? name == String.Empty
   ```

   La figura seguente ne illustra il risultato.

   ![Immagine](./media/emptystring.jpg)

1. Scegliere il pulsante **Continua** sulla barra degli strumenti per continuare l'esecuzione del programma.

1. Premere un tasto qualsiasi per chiudere la finestra della console e uscire dalla modalità di debug.

1. Rimuovere il punto di interruzione facendo clic sul punto sul margine sinistro della finestra del codice oppure scegliendo la voce di menu **Debug**, **Imposta/Rimuovi punto di interruzione**.

## <a name="stepping-through-a-program"></a>Esecuzione delle singole istruzioni di un programma ##

Visual Studio consente anche di esaminare il programma una riga alla volta e di monitorarne l'esecuzione. In genere si imposta un punto di interruzione e si usa questa funzionalità per seguire il flusso del programma, anche attraverso una piccola parte del codice. Dal momento che il programma è di piccole dimensioni, è possibile esaminarlo per intero seguendo questa procedura:

1. Nella barra dei menu scegliere **Debug**, **Esegui istruzione** oppure premere F11. Visual Studio evidenzia la riga successiva da eseguire e visualizza una freccia accanto alla riga, come mostrato nella figura seguente.

   ![Immagine](./media/step_into.jpg)

   A questo punto, nella finestra **Auto** viene indicato che il programma ha definito una sola variabile, `args`. Poiché al programma non è stato passato alcun argomento della riga di comando, il relativo valore è una matrice di stringhe vuota. Visual Studio, inoltre, ha aperto una finestra della console vuota.

1. Scegliere **Debug**, **Esegui istruzione** oppure premere F11. Visual Studio evidenzia ora la riga successiva da eseguire. Come mostrato nella figura, l'esecuzione del codice tra l'ultima istruzione e questa ha richiesto 3 millisecondi. `args` rimane l'unica variabile dichiarata e la finestra della console è ancora vuota.

   ![Immagine](./media/step_into_2.jpg)

1. Scegliere **Debug**, **Esegui istruzione** oppure premere F11. Visual Studio evidenzia l'istruzione che include l'assegnazione della variabile `name`. Nella finestra **Auto** viene mostrato che `name` è `null`, mentre nella finestra della console viene visualizzata la stringa "What is your name?".

1. Rispondere al prompt immettendo una stringa nella finestra della console e premendo INVIO. La console non risponde e la stringa immessa non viene visualizzata nella finestra della console. Il metodo [Console.ReadLine](xref:System.Console.ReadLine), tuttavia, acquisirà l'input.

1. Scegliere **Debug**, **Esegui istruzione** oppure premere F11. Visual Studio evidenzia l'istruzione che include l'assegnazione della variabile `date`. Nella finestra **Auto** vengono visualizzati il valore della proprietà [DateTime.Now](xref:System.DateTime.Now) e il valore restituito dalla chiamata al metodo [Console.ReadLine](xref:System.Console.ReadLine). Nella finestra della console viene visualizzata anche la stringa immessa quando la console ha richiesto un input.

1. Scegliere **Debug**, **Esegui istruzione** oppure premere F11. Nella finestra **Auto** viene ora visualizzato il valore della variabile `date` dopo l'assegnazione da parte della proprietà [DateTime.Now](xref:System.DateTime.Now). La finestra della console rimane invariata.

1. Scegliere **Debug**, **Esegui istruzione** oppure premere F11. Visual Studio chiama il metodo [Console.WriteLine](xref:System.Console.WriteLine(System.String,System.Object,System.Object)). I valori delle variabili `date` e `name` vengono visualizzati nella finestra **Auto**, mentre nella finestra della console viene visualizzata la stringa formattata.

1. Scegliere **Debug**, **Esci** oppure premere MAIUSC+F11. Questa operazione arresta l'esecuzione passo passo. La finestra della console visualizza un messaggio e attende che venga premuto un tasto.

1. Premere un tasto qualsiasi per chiudere la finestra della console e uscire dalla modalità di debug.

## <a name="building-a-release-version"></a>Compilazione di una versione di rilascio ##

Dopo aver testato la compilazione di debug dell'applicazione, è necessario anche compilare e testare la versione di rilascio. La versione di rilascio integra le ottimizzazioni del compilatore che possono talvolta influire sul comportamento di un'applicazione. Ad esempio, le ottimizzazioni del compilatore progettate per migliorare le prestazioni possono creare condizioni di competizione nelle applicazioni asincrone o multithreading.

Per compilare e testare la versione di rilascio dell'applicazione console, modificare la configurazione di compilazione nella barra degli strumenti da **Debug** in **Rilascio**, come mostrato nella figura seguente.

![Immagine](./media/release.jpg)

Quando si preme F5 o si sceglie **Compila soluzione** dal menu **Compila**, Visual Studio compila la versione di rilascio dell'applicazione console per consentirne il test. È possibile eseguire e testare questa versione in modo analogo alla versione di debug.

Dopo aver terminato il debug, il passo successivo consiste nel pubblicare una versione distribuibile dell'applicazione. Per informazioni su come eseguire questa operazione, vedere [Pubblicazione dell'applicazione Hello World con Visual Studio 2017](./publishing-with-visual-studio-2017.md).

