---
title: Distribuzione di applicazioni .NET Core | Microsoft Docs
description: Distribuzione di applicazioni .NET Core
keywords: .NET, .NET Core, distribuzione di .NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: da7a31a0-8072-4f23-82aa-8a19184cb701
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 0e186665619bd76c5ba3d1e605b885a12aa15c66
ms.lasthandoff: 03/07/2017

---

# <a name="net-core-application-deployment"></a>Distribuzione di applicazioni .NET Core

È possibile creare due tipi di distribuzioni per le applicazioni .NET Core: 

- Distribuzione dipendente dal framework. Come suggerisce il nome, la distribuzione dipendente dal framework si basa su una versione condivisa a livello di sistema di .NET Core che deve essere presente nel sistema di destinazione. Poiché .NET Core è già presente, l'app è anche portabile tra le installazioni di .NET Core. L'app contiene solo il proprio codice e le dipendenze di terze parti non sono comprese nelle librerie di .NET Core. Le distribuzioni dipendenti dal framework contengono i file con estensione dll che possono essere avviati dalla riga di comando tramite l'[utilità dotnet](../tools/dotnet.md). Ad esempio, `dotnet app.dll` esegue un'applicazione denominata `app`.

- Distribuzione autonoma. A differenza delle distribuzioni dipendenti dal framework, una distribuzione autonoma non si basa su tutti i componenti condivisi presenti nel sistema di destinazione. Tutti i componenti, inclusi librerie e runtime di .NET Core, sono inclusi nell'applicazione e isolati dalle altre applicazioni .NET Core. Le distribuzioni autonome includono un file eseguibile (ad esempio `app.exe` su piattaforme Windows per un'applicazione denominata `app`), che è una versione rinominata dell'host .NET Core specifico della piattaforma, e un file con estensione dll (ad esempio `app.dll`), che indica l'applicazione.

## <a name="framework-dependent-deployments-fdd"></a>Distribuzioni dipendenti dal framework ##

Per una distribuzione dipendente dal framework, viene distribuita solo l'app e le dipendenze di terze parti. Non è necessario distribuire .NET Core, poiché l'app userà la versione di .NET Core presente nel sistema di destinazione. Si tratta del modello di distribuzione predefinito per le app .NET Core.

### <a name="why-create-a-framework-dependent-deployment"></a>Perché creare una distribuzione dipendente dal framework? ###

Una distribuzione dipendente dal framework offre numerosi vantaggi:

- Non è necessario definire in anticipo i sistemi operativi di destinazione in cui verrà eseguita l'app .NET Core. Poiché .NET Core usa un formato di file PE comune per gli eseguibili e le librerie indipendentemente dal sistema operativo, .NET Core può eseguire l'app indipendentemente dal sistema operativo sottostante. Per altre informazioni sul formato di file PE, vedere [.NET Assembly File Format](../../standard/assembly-format.md) (Formato del file di assembly .NET).

- La dimensione del pacchetto di distribuzione è ridotta. È sufficiente distribuire l'app e le relative dipendenze, non .NET Core.

- Più app usano la stessa installazione di .NET Core, in questo modo si riduce sia lo spazio su disco sia l'utilizzo della memoria nei sistemi host.

Sono presenti anche alcuni svantaggi:

- L'app può essere eseguita solo se la versione di .NET Core di destinazione, o una versione successiva, è già installata nel sistema host.

- Nelle versioni successive è possibile che il runtime e le librerie di .NET Core vengano modificate senza notificare l'utente. In rari casi, questo scenario può comportare la modifica del comportamento dell'app.

### <a name="deploying-a-framework-dependent-deployment"></a>Pubblicazione di una distribuzione dipendente dal framework ###

Una distribuzione dipendente dal framework senza dipendenze di terze parti richiede la compilazione, il testing e la pubblicazione dell'app. Il processo viene illustrato da un semplice esempio scritto in C#. L'esempio usa l'[utilità dotnet](../tools/dotnet.md) dalla riga di comando; tuttavia, è possibile usare anche un ambiente di sviluppo, come Visual Studio o Visual Studio Code, per compilare, testare e pubblicare l'esempio.

