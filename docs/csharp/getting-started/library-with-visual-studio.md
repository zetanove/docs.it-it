---
title: Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017
description: Informazioni su come creare una libreria di classi scritta in C# usando Visual Studio 2017
keywords: .NET Core, libreria di classi .NET Standard, Visual Studio 2017
author: BillWagner
ms.author: wiwagn
ms.date: 04/17/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: c849ca26-6a25-4d35-9544-f343af88e0e7
ms.translationtype: Human Translation
ms.sourcegitcommit: 39e8e757a446b30ab18914465853138e1c239e40
ms.openlocfilehash: 1ecccb03bc28da51a580b790b5ba8dd594bb7f18
ms.contentlocale: it-it
ms.lasthandoff: 05/03/2017

---

# <a name="building-a-class-library-with-c-and-net-core-in-visual-studio-2017"></a>Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017

La *libreria di classi* definisce tipi e metodi chiamati da un'applicazione. Una libreria di classi sviluppata usando .NET Core supporta la libreria .NET Standard, che consente di chiamare la libreria dell'utente da qualsiasi piattaforma .NET che supporti tale versione della libreria .NET Standard. Dopo aver completato la libreria di classi, è possibile decidere se si vuole distribuirla come componente di terze parti o se si vuole includerla come componente in bundle con una o più applicazioni.

> [!NOTE]
> Per un elenco delle versioni di .NET Standard e delle piattaforme supportate, vedere [Libreria .NET Standard](../../standard/library.md).

In questo argomento si creerà una semplice libreria di utilità contenente un solo metodo di gestione delle stringhe, che verrà implementato come [metodo di estensione](../../csharp/programming-guide/classes-and-structs/extension-methods.md), in modo da poter essere chiamato come se fosse un membro della classe @System.String.

## <a name="creating-a-class-library-solution"></a>Creazione di una soluzione per la libreria di classi

Iniziare creando una soluzione per il progetto di libreria di classi e per i progetti correlati. Una soluzione Visual Studio funge solo da contenitore per uno o più progetti. Per creare la soluzione:

1. Nella barra dei menu di Visual Studio scegliere **File** > **Nuovo** > **Progetto**.

1. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Altri tipi di progetti** e selezionare **Soluzioni di Visual Studio**. Assegnare alla soluzione il nome "ClassLibraryProjects" e selezionare il pulsante **OK**.

   ![Finestra di dialogo Nuovo progetto](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a>Creazione del progetto di libreria di classi

Creare un progetto di libreria di classi:

1. In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file della soluzione **ClassLibraryProjects** e dal menu di scelta rapida selezionare **Aggiungi** > **Nuovo progetto**.

1. Nella finestra di dialogo **Aggiungi nuovo progetto** selezionare il nodo **.NET Core** seguito dal modello di progetto **Libreria di classi (.NET Core)**. Nella casella di testo **Nome** immettere "StringLibrary" come nome del progetto. Scegliere **OK** per creare il progetto di libreria di classi.

   ![Finestra di dialogo Aggiungi nuovo progetto](./media/library-with-visual-studio/libproject.png)

   ![Finestra dell'applicazione di Visual Studio che illustra il codice del modello della libreria di classi predefinito](./media/library-with-visual-studio/stringlibrary.png)

1. Nella finestra del codice sostituire il codice con il seguente:

   [!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs#1)]

   La libreria di classi `UtilityLibraries.StringLibrary` contiene un metodo denominato `StartsWithUpper`, che restituisce un valore @System.Boolean che indica se l'istanza della stringa corrente inizia con un carattere maiuscolo. Lo standard Unicode distingue i caratteri maiuscoli dai minuscoli. In .NET Core il metodo [`Char.IsUpper`](xref:System.Char.IsUpper(System.Char)) restituisce `true` se un carattere è maiuscolo.

1. Nella barra dei menu selezionare **Compila** > **Compila soluzione**. Il progetto dovrebbe essere compilato senza errori.

   ![Riquadro di output che illustra che la compilazione ha avuto esito positivo](./media/library-with-visual-studio/buildsucceeds.png)

## <a name="next-step"></a>Passaggio successivo

La compilazione della libreria è stata completata. Non è tuttavia possibile sapere se funziona come previsto poiché non è stato ancora chiamato uno dei metodi. Il passaggio successivo per lo sviluppo della libreria consiste nel testarla usando un [Progetto unit test di C#](testing-library-with-visual-studio.md).

