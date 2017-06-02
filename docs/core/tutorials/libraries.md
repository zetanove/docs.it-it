---
title: Sviluppo di librerie con strumenti multipiattaforma
description: Sviluppo di librerie con strumenti multipiattaforma
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 05/01/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 9f6e8679-bd7e-4317-b3f9-7255a260d9cf
ms.translationtype: Human Translation
ms.sourcegitcommit: e6286e65ac24de3318f9ec7c97ef6ee2c7b192ed
ms.openlocfilehash: 15528cb0a12da07763613bee79180c4941224ddf
ms.contentlocale: it-it
ms.lasthandoff: 05/02/2017

---

# <a name="developing-libraries-with-cross-platform-tools"></a>Sviluppo di librerie con strumenti multipiattaforma

Questo articolo illustra come scrivere librerie per .NET usando gli strumenti dell'interfaccia della riga di comando multipiattaforma.  L'interfaccia della riga di comando offre un'esperienza efficace e di basso livello per qualsiasi sistema operativo supportato.  È comunque sempre possibile creare librerie con Visual Studio. Se si preferisce questo tipo di esperienza, [consultare la Guida di Visual Studio](libraries-with-vs.md).

## <a name="prerequisites"></a>Prerequisiti

È necessario che [l'SDK e l'interfaccia della riga di comando di .NET Core](https://www.microsoft.com/net/core) siano installati nel computer.

Per le sezioni di questo documento relative alle versioni di .NET Framework è necessario avere [.NET Framework](http://getdotnet.azurewebsites.net/) installato in un computer Windows.  

Inoltre, se si desidera supportare destinazioni precedenti di .NET Framework, è necessario installare Targeting/Developer Pack per versioni precedenti del framework dalla [pagina delle piattaforme di destinazione .NET](http://getdotnet.azurewebsites.net/target-dotnet-platforms.html).  Fare riferimento a questa tabella:

| Versione di .NET Framework | Pacchetto da scaricare |
| ---------------------- | ----------------- |
| 4.6.1 | .NET Framework 4.6.1 Targeting Pack |
| 4.6 | .NET Framework 4.6 Targeting Pack |
| 4.5.2 | .NET Framework 4.5.2 Developer Pack |
| 4.5.1 | .NET Framework 4.5.1 Developer Pack |
| 4.5 | Windows Software Development Kit per Windows 8 |
| 4.0 | Windows SDK per Windows 7 e .NET Framework 4 |
| 2.0, 3.0 e 3.5 | Runtime di .NET Framework 3.5 SP1 (o versione per Windows 8 o successiva) |

## <a name="how-to-target-the-net-standard"></a>Come definire .NET Standard come destinazione

Se non si ha molta familiarità con .NET Standard, leggere l'articolo [.NET Standard Library](../../standard/library.md) (Libreria .NET Standard) per altre informazioni.

In questo articolo è presente una tabella in cui le diverse versioni di .NET Standard sono associate alle varie implementazioni:

[!INCLUDE [net-standard-table](../../includes/net-standard-table.md)]

Ecco cosa significa questa tabella ai fini della creazione di una libreria:

La versione di .NET Standard selezionata sarà un compromesso tra l'accesso alle API più recenti e la possibilità di definire come destinazione più piattaforme .NET e versioni di .NET Framework.  Per controllare l'intervallo di piattaforme e versioni definibili come destinazione selezionare una versione di `netstandardX.X` (dove `X.X` è un numero di versione) e aggiungerla al file di progetto (`.csproj` o `.fsproj`).

Quando si definisce .NET Standard come destinazione sono disponibili tre opzioni principali, a seconda delle esigenze.

1. È possibile usare la versione predefinita di .NET Standard inclusa nei modelli (`netstandard1.4`) che offre l'accesso alla maggior parte delle API .NET Standard pur essendo compatibile con UWP, .NET Framework 4.6.1 e con l'imminente .NET Standard 2.0.

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard1.4</TargetFramework>
        </PropertyGroup>
    </Project>
    ```

2. È possibile usare una versione inferiore o superiore di .NET Standard modificando il valore nel nodo `TargetFramework` del file di progetto.
    
    Le versioni di .NET Standard sono compatibili con le versioni precedenti. Ciò significa che le librerie `netstandard1.0` possono essere eseguite su piattaforme `netstandard1.1` e versioni successive.  Tuttavia, non è prevista la compatibilità con le versioni successive. Le piattaforme .NET Standard precedenti non possono fare riferimento a quelle più recenti.  Ciò significa che le librerie `netstandard1.0` non possono fare riferimento alle librerie `netstandard1.1` o versioni successive.  Selezionare la versione di .NET Standard che contiene la combinazione di API e supporto per piattaforme più adatta alle proprie esigenze.  Attualmente è consigliabile selezionare `netstandard1.4`.
    
3. Se si vuole definire come destinazione .NET Framework 4.0 o versione precedente, o si desidera usare un'API disponibile in .NET Framework ma non in .NET Standard (ad esempio, `System.Drawing`), leggere le sezioni seguenti per apprendere come definire più destinazioni.

## <a name="how-to-target-the-net-framework"></a>Come definire .NET Framework come destinazione

> [!NOTE]
> Queste istruzioni presuppongono che nel computer sia installato .NET Framework.  Vedere la sezione [Prerequisiti](#prerequisites) per informazioni sulle dipendenze da installare.

Tenere presente che alcune delle versioni di .NET Framework indicate in questo argomento non sono più supportate.  Per informazioni sulle versioni non supportate, vedere [Domande frequenti sui criteri relativi al ciclo di vita del supporto per Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq/en-us).

Se si vuole raggiungere il numero massimo di sviluppatori e progetti, usare .NET Framework 4.0 come destinazione di base. Per definire .NET Framework come destinazione, è necessario iniziare usando il TFM (Target Framework Moniker) corretto, corrispondente alla versione di .NET Framework da supportare.

```
.NET Framework 2.0   --> net20
.NET Framework 3.0   --> net30
.NET Framework 3.5   --> net35
.NET Framework 4.0   --> net40
.NET Framework 4.5   --> net45
.NET Framework 4.5.1 --> net451
.NET Framework 4.5.2 --> net452
.NET Framework 4.6   --> net46
.NET Framework 4.6.1 --> net461
.NET Framework 4.6.2 --> net462
.NET Framework 4.7 --> net47
```

Quindi inserire il TFM nella sezione `TargetFramework` del file di progetto.  Ad esempio, ecco come scrivere una libreria con destinazione .NET Framework 4.0:

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net40</TargetFramework>
    </PropertyGroup>
</Project>
```

L'operazione è ora completata.  Anche se compilata solo per .NET Framework 4, la libreria può essere usata nelle versioni più recenti di .NET Framework.

## <a name="how-to-multitarget"></a>Come definire più destinazioni

> [!NOTE]
> Le istruzioni seguenti presuppongono che nel computer sia installato .NET Framework.  Vedere la sezione [Prerequisiti](#prerequisites) per informazioni sulle dipendenze da installare e sull'area da cui scaricarle.

Quando il progetto supporta sia .NET Framework che .NET Core, può essere opportuno definire come destinazione le versioni precedenti di .NET Framework. In questo scenario, per usare API e costrutti di linguaggio più recenti per le destinazioni più recenti, inserire direttive `#if` nel codice. Può anche essere necessario aggiungere diversi pacchetti e dipendenze per ogni piattaforma di destinazione per includere le diverse API necessarie per ogni caso.

Si supponga ad esempio di avere una libreria che esegue operazioni di rete tramite HTTP. Per .NET Standard e .NET Framework 4.5 o versioni successive, è possibile usare la classe `HttpClient` dello spazio dei nomi `System.Net.Http`. Tuttavia, le versioni precedenti di .NET Framework non dispongono della classe `HttpClient` e per tali versioni è quindi possibile usare in alternativa la classe `WebClient` dello spazio dei nomi `System.Net`.

Il file di progetto può avere un aspetto simile al seguente:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.0 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net40'">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.5 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net45'">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>
</Project>
```

Si noteranno tre modifiche principali:

1. Il nodo `TargetFramework` è stato sostituito da `TargetFrameworks` e all'interno sono espressi tre TFM.
2. Un nodo `<ItemGroup>` per la destinazione `net40 ` chiama un riferimento di .NET Framework.
3. Un nodo `<ItemGroup>` per la destinazione `net45` chiama due riferimenti di .NET Framework.

Il sistema di compilazione è in grado di riconoscere i seguenti simboli di preprocessore usati nelle direttive `#if`:

```
.NET Framework 2.0   --> NET20
.NET Framework 3.5   --> NET35
.NET Framework 4.0   --> NET40
.NET Framework 4.5   --> NET45
.NET Framework 4.5.1 --> NET451
.NET Framework 4.5.2 --> NET452
.NET Framework 4.6   --> NET46
.NET Framework 4.6.1 --> NET461
.NET Framework 4.6.2 --> NET462
.NET Standard 1.0    --> NETSTANDARD1_0
.NET Standard 1.1    --> NETSTANDARD1_1
.NET Standard 1.2    --> NETSTANDARD1_2
.NET Standard 1.3    --> NETSTANDARD1_3
.NET Standard 1.4    --> NETSTANDARD1_4
.NET Standard 1.5    --> NETSTANDARD1_5
.NET Standard 1.6    --> NETSTANDARD1_6
```

Ecco un esempio che usa la compilazione condizionale basata sulla destinazione:

```csharp
using System;
using System.Text.RegularExpressions;
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
 // This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif

namespace MultitargetLib
{
    public class Library
    {
#if NET40
         private readonly WebClient _client = new WebClient();
         private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "http://www.dotnetfoundation.org/";

            var uri = new Uri(url);

            string result = "";

            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
         // .NET 4.5+ can use async/await!
         public async Task<string> GetDotNetCountAsync()
         {
             string url = "http://www.dotnetfoundation.org/";

             // HttpClient is thread-safe, so no need to explicitly lock here
             var result = await _client.GetStringAsync(url);

             int dotNetCount = Regex.Matches(result, ".NET").Count;

             return $"dotnetfoundation.org mentions .NET {dotNetCount} times in its HTML!";
         }
 #endif
    }
}
```

Se si compila il progetto con `dotnet build` si noteranno tre directory sotto la cartella `bin/`:

```
net40/
net45/
netstandard1.4/
```

Ogni directory contiene i file `.dll` per ciascuna destinazione.

## <a name="how-to-test-libraries-on-net-core"></a>Come testare le librerie in .NET Core

È importante essere in grado di eseguire test tra diverse piattaforme.  È possibile usare [xUnit](http://xunit.github.io/) o MSTest senza modifiche.  Entrambi sono adatti per gli unit test della libreria in .NET Core.  La modalità di configurazione della soluzione con progetti di test dipende dalla [struttura della soluzione](#structuring-a-solution).  Nell'esempio seguente si presuppone che le directory di test e di origine si trovino nella stessa directory di livello superiore.

> [!INFO] Questa procedura usa alcuni [comandi CLI .NET](../tools/index.md).  Per altre informazioni, vedere [dotnet new](../tools/dotnet-new.md) e [dotnet sln](../tools/dotnet-sln.md).

1. Configurare la soluzione.  È possibile farlo con i comandi seguenti:

```bash
mkdir SolutionWithSrcAndTest
cd SolutionWithSrcAndTest
dotnet new sln
dotnet new classlib -o MyProject
dotnet new xunit -o MyProject.Test
dotnet sln add MyProject/MyProject.csproj
dotnet sln add MyProject.Test/MyProject.Test.csproj
```

I progetti vengono creati e collegati in una soluzione.  La directory per `SolutionWithSrcAndTest` ha un aspetto simile al seguente:

```    
/SolutionWithSrcAndTest
|__SolutionWithSrcAndTest.sln
|__MyProject/
|__MyProject.Test/
```

2. Passare alla directory del progetto di test e aggiungere un riferimento a `MyProject.Test` da `MyProject`.

```bash
cd MyProject.Test
dotnet add reference ../MyProject/MyProject.csproj
```

3. Ripristinare i pacchetti e compilare i progetti:

```bash
dotnet restore
dotnet build
```

4. Verificare che xUnit sia in esecuzione con il comando `dotnet test`.  Se si sceglie di usare MSTest, va invece eseguita l'utilità di test delle console MSTest.
    
L'operazione è ora completata.  È ora possibile testare la libreria su tutte le piattaforme usando gli strumenti da riga di comando.  Una volta completata la configurazione, è possibile procedere con il testing della libreria in modo molto semplice:

1. Eseguire le opportune modifiche nella libreria.
2. Eseguire i test dalla riga di comando, nella directory di test, usando il comando `dotnet test`.

Il codice viene ricompilato automaticamente quando si richiama il comando `dotnet test`.

## <a name="how-to-use-multiple-projects"></a>Come usare più progetti

Per le librerie di maggiori dimensioni, è spesso necessario inserire funzionalità in progetti diversi.

Si supponga di voler creare una libreria che sia utilizzabile in C# e F# idiomatico.  Ciò significa che la libreria viene utilizzata in modi che sono naturali per C# o F#.  In C#, ad esempio, la libreria può essere utilizzata in un modo simile al seguente:

```csharp
using AwesomeLibrary.CSharp;

...
public Task DoThings(Data data)
{
    var convertResult = await AwesomeLibrary.ConvertAsync(data);
    var result = AwesomeLibrary.Process(convertResult);
    // do something with result
}
```  

In F#, invece, può assumere l'aspetto seguente:

```fsharp
open AwesomeLibrary.FSharp

...

let doWork data = async {
    let! result = AwesomeLibrary.AsyncConvert data // Uses an F# async function rather than C# async method
    // do something with result
}
```

Scenari di utilizzo come questo indicano che le API a cui si accede devono avere una struttura diversa per C# e F#.  Un approccio comune per gestire questa situazione consiste nel definire l'intera logica di una libreria in un progetto di base, a cui eseguono chiamate i livelli di API definiti nei progetti C# e F#.  Nella parte restante della sezione verranno usati i nomi seguenti:

* **AwesomeLibrary.Core**: un progetto di base che contiene tutta la logica della libreria
* **AwesomeLibrary.CSharp**: un progetto con API pubbliche destinato all'utilizzo in C#
* **AwesomeLibrary.FSharp**: un progetto con API pubbliche destinato all'utilizzo in F#

Eseguire i seguenti comandi nel terminale in uso per ottenere la stessa struttura mostrata in questa Guida:

```console
dotnet new sln
mkdir AwesomeLibrary.Core && cd AwesomeLibrary.Core && dotnet new classlib
cd ..
mkdir AwesomeLibrary.CSharp && cd AwesomeLibrary.CSharp && dotnet new classlib
cd ..
mkdir AwesomeLibrary.FSharp && cd AwesomeLibrary.FSharp && dotnet new classlib -lang F#
cd ..
dotnet sln add AwesomeLibrary.Core/AwesomeLibrary.Core/csproj
dotnet sln add AwesomeLibrary.CSharp/AwesomeLibrary.CSharp/csproj
dotnet sln add AwesomeLibrary.FSharp/AwesomeLibrary.FSharp/csproj
```

Verranno aggiunti i tre progetti precedenti e un file soluzione che li collega.  La creazione del file di soluzione e il collegamento dei progetti consentono di ripristinare e compilare i progetti da un livello superiore.

### <a name="project-to-project-referencing"></a>Definizione di riferimenti da progetto a progetto

Il metodo migliore per creare un riferimento a un progetto è l'uso dell'interfaccia della riga di comando di .NET per aggiungere un riferimento al progetto.  Dalle directory di progetto **AwesomeLibrary.CSharp** e **AwesomeLibrary.FSharp** è possibile eseguire il comando seguente:

```console
$ dotnet add reference ../AwesomeLibrary.Core.csproj
```

I file di progetto per **AwesomeLibrary.CSharp** e **AwesomeLibrary.FSharp** includeranno ora un riferimento a **AwesomeLibrary.Core** come destinazione `ProjectReference`.  È possibile verificare la presenza del riferimento cercando quanto segue nei file di progetto:

```xml
<ItemGroup>
    <ProjectReference Include="..\AwesomeLibrary.Core\AwesomeLibrary.Core.csproj" />
</ItemGroup>
```

Se si preferisce non usare l'interfaccia della riga di comando .NET è possibile aggiungere manualmente questa sezione a ogni file di progetto.

### <a name="structuring-a-solution"></a>Definizione della struttura di una soluzione

Un altro aspetto importante delle soluzioni basate su più progetti è quello di stabilire una buona struttura complessiva dei progetti. È possibile organizzare il codice come desiderato. A condizione che si colleghi ogni progetto al file di soluzione mediante `dotnet sln add`, sarà possibile eseguire `dotnet restore` e `dotnet build` a livello della soluzione.
