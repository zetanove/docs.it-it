---
title: Utilizzo di una libreria di classi con .NET Core in Visual Studio 2017
description: Informazioni su come chiamare i membri di una libreria di classi con Visual Studio 2017.
keywords: .NET Core, libreria di classi .NET Core, .NET Standard, distribuzione della libreria di classi .NET Standard
author: BillWagner
ms.author: wiwang
ms.date: 04/17/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: d7b94076-1108-4174-94e7-a18f00072bb7
ms.translationtype: Human Translation
ms.sourcegitcommit: 39e8e757a446b30ab18914465853138e1c239e40
ms.openlocfilehash: d980ae6c3c2f903dcabf18b26670c18fa9a49f22
ms.contentlocale: it-it
ms.lasthandoff: 05/03/2017

---

# <a name="consuming-a-class-library-with-net-core-in-visual-studio-2017"></a>Utilizzo di una libreria di classi con .NET Core in Visual Studio 2017

Dopo aver seguito le procedure descritte negli articoli [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](./library-with-visual-studio.md) e [Test di una libreria di classi con .NET Core in Visual Studio 2017](testing-library-with-visual-studio.md) per compilare e testare la libreria di classi e dopo aver compilato una versione di rilascio della libreria, il passaggio successivo consiste nel rendere tale libreria disponibile ai chiamanti. Questa operazione può essere eseguita in due modi diversi:

* Se la libreria verrà usata da una sola soluzione, ad esempio se è un componente di un'unica applicazione di grandi dimensioni, è possibile includerla come progetto all'interno della soluzione.

* Se la libreria sarà accessibile a livello generale, è possibile distribuirla come pacchetto NuGet.

## <a name="including-a-library-as-a-project-in-a-solution"></a>Inclusione di una libreria in una soluzione come progetto

È possibile includere l'applicazione come parte della soluzione, allo stesso modo in cui sono stati inclusi unit test nella soluzione della libreria di classi. Ad esempio, è possibile usare la libreria di classi in un'applicazione console che chiede all'utente di immettere una stringa e segnala se il primo carattere è in maiuscolo:

1. Aprire la soluzione `ClassLibraryProjects` creata in [Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017](./library-with-visual-studio.md). In **Esplora soluzioni**, fare clic con il pulsante destro del mouse sulla soluzione **ClassLibraryProjects** e scegliere **Aggiungi** > **Nuovo progetto** dal menu di scelta rapida.

1. Nella finestra di dialogo **Aggiungi nuovo progetto** selezionare il nodo **.NET Core** seguito dal modello di progetto **App console (.NET Core)**. Nella casella di testo **Nome**, digitare "ShowCase", quindi selezionare il pulsante **OK**.

   ![Finestra di dialogo Aggiungi nuovo progetto](./media/consuming-library-with-visual-studio/addnewproject.png)

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **ShowCase** e selezionare **Imposta come progetto di avvio** nel menu di scelta rapida.

   ![Menu di scelta rapida di ShowCase](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. All'inizio il progetto non ha accesso alla libreria di classi. Per consentire al progetto di chiamare metodi della libreria di classi, si crea un riferimento alla libreria di classi. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo **Dipendenze** del progetto `ShowCase` e selezionare **Aggiungi riferimento**.

   ![Menu di scelta rapida Dipendenze di ShowCase](./media/consuming-library-with-visual-studio/addreference.png)

1. Nella finestra di dialogo **Gestione riferimenti** selezionare **StringLibrary**, il progetto della libreria di classi e fare clic su **OK**.

   ![Gestione riferimenti](./media/consuming-library-with-visual-studio/referencemanager.png)

1. Nella finestra del codice del file *Program.cs* sostituire tutto il codice con il codice seguente:

 [!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs#1)]

   Il codice usa la proprietà [Console.WindowHeight](xref:System.Console.WindowHeight) per determinare il numero di righe della finestra della console. Quando il valore della proprietà [Console.CursorTop](xref:System.Console.CursorTop) è maggiore o uguale al numero di righe della finestra della console, il codice cancella la finestra e visualizza un messaggio.

   Il programma richiede all'utente di immettere una stringa. Indica se la stringa inizia con un carattere maiuscolo. Se l'utente preme INVIO senza immettere una stringa, l'applicazione viene terminata e la finestra della console viene chiusa.

1. Se necessario, modificare la barra degli strumenti per compilare la versione di **debug** del progetto `ShowCase`. Compilare ed eseguire il programma selezionando la freccia verde nel pulsante **ShowCase**.

   ![Immagine](./media/consuming-library-with-visual-studio/toolbar.png)

È possibile eseguire il debug e pubblicare l'applicazione che usa questa libreria seguendo i passaggi illustrati in [Debugging your C# Hello World application with Visual Studio 2017](debugging-with-visual-studio.md) (Esecuzione del debug dell'applicazione C# Hello World con Visual Studio 2017) e [Publishing your Hello World Application with Visual Studio 2017](publishing-with-visual-studio.md) (Pubblicazione dell'applicazione Hello World con Visual Studio 2017).

## <a name="distributing-the-library-in-a-nuget-package"></a>Distribuzione della libreria in un pacchetto NuGet

Per rendere la libreria di classi disponibile sul Web, è possibile pubblicarla come pacchetto NuGet. Visual Studio non supporta la creazione di pacchetti NuGet. Per creare un pacchetto, usare l'[utilità della riga di comando `dotnet`](../../core/tools/dotnet.md):

1. Aprire una finestra della console. Ad esempio, nella casella di testo **Chiedimi qualcosa** della barra delle applicazioni di Windows immettere `Command Prompt`, o `cmd` per maggiore brevità, e aprire una finestra della console selezionando l'app desktop **Prompt dei comandi** o premendo INVIO se è selezionata nei risultati della ricerca.

1. Passare alla directory del progetto della libreria. A meno che non sia stato riconfigurato il percorso tipico dei file, si tratta della directory *Documenti\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary*. La directory contiene il codice sorgente e un file di progetto, *StringLibrary.csproj*.

1. Eseguire il comando `dotnet pack --no-build`. L'utilità `dotnet` genera un pacchetto con estensione *nupkg*.

   > [!TIP]
   > Se la directory che contiene *dotnet.exe* non si trova nel percorso indicato, è possibile individuarne il percorso immettendo `where dotnet.exe` nella finestra della console.

Per altre informazioni sulla creazione di pacchetti NuGet, vedere [Come creare un pacchetto NuGet con strumenti multipiattaforma](../../core/deploying/creating-nuget-packages.md).