1. Creare una directory per il progetto e, nella riga di comando, digitare `[dotnet new console](../tools/dotnet-new.md)` per creare un nuovo progetto console C#.

2. Aprire il file `Program.cs` in un editor e sostituire il codice generato automaticamente con il codice seguente. Richiede all'utente di immettere il testo e quindi visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

    ```cs
    using System;
    using System.Text.RegularExpressions;

    namespace Applications.ConsoleApps
    {
        public class ConsoleParser
        {
            public static void Main()
            {
                 Console.WriteLine("Enter any text, followed by <Enter>:\n");
                 String s = Console.ReadLine();
                 ShowWords(s);
                 Console.Write("\nPress any key to continue... ");
                 Console.ReadKey();
          }

          private static void ShowWords(String s)
          {
              String pattern = @"\w+";
              var matches = Regex.Matches(s, pattern);
              if (matches.Count == 0)
                  Console.WriteLine("\nNo words were identified in your input.");
              else
              {
                  Console.WriteLine("\nThere are {0} words in your string:", matches.Count);
                  for (int ctr = 0; ctr < matches.Count; ctr++)
                      Console.WriteLine("   #{0,2}: '{1}' at position {2}", ctr,
                                        matches[ctr].Value, matches[ctr].Index);
              }
          }
      }
    }
    ```

3. Eseguire il comando [dotnet-restore](../tools/dotnet-restore.md) per ripristinare le dipendenze specificate nel progetto.

4. Creare una build di debug dell'app usando il comando [dotnet-build](../tools/dotnet-build.md).

5. Dopo aver eseguito il debug e aver testato il programma, è possibile creare i file da distribuire con l'app usando il comando `dotnet publish -f netcoreapp1.1 -c release`. In questo modo, viene creata la versione finale dell'app (anziché un debug).

   I file risultanti vengono inseriti in una directory denominata `publish` che si trova in una sottodirectory della sottodirectory del progetto `.\bin\release\netcoreapp1.1`.

6. Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è particolarmente utile per il debug di eccezioni. È possibile scegliere di non inserirlo nel pacchetto dei file dell'applicazione.

Il set completo dei file dell'applicazione può essere distribuito in qualsiasi modo. Ad esempio, è possibile inserirli in un file zip, usare un semplice comando `copy` o distribuirli con qualsiasi pacchetto di installazione di propria scelta.

Oltre ai file binari dell'applicazione, il programma di installazione deve anche aggregare il programma di installazione di framework condiviso oppure cercarlo come prerequisito come parte dell'installazione dell'applicazione.  L'installazione del framework condiviso richiede l'accesso amministratore o alla radice perché è a livello di computer.

### <a name="deploying-a-framework-dependent-deployment-with-third-party-dependencies"></a>Pubblicazione di una distribuzione dipendente dal framework con dipendenze di terze parti ###

Una distribuzione dipendente dal framework con una o più dipendenze di terze parti prevede tre passaggi aggiuntivi prima di poter eseguire il comando `dotnet restore`:

