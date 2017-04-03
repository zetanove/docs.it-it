---
title: Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017
description: Informazioni su come creare una libreria di classi scritta in C# usando Visual Studio 2017
keywords: .NET Core, libreria di classi .NET Standard, Visual Studio 2017
author: stevehoag
ms.author: shoag
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: c849ca26-6a25-4d35-9544-f343af88e0e7
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 28fa60cdcf8e0056314af271208759eadd8503a5
ms.lasthandoff: 03/13/2017

---

# <a name="building-a-class-library-with-c-and-net-core-in-visual-studio-2017"></a>Creazione di una libreria di classi con C# e .NET Core in Visual Studio 2017 #

Una libreria di classi definisce i tipi e i metodi che possono essere chiamati da qualsiasi applicazione. Una libreria di classi sviluppata usando .NET Core supporta la libreria .NET Standard, che consente di chiamare la libreria dell'utente da qualsiasi piattaforma .NET che supporti tale versione della libreria .NET Standard. Dopo aver completato la libreria di classi, è possibile decidere se si vuole distribuirla come componente di terze parti o se si vuole includerla come componente in bundle con una o più applicazioni.

> [!NOTE]
> Per un elenco delle versioni di .NET Standard e delle piattaforme supportate, vedere [Libreria .NET Standard](../../standard/library.md).

In questo argomento si creerà una semplice libreria di utilità contenente un solo metodo di gestione delle stringhe, che verrà implementato come [metodo di estensione](../../csharp/programming-guide/classes-and-structs/extension-methods.md), in modo da poter essere chiamato come se fosse un membro della classe @System.String.

## <a name="creating-a-class-library-solution"></a>Creazione di una soluzione per la libreria di classi ##

Per iniziare, creare una soluzione per il progetto di libreria di classi e per i progetti correlati. Una soluzione Visual Studio funge solo da contenitore per uno o più progetti. Per creare la soluzione:

1. Nella barra dei menu di Visual Studio scegliere **File**, **Nuovo**, **Progetto**.

1. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Altri tipi di progetti** e scegliere **Soluzioni di Visual Studio**, come illustrato nella figura seguente.

   ![Immagine](./media/solution.jpg)

1. Assegnare alla soluzione il nome "ClassLibraryProjects" e fare clic sul pulsante **OK**. La figura seguente ne illustra il risultato.

   ![Immagine](./media/vs_with_solution.jpg)

## <a name="creating-the-class-library-project"></a>Creazione del progetto di libreria di classi ##

È ora possibile creare il progetto di libreria di classi:

1. In **Esplora soluzioni** aprire il menu contestuale per il nodo **ClassLibraryProjects** e scegliere **Aggiungi**, **Nuovo progetto**.

1. Nella finestra di dialogo **Aggiungi nuovo progetto** scegliere il nodo **.NET Core**, quindi il modello di progetto **Class Library (.NET Standard)** (Libreria di classi (.NET Standard)).

1. Nella casella di testo **Nome** immettere "StringLibrary" come nome del progetto, come illustrato nella figura seguente.

   ![Immagine](./media/lib_project.jpg)

1. Scegliere **OK** per creare il progetto di libreria di classi. La figura seguente ne illustra il risultato.

   ![Immagine](./media/class_library.jpg)

1. Sostituire il codice nella finestra con il codice seguente:

   [!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs#1)]

   La libreria di classi `UtilityLibraries.StringLibrary` contiene un metodo denominato `StartsWithUpper`, che restituisce un valore @System.Boolean che indica se l'istanza della stringa corrente inizia con un carattere maiuscolo. Lo standard Unicode definisce i caratteri maiuscoli. In .NET Core il metodo [Char.IsUpper](xref:System.Char.IsUpper(System.Char)) restituisce `true` se un carattere è maiuscolo.

1. Nella barra dei menu scegliere **Compila**, **Compila soluzione**. Il progetto dovrebbe essere compilato senza errori.

## <a name="the-next-step"></a>Passaggio successivo ##

La compilazione della libreria finora è riuscita. Non è tuttavia possibile sapere se funziona come previsto poiché non è stato ancora chiamato uno di questi metodi. Il passaggio successivo per lo sviluppo della libreria consiste nel testarla usando un [Progetto unit test di C#](testing-library-with-visual-studio.md).



