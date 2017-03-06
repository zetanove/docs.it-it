---
title: Introduzione all&quot;uso di .NET Core su Windows/Linux/macOS dalla riga di comando (strumenti di .NET Core RC4) | Microsoft Docs
description: Introduzione all&quot;uso di .NET Core su Windows/Linux/macOS dall&quot;interfaccia della riga di comando di .NET Core
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 41632e63-d5c6-4427-a09e-51dc1116d45f
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 4c17da61f492e17edf4d69d79be430ead3dd0cc6

---

# <a name="getting-started-with-net-core-on-windowslinuxmacos-using-the-command-line-net-core-tools-rc4"></a>Introduzione all'uso di .NET Core su Windows/Linux/macOS dalla riga di comando (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [Introduzione all'uso di .NET Core su Windows/Linux/macOS dalla riga di comando](../../tutorials/using-with-xplat-cli.md).

Questa guida illustra come usare gli strumenti dell'interfaccia della riga di comando di .NET Core per creare applicazioni console multipiattaforma.  Si inizia con un'applicazione console molto semplice per poi passare a più progetti, incluso un progetto di test. Le funzionalità verranno illustrate in maniera graduale, aggiungendo nuove informazioni sulla base di quelle già acquisite.

Se non si ha familiarità con il set di strumenti dell'interfaccia della riga di comando di .NET Core, leggere [la panoramica di .NET Core SDK](../tools/dotnet.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare, assicurarsi di avere la [versione RC4 o una versione successiva degli strumenti dell'interfaccia della riga di comando di .NET Core](https://github.com/dotnet/core/blob/master/release-notes/preview3-download.md).  È necessario anche un editor di testo.

## <a name="hello-console-app"></a>Creazione di un'applicazione console

Innanzitutto, passare a un'altra cartella e crearne una nuova con il nome desiderato.  "Hello" è il nome selezionato per il codice di esempio, che è possibile trovare [qui](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/HelloMsBuild).

Aprire un prompt dei comandi e digitare quanto segue:

```
$ dotnet new
$ dotnet restore
$ dotnet run
```

Ecco una descrizione rapida dei comandi digitati:

1. `$ dotnet new`

   [`dotnet new`](../tools/dotnet-new.md) crea un file di progetto `Hello.csproj` aggiornato con le dipendenze necessarie per compilare un'applicazione console.  Crea inoltre un file `Program.cs` di base contenente il punto di ingresso per l'applicazione.
   
   `Hello.csproj`:
   ```xml
    <Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
        <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
        
        <PropertyGroup>
            <OutputType>Exe</OutputType>
            <TargetFramework>netcoreapp1.0</TargetFramework>
        </PropertyGroup>

        <ItemGroup>
            <Compile Include="**\*.cs" />
            <EmbeddedResource Include="**\*.resx" />
        </ItemGroup>

        <ItemGroup>
            <PackageReference Include="Microsoft.NETCore.App">
                <Version>1.0.1</Version>
            </PackageReference>
            <PackageReference Include="Microsoft.NET.Sdk">
                <Version>1.0.0-alpha-20161104-2</Version>
                <PrivateAssets>All</PrivateAssets>
            </PackageReference>
        </ItemGroup>
        
        <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
    </Project>
   ```

   Il file di progetto specifica tutti gli elementi necessari per recuperare le dipendenze e compilare il programma.

   * Il tag `Import` introduce alcune proprietà comuni a tutti i progetti .NET Core.
   * Il tag `OutputType` specifica che si sta compilando un file eseguibile, ovvero un'applicazione console.
   * Il tag `TargetFramework` specifica il runtime .NET di destinazione. In uno scenario avanzato è possibile specificare più framework di destinazione ed eseguire la compilazione per ciascuno di essi in un'unica operazione. In questa esercitazione verrà illustrata la procedura di compilazione solo per .NET Core 1.0.
   * Il tag `Compile` indica al compilatore di generare tutti i file nella directory corrente e in tutte le relative sottodirectory con estensione `.cs`, ovvero in tutti i file C# del progetto. Negli scenari avanzati è possibile escludere alcuni file, ma in questa esercitazione e nella maggior parte degli scenari semplici questa riga può essere lasciata invariata.
   * Il tag `EmbeddedResource` indica al sistema di compilazione di incorporare i file di localizzazione con estensione `.resx` nel file eseguibile compilato. Nell'esercitazione corrente questa funzionalità non verrà usata.
   * Il tag `PackageReference` specifica quali pacchetti di dipendenze devono essere ripristinati e inclusi durante la compilazione dell'applicazione. Ogni riferimento di pacchetto specifica il nome del pacchetto associato all'attributo `Include` e un numero di versione. Negli scenari più avanzati è possibile aggiungere altri riferimenti di pacchetti e fare riferimento ad altri progetti su disco.

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

   Il programma inizia con `using System`, che significa "porta tutti gli elementi presenti nello spazio dei nomi `System` nell'ambito relativo a questo file". Lo spazio dei nomi `System` include costrutti di base come `string` o tipi numerici.

   È quindi necessario definire uno spazio dei nomi denominato "ConsoleApplication". È comunque possibile modificare il nome secondo le proprie esigenze. All'interno dello spazio dei nomi viene definita una classe denominata "Program" con un metodo `Main` che accetta come argomento una matrice di stringhe. Nella matrice sarà contenuto l'elenco degli argomenti che verranno passati nel momento in cui verrà chiamato il programma compilato. Così com'è, questa matrice non viene usata: il programma, infatti, si limita a scrivere "Hello World!" nella console. Per rendere la procedura più interessante è possibile modificare `Console.WriteLine` nel codice seguente.

   ```csharp
   if (args.Length > 0)
   {
       Console.WriteLine($"Hello {args[0]}!");
   }
   else
   {
       Console.WriteLine("Hello World!");
   }
   ```

2. `$ dotnet restore`

   [`dotnet restore`](../tools/dotnet-restore.md) esegue una chiamata a [NuGet](http://nuget.org) (il gestore di pacchetti per .NET) per ripristinare l'albero delle dipendenze. NuGet analizza il file `Hello.csproj`, scarica le dipendenze indicate nel file (o li estrae da una cache nel computer) e scrive il file `obj/project.assets.json`.  Il file `project.assets.json` è necessario per la compilazione e l'esecuzione.
   
   Il file `project.assets.json` è un set completo e persistente del grafico delle dipendenze NuGet e include altre informazioni che descrivono un'applicazione.  Questo file viene letto da altri strumenti, ad esempio `dotnet build` e `dotnet run`, che possono quindi elaborare il codice sorgente con un set corretto di risoluzioni di binding e dipendenze NuGet.
   
3. `$ dotnet run`

   [`dotnet run`](../tools/dotnet-run.md) chiama `dotnet build` per assicurarsi che le destinazioni siano state compilate e quindi chiama `dotnet <assembly.dll>` per eseguire l'applicazione di destinazione.
   
    ```
    $ dotnet run
    Hello World!
    ```

    In alternativa, è possibile eseguire [`dotnet build`](../tools/dotnet-build.md) per compilare il codice senza eseguire la compilazione di applicazioni console. In questo caso si ottiene un'applicazione compilata `bin/Debug/netcoreapp1.0/Hello.dll` che può essere eseguita con `dotnet bin\Debug\netcoreapp1.0\Hello.dll` in Windows e con `dotnet bin/Debug/netcoreapp1.0/Hello.dll` in altri sistemi. È possibile specificare un parametro aggiuntivo nella riga di comando (presupponendo che sia in esecuzione Windows):

    ```
    $ dotnet bin\Debug\netcoreapp1.0\Hello.dll .NET
    Hello .NET!
    ```

    Come scenario avanzato, è possibile compilare l'applicazione come un set indipendente di file specifici della piattaforma che può essere distribuito ed eseguito anche in computer in cui non è installato .NET Core. Per informazioni dettagliate, vedere [Distribuzione di applicazioni .NET Core](../deploying/index.md).

### <a name="augmenting-the-program"></a>Possibilità di espansione del programma

È possibile apportare modifiche al file del programma.  Ad esempio, si può provare a inserire i numeri di Fibonacci:

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
$ dotnet bin\Debug\netcoreapp1.0\win10-x64\Fibonacci.exe
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
using NumberFun;
```

E infine eseguire la compilazione:

`$ dotnet build`

A questo punto è possibile passare alla parte più divertente della procedura: rendere operativo il nuovo file.

### <a name="example-a-fibonacci-sequence-generator"></a>Esempio: Generatore della sequenza di Fibonacci

Si supponga di voler sviluppare il precedente esempio di sequenza di Fibonacci memorizzando nella cache alcuni valori di Fibonacci e aggiungendo alcune ricorsività.  Il codice per un [esempio di sequenza di Fibonacci migliore](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/FibonacciBetterMsBuild) potrebbe usare un nuovo file `FibonacciGenerator.cs` con il codice seguente.

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

A questo punto, modificare il metodo `Main()` nel file `Program.cs`, come illustrato di seguito.

```csharp
using System;
using NumberFun;

class Program
{
    static void Main(string[] args)
    {
        var generator = new FibonacciGenerator();
        foreach (var digit in generator.Generate(15))
        {
            Console.WriteLine(digit);
        }
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

## <a name="conclusion"></a>Conclusione
 
Questa guida ha illustrato le procedure per creare un'applicazione console .NET Core, a partire dalle funzionalità di base fino a un sistema basato su più progetti con unit test.  Il passaggio successivo sarà quello di creare eccezionali applicazioni console personalizzate.
 
Per un esempio di app console più avanzato, vedere l'esercitazione successiva: [Organizzazione e testing dei progetti con la riga di comando di .NET Core (strumenti di .NET Core RC4)](using-with-xplat-cli-msbuild-folders.md).



<!--HONumber=Feb17_HO2-->