1. Aggiungere i riferimenti alle librerie di terze parti alla sezione `<ItemGroup>` del file `csproj`. La sezione `<ItemGroup>` seguente descrive l'elemento `<ItemGroup>` contenente le dipendenze nel progetto predefinito con Json.NET come libreria di terze parti.

    ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
      </ItemGroup>
    ```

 Si noti che la dipendenza dell'SDK rimane nell'esempio precedente. Si tratta di un'impostazione predefinita, in quanto questa dipendenza è necessaria per ripristinare tutte le destinazioni necessarie per consentire il funzionamento degli strumenti della riga di comando.  

2. Se non lo si è già fatto, scaricare il pacchetto NuGet contenente la dipendenza di terze parti. Per scaricare il pacchetto, eseguire il comando `dotnet restore` dopo l'aggiunta della dipendenza. Poiché la dipendenza viene risolta dalla cache NuGet locale in fase di pubblicazione, deve essere disponibile nel sistema.

Si noti che la portabilità di una distribuzione dipendente dal framework con dipendenze di terze parti dipenderà dalle relative dipendenze. Ad esempio, se una libreria di terze parti supporta solo macOS, l'app non sarà portabile in sistemi Windows. Questa situazione può verificarsi se la dipendenza di terze parti stessa dipende dal codice nativo. Un esempio valido è il server Kestrel. Quando viene creata una distribuzione dipendente dal framework per un'applicazione con questo tipo di dipendenze di terze parti, l'output pubblicato conterrà una cartella per ogni [identificatore di runtime](../rid-catalog.md#what-are-rids) supportato dalla dipendenza nativa. Quest'ultimo si trova nel relativo pacchetto NuGet.

## <a name="self-contained-deployments-scd"></a>Distribuzioni autonome ##

Per una distribuzione autonoma, si distribuisce non solo l'app e le dipendenze di terze parti, ma la versione di .NET Core con cui si compila l'app. Tuttavia, la creazione di una distribuzione autonoma non include le [dipendenze native di .NET Core](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md) su più piattaforme (ad esempio, OpenSSL in macOS), pertanto queste devono essere installate prima di eseguire l'applicazione. 

### <a name="why-deploy-a-self-contained-deployment"></a>Perché distribuire una distribuzione autonoma? ###

Una distribuzione autonoma offre due vantaggi principali:

- Si dispone del controllo esclusivo della versione di .NET Core che viene distribuita con l'app. .NET Core può essere usato solo dall'utente.

- È possibile garantire che il sistema di destinazione esegua l'app .NET Core, poiché viene specificata la versione di .NET Core in cui verrà eseguita.

Sono presenti anche alcuni svantaggi:

- Poiché .NET Core è incluso nel pacchetto di distribuzione, è necessario selezionare in anticipo le piattaforme di destinazione per cui vengono creati i pacchetti di distribuzione.

- La dimensione del pacchetto di distribuzione è relativamente elevata, poiché è necessario includere .NET Core, nonché l'app e le relative dipendenze di terze parti.

- La distribuzione di numerose app .NET Core autonome a un sistema comporta l'utilizzo di quantità significative di spazio su disco, poiché ogni app duplica i file di .NET Core.

### <a name="simpleSelf"></a> Pubblicazione di una semplice distribuzione autonoma ###

La pubblicazione di una distribuzione autonoma senza dipendenze di terze parti comporta la creazione del progetto, la modifica del file csproj, la compilazione, il testing e la pubblicazione dell'app.  Il processo viene illustrato da un semplice esempio scritto in C#. L'esempio usa l'utilità `dotnet` dalla riga di comando; tuttavia, è possibile usare anche un ambiente di sviluppo, come Visual Studio o Visual Studio Code, per compilare, testare e pubblicare l'esempio.

1. Creare una directory per il progetto e, dalla riga di comando, digitare `dotnet new console` per creare un nuovo progetto console C#.

2. Aprire il file `Program.cs` in un editor e sostituire il codice generato automaticamente con il codice seguente. Richiede all'utente di immettere il testo e quindi visualizza le singole parole immesse dall'utente. Usa l'espressione regolare `\w+` per separare le parole nel testo di input.

    ```cs
    using System;
    using System.Text.RegularExpressions;

    namespace Applications.ConsoleApps
    {
        public class ConsoleParser
        {
            public static void Main()
            {
                 Console.WriteLine("Enter any text, followed by <Enter>:\n");
                 String s = Console.ReadLine();
                 ShowWords(s);
                 Console.Write("\nPress any key to continue... ");
                 Console.ReadKey();
          }

          private static void ShowWords(String s)
          {
              String pattern = @"\w+";
              var matches = Regex.Matches(s, pattern);
              if (matches.Count == 0)
                  Console.WriteLine("\nNo words were identified in your input.");
              else {
                  Console.WriteLine("\nThere are {0} words in your string:", matches.Count);
                  for (int ctr = 0; ctr < matches.Count; ctr++)
                      Console.WriteLine("   #{0,2}: '{1}' at position {2}", ctr,
                                        matches[ctr].Value, matches[ctr].Index);
              }
          }
      }
    }
    ```

3. Creare un tag `<RuntimeIdentifiers>` nella sezione `<PropertyGroup>` del file `csproj` che definisce le piattaforme di destinazione dell'app e specifica l'identificatore di runtime di ogni piattaforma di destinazione. Per un elenco degli identificatori di runtime, vedere [Runtime IDentifier catalog](../rid-catalog.md) (Catalogo degli identificatori di runtime). L'esempio seguente indica che l'app viene eseguita in sistemi operativi Windows 10 a 64 bit e nel sistema operativo OS X versione 10.11 a 64 bit.

    ```xml
        <PropertyGroup>
          <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
        </PropertyGroup>
    ```
Si noti che è inoltre necessario aggiungere un punto e virgola per separare i RID. Si noti anche che l'elemento `<RuntimeIdentifier>` può essere inserito in qualsiasi elemento `<PropertyGroup>` presente nel file `csproj`. Un file di esempio completo `csproj` viene presentato più avanti in questa sezione.

4. Eseguire il comando `dotnet restore` per ripristinare le dipendenze specificate nel progetto.

5. Dopo aver eseguito il debug e il testing del programma, è possibile creare i file da distribuire con l'app per ogni piattaforma di destinazione usando il comando `dotnet publish` per entrambe le piattaforme di destinazione, come indicato di seguito:

   ```console
   dotnet publish -c release -r win10-x64
   dotnet publish -c release -r osx.10.11-x64
   ```
In questo modo, viene creata la versione finale dell'app per ogni piattaforma di destinazione (anziché un debug). I file risultanti vengono inseriti in una sottodirectory denominata `publish` che si trova in una sottodirectory della sottodirectory del progetto `.\bin\release\netcoreapp1.1\<runtime_identifier>`. Si noti che ogni sottodirectory contiene il set completo di file (i file dell'app e tutti i file di .NET Core) necessario per avviare l'app.

6. Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è particolarmente utile per il debug di eccezioni. È possibile scegliere di non inserirlo nel pacchetto dei file dell'applicazione.

I file pubblicati possono essere distribuiti nel modo desiderato. Ad esempio, è possibile inserirli in un file zip, usare un semplice comando `copy` o distribuirli con qualsiasi pacchetto di installazione di propria scelta. 

Di seguito è riportato il file `csproj` completo per questo progetto.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <VersionPrefix>1.0.0</VersionPrefix>
    <DebugType>Portable</DebugType>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
</Project>
```


