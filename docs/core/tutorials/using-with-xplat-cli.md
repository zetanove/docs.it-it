---
title: Introduzione all&quot;uso di .NET Core su Windows/Linux/macOS dalla riga di comando
description: Introduzione all&quot;uso di .NET Core su Windows/Linux/macOS dall&quot;interfaccia della riga di comando di .NET Core
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: be988f09-7349-43b0-97fb-3a703d4587ce
translationtype: Human Translation
ms.sourcegitcommit: 37e14d5cdf1593f6a8b1ecee9d9828647b023548
ms.openlocfilehash: 5493ccb77e62d20d5101728ef8ab1744ea697fb8

---

# <a name="getting-started-with-net-core-on-windowslinuxmacos-using-the-command-line"></a>Introduzione all'uso di .NET Core su Windows/Linux/macOS dalla riga di comando

Questa guida illustra come usare gli strumenti dell'interfaccia della riga di comando di .NET Core per creare applicazioni console multipiattaforma di base.

Se non si ha familiarità con il set di strumenti dell'interfaccia della riga di comando di .NET Core, leggere [la panoramica di .NET Core SDK](../sdk.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di avere gli [strumenti più recenti dell'interfaccia della riga di comando di .NET Core](https://www.microsoft.com/net/core). È necessario anche un editor di testo.

## <a name="hello-console-app"></a>Creazione di un'applicazione console

Passare a un'altra cartella e crearne una nuova con il nome desiderato. "Hello" è il nome selezionato per il codice di esempio, che è possibile trovare [qui](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/Hello).

Aprire un prompt dei comandi e digitare quanto segue:

```
$ dotnet new
$ dotnet restore
$ dotnet run
```

Ecco una descrizione rapida dei comandi digitati:

1. `$ dotnet new`

   [`dotnet new`](../tools/dotnet-new.md) crea un file `project.json` aggiornato con le dipendenze NuGet necessarie per compilare un'applicazione console.  Crea inoltre un file `Program.cs` di base contenente il punto di ingresso per l'applicazione.
   
   `project.json`:
   ```json
   {
        "version": "1.0.0-*",
        "buildOptions": {
            "emitEntryPoint": true
        },
        "dependencies": {
            "Microsoft.NETCore.App": {
                "type": "platform",
                "version": "1.0.0"
            }
        },   
       "frameworks": {
            "netcoreapp1.0": {
                "imports": "dnxcore50"
            }
        }
   }
   ```
   `Program.cs`:
   ```csharp
   using System;

   namespace ConsoleApplication
   {
       public class Program
       {
           public static void Main(string[] args)
           {
               Console.WriteLine("Hello World!");
           }
       }
   }
   ```

2. `$ dotnet restore`

   [`dotnet restore`](../tools/dotnet-restore.md) esegue una chiamata a NuGet per ripristinare l'albero delle dipendenze. NuGet analizza il file `project.json`, scarica le dipendenze indicate nel file (o li estrae da una cache nel computer) e scrive il file `project.lock.json`.  Il file `project.lock.json` è necessario per la compilazione e l'esecuzione.
   
   Il file `project.lock.json` è un set completo e persistente del grafico delle dipendenze NuGet e include altre informazioni che descrivono un'applicazione.  Questo file viene letto da altri strumenti, ad esempio `dotnet build` e `dotnet run`, che possono quindi elaborare il codice sorgente con un set corretto di risoluzioni di binding e dipendenze NuGet.
   
3. `$ dotnet run`

   [`dotnet run`](../tools/dotnet-run.md) chiama `dotnet build` per assicurarsi che le destinazioni siano state compilate e quindi chiama `dotnet <assembly.dll>` per eseguire l'applicazione di destinazione.
   
```
$ dotnet run
Hello, World!
```

È inoltre possibile eseguire [`dotnet build`](../tools/dotnet-build.md) per compilare il codice senza eseguire la compilazione di applicazioni console.

### <a name="building-a-self-contained-application"></a>Compilazione di un'applicazione autonoma

In questa sezione si proverà a compilare un'applicazione autonoma anziché un'applicazione portabile. È possibile leggere altre informazioni sui [tipi di portabilità in .NET Core](../deploying/index.md) per conoscere i diversi tipi di applicazione e il modo in cui vengono distribuiti.

È necessario apportare alcune modifiche al file `project.json` per indicare agli strumenti di compilare un'applicazione autonoma. Le modifiche richieste sono illustrate nel progetto [HelloNative](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/HelloNative) nella directory degli esempi.

La prima modifica consiste nel rimuovere l'elemento `"type": "platform"` da tutte le dipendenze. Finora, l'unica dipendenza del progetto è `"Microsoft.NETCore.App"`. La sezione `dependencies` assumerà un aspetto simile al seguente:

```json
"dependencies": {
    "Microsoft.NETCore.App": {
        "version": "1.0.0"
    }
},
```

Successivamente, è necessario aggiungere un nodo `runtimes` per specificare tutti gli ambienti di esecuzione di destinazione. Ad esempio, il nodo `runtimes` seguente indica al sistema di compilazione di creare file eseguibili per la versione a 64 bit di Windows 10 e la versione a 64 bit di Mac OS X 10.11.
Il sistema di compilazione genererà file eseguibili nativi per l'ambiente corrente. Se si seguono questi passaggi in un computer Windows, verrà creato un file eseguibile per Windows. Se si seguono questi passaggi in un computer Mac, verrà creato un file eseguibile per OS X.

```json 
"runtimes": {
  "win10-x64": {},
  "osx.10.11-x64": {}
}
```

Visualizzare l'elenco completo dei runtime supportati nel [catalogo RID](../rid-catalog.md). 
 
Dopo aver apportato queste due modifiche, eseguire `dotnet restore`, seguito da `dotnet build` per creare il file eseguibile nativo. Sarà quindi possibile eseguire il file eseguibile nativo generato. 

L'esempio seguente mostra i comandi per Windows. Nell'esempio è indicato il percorso in cui viene generato il file eseguibile nativo e si presuppone che la directory del progetto sia denominata HelloNative.

```
$ dotnet restore 
$ dotnet build 
$ .\bin\Debug\netcoreapp1.0\win10-x64\HelloNative.exe
Hello World!
```

È possibile notare che l'applicazione nativa richiede leggermente più tempo per la compilazione, ma viene eseguita con una velocità leggermente maggiore. Questo comportamento diventa più evidente con la crescita delle dimensioni dell'applicazione.

Il processo di compilazione genera alcuni altri file quando `project.json` crea una build nativa. Questi file vengono creati in `bin\Debug\netcoreapp1.0\<platform>`, dove `<platform>` è il RID selezionato. Oltre al file `HelloNative.dll` del progetto è presente un file `HelloNative.exe` che carica il runtime e avvia l'applicazione.
Si noti che il nome dell'applicazione generata è cambiato in base al nuovo nome della directory del progetto.  

Può essere opportuno creare un pacchetto dell'applicazione per eseguirlo in un computer che non include il runtime .NET.
Per ottenere questo risultato, eseguire il comando `dotnet publish`. Il comando `dotnet publish` crea una nuova sottodirectory denominata `publish` all'interno della directory `./bin/Debug/netcoreapp1.0/<platform>`. Copia il file eseguibile, tutte le DLL dipendenti e il framework in questa sottodirectory. È possibile creare un pacchetto di tale directory e trasferirlo in un altro computer (o in un contenitore) e quindi eseguire l'applicazione da tale posizione. 

Si metta a confronto questo comportamento con quello di `dotnet publish` nel primo esempio Hello World. In tale esempio, l'applicazione è di tipo *portabile*, ovvero il tipo predefinito delle applicazioni per .NET Core. Per un'applicazione portabile è necessario che .NET Core sia installato nel computer di destinazione. Le applicazioni portabili possono essere compilate in un computer ed eseguite da un'altra postazione. Le applicazioni native devono essere compilate separatamente per ogni computer di destinazione. `dotnet publish` crea una directory con la DLL dell'applicazione ed eventuali DLL dipendenti che non fanno parte dell'installazione della piattaforma.

### <a name="augmenting-the-program"></a>Possibilità di espansione del programma

È possibile apportare modifiche al file del programma.  Ad esempio, si può provare a inserire i numeri di Fibonacci (usando la versione nativa):

`Program.cs`:

```csharp
using static System.Console;

namespace ConsoleApplication
{
    public class Program
    {
        public static int FibonacciNumber(int n)
        {
            int a = 0;
            int b = 1;
            int tmp;
            
            for (int i = 0; i < n; i++)
            {
                tmp = a;
                a = b;
                b += tmp;
            }
            
            return a;   
        }
        
        public static void Main(string[] args)
        {
            WriteLine("Hello World!");
            WriteLine("Fibonacci Numbers 1-15:");
            
            for (int i = 0; i < 15; i++)
            {
                WriteLine($"{i+1}: {FibonacciNumber(i)}");
            }
        }
    }
}
```

E quindi eseguire il programma (si presuppone che il file venga eseguito in Windows e il nome della directory del progetto è stato modificato in Fibonacci):

```
$ dotnet build
$ .\bin\Debug\netcoreapp1.0\win10-x64\Fibonacci.exe
1: 0
2: 1
3: 1
4: 2
5: 3
6: 5
7: 8
8: 13
9: 21
10: 34
11: 55
12: 89
13: 144
14: 233
15: 377
```

L'operazione è ora completata.  `Program.cs` offre innumerevoli possibilità di espansione.

## <a name="adding-some-new-files"></a>Aggiunta di nuovi file

Per i programmi semplici sono sufficienti singoli file, ma è probabile che sia opportuno suddividere il codice in più file se si creano programmi con più componenti.  Un progetto con più file può offrire una buona soluzione.

Creare un nuovo file e assegnargli uno spazio dei nomi univoco:

```csharp
using System;

namespace NumberFun
{
    // code can go here
} 
```

Includerlo quindi nel file `Program.cs`:

```csharp
using static System.Console;
using NumberFun;
```

E infine eseguire la compilazione:

`$ dotnet build`

A questo punto è possibile passare alla parte più divertente della procedura: rendere operativo il nuovo file.

### <a name="example-a-fibonacci-sequence-generator"></a>Esempio: Generatore della sequenza di Fibonacci

Si supponga di voler sviluppare il precedente [esempio di sequenza di Fibonacci](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/Fibonacci) memorizzando nella cache alcuni valori di Fibonacci e aggiungendo alcune ricorsività.  Il codice per un [esempio di sequenza di Fibonacci migliore](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/FibonacciBetter) potrebbe avere un aspetto simile al seguente:

```csharp
using System;
using System.Collections.Generic;

namespace NumberFun
{
    public class FibonacciGenerator
    {
        private Dictionary<int, int> _cache = new Dictionary<int, int>();
        
        private int Fib(int n) => n < 2 ? n : FibValue(n - 1) + FibValue(n - 2);
        
        private int FibValue(int n)
        {
            if (!_cache.ContainsKey(n))
            {
                _cache.Add(n, Fib(n));
            }
            
            return _cache[n];
        }
        
        public IEnumerable<int> Generate(int n)
        {
            for (int i = 0; i < n; i++)
            {
                yield return FibValue(i);
            }
        }
    }
}
```

Si noti che l'uso di `Dictionary<int, int>` e `IEnumerable<int>` implica l'inclusione dello spazio dei nomi `System.Collections`.
Il pacchetto `Microsoft.NetCore.App` è un *metapacchetto* che contiene molti degli assembly principali di .NET Framework. Se si include questo metapacchetto, l'assembly `System.Collections.dll` risulterà già incluso nel progetto. È possibile verificarlo eseguendo `dotnet publish` ed esaminando i file che fanno parte del pacchetto installato. `System.Collections.dll` risulterà incluso nell'elenco. 

```json
{ 
  "version": "1.0.0-*", 
  "buildOptions": { 
    "debugType": "portable", 
    "emitEntryPoint": true 
  }, 
  "dependencies": {}, 
  "frameworks": { 
    "netcoreapp1.0": { 
      "dependencies": { 
        "Microsoft.NETCore.App": { 
          "version": "1.0.0" 
        } 
      }, 
      "imports": "dnxcore50" 
    } 
  },
  "runtimes": {
    "win10-x64": {},
    "osx.10.11-x64": {}
  }
}
```

A questo punto, modificare il metodo `Main()` nel file `Program.cs`, come illustrato di seguito. L'esempio presuppone che `Program.cs` abbia un'istruzione `using System;`. Se è presente un' istruzione `using static System.Console;`, rimuovere `Console.` da `Console.WriteLine`.  

```csharp
public static void Main(string[] args)
{
    var generator = new FibonacciGenerator();
    foreach (var digit in generator.Generate(15))
    {
        WriteLine(digit);
    }
}
```

Infine, eseguire l'applicazione.

```
$ dotnet run
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

L'operazione è ora completata.

## <a name="using-folders-to-organize-code"></a>Uso di cartelle per organizzare il codice

Si supponga di voler introdurre alcuni nuovi tipi su cui lavorare.  A tale scopo è possibile aggiungere altri file assicurandosi di assegnare loro spazi dei nomi che possono essere inclusi nel file `Program.cs`.

```
/MyProject
|__Program.cs
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__project.json
```

Questa è un'ottima soluzione quando le dimensioni del progetto sono relativamente piccole.  Tuttavia, se si ha un'applicazione più grande con molti tipi di dati diversi e potenzialmente più livelli, può essere opportuno organizzare i dati in maniera logica.  A questo punto entrano in gioco le cartelle.  È possibile seguire [il progetto di esempio NewTypes](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypes) descritto in questa guida o creare file e cartelle personalizzati.

Per iniziare, creare una nuova cartella sotto la radice del progetto.  `/Model` è la cartella scelta in questo esempio.

```
/NewTypes
|__/Model
|__Program.cs
|__project.json
```

Aggiungere ora alcuni nuovi tipi nella cartella:

```
/NewTypes
|__/Model
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__Program.cs
|__project.json
```

Come per i file presenti in una stessa directory, assegnare a tutti i tipi lo stesso spazio dei nomi in modo da poterli includere in `Program.cs`.

### <a name="example-pet-types"></a>Esempio: Tipi di animali domestici

In questo esempio vengono creati due nuovi tipi, `Dog` e `Cat`, che implementano un'interfaccia, `IPet`.

Struttura di cartelle:

```
/NewTypes
|__/Pets
   |__Dog.cs
   |__Cat.cs
   |__IPet.cs
|__Program.cs
|__project.json
```

`IPet.cs`:
```csharp
using System;

namespace Pets
{
    public interface IPet
    {
        string TalkToOwner();
    }
}
```

`Dog.cs`:
```csharp
using System;

namespace Pets
{
    public class Dog : IPet
    {
        public string TalkToOwner() => "Woof!";
    }
}
```

`Cat.cs`:
```csharp
using System;

namespace Pets
{
    public class Cat : IPet
    {
        public string TalkToOwner() => "Meow!";
    }
}
```

`Program.cs`:
```csharp
using System;
using Pets;
using System.Collections.Generic;

namespace ConsoleApplication
{
    public class Program
    {
        public static void Main(string[] args)
        {
            List<IPet> pets = new List<IPet>
            {
                new Dog(),
                new Cat()  
            };
            
            foreach (var pet in pets)
            {
                Console.WriteLine(pet.TalkToOwner());
            }
        }
    }
}
```

`project.json`:
```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "emitEntryPoint": true
  },
  "dependencies": {
    "Microsoft.NETCore.App": {
      "type": "platform",
      "version": "1.0.0"
    }
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": "dnxcore50"
    }
  }
}
```

E se si esegue questo codice:

```
$ dotnet restore
$ dotnet run
Woof!
Meow!
```

È possibile aggiungere nuovi tipi di animali domestici (come `Bird`) estendendo il progetto.

## <a name="testing-your-console-app"></a>Test dell'applicazione console

È probabile che a un certo punto si decida di testare i progetti.  Ecco un buon metodo per eseguire questa operazione:

1. Spostare l'origine del progetto esistente in una nuova cartella `src`.

   ```
   /Project
   |__/src
   ```

2. Creare una directory `/test`.

   ```
   /Project
   |__/src
   |__/test
   ```

3. Creare un nuovo file `global.json`:

   ```
   /Project
   |__/src
   |__/test
   |__global.json
   ```

   `global.json`:
   ```json
   {
      "projects": [
         "src", "test"
      ]
   }
   ```

   Il file indica al sistema di compilazione che il sistema è basato più progetti. È quindi possibile cercare le dipendenze in più percorsi e non soltanto nella cartella corrente su cui è in esecuzione.  Questo è importante perché consente di inserire una dipendenza sul codice da testare nel progetto di test.
   
### <a name="example-extending-the-newtypes-project"></a>Esempio: Estensione del progetto NewTypes

Ora che il sistema del progetto è stato creato, è possibile creare il progetto di test e iniziare a scrivere i test.  A partire da questo punto, nella guida verrà usato ed esteso [il progetto NewTypes di esempio](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypes).  Inoltre, verrà usato il framework di test [xUnit](https://xunit.github.io/).  È possibile proseguire o creare un sistema personalizzato basato su più progetti con test.


La struttura dell'intero progetto avrà un aspetto simile al seguente:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__project.json
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__project.json
|__global.json
```

