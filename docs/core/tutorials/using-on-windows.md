---
title: Introduzione a .NET Core su Windows
description: Introduzione all&quot;uso di .NET Core su Windows con Visual Studio 2015
keywords: .NET, .NET Core
author: bleroy
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d743134a-08a3-4ff6-aab7-49f71f0568c3
translationtype: Human Translation
ms.sourcegitcommit: 54da8aebd64e86c064214074bc261f72c3b0aedc
ms.openlocfilehash: 299d479ce74a0e1f41ff42a0e6619f4964788194

---

# <a name="getting-started-with-net-core-on-windows-using-visual-studio-2015"></a>Introduzione all'uso di .NET Core su Windows con Visual Studio 2015

di [Bertrand Le Roy](https://github.com/bleroy) e [Phillip Carter](https://github.com/cartermp)

Visual Studio 2015 offre un ambiente completo per lo sviluppo di applicazioni .NET Core. Le procedure riportate in questo documento descrivono i passaggi necessari per creare alcune soluzioni .NET Core tipiche, o soluzioni che includono componenti .NET Core, tramite Visual Studio. Gli scenari prevedono l'esecuzione di test e l'uso di librerie di terze parti che non sono state compilate in modo esplicito per la versione più recente di .NET Core. 

## <a name="prerequisites"></a>Prerequisiti

Seguire le istruzioni nella [pagina dei prerequisiti](../windows-prerequisites.md) per aggiornare l'ambiente.

## <a name="getting-started"></a>Introduzione

I passaggi seguenti consentono di configurare Visual Studio 2015 per lo sviluppo di applicazioni .NET Core:

1. In Visual Studio fare clic sul menu **File** e scegliere **Nuovo**, **Progetto**.

2. Nella finestra di dialogo **Nuovo progetto**, nell'elenco **Modelli**, espandere il nodo **Visual C#** e scegliere **.NET Core**. Verranno visualizzati tre nuovi modelli di progetto: **Class Library (.NET Core)** (Libreria di classi (.NET Core)), **Console Application (.NET Core)** (Applicazione console (.NET Core)) e **ASP.NET Core Web Application (.NET Core)** (Applicazione Web di ASP.NET Core (.NET Core)).

<a name="a-solution-using-only-net-core-projects"></a>Una soluzione basata solo su progetti .NET Core
----------------------------------------

### <a name="writing-the-library"></a>Scrittura della libreria

1. In Visual Studio scegliere **File**, **Nuovo**, **Progetto**. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Visual C#**, scegliere il nodo **.NET Core** e quindi **Class Library (.NET Core)** (Libreria di classi (.NET Core)). 

2. Assegnare il nome "Library" al progetto e il nome "Golden" alla soluzione. Lasciare selezionata l'opzione **Crea directory per soluzione**. Fare clic su **OK**.

3. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

4. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Cercare e selezionare **Newtonsoft.Json**. Fare clic su **Installa**. 

5. Aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Ripristina pacchetti**.

6. Rinominare il file `Class1.cs` in `Thing.cs`. Accettare il nuovo nome della classe. Rimuovere il costruttore e aggiungere un metodo: `public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. Scegliere **Compila soluzione** dal menu **Compila**.

   La soluzione dovrebbe essere compilata senza errori.

### <a name="writing-the-test-project"></a>Scrittura del progetto di test

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Soluzione** e scegliere **Aggiungi**, **Nuova cartella Soluzione**. Assegnare il nome "test" alla cartella. 
   Questa è solo la cartella di una soluzione, non una cartella fisica.

2. Aprire il menu di scelta rapida per la cartella **test** e scegliere **Aggiungi**. **Nuovo progetto**. Nella finestra di dialogo **Nuovo progetto** scegliere **Console Application (.NET Core)** (Applicazione console (.NET Core)). Assegnare il nome "TestLibrary" al progetto e inserirlo esplicitamente nel percorso `Golden\test`. 

> [!IMPORTANT]
> Il progetto deve essere un'applicazione console, non una libreria di classi.

3. Nel progetto **TestLibrary** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Aggiungi riferimento**. 

4. Nella finestra di dialogo **Gestione riferimenti** selezionare **Libreria** sotto il nodo **Progetti**, **Soluzione** e quindi fare clic su **OK**. 

5. Nel progetto **TestLibrary** aprire il file `project.json` e sostituire `"Library": "1.0.0-*"` con `"Library": {"target": "project", "version": "1.0.0-*"}`. 

   Ciò consente di evitare la risoluzione del progetto `Library` in un pacchetto NuGet con lo stesso nome. Impostando esplicitamente "target" come "project" si ha la sicurezza che gli strumenti eseguano prima la ricerca di un progetto, e non di un pacchetto, con tale nome. 
   
6. Nel progetto **TestLibrary** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Ripristina pacchetti**.

7. Aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

8. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Selezionare la casella di controllo **Includi versione preliminare**, cercare e selezionare **xUnit** versione 2.2.0 o successive e quindi fare clic su **Installa**. 

9. Cercare e selezionare **dotnet-test-xunit** versione 2.2.0 o successive, quindi fare clic su **Installa**.

10. Modificare `project.json` e sostituire `"imports": "dnxcore50"` con `"imports": [ "dnxcore50", "portable-net45+win8" ]`. 

   In questo modo, le librerie xUnit verranno correttamente ripristinate e usate dal progetto. Tali librerie sono state compilate per l'uso con profili portabili che includono "portabile-net45+win8", ma non .NET Core, che non esisteva al momento della compilazione. Il comando `import` riduce i controlli di versione degli strumenti in fase di compilazione. È ora possibile ripristinare i pacchetti senza errori.

11. Modificare `project.json` per aggiungere `"testRunner": "xunit",` dopo la sezione `"frameworks"`.

12. Aggiungere un file di classe `LibraryTests.cs` al progetto **TestLibrary**, quindi aggiungere le direttive `using` `using Xunit;` e `using Library;` all'inizio del file e infine aggiungere il codice seguente alla classe:
    ```csharp
    [Fact]
    public void ThingGetsObjectValFromNumber() {
        Assert.Equal(42, new Thing().Get(42));
    }
    ```
    * Facoltativamente, eliminare il file `Program.cs` dal progetto **TestLibrary** e rimuovere `"buildOptions": {"emitEntryPoint": true},` da `project.json`.

   Sarà ora possibile compilare la soluzione. 
   
13. Scegliere **Windows**, **Esplora test** dal menu **Test** e quindi scegliere **Esegui tutto** in Esplora test.
   
   Il test dovrebbe essere superato.

### <a name="writing-the-console-app"></a>Scrittura dell'applicazione console

1. In Esplora soluzioni aprire il menu di scelta rapida per la cartella `src` e aggiungere un nuovo progetto **Console Application (.NET Core)** (Applicazione console (.NET Core)). Assegnare il nome "App" al progetto e impostare il percorso su `Golden\src`.

2. Nel progetto **App** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Aggiungi**, **Riferimento**. 

3. Nella finestra di dialogo **Gestione riferimenti** selezionare **Library** sotto il nodo **Progetti**, **Soluzione** e quindi fare clic su **OK**.

4. Nel progetto **App** aprire il file `project.json` e sostituire `"Library": "1.0.0-*"` con `"Library": {"target": "project"}`.

5. Aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Ripristina pacchetti**.

6. Aprire il menu di scelta rapida per il nodo **App** e scegliere **Imposta come progetto di avvio**.

7. Aprire il file `Program.cs`, aggiungere una direttiva `using Library;` all'inizio del file e quindi aggiungere `Console.WriteLine($"The answer is {new Thing().Get(42)}");` al metodo `Main`.

8. Impostare un punto di interruzione dopo la riga appena aggiunta.

9. Premere F5 per eseguire l'applicazione.

   L'applicazione dovrebbe essere compilata senza errori e dovrebbe raggiungere il punto di interruzione. Dovrebbe inoltre essere possibile verificare che l'output dell'applicazione sia "The answer is 42".

<a name="a-mixed-net-core-library-and-net-framework-application"></a>Una soluzione mista con libreria .NET Core e applicazione .NET Framework
--------------------------------------------------------

A partire dalla soluzione ottenuta con lo script precedente, eseguire questi passaggi:

1. In Esplora soluzioni aprire il file `project.json` per il progetto **Library** e sostituire `"frameworks": {
    "netstandard1.6" }` con `"frameworks": {
    "netstandard1.4" }`.

2. Nel progetto **Library** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Ripristina pacchetti**.

   La soluzione dovrebbe comunque essere compilata ed eseguita come nel caso precedente. Il test dovrebbe essere superato e dovrebbe essere possibile eseguire l'applicazione console e sottoporla a debug.

3. Nel progetto **Library** aprire il menu di scelta rapida e scegliere **Compila**.

4. In Esplora soluzioni aprire il menu di scelta rapida per la cartella `src` e quindi scegliere **Aggiungi**, **Nuovo progetto**.

5. Nella finestra di dialogo **Nuovo progetto** scegliere il nodo **Visual C#** e quindi **Applicazione console**.

> [!IMPORTANT]
> Assicurarsi di scegliere un'applicazione console standard, non la versione per .NET Core. In questa sezione, verrà utilizzata la libreria di un'applicazione .NET Framework.

6. Assegnare il nome "FxApp" al progetto e impostare il percorso su `Golden\src`.

7. Nel progetto **FxApp** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Aggiungi riferimento**.

8. Nella finestra di dialogo **Gestione riferimenti** scegliere **Sfoglia** e selezionare il percorso del file `Library.dll` compilato (in ..Golden\src\Library\bin\Debug\netstandard1.4), quindi fare clic su **Aggiungi**. 

   È inoltre possibile creare un pacchetto della libreria e fare riferimento al pacchetto, come metodo alternativo per fare riferimento al codice .NET Core da .NET Framework.

9. Aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

10. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Selezionare la casella di controllo **Includi versione preliminare** e quindi cercare e selezionare **Newtonsoft.Json**. Fare clic su **Installa**. 

11. Nel progetto **FxApp** aprire il file `Program.cs` e aggiungere una direttiva `using Library;` all'inizio del file, quindi aggiungere `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` al metodo `Main` del programma.

12. Impostare un punto di interruzione dopo la riga appena aggiunta.

13. Impostare **FxApp** come applicazione di avvio per la soluzione.

14. Premere F5 per eseguire l'app.

   L'applicazione dovrebbe essere compilata e dovrebbe raggiungere il punto di interruzione. L'output dell'applicazione dovrebbe essere "The answer is 42".
   
   > [!TIP]
   > Nella piattaforma Windows è possibile usare MSTest. Per altre informazioni, vedere il [documento sull'uso di MSTest in Windows](../testing/using-mstest-on-windows.md).

<a name="moving-a-library-from-netstandard-14-to-13"></a>Passaggio di una libreria dalla versione 1.4 alla 1.3 di netstandard
--------------------------------------------

1. In Esplora soluzioni aprire il file `project.json` per il progetto **Library**.

2. Sostituire `frameworks": { "netstandard1.4" }` con `frameworks": { "netstandard1.3" }`.

3. Nel progetto **Library** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Ripristina pacchetti**.

4. Scegliere **Compila Library** dal menu **Compila**.

5. Rimuovere il riferimento `Library` dal progetto **FxApp** e quindi aggiungerlo nuovamente usando il percorso ..Golden\src\Library\bin\Debug\netstandard1.3. Verrà ora fatto riferimento alla versione 1.3.

6. Premere F5 per eseguire l'applicazione.

   Tutto dovrebbe funzionare come in precedenza. Verificare che l'output dell'applicazione sia "The answer is 42", che sia stato raggiunto il punto di interruzione e che le variabili possano essere controllate.

<a name="a-mixed-pcl-library-and-net-framework-application"></a>Una soluzione mista con libreria di classi portabile e applicazione .NET Framework
--------------------------------------------------

Chiudere la soluzione precedente, se aperta. A partire da questa sezione si inizierà un nuovo script.

### <a name="writing-the-library"></a>Scrittura della libreria

1. In Visual Studio scegliere **File**, **Nuovo**, **Progetto**. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Visual C#** e scegliere **Libreria di classi (portabile per iOS, Android e Windows)**. 

2. Assegnare il nome "PCLLibrary" al progetto e il nome "GoldenPCL" alla soluzione. Lasciare selezionata l'opzione **Crea directory per soluzione**. Fare clic su **OK**.

3. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Gestisci pacchetti NuGet**.

4. Scegliere "nuget.org" come **Origine pacchetto** e fare clic sulla scheda **Sfoglia**. Selezionare la casella di controllo **Includi versione preliminare** e quindi cercare e selezionare **Newtonsoft.Json**. Fare clic su **Installa**. 

5. Rinominare la classe "Thing" e aggiungere un metodo: `public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

6. Scegliere **Compila soluzione** dal menu **Compila** e verificare che la soluzione venga compilata.

### <a name="writing-the-console-app"></a>Scrittura dell'applicazione console

1. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **Soluzione 'GoldenPCL'** e scegliere **Aggiungi**, **Nuovo progetto**. Nella finestra di dialogo **Nuovo progetto** espandere il nodo **Visual C#**, scegliere **Applicazione console** e quindi assegnare il nome "App" al progetto. 

2. Nel progetto **App** aprire il menu di scelta rapida per il nodo **Riferimenti** e scegliere **Aggiungi**, **Riferimento**. 

3. Nella finestra di dialogo **Gestione riferimenti** scegliere **Sfoglia** e selezionare il percorso del file `PCLLibrary.dll` compilato (in ..\GoldenPCL\PCLLibrary\bin\Debug), quindi fare clic su **Aggiungi**. 

4. Nel progetto **App** aprire il file `Program.cs` e aggiungere una direttiva `using PCLLibrary;` all'inizio del file, quindi aggiungere `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` al metodo `Main` del programma.

5. Impostare un punto di interruzione dopo la riga appena aggiunta.

6. In Esplora soluzioni aprire il menu di scelta rapida per il nodo **App** e scegliere **Imposta come progetto di avvio**.

7. Premere F5 per eseguire l'app.

   L'applicazione dovrebbe essere compilata ed eseguita e dovrebbe raggiungere il punto di interruzione dopo aver restituito "The answer is 42".

<a name="moving-a-pcl-to-a-netstandard-library"></a>Passaggio da una libreria di classi portabile a una libreria NetStandard
-------------------------------------
Gli strumenti della libreria di classi portabile possono modificare automaticamente la libreria di classi portabile in modo da definire .NET Standard come destinazione. 

1.  Fare doppio clic sul nodo "Proprietà" per aprire la pagina delle proprietà del progetto

2.  Sotto l'intestazione di destinazione fare clic sul collegamento ipertestuale "Imposta come destinazione la piattaforma standard .NET".

3.  Fare clic su "Sì" quando viene chiesto di confermare l'operazione.

Gli strumenti selezioneranno automaticamente la versione di .NET Standard che include tutte le destinazioni inizialmente definite per la libreria di classi portabile. È possibile definire come destinazione una versione diversa di .NET Standard usando l'elenco a discesa .NET Standard nella pagina delle proprietà del progetto.
 
* Se in precedenza era definito un file packages.config, è possibile venga chiesto di disinstallare i pacchetti installati prima della conversione.

### <a name="manually-edit-projectjson-to-target-net-standard-from-an-existing-portable-class-library"></a>Modificare manualmente project.json per definire .NET Standard come destinazione da una libreria di classi portabile esistente

1.  Se il file project.json contiene "dnxcore50" nell'elemento "supports", rimuoverlo.

2.  Rimuovere la dipendenza su "Microsoft.NETCore".

3.  Modificare la dipendenza da "Microsoft.NETCore.Portable.Compatibility" versione "1.0.0" alla versione "1.0.1".

4.  Aggiungere una dipendenza da "NETStandard.Library" versione "1.6.0".

5.  Dall'elemento "frameworks" rimuovere il framework "dotnet" (e l'elemento "imports" al suo interno).

6.  Aggiungere ` "netstandard1.x” : { } ` all'elemento frameworks, dove la x è sostituita dalla versione di .NET Standard da usare come destinazione.

### <a name="example-projectjson"></a>Esempio di project.json

Questo file project.json supporta clausole per UWP e .NET 4.6 e definisce netstandard1.3 come destinazione:
```
{
  "supports": {
    "net46.app": {},
    "uwp.10.0.app": {},
  },
  "dependencies": {
    "NETStandard.Library": "1.6.0",
    "Microsoft.NETCore.Portable.Compatibility": "1.0.1"
  },
  "frameworks": {
    "netstandard1.3" : {}
  }
}
```





<!--HONumber=Nov16_HO1-->


