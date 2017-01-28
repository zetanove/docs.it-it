---
title: "Modello di estendibilità dell&quot;interfaccia della riga di comando di .NET Core"
description: "Modello di estendibilità dell&quot;interfaccia della riga di comando di .NET Core"
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 11/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 1bebd25a-120f-48d3-8c25-c89965afcbcd
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 2cf58161a75894a12f47cf67a5760dc26f9d261c

---

# <a name="net-core-cli-extensibility-model"></a>Modello di estendibilità dell'interfaccia della riga di comando di .NET Core 

## <a name="overview"></a>Panoramica
Questo documento analizza i principali metodi per estendere gli strumenti dell'interfaccia della riga di comando e illustra gli scenari relativi a ciascuno di essi. Viene indicato come utilizzare gli strumenti e vengono fornite brevi note riguardanti la compilazione di entrambi i tipi di strumenti. 

## <a name="how-to-extend-cli-tools"></a>Come estendere gli strumenti dell'interfaccia della riga di comando
Gli strumenti dell'interfaccia della riga di comando dell'anteprima 3 possono essere estesi in tre modi principali:

1. Tramite pacchetti NuGet in base al progetto
2. Tramite pacchetti NuGet con destinazioni personalizzate  
3. Tramite il PATH di sistema

I tre meccanismi di estendibilità sopra indicati non sono mutualmente esclusivi: è possibile usarli tutti, usarne una combinazione o usarne uno soltanto. La scelta dipende in larga misura dall'obiettivo che si intende raggiungere con l'estensione.

## <a name="per-project-based-extensibility"></a>Estendibilità in base al progetto
Gli strumenti in base al progetto sono [installazioni dipendenti dal framework](../deploying/index.md) distribuite come pacchetti NuGet. Gli strumenti sono disponibili solo nel contesto del progetto che fa riferimento ad essi e per il quale vengono ripristinati. La chiamata all'esterno del contesto del progetto, ad esempio all'esterno della directory contenente il progetto, avrà esito negativo perché non sarà possibile trovare il comando.

Questi strumenti sono perfetti anche per i server di compilazione, dal momento che non è necessario nulla al di fuori del file di progetto. Il processo di compilazione esegue il ripristino del progetto compilato e gli strumenti saranno disponibili. Rientrano in questa categoria anche i progetti in un particolare linguaggio, ad esempio F#. In definitiva, ogni progetto può essere scritto soltanto in uno specifico linguaggio. 

Questo modello di estendibilità, infine, fornisce il supporto per la creazione di strumenti che devono accedere all'output compilato del progetto. Ad esempio, rientrano in questa categoria diversi strumenti di visualizzazione Razor presenti in applicazioni MVC [ASP.NET](https://www.asp.net/). 

### <a name="consuming-per-project-tools"></a>Utilizzo di strumenti in base al progetto
Per utilizzare questi strumenti, è necessario aggiungere al file di progetto un elemento `<DotNetCliToolReference>` per ciascuno degli strumenti da usare. All'interno dell'elemento `<DotNetCliToolReference>` l'utente fa riferimento al pacchetto in cui si trova lo strumento e specifica la versione necessaria. Dopo l'esecuzione di `dotnet restore`, viene eseguito il ripristino dello strumento e delle relative dipendenze. 

Per gli strumenti che devono caricare l'output di compilazione del progetto per l'esecuzione, è in genere presente un'altra dipendenza elencata sotto le normali dipendenze del file di progetto. Poiché la versione di anteprima 3 dell'interfaccia della riga di comando usa MSBuild come motore di compilazione, è consigliabile che queste parti dello strumento vengano scritte come destinazioni e attività MSBuild personalizzate, in quanto fanno parte del processo complessivo di compilazione. Tali destinazioni e attività, inoltre, possono ottenere facilmente alcuni o tutti i dati prodotti tramite la compilazione, ad esempio la posizione dei file di output, la configurazione corrente in fase di compilazione e così via. Nell'anteprima 3 tutte queste informazioni diventano un set di proprietà MSBuild leggibili da qualsiasi destinazione. Nel documento verrà illustrato come aggiungere una destinazione personalizzata usando NuGet. 

