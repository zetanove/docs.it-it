---
title: Sviluppo di librerie con strumenti multipiattaforma
description: Sviluppo di librerie con strumenti multipiattaforma
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 9f6e8679-bd7e-4317-b3f9-7255a260d9cf
translationtype: Human Translation
ms.sourcegitcommit: 0882a5ca2f7814e2fd168dce40705d11b199f102
ms.openlocfilehash: de44f103bef6006dd1a952c48c1e172f6277a95b

---

# <a name="developing-libraries-with-cross-platform-tools"></a>Sviluppo di librerie con strumenti multipiattaforma

**Alcune informazioni sono soggette a modifiche in base all'evoluzione della toolchain.**

Questo articolo illustra come scrivere librerie per .NET usando gli strumenti dell'interfaccia della riga di comando multipiattaforma.  L'interfaccia della riga di comando offre un'esperienza efficace e di basso livello per qualsiasi sistema operativo supportato.  È comunque sempre possibile creare librerie con Visual Studio. Se si preferisce questo tipo di esperienza, [consultare la Guida di Visual Studio](libraries-with-vs.md).

## <a name="prerequisites"></a>Prerequisiti

È necessario che [l'SDK e l'interfaccia della riga di comando di .NET Core](https://www.microsoft.com/net/core) siano installati nel computer.

Per le sezioni di questo documento che trattano delle versioni di .NET Framework o delle librerie di classi portabili, è necessario [.NET Framework](http://getdotnet.azurewebsites.net/) installato in un computer Windows.  

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

| Nome della piattaforma | Alias |  |  |  |  |  | | |
| :---------- | :--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|.NET Standard | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1,5 | 1.6 |
|.NET Core|netcoreapp|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|1.0|
|.NET Framework|net|&rarr;|4.5|4.5.1|4.6|4.6.1|4.6.2|4.6.3|
|Piattaforme Mono/Xamarin||&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|*|
|Piattaforma UWP (Universal Windows Platform)|uap|&rarr;|&rarr;|&rarr;|&rarr;|10.0|||
|Windows|win|&rarr;|8.0|8.1|||||
|Windows Phone|wpa|&rarr;|&rarr;|8.1|||||
|Silverlight per Windows Phone|wp|8.0|||||||

Ecco cosa significa questa tabella ai fini della creazione di una libreria:

La versione di .NET Standard selezionata sarà un compromesso tra l'accesso alle API più recenti e la possibilità di definire come destinazione più piattaforme .NET e versioni di .NET Framework.  Selezionando una versione di `netstandardX.X` (dove `X.X` è un numero di versione) e aggiungendola al file `project.json`, si controlla l'intervallo di piattaforme e versioni definibili come destinazione.

Inoltre, il corrispondente [pacchetto NuGet in base al quale definire la dipendenza](https://www.nuget.org/packages/NETStandard.Library/) è `NETStandard.Library` versione `1.6.0`.  Anche se nulla impedisce di definire la dipendenza da `Microsoft.NETCore.App`, come con le applicazioni console, questa non è in genere un'opzione consigliabile.  Se sono necessarie API di un pacchetto non specificato in `NETStandard.Library`, è sempre possibile definire tale pacchetto in aggiunta a `NETStandard.Library` nella sezione `dependencies` del file `project.json`.

Quando si definisce .NET Standard come destinazione sono disponibili tre opzioni principali, a seconda delle esigenze.

1. È possibile usare la versione più recente di .NET Standard, `netstandard1.6`, adatta ai casi in cui si vuole accedere alla maggior parte delle API e una copertura più limitata fra le implementazioni non rappresenta un problema.
2. È possibile usare una versione precedente di .NET Standard per definire come destinazione le implementazioni di .NET meno recenti. Questa opzione ha lo svantaggio di non consentire l'accesso ad alcune delle API più recenti.
    
    Ad esempio, se si vuole avere la garanzia della compatibilità con .NET Framework 4.6 e versioni successive, è necessario selezionare `netstandard1.3`:

    ```json
    {
        "dependencies":{
            "NETStandard.Library":"1.6.0"
        },
        "frameworks":{
            "netstandard1.3":{}
        }
    }
    ```
    
    Le versioni di .NET Standard sono compatibili con le versioni precedenti. Ciò significa che le librerie `netstandard1.0` possono essere eseguite su piattaforme `netstandard1.1` e versioni successive.  Tuttavia, non è prevista la compatibilità con le versioni successive. Le piattaforme .NET Standard precedenti non possono fare riferimento a quelle più recenti.  Ciò significa che le librerie `netstandard1.0` non possono fare riferimento alle librerie `netstandard1.1` o versioni successive.  Selezionare la versione di .NET Standard che contiene la combinazione di API e supporto per piattaforme più adatta alle proprie esigenze.
    
3. Se si vuole definire come destinazione .NET Framework 4.0 o versione precedente, o si desidera usare un'API disponibile in .NET Framework ma non in .NET Standard (ad esempio, `System.Drawing`), leggere le sezioni seguenti per apprendere come definire più destinazioni.

## <a name="how-to-target-the-net-framework"></a>Come definire .NET Framework come destinazione

> [!NOTE]
> Queste istruzioni presuppongono che nel computer sia installato .NET Framework.  Vedere la sezione [Prerequisiti](#prerequisites) per informazioni sulle dipendenze da installare.

Tenere presente che alcune delle versioni di .NET Framework indicate in questo argomento non sono più supportate.  Per informazioni sulle versioni non supportate, vedere [Domande frequenti sui criteri relativi al ciclo di vita del supporto per Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq/en-us).

Se si vuole raggiungere il numero massimo di sviluppatori e progetti, usare .NET Framework 4 come destinazione di base. Per definire .NET Framework come destinazione, è necessario iniziare usando il TFM (Target Framework Moniker) corretto, corrispondente alla versione di .NET Framework da supportare.

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
.NET Framework 4.6.3 --> net463
```

Ad esempio, ecco come scrivere una libreria che ha .NET Framework 4 come destinazione:

```json
{
    "frameworks":{
        "net40":{}
    }
}
```

L'operazione è ora completata.  Anche se compilata solo per .NET Framework 4, la libreria può essere usata nelle versioni più recenti di .NET Framework.

## <a name="how-to-target-a-portable-class-library-pcl"></a>Come definire una libreria di classi portabile come destinazione

> [!NOTE]
> Queste istruzioni presuppongono che nel computer sia installato .NET Framework.  Vedere la sezione [Prerequisiti](#prerequisites) per informazioni sulle dipendenze da installare.

La definizione di un profilo di libreria di classi portabile come destinazione presenta qualche difficoltà in più rispetto a quella di .NET Standard o .NET Framework.  Per i principianti, [fare riferimento a questo elenco di profili di librerie di classi portabili](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) per trovare la destinazione NuGet corrispondente allo specifico profilo della libreria di classi portabile.

Eseguire quindi queste operazioni:

1. Creare una nuova voce sotto `frameworks` nel file `project.json`, denominato `.NETPortable,Version=v{version},Profile=Profile{profile}`, dove `{version}` e `{profile}` corrispondono rispettivamente a un numero di versione della libreria di classi portabile e a un numero di profilo.
2. In questa nuova voce elencare ogni singolo assembly usato per la destinazione sotto una voce `frameworkAssemblies`.  Sono inclusi `mscorlib`, `System` e `System.Core`.
3. Se si definiscono più destinazioni (vedere la sezione successiva), è necessario elencare in modo esplicito le dipendenze per ogni destinazione sotto le rispettive voci di destinazione.  Non sarà più possibile usare una voce `dependencies` globale.

Di seguito è riportato un esempio di profilo di la libreria di classi portabile 328 di destinazione. Il profilo 328 supporta: .NET Standard 1.4, .NET Framework 4, Windows 8, Windows Phone 8.1, Windows Phone Silverlight 8.1 e Silverlight 5.

```json
{
    "frameworks":{
        ".NETPortable,Version=v4.0,Profile=Profile328":{
            "frameworkAssemblies":{
                "mscorlib":"",
                "System":"",
                "System.Core":""
            }
        }
    }
}
```

Quando si crea un progetto che include il profilo di libreria di classi portabile 328 come framework nel file *project.json*, nella cartella */bin/debug* sarà inclusa questa sottocartella:

```
portable-net40+sl50+netcore45+wpa81+wp8/
```

Questa cartella contiene i file `.dll` necessari per eseguire la libreria.

## <a name="how-to-multitarget"></a>Come definire più destinazioni

> [!NOTE]
> Le istruzioni seguenti presuppongono che nel computer sia installato .NET Framework.  Vedere la sezione [Prerequisiti](#prerequisites) per informazioni sulle dipendenze da installare e sull'area da cui scaricarle.

Quando il progetto supporta sia .NET Framework che .NET Core, può essere opportuno definire come destinazione le versioni precedenti di .NET Framework. In questo scenario, per usare API e costrutti di linguaggio più recenti per le destinazioni più recenti, inserire direttive `#if` nel codice. Può anche essere necessario aggiungere nel `project.json file` diversi pacchetti e dipendenze per ogni piattaforma di destinazione in modo da includere le diverse API necessarie per ogni caso.

Si supponga ad esempio di avere una libreria che esegue operazioni di rete tramite HTTP. Per .NET Standard e .NET Framework 4.5 o versioni successive, è possibile usare la classe `HttpClient` dello spazio dei nomi `System.Net.Http`. Tuttavia, le versioni precedenti di .NET Framework non dispongono della classe `HttpClient` e per tali versioni è quindi possibile usare in alternativa la classe `WebClient` dello spazio dei nomi `System.Net`.

Pertanto, il file `project.json` può avere un aspetto simile al seguente:

```json
{
    "frameworks":{
        "net40":{
            "frameworkAssemblies": {
                "System.Net":"",
                "System.Text.RegularExpressions":""
            }
        },
        "net452":{
            "frameworkAssemblies":{
                "System.Net":"",
                "System.Net.Http":"",
                "System.Text.RegularExpressions":"",
                "System.Threading.Tasks":""
            }
        },
        "netstandard1.6":{
            "dependencies": {
                "NETStandard.Library":"1.6.0",
            }
        }
    }
}
```

Si noti che i riferimenti agli assembly di .NET Framework devono essere definiti in modo esplicito nelle destinazioni `net40` e `net452` e i riferimenti NuGet sono anche elencati in modo esplicito nella destinazione `netstandard1.6`.  Questa impostazione è necessaria negli scenari con più destinazioni.

Successivamente, le istruzioni `using` nel file di origine possono essere modificate nel modo seguente:

```csharp
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
// This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif
```

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

E al centro dell'origine, è possibile inserire direttive `#if` per usare tali librerie in modo condizionale. Ad esempio:

```csharp
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
            
            return $"dotnetfoundation.orgmentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
```

Quando si crea un progetto che include `net40`, `net45` e `netstandard1.6` come framework nel file *project.json*, nella cartella */bin/debug* verranno incluse queste sottocartelle:

```
net40/
net45/
netstandard1.6/
```

### <a name="but-what-about-multitargeting-with-portable-class-libraries"></a>Definizione di più destinazioni con le librerie di classi portabili

Se si desidera eseguire la compilazione incrociata con una destinazione di libreria di classi portabile, è necessario aggiungere una definizione di compilazione nel file `project.json` sotto `buildOptions` nella destinazione di libreria di classi portabile.  È quindi possibile inserire nell'origine direttive `#if` che usano la definizione di compilazione come simbolo di preprocessore.

Ad esempio, se si vuole definire come destinazione il [profilo di libreria di classi portabile 328](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (.NET Framework 4, Windows 8, Windows Phone Silverlight 8, Windows Phone 8.1, Silverlight 5), è possibile fare riferimento a tale profilo come "PORTABLE328" durante la compilazione incrociata.  È sufficiente aggiungerlo al file `project.json` come attributo `buildOptions`:

```json
{
    "frameworks":{
        "netstandard1.6":{
           "dependencies":{
                "NETStandard.Library":"1.6.0",
            }
        },
        ".NETPortable,Version=v4.0,Profile=Profile328":{
            "buildOptions": {
                "define": [ "PORTABLE328" ]
            },
            "frameworkAssemblies":{
                "mscorlib":"",
                "System":"",
                "System.Core":"",
                "System.Net"
            }
        }
    }
}

```

A questo punto è possibile eseguire la compilazione condizionale rispetto a tale destinazione:

```csharp
#if !PORTABLE328
using System.Net.Http;
using System.Threading.Tasks;
// Potentially other namespaces which aren't compatible with Profile 328
#endif
```

Poiché `PORTABLE328` è ora riconosciuto dal compilatore, la libreria del profilo di libreria di classi portabile 328 generata da un compilatore non includerà `System.Net.Http` o `System.Threading.Tasks`.

Quando si crea un progetto che include il profilo di libreria di classi portabile 328 e `netstandard1.6` come framework nel file *project.json*, nella cartella */bin/debug* verranno incluse queste sottocartelle:

```
portable-net40+sl50+netcore45+wpa81+wp8/
netstandard1.6/
```

## <a name="how-to-use-native-dependencies"></a>Come usare le dipendenze native

Se si vuole scrivere una libreria che dipende da un file `.dll` nativo,  sono disponibili due opzioni:

1. Fare riferimento al file `.dll` nativo direttamente in `project.json`.
2. Includere il file `.dll` nello specifico pacchetto NuGet e definire una dipendenza da tale pacchetto.

Per la prima opzione, è necessario eseguire le operazioni seguenti nel file `project.json`:

1. Impostare `allowUnsafe` su `true` in una sezione `buildOptions`.
2. Specificare un [identificatore di runtime (RID)](../rid-catalog.md) in una sezione `runtimes`.
3. Specificare il percorso dei file `.dll` nativi a cui si fa riferimento.

Ecco un esempio di `project.json` per un file `.dll` nativo nella directory radice del progetto che viene eseguito in Windows:

```json
{
    "buildOptions":{
        "allowUnsafe":true
    },
    "runtimes":{
        "win10-x64":{}
    },
    "packOptions":{
        "files":{
            "mappings":{
                "runtimes/win10-x64/native":{
                    "includeFiles":[ "native-lib.dll"]
                }
            }            
        }
    }
}
```

Se si distribuisce la libreria come pacchetto, è consigliabile posizionare il file `.dll` a livello di radice del progetto.

Per la seconda opzione, è necessario creare un pacchetto NuGet esterno ai file `.dll`, eseguirne l'hosting su un feed MyGet o NuGet e definire una dipendenza diretta da tale pacchetto.  Sarà comunque necessario impostare `allowUnsafe` su `true` nella sezione `buildOptions` di `project.json`.  Di seguito è riportato un esempio (supponendo che `MyNativeLib` sia un pacchetto NuGet con versione `1.2.0`):

```json
{
    "buildOptions":{
        "allowUnsafe":true
    },
    "dependencies":{
        "MyNativeLib":"1.2.0"
    }
}
```

Per un esempio di creazione dei pacchetti di file binari nativi multipiattaforma, vedere [ASP.NET Libuv Package](https://github.com/aspnet/libuv-package) (Pacchetto Libuv ASP.NET) e il [riferimento corrispondente in KestrelHttpServer](https://github.com/aspnet/KestrelHttpServer/blob/1.0.0/src/Microsoft.AspNetCore.Server.Kestrel/project.json#L19).

## <a name="how-to-test-libraries-on-net-core"></a>Come testare le librerie in .NET Core

È importante essere in grado di eseguire test tra diverse piattaforme.  Lo strumento più semplice da usare è [xUnit](http://xunit.github.io/), che è anche lo strumento di test usato dai progetti .NET Core.  La modalità di configurazione della soluzione con progetti di test dipende dalla [struttura della soluzione](#structuring-a-solution).  L'esempio seguente presuppone che tutti i progetti di origine siano inclusi in una cartella `/src` di livello più alto e che tutti i progetti di test si trovino in una cartella `/test` di livello più alto.

1. Verificare di avere un file `global.json` a livello di soluzione in grado di riconoscere la posizione dei progetti di test:
    
    ```json
    {
        "projects":[ "src", "test"]
    }
    ```
    
    La struttura di cartelle della soluzione avrà quindi un aspetto simile al seguente:
    
    ```
    /SolutionWithSrcAndTest
    |__global.json
    |__/src
    |__/test
    ```
    
2. Definire un nuovo progetto di test creando una cartella di progetto all'interno della cartella `/test` e un file `project.json` nella nuova cartella di progetto.  Per creare il file `project.json` è possibile eseguire il comando `dotnet new` e modificare il file `project.json` in un secondo momento.  Il file deve includere gli elementi seguenti:

   * `netcoreapp1.0` elencato come unica voce sotto `frameworks`.
   * Un riferimento a `Microsoft.NETCore.App` versione `1.0.0`.
   * Un riferimento a xUnit versione `2.2.0-beta2-build3300`.
   * Un riferimento a `dotnet-test-xunit` versione `2.2.0-preview2-build1029`
   * Un riferimento di progetto alla libreria sottoposta a test.
   * La voce `"testRunner":"xunit"`.
   
   Di seguito è riportato un esempio (`LibraryUnderTest` versione `1.0.0` è la libreria sottoposta a test):
   
   ```json
   {
        "testRunner":"xunit",
        "dependencies":{
            "LibraryUnderTest":{
                "version":"1.0.0",
                "target":"project"
            },
            "Microsoft.NETCore.App":{
                "version":"1.0.0",
                "type":"platform"
            },
            "xunit":"2.2.0-beta2-build3300",
            "dotnet-test-xunit":"2.2.0-preview2-build1029",
        },
        "frameworks":{
            "netcoreapp1.0":{}
        }
   }
   ```
3. Ripristinare i pacchetti eseguendo `dotnet restore`.  Eseguire questa operazione a livello di soluzione se non si sono ancora ripristinati pacchetti.

4. Passare al progetto di test ed eseguire test con `dotnet test`:

    ```
    $ cd path-to-your-test-project
    $ dotnet test
    ```

L'operazione è ora completata.  È ora possibile testare la libreria su tutte le piattaforme usando gli strumenti da riga di comando.  Una volta completata la configurazione, è possibile procedere con il testing della libreria in modo molto semplice:

1. Eseguire le opportune modifiche nella libreria.
2. Eseguire i test dalla riga di comando, nella directory di test, usando il comando `dotnet test`.

Il codice viene ricompilato automaticamente quando si richiama il comando `dotnet test`.

Basta ricordare di eseguire `dotnet restore` dalla riga di comando ogni volta che si aggiunge una nuova dipendenza e si è pronti per iniziare.

## <a name="how-to-use-multiple-projects"></a>Come usare più progetti

Per le librerie di maggiori dimensioni, è spesso necessario inserire funzionalità in progetti diversi.

Si supponga di voler creare una libreria che sia utilizzabile in C# e F# idiomatico.  Ciò significa che la libreria viene utilizzata in modi che sono naturali per C# o F#.  In C#, ad esempio, la libreria può essere utilizzata in un modo simile al seguente:

```csharp
var convertResult = await AwesomeLibrary.ConvertAsync(data);
var result = AwesomeLibrary.Process(convertResult);
```  

In F#, invece, può assumere l'aspetto seguente:

```fsharp
let result =
    data
    |> AwesomeLibrary.convertAsync 
    |> Async.RunSynchronously 
    |> AwesomeLibrary.process
```

Scenari di utilizzo come questo indicano che le API a cui si accede devono avere una struttura diversa per C# e F#.  Un approccio comune per gestire questa situazione consiste nel definire l'intera logica di una libreria in un progetto di base, a cui eseguono chiamate i livelli di API definiti nei progetti C# e F#.  Nella parte restante della sezione verranno usati i nomi seguenti:

* **AwesomeLibrary.Core**: un progetto di base che contiene tutta la logica della libreria
* **AwesomeLibrary.CSharp**: un progetto con API pubbliche destinato all'utilizzo in C#
* **AwesomeLibrary.FSharp**: un progetto con API pubbliche destinato all'utilizzo in F#

### <a name="project-to-project-referencing"></a>Definizione di riferimenti da progetto a progetto

Il modo migliore per fare riferimento a un progetto è il seguente:

1. Verificare che il progetto a cui si vuole fare riferimento abbia un nome significativo per la rispettiva cartella sul disco.  Questo nome verrà usato per fare riferimento al progetto.
2. Fare riferimento al nome da (1) nel file `project.json` del progetto che utilizzerà la libreria specificando `"target":"project"`.

A questo punto, nei file `project.json` per **AwesomeLibrary.CSharp** e **AwesomeLibrary.FSharp** è necessario fare riferimento a **AwesomeLibrary.Core** come destinazione `project`.  Se non si definiscono più destinazioni, è possibile usare la voce `dependencies` globale:

```json
{
    "dependencies":{
        "AwesomeLibrary.Core":{
            "target":"project"
        }
    }
}
```

Se invece si definiscono più destinazioni, può non essere possibile usare una voce `dependencies` globale e può essere necessario fare riferimento a **AwesomeLibrary.Core** in una voce `dependencies` a livello di destinazione.  Ad esempio, se si definisce `netstandard1.6` come destinazione, è possibile eseguire questa operazione nel modo seguente:

```json
{
    "frameworks":{
        "netstandard1.6":{
            "dependencies":{
                "AwesomeLibrary.Core":{
                    "target":"project"
                }
            }
        }
    }
}
```

### <a name="structuring-a-solution"></a>Definizione della struttura di una soluzione

Un altro aspetto importante delle soluzioni basate su più progetti è quello di stabilire una buona struttura complessiva dei progetti. Per definire la struttura di una libreria con più progetti, è necessario usare le cartelle `/src` e `/test` di livello più alto:

```
/AwesomeLibrary
|__global.json
|__/src
   |__/AwesomeLibrary.Core
      |__Source Files
      |__project.json
   |__/AwesomeLibrary.CSharp
      |__Source Files
      |__project.json
   |__/AwesomeLibrary.FSharp
      |__Source Files
      |__project.json
|__/test
   |__/AwesomeLibrary.Core.Tests
      |__Test Files
      |__project.json
   |__/AwesomeLibrary.CSharp.Tests
      |__Test Files
      |__project.json
   |__/AwesomeLibrary.FSharp.Tests
      |__Test Files
      |__project.json
```

Il file `global.json` per questa soluzione avrà un aspetto simile al seguente:

```json
{
    "projects":["src", "test"]
}
```

Questo approccio segue lo stesso schema stabilito dai modelli di progetto nel comando `dotnet new`, dove tutti i progetti sono posizionati in una directory `/src` e tutti i test in una directory `/test`.

Ecco come è possibile ripristinare i pacchetti, compilare l'intero progetto e testarlo:

```
$ dotnet restore
$ cd src/AwesomeLibrary.FSharp
$ dotnet build
$ cd ../AwesomeLibrary.CSharp
$ dotnet build
$ cd ../../test/AwesomeLibrary.Core.Tests
$ dotnet test
$ cd ../AwesomeLibrary.CSharp.Tests
$ dotnet test
$ cd ../AwesomeLibrary.FSharp.Tests
$ dotnet test
```

L'operazione è ora completata.



<!--HONumber=Nov16_HO3-->


