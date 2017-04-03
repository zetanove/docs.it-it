---
title: Creazione di un&quot;applicazione C# Hello World con .NET Core in Visual Studio 2017
description: Informazioni su come creare una semplice applicazione console .NET Core usando Visual Studio 2017.
keywords: .NET Core, applicazione console .NET Core, Visual Studio 2017
author: stevehoag
ms.author: shoag
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 97aa50bf-bdf8-416d-a56c-ac77504c14ea
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f1a20f399b4ab34986d700622ff3bf3859b001bd
ms.lasthandoff: 03/13/2017

---

# <a name="building-a-c-hello-world-application-with-net-core-in-visual-studio-2017"></a>Creazione di un'applicazione C# Hello World con .NET Core in Visual Studio 2017 #

Questo argomento offre un'introduzione dettagliata per la creazione, il debug e la pubblicazione di una semplice applicazione console .NET Core usando Visual Studio 2017. Visual Studio 2017 offre un ambiente di sviluppo completo per la creazione di applicazioni .NET Core. Se l'applicazione non ha alcuna dipendenza specifica della piattaforma, è possibile eseguirla su qualsiasi piattaforma usata come destinazione da .NET Core o su qualsiasi sistema in cui è installato .NET Core.

## <a name="prerequisites"></a>Prerequisiti ##

- [Visual Studio 2017](https://www.visualstudio.com/downloads/) con il carico di lavoro "Sviluppo multipiattaforma .NET Core" installato. 

Per altre informazioni, vedere la sezione [Visual Studio 2017](../../core/windows-prerequisites.md) dell'argomento Prerequisiti per .NET Core in Windows.

## <a name="a-simple-hello-world-application"></a>Semplice applicazione "Hello World" ##

Di seguito viene descritta la creazione di una semplice applicazione console "Hello World". Di seguito la procedura:

1. Avviare Visual Studio e scegliere **Nuovo** > **Progetto** dal menu **File**. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Visual C#** nel riquadro sinistro e quindi scegliere il nodo **.NET Core**.

2. Nel riquadro destro scegliere **Console App (.NET Core)** (App console (.NET Core)). Immettere il nome del progetto, `HelloWorld`, e verificare che la casella **Crea directory per soluzione** sia selezionata, come mostrato nella figura seguente.

   ![Screenshot che mostra la finestra di dialogo Nuovo progetto con App console selezionato](./media/with-visual-studio/vs_newproject.jpg)
   
3. Fare clic sul pulsante **OK**. Visual Studio visualizza l'ambiente di sviluppo con la finestra del codice, come mostrato nella figura seguente. Il modello C# Console Application per .NET Core definisce automaticamente una classe, `Program`, con un singolo metodo, `Main`, che accetta una matrice @System.String come argomento. `Main` è il punto di ingresso dell'applicazione, ovvero il metodo chiamato automaticamente dal runtime quando viene avviata l'applicazione. Gli argomenti della riga di comando forniti all'avvio dell'applicazione sono disponibili nella matrice *args*.

   ![Visual Studio e il nuovo progetto HelloWorld](./media/with-visual-studio/vs_devenv.jpg)

   Il modello crea un'applicazione "Hello World" molto semplice: chiama il metodo @System.Console.WriteLine(System.String) per visualizzare la stringa letterale "Hello World!" nella finestra della console. Facendo clic sul pulsante "HelloWorld" con la freccia verde sulla barra degli strumenti, è possibile eseguire il programma in modalità di debug. Se si esegue questa operazione, la finestra della console rimane visibile solo per un intervallo di tempo molto breve. Questo si verifica perché `Main` termina e l'applicazione viene chiusa non appena viene eseguita l'unica istruzione del metodo `Main`.

4. A questo punto è opportuno mettere in pausa l'applicazione prima che chiuda la finestra della console. Immediatamente dopo la chiamata al metodo @System.Console.WriteLine(System.String) aggiungere il codice seguente:

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```
   Il codice chiede all'utente di premere un tasto qualsiasi e quindi sospende il programma fino a quando non viene premuto un tasto.

5. Nella barra dei menu scegliere **Compila**, **Compila soluzione**. Il programma viene compilato in IL, un linguaggio intermedio che viene successivamente convertito in codice binario da un compilatore JIT (Just-In-Time).

6. Eseguire il programma facendo clic sul pulsante "HelloWorld" con la freccia verde sulla barra degli strumenti. Il risultato è illustrato nella figura seguente.

   ![Immagine](./media/with-visual-studio/simple_hello.jpg)

7. Premere un tasto qualsiasi per chiudere la finestra.

## <a name="enhancing-the-hello-world-application"></a>Miglioramento dell'applicazione "Hello World" ##

Di seguito viene descritto come migliorare l'applicazione in modo che chieda il nome dell'utente e quindi visualizzi tale nome, insieme alla data e all'ora, nella finestra della console. Per modificare e testare il programma, seguire questa procedura:

1. Immettere il codice C# seguente nella finestra del codice immediatamente dopo la parentesi quadra di apertura che segue la riga `public static void Main(string[] args)` e prima della prima parentesi quadra di chiusura.

   [!CODE [GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   La figura seguente mostra la finestra del codice risultante.

   ![Esecuzione del programma modificato](./media/with-visual-studio/codewindow.jpg)

   Il codice visualizza "What is your name?" nella console e attende che l'utente inserisca una stringa e prema INVIO. In codice archivia la stringa in una variabile denominata `name`. Recupera inoltre il valore della proprietà @System.DateTime.Now, contenente l'ora locale corrente, e lo assegna a una variabile denominata `date`. Usa quindi una [stringa in formato composito](../../standard/base-types/composite-format.md) per visualizzare questi valori nella console.

2. Compilare il programma scegliendo **Compila** > **Compila soluzione**. Il programma viene compilato in IL, un linguaggio intermedio che viene successivamente convertito in codice binario da un compilatore JIT (Just-In-Time).

3. Eseguire il programma in modalità di debug in Visual Studio selezionando la freccia verde sulla barra degli strumenti, premendo F5 oppure scegliendo la voce di menu**Debug** > **Avvia debug**. Dopo che l'utente ha risposto alle richieste immettendo un nome e premendo INVIO, la finestra della console avrà un aspetto simile al seguente:

   ![Esecuzione del programma modificato](./media/with-visual-studio/console.jpg)

4. Premere un tasto qualsiasi per chiudere la finestra della console. In questo modo la modalità di debug viene terminata.

A questo punto la semplice applicazione Hello World è stata creata ed eseguita. Per sviluppare un'applicazione professionale, esistono alcuni passaggi aggiuntivi che è possibile eseguire per rendere un'applicazione pronta per il rilascio:

- Per altre informazioni sul debug dell'applicazione, vedere [Debugging the Hello World Application](debugging-with-visual-studio-2017.md) (Debug dell'applicazione Hello World).

- Per informazioni sullo sviluppo e la pubblicazione di una versione distribuibile dell'applicazione, vedere [Pubblicazione dell'applicazione Hello World](publishing-with-visual-studio-2017.md).

## <a name="related-topics"></a>Argomenti correlati ##

Anziché un'applicazione console, è possibile creare una libreria di classi con .NET Core e Visual Studio 2017. Per un'introduzione dettagliata, vedere [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](library-with-visual-studio-2017.md).

È anche possibile sviluppare un'app console .NET Core in Mac, Linux e Windows usando Visual Studio Code, un editor di codice scaricabile gratuitamente. Per un'esercitazione dettagliata, vedere [Introduzione a Visual Studio Code](with-visual-studio-code.md).

