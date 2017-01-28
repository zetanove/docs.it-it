---
title: Usare MSTest con .NET Core in Windows
description: Come usare MSTest con .NET Core in Windows mediante Visual Studio 2015
keywords: MSTest, .NET, .NET Core
author: ncarandini
ms.author: wiwagn
ms.date: 08/18/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ed447641-3e85-4e50-b7ed-004630048a3e
translationtype: Human Translation
ms.sourcegitcommit: 6795f1ace77e6f4d1b2fe07e6281f4acb6d21271
ms.openlocfilehash: 11faa46347b18240e9ddf1c27f27a814103e2565

---

# <a name="unit-testing-with-mstest-and-net-core-on-windows-using-visual-studio-2015"></a>Eseguire unit test con MSTest e .NET Core in Windows mediante Visual Studio 2015

xUnit può essere la scelta migliore quando è presente una destinazione a piattaforme multiple, mentre con .NET Core in Windows è possibile anche usare MSTest.

## <a name="prerequisites"></a>Prerequisiti

Per creare il progetto di libreria, seguire le istruzioni presenti in [Introduzione a .NET Core su Windows](../tutorials/using-on-windows.md).

### <a name="writing-the-test-project-using-mstest"></a>Scrittura del progetto di test usando MSTest

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Soluzione** e scegliere **Aggiungi**, **Nuova cartella Soluzione**. Assegnare il nome "test" alla cartella. 
   Questa è solo la cartella di una soluzione, non una cartella fisica.

2. Aprire il menu di scelta rapida per la cartella **test** e scegliere **Aggiungi**. **Nuovo progetto**. Nella finestra di dialogo **Nuovo progetto** scegliere **Console Application (.NET Core)** (Applicazione console (.NET Core)). Assegnare il nome "TestLibrary" al progetto e inserirlo esplicitamente nel percorso `Golden\test`. 

   > [!IMPORTANT]
   > Il progetto deve essere un'applicazione console, non una libreria di classi.

3. Nel progetto **TestLibrary** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Aggiungi riferimento**. 

4. Nella finestra di dialogo **Gestione riferimenti** selezionare **Libreria** sotto il nodo **Progetti**, **Soluzione** e quindi fare clic su **OK**. 

5. Nel progetto **TestLibrary** aprire il file `project.json` e sostituire `"Library": "1.0.0-*"` con `"Library": {"target": "project"}`. 

   Ciò consente di evitare la risoluzione del progetto `Library` in un pacchetto NuGet con lo stesso nome. Impostando esplicitamente la destinazione su "progetto" si ha la sicurezza che gli strumenti eseguano prima la ricerca di un progetto, e non di un pacchetto, con tale nome. 

6. Aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

7. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Selezionare la casella di controllo **Includi versione preliminare**, cercare e selezionare **MSTest.TestFramework** versione 1.0.1 o successive e quindi fare clic su **Installa**. 

8. Cercare e selezionare **dotnet-test-mstest** versione 1.1.1 o successive, quindi fare clic su **Installa**.

9. Modificare `project.json` per aggiungere `"testRunner": "mstest",` dopo la sezione `"version"`.

10. Aggiungere un file di classe `LibraryTests.cs` al progetto **TestLibrary**, quindi aggiungere le direttive `using` `Microsoft.VisualStudio.TestTools.UnitTesting;` e `using Library;` all'inizio del file e infine aggiungere il codice seguente alla classe:
    ```csharp
    [TestClass]
    public class LibraryTests
    {
        [TestMethod]
        public void ThingGetsObjectValFromNumber()
        {
            Assert.AreEqual(42, new Thing().Get(42));
        }
    }
    ```
    * Facoltativamente, eliminare il file `Program.cs` dal progetto **TestLibrary** e rimuovere `"buildOptions": {"emitEntryPoint": true},` da `project.json`.

   Sarà ora possibile compilare la soluzione. 
   
11. Scegliere **Windows**, **Esplora test** dal menu **Test** e quindi scegliere **Esegui tutto** in Esplora test.
   
   Il test dovrebbe essere superato.



<!--HONumber=Nov16_HO3-->