### <a name="deploying-a-self-contained-deployment-with-third-party-dependencies"></a>Pubblicazione di una distribuzione autonoma con dipendenze di terze parti ###

Una distribuzione autonoma con una o più dipendenze di terze parti comporta l'aggiunta della dipendenza di terze parti:

1. Aggiungere i riferimenti alle librerie di terze parti alla sezione `<ItemGroup>` del file `csproj`. La sezione `<ItemGroup>` seguente usa Json.NET come libreria di terze parti.

    ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
      </ItemGroup>
    ```
2. Se non lo si è già fatto, scaricare nel sistema il pacchetto NuGet contenente la dipendenza di terze parti. Per rendere la dipendenza disponibile per l'app, eseguire il comando `dotnet restore` dopo l'aggiunta della dipendenza. Poiché la dipendenza viene risolta dalla cache NuGet locale in fase di pubblicazione, deve essere disponibile nel sistema.

Di seguito è riportato il file csproj completo per questo progetto:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <VersionPrefix>1.0.0</VersionPrefix>
    <DebugType>Portable</DebugType>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
</Project>
```

Quando si distribuisce l'applicazione, anche le dipendenze di terze parti usate nell'app sono contenute nei file dell'applicazione. Le librerie di terze parti non devono essere già presenti nel sistema in cui l'app viene eseguita.

Si noti che è possibile distribuire una distribuzione autonoma solo con una libreria di terze parti alle piattaforme supportate da tale libreria. Questo scenario è simile a quello in cui nella distribuzione dipendente dal framework sono disponibili dipendenze di terze parti con dipendenze native. 

### <a name="deploying-a-self-contained-deployment-with-a-smaller-footprint"></a>Pubblicazione di una distribuzione autonoma con impatto ridotto ###

