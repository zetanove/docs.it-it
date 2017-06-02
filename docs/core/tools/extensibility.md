---
title: "Modello di estendibilità dell&quot;interfaccia della riga di comando di .NET Core | Microsoft Docs"
description: "Informazioni sull&quot;estendibilità degli strumenti dell&quot;interfaccia della riga di comando (CLI)."
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 04/12/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fffc3400-aeb9-4c07-9fea-83bc8dbdcbf3
ms.translationtype: Human Translation
ms.sourcegitcommit: 5a9c7ba999e278f4c5fbec51fa547b3e35828f88
ms.openlocfilehash: 7e5cfdf644b3f4c6c5cc4f4e6f77ec72910b1f47
ms.contentlocale: it-it
ms.lasthandoff: 04/26/2017

---

# <a name="net-core-cli-tools-extensibility-model"></a>Modello di estendibilità degli strumenti CLI di .NET Core

Questo documento illustra le diverse modalità per l'estensione degli strumenti della riga di comando (CLI) di .NET Core e descrive gli scenari d'uso di ogni strumento.
Si vedrà come usare gli strumenti e come creare i diversi tipi di strumenti.

## <a name="how-to-extend-cli-tools"></a>Come estendere gli strumenti dell'interfaccia della riga di comando
Gli strumenti dell'interfaccia della riga di comando possono essere estesi in tre modi principali:

