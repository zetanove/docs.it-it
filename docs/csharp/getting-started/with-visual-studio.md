---
title: Creazione di un&quot;applicazione C# Hello World con .NET Core in Visual Studio 2017
description: Informazioni su come creare una semplice applicazione console .NET Core usando Visual Studio 2017.
keywords: .NET Core, applicazione console .NET Core, Visual Studio 2017
author: BillWagner
ms.author: wiwagn
ms.date: 05/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 97aa50bf-bdf8-416d-a56c-ac77504c14ea
ms.translationtype: Human Translation
ms.sourcegitcommit: 6edd52bc56a03138fe16048fa06cad00a2af4847
ms.openlocfilehash: b19bf07b2a2bba944bb33ddb1c887f77331ba8d1
ms.contentlocale: it-it
ms.lasthandoff: 05/16/2017

---

# <a name="building-a-c-hello-world-application-with-net-core-in-visual-studio-2017"></a>Creazione di un'applicazione C# Hello World con .NET Core in Visual Studio 2017

Questo argomento offre un'introduzione dettagliata per la creazione, il debug e la pubblicazione di una semplice applicazione console .NET Core usando Visual Studio 2017. Visual Studio 2017 offre un ambiente di sviluppo completo per la creazione di applicazioni .NET Core. Se l'applicazione non ha alcuna dipendenza specifica della piattaforma, è possibile eseguirla su qualsiasi piattaforma usata come destinazione da .NET Core o su qualsiasi sistema in cui è installato .NET Core.

## <a name="prerequisites"></a>Prerequisiti

[Visual Studio 2017](https://www.visualstudio.com/downloads/) con il carico di lavoro "Sviluppo multipiattaforma .NET Core" installato. 

Per altre informazioni, vedere [Prerequisiti per .NET Core in Windows](../../core/windows-prerequisites.md).

## <a name="a-simple-hello-world-application"></a>Semplice applicazione Hello World

Di seguito viene descritta la creazione di una semplice applicazione console "Hello World". Attenersi ai passaggi riportati di seguito.

1. Avviare Visual Studio 2017. Selezionare **File** > **Nuovo** > **Progetto** dalla barra dei menu. Nella finestra di dialogo **Aggiungi nuovo progetto** selezionare il nodo **.NET Core** seguito dal modello di progetto **App console (.NET Core)**. Nella casella di testo **Nome** digitare "HelloWorld". Selezionare il pulsante **OK** .

   ![Finestra di dialogo Nuovo progetto con App console selezionata](./media/with-visual-studio/newproject.png)
   
1. Viene caricato l'ambiente di sviluppo. Il modello C# Console Application per .NET Core definisce automaticamente una classe, `Program`, con un singolo metodo, `Main`, che accetta una matrice <xref:System.String> come argomento. `Main` è il punto di ingresso dell'applicazione, ovvero il metodo chiamato automaticamente dal runtime quando viene avviata l'applicazione. Gli argomenti della riga di comando forniti all'avvio dell'applicazione sono disponibili nella matrice *args*.

   ![Visual Studio e il nuovo progetto HelloWorld](./media/with-visual-studio/devenv.png)

   Il modello crea una semplice applicazione "Hello World". Chiama il metodo <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> per visualizzare la stringa letterale "Hello World!" nella finestra della console. Facendo clic sul pulsante **HelloWorld** con la freccia verde sulla barra degli strumenti è possibile eseguire il programma in modalità debug. Se si esegue questa operazione, la finestra della console rimane visibile solo per un intervallo di tempo molto breve. Questo si verifica perché il metodo `Main` termina e l'applicazione viene chiusa non appena viene eseguita l'unica istruzione del metodo `Main`.

1. Per impostare l'applicazione in modo che sospenda la finestra della console prima di chiuderla, aggiungere il codice seguente immediatamente dopo la chiamata al metodo <xref:System.Console.WriteLine(System.String)?displayProperty=fullName>:

   ```csharp
   Console.Write("Press any key to continue...");
   Console.ReadKey(true);
   ```
   Il codice chiede all'utente di premere un tasto qualsiasi e quindi sospende il programma fino a quando non viene premuto un tasto.

1. Nella barra dei menu selezionare **Compila** > **Compila soluzione**. Il programma viene compilato in un linguaggio intermedio (IL) che viene successivamente convertito in codice binario da un compilatore JIT (Just-In-Time).

1. Eseguire il programma facendo clic sul pulsante **HelloWorld** con la freccia verde sulla barra degli strumenti.

   ![Finestra della console con il messaggio Hello World che chiede di premere un tasto qualsiasi per continuare](./media/with-visual-studio/helloworld1.png)

1. Premere un tasto qualsiasi per chiudere la finestra della console.

## <a name="enhancing-the-hello-world-application"></a>Miglioramento dell'applicazione Hello World

Migliorare l'applicazione per richiedere il nome dell'utente e visualizzarlo insieme alla data e ora. Per modificare e testare il programma, seguire questa procedura:

1. Immettere il codice C# seguente nella finestra del codice immediatamente dopo la parentesi quadra di apertura che segue la riga `public static void Main(string[] args)` e prima della prima parentesi quadra di chiusura:

   [!code-csharp[GettingStarted#1](../../../samples/snippets/csharp/getting_started/with_visual_studio/helloworld.cs#1)]

   ![File C# programma Visual Studio con il metodo Main aggiornato](./media/with-visual-studio/codewindow.png)

   Il codice visualizza "What is your name?" nella console e attende che l'utente inserisca una stringa e prema INVIO. Archivia la stringa in una variabile denominata `name`. Recupera inoltre il valore della proprietà <xref:System.DateTime.Now?displayProperty=fullName>, contenente l'ora locale corrente, e lo assegna a una variabile denominata `date`. Usa infine una [stringa in formato composito](../../standard/base-types/composite-format.md) per visualizzare questi valori nella finestra della console.

1. Compilare il programma scegliendo **Compila** > **Compila soluzione**.

1. Eseguire il programma in modalità debug in Visual Studio selezionando la freccia verde sulla barra degli strumenti, premendo F5 oppure scegliendo la voce di menu **Debug** > **Avvia debug**. Rispondere alla richiesta immettendo un nome e premendo il tasto INVIO.

   ![Finestra della console con output del programma modificato](./media/with-visual-studio/helloworld2.png)

1. Premere un tasto qualsiasi per chiudere la finestra della console.

L'applicazione è stata creata ed eseguita. Per sviluppare un'applicazione professionale, eseguire alcuni passaggi aggiuntivi per rendere un'applicazione pronta per il rilascio:

- Per altre informazioni sul debug dell'applicazione, vedere [Debug dell'applicazione C# Hello World con Visual Studio 2017](debugging-with-visual-studio.md).

- Per informazioni sullo sviluppo e la pubblicazione di una versione distribuibile dell'applicazione, vedere [Pubblicazione dell'applicazione Hello World con Visual Studio 2017](publishing-with-visual-studio.md).

## <a name="related-topics"></a>Argomenti correlati

Anziché un'applicazione console, è possibile creare una libreria di classi con .NET Core e Visual Studio 2017. Per un'introduzione dettagliata, vedere [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](library-with-visual-studio.md).

È anche possibile sviluppare un'app console .NET Core in Mac, Linux e Windows usando [Visual Studio Code](https://code.visualstudio.com/), un editor di codice scaricabile gratuitamente. Per un'esercitazione dettagliata, vedere [Introduzione a Visual Studio Code](with-visual-studio-code.md).