È necessario verificare che nel progetto di test siano presenti due nuovi elementi:

1. Un file `project.json` corretto con i riferimenti seguenti:

   * Un riferimento a `xunit`
   * Un riferimento a `dotnet-test-xunit`
   * Un riferimento allo spazio dei nomi corrispondente al codice sottoposto a test

2. Una classe di test xUnit.

`NewTypesTests/project.json`:
```json
{
  "version": "1.0.0-*",
  "testRunner": "xunit",

  "dependencies": {
    "Microsoft.NETCore.App": {
      "type":"platform",
      "version": "1.0.0"
    },
    "xunit":"2.2.0-beta2-build3300",
    "dotnet-test-xunit": "2.2.0-preview2-build1029",
    "NewTypes": "1.0.0"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "portable-net45+win8" 
      ]
    }
  }
}
```

`PetTests.cs`: 
```csharp
using System;
using Xunit;
using Pets;
public class PetTests
{
    [Fact]
    public void DogTalkToOwnerTest()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();
        
        Assert.Equal(expected, actual);
    }
    
    [Fact]
    public void CatTalkToOwnerTest()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();
        
        Assert.Equal(expected, actual);
    }
}
```
   
A questo punto è possibile eseguire i test.  Il comando [`dotnet test`](../tools/dotnet-test.md) esegue il Test Runner specificato nel progetto. Assicurarsi di iniziare dalla directory di livello più alto.
 
```
$ dotnet restore
$ cd test/NewTypesTests
$ dotnet test
```
 
L'output dovrebbe essere simile al seguente:
 
```
xUnit.net .NET CLI test runner (64-bit win10-x64)
  Discovering: NewTypesTests
  Discovered:  NewTypesTests
  Starting:    NewTypesTests
  Finished:    NewTypesTests
=== TEST EXECUTION SUMMARY ===
   NewTypesTests  Total: 2, Errors: 0, Failed: 0, Skipped: 0, Time: 0.144s
SUMMARY: Total: 1 targets, Passed: 1, Failed: 0.
```
 
## <a name="conclusion"></a>Conclusione
 
Questa guida ha illustrato le procedure per creare un'applicazione console .NET Core, a partire dalle funzionalità di base fino a un sistema basato su più progetti con unit test.  Il passaggio successivo sarà quello di creare eccezionali applicazioni console personalizzate.
 
Per un esempio più avanzato di un'applicazione console, esaminare l'esercitazione successiva: [Scrittura di applicazioni console .NET Core mediante gli strumenti dell'interfaccia della riga di comando: guida dettagliata avanzata](cli-console-app-tutorial-advanced.md).



<!--HONumber=Nov16_HO3-->