1. [Tramite pacchetti NuGet in base al progetto](#per-project-based-extensibility)

  Gli strumenti in base al progetto sono contenuti nel contesto del progetto stesso, ma consentono un'installazione facile mediante il ripristino.

2. [Tramite pacchetti NuGet con destinazioni personalizzate](#custom-targets)

  Le destinazioni personalizzate consentono di estendere facilmente il processo di compilazione con attività personalizzate.

3. [Tramite il PATH di sistema](#path-based-extensibility)

  Gli strumenti basati su PATH sono ottimi per scopi di carattere generale e validi per più progetti. Sono utilizzabili su un singolo computer.

I tre meccanismi di estendibilità sopra indicati non si escludono a vicenda. È possibile usarne uno, usarli tutti o usare una combinazione dei meccanismi. La scelta dipende dall'obiettivo che si vuole ottenere con l'estensione.

## <a name="per-project-based-extensibility"></a>Estendibilità in base al progetto
Gli strumenti in base al progetto sono [installazioni dipendenti dal framework](../deploying/index.md#framework-dependent-deployments-fdd) distribuite come pacchetti NuGet. Sono disponibili solo nel contesto del progetto di riferimento, per il quale vengono ripristinati. La chiamata all'esterno del contesto del progetto (ad esempio all'esterno della directory contenente il progetto) non riesce perché il comando non viene trovato.

Questi strumenti sono perfetti anche per i server di compilazione, dal momento che non è necessario nulla al di fuori del file di progetto. Il processo di compilazione esegue il ripristino del progetto compilato e gli strumenti saranno disponibili. Rientrano in questa categoria anche i progetti in un particolare linguaggio, ad esempio F#, perché ogni progetto può essere scritto in un solo linguaggio specifico.

Questo modello di estendibilità, infine, fornisce il supporto per la creazione di strumenti che devono accedere all'output compilato del progetto. Ad esempio, rientrano in questa categoria diversi strumenti di visualizzazione Razor presenti in applicazioni MVC [ASP.NET](https://www.asp.net/).

### <a name="consuming-per-project-tools"></a>Utilizzo di strumenti in base al progetto
Per usare questi strumenti è necessario aggiungere al file di progetto un elemento `<DotNetCliToolReference>` per ogni strumento da usare. All'interno dell'elemento `<DotNetCliToolReference>` si fa riferimento al pacchetto in cui risiede lo strumento e si specifica la versione necessaria. Dopo l'esecuzione di [`dotnet restore`](dotnet-restore.md) lo strumento e le relative dipendenze vengono ripristinati.

Per gli strumenti che devono caricare l'output di compilazione del progetto per l'esecuzione, è in genere presente un'altra dipendenza elencata sotto le normali dipendenze del file di progetto. Poiché l'interfaccia della riga di comando usa MSBuild come motore di compilazione, è consigliabile che queste parti dello strumento vengano scritte come [destinazioni](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) e [attività](https://docs.microsoft.com/visualstudio/msbuild/msbuild-tasks) MSBuild personalizzate, dato che possono essere incluse nel processo di compilazione globale. Tali destinazioni e attività possono anche ottenere facilmente alcuni o tutti i dati prodotti con la compilazione, ad esempio la posizione dei file di output, la configurazione corrente in fase di compilazione e così via. Tutte queste informazioni diventano un set di proprietà MSBuild leggibili da qualsiasi destinazione. Il presente documento illustra come aggiungere una destinazione personalizzata usando NuGet.

Di seguito è riportato un esempio di aggiunta di un semplice strumento "tools" a un semplice progetto. Si consideri un comando di esempio denominato `dotnet-api-search` che consente di cercare nei pacchetti NuGet l'API specificata. Di seguito è riportato un file di progetto di un'applicazione console che usa tale strumento:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <!-- The tools reference -->
  <ItemGroup>
    <DotNetCliToolReference Include="dotnet-api-search" Version="1.0.0" />
  </ItemGroup>
</Project>
```

L'elemento `<DotNetCliToolReference>` è strutturato in modo analogo all'elemento `<PackageReference>`. Il ripristino richiede l'ID del pacchetto contenente lo strumento e la relativa versione.

### <a name="building-tools"></a>Compilazione degli strumenti
Come affermato in precedenza, gli strumenti sono essenzialmente applicazioni console portabili. La compilazione degli strumenti è analoga a quella di qualsiasi applicazione console.
Dopo la compilazione usare il comando [`dotnet pack`](dotnet-pack.md) per creare un pacchetto NuGet (file nupkg) contenente il codice, le informazioni sulle dipendenze e così via. È possibile assegnare qualsiasi nome al pacchetto, ma l'applicazione in esso contenuta, ovvero il file binario dello strumento, deve essere conforme alla convenzione `dotnet-<command>` per consentire a `dotnet` di chiamare il pacchetto.

> [!NOTE]
> Nelle versioni precedenti alla RC3 degli strumenti della riga di comando di .NET Core, il comando `dotnet pack` ha un bug a causa del quale il file `runtime.config.json` non viene incluso nel pacchetto dello strumento. La mancanza di tale file causa errori in fase di esecuzione. Se si verifica questo problema, assicurarsi di eseguire l'aggiornamento alla versione più recente degli strumenti e ritentare il comando `dotnet pack`.

Poiché gli strumenti sono applicazioni portabili, per eseguire uno strumento l'utente deve avere la versione delle librerie .NET Core con le quali lo strumento è stato creato. Qualsiasi altra dipendenza usata dallo strumento e non contenuta nelle librerie .NET Core viene ripristinata e posizionata nella cache NuGet. Di conseguenza, l'intero strumento viene eseguito usando gli assembly delle librerie .NET Core oltre agli assembly della cache NuGet.

Gli strumenti di questo tipo hanno un grafico delle dipendenze completamente separato da quello del progetto che li usa. Il processo di ripristino ripristina innanzitutto le dipendenze del progetto, quindi ogni strumento e le relative dipendenze.

Esempi più dettagliati e differenti combinazioni sono disponibili in [.NET Core CLI repo](https://github.com/dotnet/cli/tree/rel/1.0.1/TestAssets/TestProjects) (Archivio .NET Core dell'interfaccia della riga di comando).
Nello stesso archivio è possibile vedere anche l'[implementazione degli strumenti usati](https://github.com/dotnet/cli/tree/rel/1.0.1/TestAssets/TestPackages).

### <a name="custom-targets"></a>Destinazioni personalizzate
NuGet è in grado di [creare pacchetti di destinazioni MSBuild personalizzate e file props](https://docs.microsoft.com/nuget/create-packages/creating-a-package#including-msbuild-props-and-targets-in-a-package). Con il passaggio all'uso di MSBuild per gli strumenti CLI di .NET Core, lo stesso meccanismo di estendibilità è ora applicabile ai progetti .NET Core. È opportuno usare questo tipo di estendibilità quando si vuole estendere il processo di compilazione, quando si vuole accedere a qualsiasi elemento di tale processo, ad esempio i file generati, quando si vuole esaminare la configurazione in cui viene chiamata la compilazione e così via.

Nell'esempio seguente è possibile visualizzare il file di progetto della destinazione con la sintassi `csproj`. Il codice indica al comando [`dotnet pack`](dotnet-pack.md) quali elementi aggiungere al pacchetto, posizionando i file di destinazioni e gli assembly nella cartella *build* all'interno del pacchetto. Si noti l'elemento `<ItemGroup>` con la proprietà `Label` impostata su `dotnet pack instructions` e la destinazione definita sotto tale elemento.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <Description>Sample Packer</Description>
    <VersionPrefix>0.1.0-preview</VersionPrefix>
    <TargetFramework>netstandard1.3</TargetFramework>
    <DebugType>portable</DebugType>
    <AssemblyName>SampleTargets.PackerTarget</AssemblyName>
  </PropertyGroup>
  <ItemGroup>
    <EmbeddedResource Include="Resources\Pkg\dist-template.xml;compiler\resources\**\*" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <None Include="build\SampleTargets.PackerTarget.targets" />
  </ItemGroup>
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  <ItemGroup>
    <PackageReference Include="Microsoft.Extensions.DependencyModel" Version="1.0.1-beta-000933"/>
    <PackageReference Include="Microsoft.Build.Framework" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Microsoft.Build.Utilities.Core" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
  <ItemGroup />
  <PropertyGroup Label="Globals">
    <ProjectGuid>463c66f0-921d-4d34-8bde-7c9d0bffaf7b</ProjectGuid>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <DefineConstants>$(DefineConstants);NETSTANDARD1_3</DefineConstants>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <DefineConstants>$(DefineConstants);RELEASE</DefineConstants>
  </PropertyGroup>
</Project>
```

L'utilizzo delle destinazioni personalizzate è reso possibile dalla specifica di un elemento `<PackageReference>` che punta al pacchetto e alla relativa versione all'interno del progetto in fase di estensione. A differenza degli strumenti, il pacchetto di destinazione personalizzato non viene incluso nella chiusura delle dipendenze del progetto.

L'uso della destinazione personalizzata dipende esclusivamente dal modo in cui questa viene configurata. Dal momento che si tratta di una destinazione MSBuild, può dipendere da una destinazione data, essere eseguita dopo un'altra destinazione e anche essere chiamata manualmente mediante il comando `dotnet msbuild /t:<target-name>`.

Tuttavia per offrire agli utenti una migliore esperienza d'uso è possibile combinare strumenti in base al progetto e destinazioni personalizzate. In questo scenario lo strumento in base al progetto si limita ad accettare qualsiasi parametro necessario e lo traduce nella chiamata a [`dotnet msbuild`](dotnet-msbuild.md) richiesta, che esegue la destinazione. È possibile visualizzare un esempio di questo tipo di sinergia nel repository degli [esempi di MVP Summit 2016 Hackathon](https://github.com/dotnet/MVPSummitHackathon2016) nel progetto [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer).

### <a name="path-based-extensibility"></a>Estendibilità basata su PATH
L'estendibilità basata sul PATH viene in genere usata per i computer di sviluppo in cui è necessario disporre di uno strumento in grado di coprire concettualmente più di un singolo progetto. Il principale svantaggio di questo meccanismo di estensione sta nel fatto che è vincolato al computer in cui è presente lo strumento. Se si vuole usare questo meccanismo in un altro computer, è necessario eseguire un'attività di distribuzione.

Questo modello di estendibilità del set di strumenti dell'interfaccia della riga di comando è molto semplice. Come illustrato in [.NET Core CLI overview](index.md) (Panoramica sull'interfaccia della riga di comando di .NET Core), il driver `dotnet` può eseguire qualsiasi comando denominato in base alla convenzione `dotnet-<command>`. La logica di risoluzione predefinita verifica diverse posizioni e infine sceglie il percorso specificato dal PATH di sistema. Se il comando richiesto è presente nel PATH di sistema ed è un file binario che è possibile richiamare, il driver `dotnet` lo richiamerà.

Il file deve essere un file eseguibile. Nei sistemi Unix può trattarsi di qualsiasi file con il bit eseguibile impostato tramite `chmod +x`. In Windows è possibile usare file *cmd*.

Di seguito è riportata un'implementazione molto semplice di uno strumento "Hello World". Si usa sia `bash` sia `cmd` in Windows.
Il comando che segue trasmette semplicemente "Hello World" alla console.

```bash
#!/bin/bash

echo "Hello World!"
```

```cmd
echo "Hello World"
```

Nei sistemi MacOS è possibile salvare lo script come `dotnet-hello` e impostarne il bit eseguibile con `chmod +x dotnet-hello`. È quindi possibile creare un collegamento simbolico in `/usr/local/bin` usando il comando `ln -s dotnet-hello /usr/local/bin/`. In questo modo sarà possibile chiamare il comando usando la sintassi `dotnet hello`.

In Windows è possibile salvare lo script come `dotnet-hello.cmd` e inserirlo in una posizione inclusa in un percorso di sistema (o è possibile aggiungerlo a una cartella che si trova già in tale percorso). In seguito è sufficiente usare `dotnet hello` per eseguire questo esempio.

