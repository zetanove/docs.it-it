---
title: Introduzione a .NET Core su macOS
description: Introduzione all&quot;uso di .NET Core su macOS con Visual Studio Code
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 02/08/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 8ad82148-dac8-4b31-9128-b0e9610f4d9b
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: c4d1b7690ca87f2a1a9ced4d82e47aee2f7ecc9f
ms.lasthandoff: 03/07/2017

---

# <a name="getting-started-with-net-core-on-macos-using-visual-studio-code"></a>Introduzione all'uso di .NET Core su macOS con Visual Studio Code

Questo documento offre una panoramica dei passaggi e del flusso di lavoro da seguire per creare una soluzione .NET Core usando [Visual Studio Code](http://code.visualstudio.com).
Si imparerà come creare progetti, creare unit test, usare gli strumenti di debug e incorporare librerie di terze parti tramite [NuGet](http://nuget.org).

In questo articolo Visual Studio Code viene usato su Mac OS. Le eventuali differenze rispetto alla piattaforma Windows verranno segnalate.

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, è necessario installare [.NET Core SDK](https://www.microsoft.com/net/core). .NET Core SDK include la versione più recente del framework e del runtime di .NET Core.

È inoltre necessario installare [Visual Studio Code](http://code.visualstudio.com).
Nel corso di questo articolo si installeranno anche le estensioni che consentono di migliorare l'esperienza di sviluppo .NET Core.

## <a name="getting-started"></a>Introduzione

Il codice sorgente per questa esercitazione è disponibile su [GitHub](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/golden).

Avviare Visual Studio Code. Premere CTRL+\` (carattere di virgoletta aperta) per aprire un terminale incorporato in Visual Studio Code. In alternativa, è possibile usare una finestra di terminale separata.

Una volta completata questa operazione, si creeranno tre progetti: un progetto di libreria, i test per tale progetto e un'applicazione console che usa la libreria. 

La prima operazione da eseguire consiste nel creare le cartelle. Nel terminale creare una directory "golden" Nel codice di Visual Studio aprire la directory *golden*, ossia la directory radice della soluzione. Eseguire il comando [`dotnet new`](../tools/dotnet-new.md) per creare una nuova soluzione:

```
dotnet new sln
```

Questo comando crea un file *golden.sln* per l'intera soluzione.

L'attività successiva consiste nel creare la libreria. Nella finestra del terminale (incorporato nel codice di Visual Studio o in altro terminale) passare alla directory *golden/* e digitare il comando:

```
dotnet new classlib -o library
```

Verrà creato un progetto di libreria con due file, *library.csproj* e *Class1.cs* nella directory *library*. Si vuole che la soluzione includa tale progetto di libreria. Eseguire il comando [`dotnet sln`](../tools/dotnet-sln.md) per aggiungere il progetto *library.csproj* appena creato alla soluzione:

```
dotnet sln add library/library.csproj
```

Rivedere il progetto creato. Il file *library.csproj* contiene le informazioni seguenti:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard1.4</TargetFramework>
  </PropertyGroup>

</Project>
```

Questo progetto di libreria userà la rappresentazione JSON degli oggetti. Sarà pertanto opportuno aggiungere un riferimento al pacchetto NuGet `Newtonsoft.Json`. Il comando `dotnet add` aggiunge nuovi elementi a un progetto. Per aggiungere un riferimento al pacchetto NuGet, usare il comando `package` e specificare il nome del pacchetto. 

```
dotnet add library package Newtonsoft.Json
```

Questa operazione aggiunge `Newtonsoft.Json` e le relative dipendenze al progetto di libreria. In alternativa, è possibile modificare manualmente il file *library.csproj* e aggiungere il nodo seguente:

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json">
    <Version>9.0.1</Version>
  </PackageReference>
</ItemGroup>
```

Dopo aver aggiunto tali dipendenze, è necessario installare i pacchetti nell'area di lavoro. Eseguire il comando `dotnet restore` per aggiornare tutte le dipendenze e scrivere un file *obj/project.assets.json* nella directory del progetto. Il file contiene l'albero completo di tutte le dipendenze del progetto. Non è necessario leggere il file. Viene usato dagli strumenti di .NET Core SDK.

A questo punto, aggiornare il codice C#. Creare una classe `Thing` contenente un unico metodo pubblico. Il metodo restituirà la somma dei due numeri, me eseguirà tale operazione convertendo il numero in una stringa JSON e quindi deserializzandola. Assegnare il nome *Thing.cs* al file *Class1.cs*. Sostituire quindi il codice esistente (per l'oggetto Class1 generato in base al modello) con il codice seguente:

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

Il codice usa alcune moderne funzionalità di C#, ad esempio direttive using statiche, membri con corpo di espressione e stringhe interpolate, che sono illustrate nella sezione [Informazioni su C#](../../csharp/index.md) .

Una volta aggiornato il codice, è possibile compilare la libreria usando `dotnet build`.

È disponibile ora un file compilato *library.dll* in *golden/library/bin/Debug/netstandard1.4*.

### <a name="writing-the-test-project"></a>Scrittura del progetto di test

A questo punto, creare un progetto di test per la libreria che è stata compilata. Passare alla directory *golden*. Eseguire `dotnet new xunit -o test-library` per creare un nuovo progetto di test. Aggiungere anche questo progetto alla soluzione eseguendo `dotnet sln add test-library/test-library.csproj`.

Sarà necessario aggiungere un nodo di dipendenza per la libreria che è stata scritta nei passaggi precedenti. Il comando `dotnet add reference` esegue tale operazione:

```
dotnet add test-library/test-library.csproj reference library/library.csproj
```

Oppure è possibile modificare manualmente il file *test-library.csproj* e aggiungere il nodo seguente:

```xml
<ItemGroup>
  <ProjectReference Include="..\library\library.csproj" />
</ItemGroup>
```

Il nodo `library` specifica che la dipendenza deve essere risolta in un progetto nell'area di lavoro corrente. Senza che sia specificato in modo esplicito, è possibile che il progetto di test venga compilato usando un pacchetto NuGet con lo stesso nome.

Ora che le dipendenze sono state configurate correttamente, è possibile creare i test per la libreria. Aprire *UnitTest1.cs* e sostituirne il contenuto con il codice seguente:

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

Eseguire ora `dotnet restore` e `dotnet build`. Questi comandi troveranno in modo ricorsivo tutti i progetti per ripristinare le dipendenze e ricompilarle.
Alla fine eseguire `dotnet test test-library/test-library.csproj` per avviare i test.
Il Test Runner della console xUnit eseguirà il test e segnalerà che è stato superato. 

### <a name="writing-the-console-app"></a>Scrittura dell'applicazione console

Nel terminale eseguire `dotnet new console -o app` per creare una nuova applicazione console. Il progetto fa anche parte della soluzione, quindi eseguire `dotnet sln add app/app.csproj` per aggiungere il progetto alla soluzione.

L'applicazione console dipende dalla libreria compilata e testata nei passaggi precedenti. È necessario specificarlo eseguendo di nuovo `dotnet add reference`:

```
dotnet add app/app.csproj reference library/library.csproj
```

Eseguire `dotnet restore` per ripristinare tutte le dipendenze. Aprire *program.cs* e sostituire il contenuto del metodo `Main` con questa riga:

```csharp
WriteLine($"The answer is {new Thing().Get(19, 23)}");
```

Sarà necessario aggiungere due direttive `using` all'inizio del file:

```csharp
using static System.Console;
using Library;
```

Eseguire quindi `dotnet build`. Per effetto di questa operazione, vengono creati gli assembly ed è possibile digitare `dotnet run -p app/app.csproj` per avviare l'eseguibile.
L'argomento `-p` in `dotnet run` specifica il progetto dell'applicazione principale.

### <a name="debugging-your-application"></a>Debug dell'applicazione

È possibile eseguire il debug del codice in Visual Studio Code usando l'estensione C#.
Installare l'estensione premendo `F1` per aprire la tavolozza di Visual Studio Code. Digitare `ext install` per visualizzare l'elenco delle estensioni. Selezionare l'estensione C#. Altri dettagli sono disponibili nella pagina della [documentazione dell'estensione C# di Visual Studio Code](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md).

Dopo l'installazione dell'estensione, Visual Studio Code chiederà di riavviare l'applicazione per caricare la nuova estensione. A questo punto, è possibile aprire la scheda del debugger, come illustrato nella figura.

![Debugger di Visual Studio Code](./media/using-on-macos/vscodedebugger.png)

Impostare un punto di interruzione nell'istruzione `WriteLine` in `Main`. A tale scopo, premere `F9` o fare clic sul margine sinistro della riga in cui si vuole inserire il punto di interruzione. Aprire il debugger premendo l'icona per il debug a sinistra della schermata di Visual Studio Code (vedere la figura). Fare quindi clic sul pulsante per la riproduzione per avviare l'applicazione nel debugger.

Si raggiungerà il punto di interruzione. Eseguire un'istruzione nel metodo `Get` e assicurarsi di aver passato gli argomenti corretti. Verificare che la risposta sia effettivamente 42.