Di seguito è riportato un esempio di aggiunta di un semplice strumento "tools" a un semplice progetto. Si consideri un comando di esempio denominato `dotnet-api-search` che consente di cercare nei pacchetti NuGet l'API specificata. Di seguito è riportato un file di progetto di un'applicazione console che usa tale strumento:


```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1/TargetFramework>
    <VersionPrefix>1.0.0</VersionPrefix>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="**\*.cs" />
    <EmbeddedResource Include="**\*.resx" />
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.NETCore.App">
      <Version>1.1.0</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161102-2</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
  </ItemGroup>

  <!-- The tools reference -->
  <ItemGroup>
    <DotNetCliToolReference Include="dotnet-api-search">
      <Version></Version>
    </DotNetCliToolReference>
  </ItemGroup>

  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

L'elemento `<DotNetCliToolReference>` è strutturato in modo analogo all'elemento `<PackageReference>` e richiede l'ID pacchetto del pacchetto contenente almeno lo strumento e la relativa versione. 

### <a name="building-tools"></a>Compilazione degli strumenti
Come affermato in precedenza, gli strumenti sono essenzialmente applicazioni console portabili. La compilazione di uno strumento è analoga a quella di qualsiasi applicazione console. Dopo la compilazione, usare il comando [`dotnet pack`](dotnet-pack.md) per creare un pacchetto NuGet (nupkg) contenente il codice, informazioni sulle relative dipendenze e così via. Il nome del pacchetto è a scelta dell'autore, ma è necessario che l'applicazione in esso contenuta, l'effettivo file binario dello strumento, sia conforme alla convenzione di `dotnet-<command>` per consentire a `dotnet` di richiamare il pacchetto. 

Nei componenti dell'anteprima 3 il comando `dotnet pack` non include il file `runtimeconfig.json` necessario per eseguire lo strumento. Per includere il file sono disponibili due opzioni:

1. Creare un file `nuspec` e usare il nuovo comando `dotnet nuget pack` disponibile nell'interfaccia della riga di comando dell'anteprima 3 per includere il file
2. Usare il nuovo elemento `<Content>` in un elemento `<ItemGroup>` del file di progetto per includere il file manualmente

L'utilizzo dei file nuspec esula dall'ambito di questo articolo. È tuttavia possibile trovare informazioni utili nei [documenti ufficiali NuGet](https://docs.nuget.org/ndocs/create-packages/creating-a-package#the-role-and-structure-of-the--nuspec-file). Se si sceglie il secondo approccio, di seguito è possibile esaminare il file di esempio `csproj` e la relativa configurazione:

```xml
  <ItemGroup>
    <Content Include="$(OutputPath)\*.runtimeconfig.json">
      <Pack>true</Pack>
      <PackagePath>lib\$(TargetFramework)</PackagePath>
    </Content>
  </ItemGroup>
