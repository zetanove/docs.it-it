---
title: Utilizzo di una libreria di classi con .NET Core in Visual Studio 2017
description: Informazioni su come chiamare i membri di una libreria di classi con Visual Studio 2017
keywords: .NET Core, libreria di classi .NET Core, .NET Standard, distribuzione della libreria di classi .NET Standard
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: d7b94076-1108-4174-94e7-a18f00072bb7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0b42eeb0149feec09ddacba98383da3abd53bb5e
ms.lasthandoff: 03/13/2017

---

# <a name="consuming-a-class-library-with-net-core-in-visual-studio-2017"></a>Utilizzo di una libreria di classi con .NET Core in Visual Studio 2017 #

Dopo aver seguito le procedure descritte negli articoli [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](./library-with-visual-studio-2017.md) e [Test di una libreria di classi con .NET Core in Visual Studio 2017](testing-library-with-visual-studio.md) per compilare e testare la libreria di classi e dopo aver compilato una versione di rilascio della libreria, il passaggio successivo consiste nel rendere tale libreria disponibile ai chiamanti. Questa operazione può essere eseguita in due modi diversi:

- Se la libreria verrà usata da una sola soluzione, ad esempio se è un componente di un'unica applicazione di grandi dimensioni, è possibile includerla semplicemente come progetto all'interno della soluzione.

- Se la libreria sarà accessibile a livello generale, è possibile distribuirla come pacchetto NuGet.

## <a name="including-a-library-as-a-project-in-a-solution"></a>Inclusione di una libreria in una soluzione come progetto ##

Così come sono stati inclusi unit test nella stessa soluzione della libreria di classi, è possibile includere l'applicazione come parte di tale soluzione. Si supponga, ad esempio, di usare la libreria di classi in un'applicazione console che chiede all'utente di immettere una stringa e segnala se il primo carattere è in maiuscolo:

1. Aprire la soluzione `ClassLibraryProjects` creata nell'argomento [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](./library-with-visual-studio-2017.md) e, in Esplora soluzioni, aprire il menu di scelta rapida per il nodo **ClassLibraryProjects** e scegliere **Aggiungi**, **Nuovo progetto**.

1. Nella finestra di dialogo **Aggiungi nuovo progetto** espandere i nodi **Visual C#** e **.NET Core** e quindi scegliere il modello di progetto **Console App (.NET Core)** (App console (.NET Core)), come mostrato nella figura seguente.

   ![Immagine](./media/use-library.jpg)

1. Nella casella di testo **Nome** immettere `ShowCase` e quindi scegliere il pulsante **OK**.

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo del progetto **ShowCase** e scegliere **Imposta come progetto di avvio**.

1. Inizialmente il progetto non ha accesso alla libreria di classi. Per consentire al progetto di chiamare metodi nella libreria di classi, in **Esplora soluzioni** aprire il menu di scelta rapida per il nodo **Dependencies** del progetto **ShowCase** e scegliere **Aggiungi riferimento**.

1. Nella finestra di dialogo **Gestione riferimenti** scegliere **StringLibrary**, il progetto della libreria di classi, come mostrato nella figura seguente e quindi scegliere il pulsante **OK**.

   ![Immagine](./media/add-lib-ref.jpg)

1. Nella finestra del codice relativa al file "program.cs" sostituire il codice con quanto riportato di seguito:

 [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs#1)]

   Il codice usa la proprietà [Console.WindowHeight](xref:System.Console.WindowHeight) per determinare il numero di righe della finestra della console. Quando la proprietà [Console.CursorTop](xref:System.Console.CursorTop) è maggiore o uguale al numero totale di righe della finestra della console, il codice cancella tale finestra e visualizza di nuovo un messaggio.

   Il programma richiede all'utente di immettere una stringa e quindi indica se la stringa inizia con un carattere maiuscolo. Se l'utente preme **INVIO** senza immettere una stringa, la finestra della console viene chiusa e l'applicazione viene terminata.

1. Se necessario, modificare la barra degli strumenti per compilare la versione di **debug** del progetto `ShowCase`, come mostrato nella figura seguente.

   ![Immagine](./media/showcase-toolbar.jpg)

1. Compilare ed eseguire il programma facendo clic sulla freccia verde sul pulsante **ShowCase**.

È possibile eseguire il debug dell'applicazione che usa la libreria e quindi pubblicarla seguendo le procedure descritte in [Debug dell'applicazione C# Hello World con Visual Studio 2017](debugging-with-visual-studio-2017.md) e [Pubblicazione dell'applicazione Hello World con Visual Studio 2017](publishing-with-visual-studio-2017.md).

## <a name="distributing-the-library-in-a-nuget-package"></a>Distribuzione della libreria in un pacchetto NuGet ##

È possibile rendere la libreria di classi più ampiamente disponibile pubblicandola come pacchetto NuGet. Visual Studio non supporta la creazione di pacchetti NuGet. Per crearne uno, usare l'[utilità della riga di comando `dotnet.exe`](../../core/tools/dotnet.md) come indicato di seguito:

1. Aprire una finestra della console. Ad esempio, nella casella di testo **Chiedimi qualcosa** della barra delle applicazioni di Windows immettere `Command Prompt` e quindi scegliere l'app desktop **Prompt dei comandi** per aprire la finestra della console.

1. Passare alla directory del progetto della libreria. In genere, a meno che non sia stato riconfigurato il percorso del file, si tratta della directory `Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary`. La directory contiene il codice sorgente e un file di progetto, `StringLibrary.csproj`.

1. Eseguire il comando `dotnet.exe pack --no-build`. L'utilità `dotnet.exe` genera un pacchetto con estensione nupkg.

   > [!TIP]
   > Se la directory che contiene `dotnet.exe` non si trova nel percorso indicato, è possibile individuarne la posizione immettendo `where dotnet.exe` nella finestra della console.

Per altre informazioni sulla creazione di pacchetti NuGet, vedere [Come creare un pacchetto NuGet con strumenti multipiattaforma](../../core/deploying/creating-nuget-packages.md).