Se la disponibilità di spazio di archiviazione adeguato sui sistemi di destinazione può rappresentare un problema, è possibile ridurre l'impatto generale dell'app escludendo alcuni componenti di sistema. A tale scopo, definire in modo esplicito i componenti di .NET Core che l'app include nel file csproj.

Per creare una distribuzione autonoma con un impatto ridotto, seguire i primi due passaggi per la creazione di una distribuzione autonoma. Dopo aver eseguito il comando `dotnet new console` e aggiunto il codice sorgente C# all'app, seguire questa procedura:

1. Aprire il file `csproj` e sostituire l'elemento `<TargetFramework>` con quanto segue:

  ```xml
  <TargetFramework>netstandard1.6</TargetFramework>
  ```
Questa operazione indica che, anziché usare l'intero framework `netcoreapp1.0`, che include .NET Core CLR, la libreria di .NET Core e vari altri componenti del sistema, l'app usa solo la libreria .NET Standard.

2. Sostituire `<ItemGroup>` contenente riferimenti al pacchetto con quanto segue:

  ```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.Runtime.CoreCLR" Version="1.0.2" />
    <PackageReference Include="Microsoft.NETCore.DotNetHostPolicy" Version="1.0.1" />
  </ItemGroup>
  ```

   In questo modo, vengono definiti i componenti di sistema usati dall'app. I componenti di sistema forniti con l'app includono la libreria .NET Standard, il runtime e l'host di .NET Core. In questo modo, si ottiene una distribuzione autonoma con impatto ridotto.

3. Come nell'esempio [Pubblicazione di una semplice distribuzione autonoma](#simpleSelf), creare un elemento `<RuntimeIdentifiers>` in un'istanza di `<PropertyGroup>` nel file `csproj` che definisce le piattaforme di destinazione dell'app e specifica l'identificatore di runtime di ogni piattaforma di destinazione. Per un elenco degli identificatori di runtime, vedere [Runtime IDentifier catalog](../rid-catalog.md) (Catalogo degli identificatori di runtime). L'esempio seguente indica che l'app viene eseguita in sistemi operativi Windows 10 a 64 bit e nel sistema operativo OS X versione 10.11 a 64 bit.

    ```xml
    <PropertyGroup>
      <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
    </PropertyGroup>
    ```
    
   Un file di esempio completo `csproj` viene presentato più avanti in questa sezione.

4. Eseguire il comando `dotnet restore` per ripristinare le dipendenze specificate nel progetto.

5. Dopo aver eseguito il debug e il testing del programma, è possibile creare i file da distribuire con l'app per ogni piattaforma di destinazione usando il comando `dotnet publish` per entrambe le piattaforme di destinazione, come indicato di seguito:

   ```console
   dotnet publish -c release -r win10-x64
   dotnet publish -c release -r osx.10.11-x64
   ```
In questo modo, viene creata la versione finale dell'app per ogni piattaforma di destinazione (anziché un debug). I file risultanti vengono inseriti in una sottodirectory denominata `publish` che si trova in una sottodirectory della sottodirectory del progetto `.\bin\release\netstandard1.6\<runtime_identifier>`. Si noti che ogni sottodirectory contiene il set completo di file (i file dell'app e tutti i file di .NET Core) necessario per avviare l'app.

6. Insieme ai file dell'applicazione, il processo di pubblicazione genera un file del database di programma (con estensione pdb) che contiene le informazioni di debug relative all'app. Il file è particolarmente utile per il debug di eccezioni. È possibile scegliere di non inserirlo nel pacchetto dei file dell'applicazione.

I file pubblicati possono essere distribuiti nel modo desiderato. Ad esempio, è possibile inserirli in un file zip, usare un semplice comando `copy` o distribuirli con qualsiasi pacchetto di installazione di propria scelta. 

Di seguito è riportato il file `csproj` completo per questo progetto.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netstandard1.6</TargetFramework>
    <VersionPrefix>1.0.0</VersionPrefix>
    <DebugType>Portable</DebugType>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.Runtime.CoreCLR" Version="1.0.2" />
    <PackageReference Include="Microsoft.NETCore.DotNetHostPolicy" Version="1.0.1" />
  </ItemGroup>
</Project>
```