```

Questo `<ItemGroup>` indica al comando `dotnet pack` di includere qualsiasi file `runtimeconfig.json` nella directory di output della compilazione (designata dalla variabile `$(OutputPath)`) e di inserirlo nella cartella `lib` per il framework di destinazione della compilazione. Il framework di destinazione della compilazione viene designato in modo analogo al percorso di output mediante la proprietà MSBuild. Dopo l'impostazione di questa proprietà, il file nupkg dello strumento risultante conterrà tutti gli elementi necessari per l'esecuzione dello strumento stesso.

Poiché gli strumenti sono applicazioni portabili, l'utente che utilizza lo strumento deve disporre della versione delle librerie .NET Core in base a cui tale strumento è stato creato. Solo in questo modo è possibile eseguire lo strumento. Qualsiasi altra dipendenza usata dallo strumento e non contenuta nelle librerie .NET Core viene ripristinata e posizionata nella cache NuGet. Di conseguenza, l'intero strumento viene eseguito usando gli assembly delle librerie .NET Core oltre agli assembly della cache NuGet. 

Gli strumenti di questo tipo hanno un grafico delle dipendenze completamente separato da quello del progetto che li usa. Il processo di ripristino ripristinerà innanzitutto le dipendenze del progetto e quindi ciascuno degli strumenti e le relative dipendenze. 

Esempi più dettagliati e differenti combinazioni sono disponibili in [.NET Core CLI repo](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestProjects) (Archivio .NET Core dell'interfaccia della riga di comando). Nello stesso archivio è possibile vedere anche l'[implementazione degli strumenti usati](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages). 

### <a name="custom-targets"></a>Destinazioni personalizzate
Per un determinato periodo NuGet ha consentito di includere destinazioni MSBuild personalizzate e file props. La documentazione ufficiale su questo argomento è disponibile nel [sito della documentazione NuGet](https://docs.nuget.org/ndocs/create-packages/creating-a-package#including-msbuild-props-and-targets-in-a-package). Con il passaggio nell'interfaccia della riga di comando all'uso di MSBuild, lo stesso meccanismo di estendibilità viene applicato ai progetti .NET Core. È opportuno usare questo tipo di estendibilità quando si vuole estendere il processo di compilazione, quando si vuole accedere a qualsiasi elemento di tale processo, ad esempio i file generati, oppure quando si vuole esaminare la configurazione in cui viene richiamata la compilazione e così via. 

Il file di progetto della destinazione di esempio viene riportato di seguito a scopo di riferimento. Mostra come usare la nuova sintassi `csproj` per indicare al comando `dotnet pack` gli elementi da includere per inserire i file di destinazione, nonché gli assembly, nella cartella `build` all'interno del pacchetto. Notare che l'elemento `<ItemGroup>` riportato di seguito ha la proprietà `Label` impostata su "dotnet pack instructions". 

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" />
  <PropertyGroup>
    <Description>Sample Packer</Description>
    <VersionPrefix>0.1.0-preview</VersionPrefix>
    <TargetFramework>netstandard1.3</TargetFramework>
    <DebugType>portable</DebugType>
    <AssemblyName>SampleTargets.PackerTarget</AssemblyName>
  </PropertyGroup>
  <ItemGroup>
    <Compile Include="**\*.cs" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <EmbeddedResource Include="**\*.resx" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <EmbeddedResource Include="Resources\Pkg\dist-template.xml;compiler\resources\**\*" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
  </ItemGroup>
  <ItemGroup>
    <None Include="build\SampleTargets.PackerTarget.targets" />
  </ItemGroup>
  <ItemGroup Label="dotent pack instructions">
    <Content Include="build\*.targets;$(OutputPath)\*.dll;$(OutputPath)\*.json">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Sdk">
      <Version>1.0.0-alpha-20161029-1</Version>
      <PrivateAssets>All</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.Extensions.DependencyModel">
      <Version>1.0.1-beta-000933</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.Build.Framework">
      <Version>0.1.0-preview-00028-160627</Version>
    </PackageReference>
    <PackageReference Include="Microsoft.Build.Utilities.Core">
      <Version>0.1.0-preview-00028-160627</Version>
    </PackageReference>
    <PackageReference Include="Newtonsoft.Json">
      <Version>9.0.1</Version>
    </PackageReference>
  </ItemGroup>
  <ItemGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <PackageReference Include="NETStandard.Library">
      <Version>1.6.0</Version>
    </PackageReference>
  </ItemGroup>
  <ItemGroup />
  <PropertyGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <DefineConstants>$(DefineConstants);NETSTANDARD1_3</DefineConstants>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <DefineConstants>$(DefineConstants);RELEASE</DefineConstants>
  </PropertyGroup>
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
</Project>
```

L'utilizzo delle destinazioni personalizzate è reso possibile dalla specifica di un elemento `<PackageReference>` che punta al pacchetto e alla relativa versione all'interno del progetto in fase di estensione. A differenza degli strumenti, il pacchetto di destinazione personalizzato non viene incluso nella chiusura delle dipendenze del progetto. 

