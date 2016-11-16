---
title: Introduzione a .NET Core su macOS
description: Introduzione all&quot;uso di .NET Core su macOS con Visual Studio Code
keywords: .NET, .NET Core
author: bleroy
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8ad82148-dac8-4b31-9128-b0e9610f4d9b
translationtype: Human Translation
ms.sourcegitcommit: 2339be6aef7e2ff942f1f1999a12f48ee4a77ee8
ms.openlocfilehash: 12b7bed380db53aad04f0615c6efa6152b3035b7

---

# <a name="getting-started-with-net-core-on-macos-using-visual-studio-code"></a>Introduzione all'uso di .NET Core su macOS con Visual Studio Code

di [Bertrand Le Roy](https://github.com/bleroy), [Phillip Carter](https://github.com/cartermp) e [Bill Wagner](https://github.com/billwagner)

Con il contributo di [Toni Solarin-Sodara](https://github.com/tsolarin)

Questo documento offre una panoramica dei passaggi e del flusso di lavoro da seguire per creare una soluzione .NET Core usando [Visual Studio Code](http://code.visualstudio.com).
Si imparerà come creare progetti, creare unit test, usare gli strumenti di debug e incorporare librerie di terze parti tramite [NuGet](http://nuget.org).

In questo articolo Visual Studio Code viene usato su Mac OS. Le eventuali differenze rispetto alla piattaforma Windows verranno segnalate.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, è necessario installare [.NET Core SDK](https://www.microsoft.com/net/core), attualmente disponibile in versione di anteprima. .NET Core SDK include la versione più recente del framework e del runtime di .NET Core.

È inoltre necessario installare [Visual Studio Code](http://code.visualstudio.com).
Nel corso di questo articolo si installeranno anche le estensioni che consentono di migliorare l'esperienza di sviluppo .NET Core.

I collegamenti a tutti questi componenti sono disponibili nella [home page di .NET](http://dot.net).

## <a name="getting-started"></a>Introduzione

Il codice sorgente per questa esercitazione è disponibile su [GitHub](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/golden).

Avviare Visual Studio Code. Premere CTRL+\` (carattere di virgoletta aperta) per aprire un terminale incorporato in Visual Studio Code. In alternativa, è possibile usare una finestra di terminale separata.

Una volta completata questa operazione, si creeranno tre progetti: un progetto di libreria, i test per tale progetto e un'applicazione console che usa la libreria. Per i tre progetti si adotterà una struttura di cartelle standard. In questo modo, gli strumenti di .NET Core SDK saranno in grado di riconoscere la relazione tra i progetti del codice di produzione e quelli del codice di test, rendendo più produttiva l'esperienza di sviluppo.

La prima operazione da eseguire consiste nel creare le cartelle. Nel terminale creare una directory "golden" e all'interno di essa creare le directory `src` e `test`. In `src` creare le directory `app` e `library`. In `test` creare una directory `test-library`. Per eseguire queste operazioni, usare il terminale nel codice di Visual Studio o fare clic sulla cartella padre nel codice di Visual Studio e selezionare l'icona "Nuova cartella".

Nel codice di Visual Studio aprire la directory "golden", ossia la directory radice della soluzione.

Creare quindi un file `global.json` nella directory radice della soluzione.
Di seguito è riportato il contenuto del file `global.json`:

```json
{
    "projects": [
        "src",
        "test"
    ]
}
```

A questo punto, la struttura di directory avrà un aspetto simile al seguente:


```
/golden
|__global.json
|__/src
   |__/app
   |__/library
|__/test
   |__/test-library
```

### <a name="writing-the-library"></a>Scrittura della libreria

L'attività successiva consiste nel creare la libreria. Dalla finestra del terminale (quello incorporato nel codice di Visual Studio o un altro terminale) spostarsi nella directory `golden/src/library` e digitare il comando `dotnet new -t lib`.
Verrà così creato un progetto di libreria, con due file: `project.json` e `Library.cs`.

`project.json` include le informazioni seguenti:

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable"
  },
  "dependencies": {},
  "frameworks": {
    "netstandard1.6": {
      "dependencies": {
        "NETStandard.Library": "1.6.0"
      }
    }
  }
}
```


Questo progetto di libreria userà la rappresentazione JSON degli oggetti. Sarà pertanto opportuno aggiungere un riferimento al pacchetto NuGet `Newtonsoft.Json`. In `project.json` aggiungere la versione provvisoria più recente del pacchetto come dipendenza:

```json
"dependencies": {
    "Newtonsoft.Json": "9.0.1-beta1"
},
```

Dopo aver aggiunto tali dipendenze, è necessario installare i pacchetti nell'area di lavoro. Eseguire il comando `dotnet restore` per aggiornare tutte le dipendenze e scrivere un file `project.lock.json` nella directory del progetto. Il file contiene l'albero completo di tutte le dipendenze del progetto. Non è necessario leggere il file. Viene usato dagli strumenti di .NET Core SDK.

A questo punto, aggiornare il codice C#. Creare una classe `Thing` contenente un unico metodo pubblico. Il metodo restituirà la somma dei due numeri, me eseguirà tale operazione convertendo il numero in una stringa JSON e quindi deserializzandola. Rinominare il file `Library.cs` in `Thing.cs`. Sostituire quindi il codice esistente (per l'oggetto Class1 generato in base al modello) con il codice seguente:

```csharp
using static Newtonsoft.Json.JsonConvert;

namespace Library
{
    public class Thing
    {
        public int Get(int left, int right) =>
            DeserializeObject<int>($"{left + right}");
    }
}
```

Il codice usa alcune moderne funzionalità di C#, ad esempio direttive using static, membri con corpo di espressione e stringhe interpolate, che sono illustrate nella [Guida di C#](../../csharp/index.md) .

Una volta aggiornato il codice, è possibile compilare la libreria usando `dotnet build`.

Si otterrà così un file `library.dll` compilato in `golden/src/library/bin/Debug/netstandard1.6`.

### <a name="writing-the-test-project"></a>Scrittura del progetto di test

A questo punto, creare un progetto di test per la libreria che è stata compilata. Spostarsi nella directory `test/test-library`. Eseguire `dotnet new -t xunittest` per creare un nuovo progetto di test. 

Sarà necessario aggiungere un nodo di dipendenza per la libreria che è stata scritta nei passaggi precedenti. Aprire `project.json` e aggiornare la sezione delle dipendenze in base ai nodi seguenti (incluso il nodo `library`, che è l'ultimo nodo elencato di seguito):

```json
"dependencies": {
  "System.Runtime.Serialization.Primitives": "4.1.1",
  "xunit": "2.1.0",
  "dotnet-test-xunit": "1.0.0-rc2-192208-24",
  "library": {
    "target": "project"
  }
}
```

Il nodo `library` specifica che la dipendenza deve essere risolta in un progetto nell'area di lavoro corrente. Senza che sia specificato in modo esplicito, è possibile che il progetto di test venga compilato usando un pacchetto NuGet con lo stesso nome.

Ora che le dipendenze sono state configurate correttamente, è possibile creare i test per la libreria. Aprire `Tests.cs` e sostituirne il contenuto con il codice seguente:

```csharp
using Library;
using Xunit;

namespace TestApp
{
    public class LibraryTests
    {
        [Fact]
        public void TestThing() {
            Assert.Equal(42, new Thing().Get(19, 23));
        }
    }
}
```

A questo punto, eseguire `dotnet restore`, `dotnet build` e `dotnet test`.
Il Test Runner della console xUnit eseguirà il test e segnalerà che è stato superato. 

### <a name="writing-the-console-app"></a>Scrittura dell'applicazione console

Dalla finestra del terminale spostarsi nella directory `golden/src/app`. Eseguire `dotnet new` per creare una nuova applicazione console.

L'applicazione console dipende dalla libreria compilata e testata nei passaggi precedenti. È necessario indicarlo modificando `project.json` per aggiungere questa dipendenza.  Nel nodo `dependencies` aggiungere il nodo `library` come indicato di seguito:

```json
"dependencies": {
  "library": {
    "target": "project"
  }
}
```

Il nodo `project` è importante in questo caso, come lo era nella libreria di test. Indica che il progetto è incluso nella soluzione corrente e non è un pacchetto NuGet.

Eseguire `dotnet restore` per ripristinare tutte le dipendenze. Aprire `program.cs` e sostituire il contenuto del metodo `Main` con questa riga:

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

Sarà necessario aggiungere due direttive `using` all'inizio del file:

```csharp
using static System.Console;
using Library;
```

Eseguire quindi `dotnet build`. Per effetto di questa operazione, vengono creati gli assembly ed è possibile digitare `dotnet run` per avviare l'eseguibile.

### <a name="debugging-your-application"></a>Debug dell'applicazione

È possibile eseguire il debug del codice in Visual Studio Code usando l'estensione C#.
Installare l'estensione premendo `F1` per aprire la tavolozza di Visual Studio Code. Digitare `ext install` per visualizzare l'elenco delle estensioni. Selezionare l'estensione C#. Altri dettagli sono disponibili nella pagina della [documentazione dell'estensione C# di Visual Studio Code](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md).

Dopo l'installazione dell'estensione, Visual Studio Code chiederà di riavviare l'applicazione per caricare la nuova estensione. A questo punto, è possibile aprire la scheda del debugger, come illustrato nella figura.

![Debugger di Visual Studio Code](./media/using-on-macos/vscodedebugger.png)


Quando si avvia il debugger, Visual Studio Code chiede di configurare il debugger. Quando si esegue questa operazione, viene creata una directory `.vscode` con due file: `tasks.json` e `launch.json`. I due file controllano la configurazione del debugger. Nella maggior parte dei progetti questa directory non è inclusa nel controllo del codice sorgente.
È presente nell'esempio associato a questa procedura dettagliata per consentire di visualizzare le modifiche da apportare.

La soluzione contiene più progetti ed è pertanto opportuno modificare ciascuno dei file per eseguire i comandi corretti. Innanzitutto, aprire `tasks.json`. L'attività di compilazione predefinita esegue `dotnet build` nella directory di origine dell'area di lavoro. Si decide tuttavia di eseguire il comando nella directory `src/app`. È quindi necessario aggiungere un nodo `options` per impostare il percorso seguente come directory di lavoro corrente:

```json
"options": {
    "cwd": "${workspaceRoot}/src/app"
}
```

Successivamente, sarà necessario aprire `launch.json` e aggiornare il percorso del programma. In "configurations" verrà visualizzato un nodo che descrive il programma. Verrà visualizzata la riga:

```json
"program": "${workspaceRoot}/bin/Debug/<target-framework>/<project-name.dll>",
```

Modificarla nel modo seguente:

```json
"program": "${workspaceRoot}/src/app/bin/Debug/netcoreapp1.0/app.dll",
```

Se si usa Windows, è necessario aggiornare il file `project.json` dell'applicazione (nella directory `src/app`) per generare file PDB portabili, mentre questo avviene per impostazione predefinita in Mac OSX e Linux.
Aggiungere il nodo `debugType` in `buildOptions`. Sarà necessario aggiungere il nodo `debugType` in `project.json` per entrambe le cartelle `src/app` e `src/library`.

```json
  "buildOptions": {
    "debugType": "portable"
  },
```

Impostare un punto di interruzione nell'istruzione `WriteLine` in `Main`. A tale scopo, premere `F9` o fare clic sul margine sinistro della riga in cui si vuole inserire il punto di interruzione. Aprire il debugger premendo l'icona per il debug a sinistra della schermata di Visual Studio Code (vedere la figura). Fare quindi clic sul pulsante per la riproduzione per avviare l'applicazione nel debugger.

Si raggiungerà il punto di interruzione. Eseguire un'istruzione nel metodo `Get` e assicurarsi di aver passato gli argomenti corretti. Verificare che la risposta sia effettivamente 42.



<!--HONumber=Nov16_HO1-->


