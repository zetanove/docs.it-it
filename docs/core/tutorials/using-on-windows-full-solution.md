---
title: Creazione di una soluzione .NET Core completa in Windows tramite Visual Studio 2017 | Microsoft Docs
description: Creazione di una soluzione .NET Core completa in Windows tramite Visual Studio 2017
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ba7e082c-a7c8-431e-a342-f67734b660f6
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: b8505f88b324fcdf3a51d75c455ec5869e058774
ms.lasthandoff: 03/07/2017

---

# <a name="building-a-complete-net-core-solution-on-windows-using-visual-studio-2017"></a>Creazione di una soluzione .NET Core completa in Windows tramite Visual Studio 2017

Visual Studio 2017 offre un ambiente completo per lo sviluppo di applicazioni .NET Core. Questo documento descrive le procedure necessarie per creare una soluzione .NET Core tipica contenente librerie riutilizzabili, funzionalità di test e librerie di terze parti. 

## <a name="prerequisites"></a>Prerequisiti

Seguire le istruzioni nella [pagina dei prerequisiti](../windows-prerequisites.md) per aggiornare l'ambiente.

## <a name="a-solution-using-only-net-core-projects"></a>Una soluzione basata solo su progetti .NET Core

### <a name="writing-the-library"></a>Scrittura della libreria

1. In Visual Studio scegliere **File**, **Nuovo**, **Progetto**. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Visual C#**, scegliere il nodo **.NET Core** e quindi **Libreria di classi (.NET Standard)**. 

2. Assegnare il nome "Library" al progetto e il nome "Golden" alla soluzione. Lasciare selezionata l'opzione **Crea directory per soluzione**. Fare clic su **OK**.

3. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Dipendenze** e scegliere **Gestisci pacchetti NuGet**.

4. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Cercare e selezionare **Newtonsoft.Json**. Fare clic su **Installa** e accettare i termini del Contratto di Licenza Microsoft. Il pacchetto è ora visibile in **Dipendenze/NuGet** e viene ripristinato automaticamente.

5. Rinominare il file `Class1.cs` in `Thing.cs`. Accettare il nuovo nome della classe. Aggiungere un metodo: `public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. Scegliere **Compila soluzione** dal menu **Compila**.

   La soluzione dovrebbe essere compilata senza errori.

### <a name="writing-the-test-project"></a>Scrittura del progetto di test

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Soluzione** e scegliere **Aggiungi**, **Nuovo progetto**. Nell'area **Visual C# / .NET Core** della finestra di dialogo **Nuovo progetto** scegliere **Progetto unit test (.NET Core)**. Assegnare il nome "TestLibrary" al progetto e fare clic su OK. 

2. Nel progetto **TestLibrary** aprire il menu di scelta rapida per il nodo **Dipendenze** e scegliere **Aggiungi riferimento**. Fare clic su **Progetti**, selezionare il progetto Libreria e scegliere OK. Verrà aggiunto un riferimento alla libreria dal progetto di test.

3. Rinominare il file `UnitTest1.cs` in `LibraryTests.cs` e accettare la ridenominazione della classe. Aggiungere `using Library;` all'inizio del file e sostituire il metodo `TestMethod1` con il codice seguente:
    ```csharp
    [TestMethod]
    public void ThingGetsObjectValFromNumber()
    {
        Assert.AreEqual(42, new Thing().Get(42));
    }
    ```

   Sarà ora possibile compilare la soluzione. 
   
4. Dal menu **Test** scegliere **Windows**, **Esplora Test** per visualizzare la finestra Esplora test nella propria area di lavoro. Dopo alcuni secondi in Esplora test viene visualizzato il test `ThingGetsObjectValFromNumber`. Scegliere **Esegui tutto**.
   
   Il test dovrebbe essere superato.

### <a name="writing-the-console-app"></a>Scrittura dell'applicazione console

1. In Esplora soluzioni aprire il menu di scelta rapida relativo alla soluzione e aggiungere un nuovo progetto **Applicazione console (.NET Core)**. Assegnare il nome "App".

2. Nel progetto **App** aprire il menu di scelta rapida per il nodo **Dipendenze** e scegliere **Aggiungi**, **Riferimento**. 

3. Nella finestra di dialogo **Gestione riferimenti** selezionare **Library** sotto il nodo **Progetti**, **Soluzione** e quindi fare clic su **OK**.

6. Aprire il menu di scelta rapida per il nodo **App** e scegliere **Imposta come progetto di avvio**. In questo modo sarà possibile avviare l'applicazione console premendo F5 o CTRL + F5.

7. Aprire il file `Program.cs`, aggiungere una direttiva `using Library;` all'inizio del file e quindi aggiungere `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` al metodo `Main`.

8. Impostare un punto di interruzione dopo la riga appena aggiunta.

9. Premere F5 per eseguire l'applicazione.

   L'applicazione dovrebbe essere compilata senza errori e dovrebbe raggiungere il punto di interruzione. Dovrebbe inoltre essere possibile verificare che l'output dell'applicazione sia "The answer is 42".