L'uso della destinazione personalizzata dipende esclusivamente dal modo in cui questa viene configurata. Dal momento che si tratta della normale destinazione MSBuild, può dipendere da una destinazione data, eseguita dopo un'altra destinazione, e può anche essere richiamata manualmente mediante il comando `dotnet msbuild /t:<target-name>`. 

Tuttavia, se si vuole offrire agli utenti una migliore esperienza di utilizzo, è possibile combinare gli strumenti in base al progetto e destinazioni personalizzate. In questo scenario, lo strumento in base al progetto si limita ad accettare qualsiasi parametro necessario e lo traduce nella chiamata a `dotnet msbuild` richiesta che eseguirà la destinazione. È possibile visualizzare un esempio di questo tipo di sinergia nel repository degli esempi di [MVP Summit 2016 Hackathon](https://github.com/dotnet/MVPSummitHackathon2016) nel progetto [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer). 

### <a name="path-based-extensibility"></a>Estendibilità basata su PATH
L'estendibilità basata sul PATH viene in genere usata per i computer di sviluppo in cui è necessario disporre di uno strumento in grado di coprire concettualmente più di un singolo progetto. Il principale svantaggio di questo meccanismo di estensione è che è vincolato al computer in cui è presente lo strumento. Se si vuole usare questo meccanismo in un altro computer, è necessario eseguire un'attività di distribuzione.

Questo modello di estendibilità del set di strumenti dell'interfaccia della riga di comando è molto semplice. Come illustrato in [.NET Core CLI overview](index.md) (Panoramica sull'interfaccia della riga di comando di .NET Core), il driver `dotnet` può eseguire qualsiasi comando denominato in base alla convenzione `dotnet-<command>`. La logica di risoluzione predefinita testerà prima diverse posizioni e alla fine sceglierà il percorso specificato dal PATH di sistema. Se il comando richiesto è presente nel PATH di sistema ed è un file binario che è possibile richiamare, il driver `dotnet` lo richiamerà. 

Il file binario può essere un qualsiasi file eseguibile dal sistema operativo. Nei sistemi Unix può trattarsi di qualsiasi file con il bit eseguibile impostato tramite `chmod +x`. Nei sistemi Windows può trattarsi di qualsiasi file eseguibile da Windows. 

Di seguito è riportata un'implementazione molto semplice di un comando `dotnet clean`. Per implementare il comando verrà usato `bash`. Il comando eliminerà semplicemente le directory `bin/` e `obj/` nella directory corrente. Se gli viene passato l'argomento `--lock`, il comando eliminerà anche il file `project.lock.json`. Il comando è riportato di seguito per intero. 

```bash
#!/bin/bash

# Delete the bin and obj dirs
rm -rf bin/ obj/

LOCK_FILE=$1
if [[ "$LOCK_FILE" = "--lock" ]]; then
    rm project.lock.json
fi


echo "Cleaning complete..."
```

Nei sistemi MacOS è possibile salvare lo script come `dotnet-clean` e impostarne il bit eseguibile con `chmod +x dotnet-clean`. È quindi possibile creare un collegamento simbolico in `/usr/local/bin` usando il comando `ln -s dotnet-clean /usr/local/bin/`. In questo modo sarà possibile richiamare il comando Clean usando la sintassi `dotnet clean`. È possibile testare questo scenario creando un'app, eseguendo `dotnet build` su tale app e quindi eseguendo `dotnet clean`. 

## <a name="conclusion"></a>Conclusione
Gli strumenti dell'interfaccia della riga di comando di .NET Core offrono tre approcci diversi all'estendibilità. Gli strumenti in base al progetto sono contenuti nel contesto del progetto stesso, ma consentono una facile installazione mediante il ripristino. Le destinazioni personalizzate consentono di estendere facilmente il processo di compilazione con attività personalizzate. Gli strumenti basati su PATH sono ottimi per scopi di carattere generale e validi per più progetti. Sono utilizzabili su un singolo computer. 




<!--HONumber=Nov16_HO3-->


