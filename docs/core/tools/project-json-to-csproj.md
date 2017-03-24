---
title: Confronto tra project.json e csproj - .NET Core | Microsoft Docs
description: Vedere il mapping tra gli elementi project.json e csproj.
keywords: project.json, csproj, .NET Core, MSBuild
author: natemcmaster
ms.author: mairaw
ms.date: 03/02/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 79c50621-a24a-4e64-bbb9-b953113e841c
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: beaae03add6f90692189325c0e1cff5ab761abb5
ms.lasthandoff: 03/07/2017

---

# <a name="a-mapping-between-projectjson-and-csproj-properties"></a>Mapping tra le proprietà di project.json e csproj

di [Nate McMaster](http://github.com/natemcmaster)

Durante lo sviluppo degli strumenti di .NET Core, è stata apportata una modifica importante che non supporta più i file *project.json* e sposta invece i progetti .NET Core nel formato MSBuild/csproj.

Questo articolo illustra come vengono rappresentate le impostazioni di *project.json* nel formato MSBuild/csproj, offre informazioni sull'uso del nuovo formato e consente di capire le modifiche apportate dagli strumenti di migrazione quando si aggiorna un progetto alla nuova versione degli strumenti. 
 
## <a name="the-csproj-format"></a>Formato csproj

Il nuovo formato, \*.csproj, è un formato basato su XML. L'esempio seguente illustra il nodo radice di un progetto .NET Core usando `Microsoft.NET.Sdk`. Per i progetti Web, l'SDK usato è `Microsoft.NET.Sdk.Web`.

```xml
<Project Sdk="Microsoft.NET.Sdk">
...
</Project>
```

## <a name="common-top-level-properties"></a>Proprietà comuni di livello superiore

### <a name="name"></a>name
```json
{
  "name": "MyProjectName"
}
```

Non è più supportato. In csproj, ciò è determinato dal nome del file di progetto, che viene definito dal nome della directory. Ad esempio `MyProjectName.csproj`.

Per impostazione predefinita, il nome del file di progetto specifica anche il valore delle proprietà `<AssemblyName>` e `<PackageId>`. 

```xml
<PropertyGroup>
  <AssemblyName>MyProjectName</AssemblyName>
  <PackageId>MyProjectName</PackageId>
</PropertyGroup>
```

La proprietà `<AssemblyName>` avrà un valore diverso di `<PackageId>` se la proprietà `buildOptions\outputName` è stata definita in project.json. Per altre informazioni, vedere [Altre opzioni comuni di compilazione](#other-common-build-options).

### <a name="version"></a>version

```json
{
  "version": "1.0.0-alpha-*"
}
```
Usare le proprietà `VersionPrefix` e `VersionSuffix`:

```xml
<PropertyGroup>
  <VersionPrefix>1.0.0</VersionPrefix>
  <VersionSuffix>alpha</VersionSuffix>
</PropertyGroup>
```

È anche possibile usare la proprietà `Version`, ma questa operazione potrebbe causare la sovrascrittura delle impostazioni della versione durante la creazione di pacchetti:

```xml
<PropertyGroup>
  <Version>1.0.0-alpha</Version>
</PropertyGroup>
```

### <a name="other-common-root-level-options"></a>Altre opzioni comuni a livello radice

```json
{
  "authors": [ "Anne", "Bob" ],
  "company": "Contoso",
  "language": "en-US",
  "title": "My library",
  "description": "This is my library.\r\nAnd it's really great!",
  "copyright": "Nugetizer 3000",
  "userSecretsId": "xyz123"
}
```

```xml
<PropertyGroup>
  <Authors>Anne;Bob</Authors>
  <Company>Contoso</Company>
  <NeutralLanguage>en-US</NeutralLanguage>
  <AssemblyTitle>My library</AssemblyTitle>
  <Description>This is my library.
And it's really great!</Description>
  <Copyright>Nugetizer 3000</Copyright>
  <UserSecretsId>xyz123</UserSecretsId>
</PropertyGroup>
```

## <a name="frameworks"></a>frameworks

### <a name="one-target-framework"></a>Un solo framework di destinazione
```json
{
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

```xml
<PropertyGroup>
  <TargetFramework>netcoreapp1.0</TargetFramework>
</PropertyGroup>
```

### <a name="multiple-target-frameworks"></a>Più framework di destinazione

```json
{
  "frameworks": {
    "netcoreapp1.0": {},
    "net451": {}
  }
}
```

Usare la proprietà `TargetFrameworks` per definire l'elenco dei framework di destinazione. Usare un punto e virgola per separare più valori di framework. 

```xml
<PropertyGroup>
  <TargetFrameworks>netcoreapp1.0;net451</TargetFrameworks>
</PropertyGroup>
```

## <a name="dependencies"></a>dependencies

> [!IMPORTANT]
> Se la dipendenza è un **progetto** e non un pacchetto, il formato è diverso. Per altre informazioni, vedere la sezione [Tipo di dipendenza](#dependency-type).

### <a name="netstandardlibrary-metapackage"></a>Metapacchetto NETStandard.Library

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  }
}
```

```xml
<PropertyGroup>
  <NetStandardImplicitPackageVersion>1.6.0</NetStandardImplicitPackageVersion>
</PropertyGroup>
```

### <a name="microsoftnetcoreapp-metapackage"></a>Metapacchetto Microsoft.NETCore.App

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0"
  }
}
```

```xml
<PropertyGroup>
  <RuntimeFrameworkVersion>1.0.3</RuntimeFrameworkVersion>
</PropertyGroup>
```

Si noti che il valore `<RuntimeFrameworkVersion>` nel progetto migrato è determinato dalla versione dell'SDK installato.

### <a name="top-level-dependencies"></a>Dipendenze di livello superiore
```json
{
  "dependencies": {
    "Microsoft.AspNetCore": "1.1.0"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.AspNetCore" Version="1.1.0" />
</ItemGroup>
```

### <a name="per-framework-dependencies"></a>Dipendenze per framework
```json
{
  "framework": {
    "net451": {
      "dependencies": {
        "System.Collections.Immutable": "1.3.1"
      }
    },
    "netstandard1.5": {
      "dependencies": {
        "Newtonsoft.Json": "9.0.1"
      }
    }
  }
}
```

```xml
<ItemGroup Condition="'$(TargetFramework)'=='net451'">
  <PackageReference Include="System.Collections.Immutable" Version="1.3.1" />
</ItemGroup>

<ItemGroup Condition="'$(TargetFramework)'=='netstandard1.5'">
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
</ItemGroup>
```

### <a name="imports"></a>importazioni

```json
{
  "dependencies": {
    "YamlDotNet": "4.0.1-pre309"
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dnxcore50",
        "dotnet"
      ]
    }
  }
}
```

```xml
<PropertyGroup>
  <PackageTargetFallback>dnxcore50;dotnet</PackageTargetFallback>
</PropertyGroup>
<ItemGroup>
  <PackageReference Include="YamlDotNet" Version="4.0.1-pre309" />
</ItemGroup>
```

### <a name="dependency-type"></a>Tipo di dipendenza

#### <a name="type-project"></a>Tipo: progetto
```json
{
  "dependencies": {
    "MyOtherProject": "1.0.0-*",
    "AnotherProject": {
      "type": "project"
    }
  }
}
```

```xml
<ItemGroup>
  <ProjectReference Include="..\MyOtherProject\MyOtherProject.csproj" />
  <ProjectReference Include="..\AnotherProject\AnotherProject.csproj" />
</ItemGroup>
```

> [!NOTE]
> Questa operazione interrompe il modo in cui `dotnet pack --version-suffix $suffix` determina la versione di dipendenza di un riferimento al progetto.


#### <a name="type-build"></a>Tipo: compilazione
```json
{
  "dependencies": {
    "Microsoft.EntityFrameworkCore.Design": {
      "version": "1.1.0",
      "type": "build"
    }
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="1.1.0" PrivateAssets="All" />
</ItemGroup>
```

#### <a name="type-platform"></a>Tipo: piattaforma
```json
{
  "dependencies": {
    "Microsoft.NETCore.App": {
      "version": "1.1.0",
      "type": "platform"
    }
  }
}
```

Non è disponibile nessuna opzione equivalente in csproj. 

## <a name="runtimes"></a>runtimes
```json
{
  "runtimes": {
    "win7-x64": {},
    "osx.10.11-x64": {},
    "ubuntu.16.04-x64": {}
  }
}
```

```xml
<PropertyGroup>
  <RuntimeIdentifiers>win7-x64;osx.10-11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
</PropertyGroup>
```

### <a name="standalone-apps-self-contained-deployment"></a>App indipendenti (distribuzione autonoma)
In project.json, la definizione di una sezione `runtimes` indica che l'app era indipendente durante la compilazione e la pubblicazione.
In MSBuild, tutti i progetti sono *portatili* durante la creazione, ma possono essere pubblicati come autonomi.

`dotnet publish --framework netcoreapp1.0 --runtime osx.10.11-x64`

Per altre informazioni, vedere [Distribuzioni autonome (SCD)](../deploying/index.md#self-contained-deployments-scd).

## <a name="tools"></a>tools
```json
{
  "tools": {
    "Microsoft.EntityFrameworkCore.Tools.DotNet": "1.0.0-*"
  }
}
```

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="1.0.0" />
</ItemGroup>
```

> [!NOTE]
> Gli `imports` sugli strumenti non sono supportati in csproj. Gli strumenti che hanno bisogno di imports non funzionano con il nuovo `Microsoft.NET.Sdk`.

## <a name="buildoptions"></a>buildOptions

Vedere anche [Files](#files).

### <a name="emitentrypoint"></a>emitEntryPoint

```json
{
  "buildOptions": {
    "emitEntryPoint": true
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Se `emitEntryPoint` fosse `false`, il valore di `OutputType` verrebbe convertito in `Library`, ovvero il valore predefinito:

```json
{
  "buildOptions": {
    "emitEntryPoint": false
  }
}
```

```xml
<PropertyGroup>
  <OutputType>Library</OutputType>
  <!-- or, omit altogether. It defaults to 'Library' -->
</PropertyGroup>
```

### <a name="keyfile"></a>keyFile

```json
{
  "buildOptions": {
    "keyFile": "MyKey.snk"
  }
}
```

L'elemento `keyFile` si espande a tre proprietà in MSBuild:

```xml
<PropertyGroup>
  <AssemblyOriginatorKeyFile>MyKey.snk</AssemblyOriginatorKeyFile>
  <SignAssembly>true</SignAssembly>
  <PublicSign Condition="'$(OS)' != 'Windows_NT'">true</PublicSign>
</PropertyGroup>
```

### <a name="other-common-build-options"></a>Altre opzioni comuni di compilazione

```json
{
  "buildOptions": {
    "warningsAsErrors": true,
    "nowarn": ["CS0168", "CS0219"],
    "xmlDoc": true,
    "preserveCompilationContext": true,
    "outputName": "Different.AssemblyName",
    "debugType": "portable",
    "allowUnsafe": true,
    "define": ["TEST", "OTHERCONDITION"]
  }
}
```

```xml
<PropertyGroup>
  <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
  <NoWarn>$(NoWarn);CS0168;CS0219</NoWarn>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
  <PreserveCompilationContext>true</PreserveCompilationContext>
  <AssemblyName>Different.AssemblyName</AssemblyName>
  <DebugType>portable</DebugType>
  <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
  <DefineConstants>$(DefineConstants);TEST;OTHERCONDITION</DefineConstants>
</PropertyGroup>
```

## <a name="packoptions"></a>packOptions

Vedere anche [Files](#files).

### <a name="common-pack-options"></a>Opzioni comuni di pacchetto

```json
{
  "packOptions": {    
    "summary": "numl is a machine learning library intended to ease the use of using standard modeling techniques for both prediction and clustering.",
    "tags": ["machine learning", "framework"],
    "releaseNotes": "Version 0.9.12-beta",
    "iconUrl": "http://numl.net/images/ico.png",
    "projectUrl": "http://numl.net",
    "licenseUrl": "https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md",
    "requireLicenseAcceptance": false,
    "repository": {
      "type": "git",
      "url": "https://raw.githubusercontent.com/sethjuarez/numl"
    },
    "owners": ["Seth Juarez"]
  }
}
```

```xml
<PropertyGroup>
  <!-- summary is not migrated from project.json, but you can use the <Description> property for that if needed. -->
  <PackageTags>machine learning;framework</PackageTags>
  <PackageReleaseNotes>Version 0.9.12-beta</PackageReleaseNotes>
  <PackageIconUrl>http://numl.net/images/ico.png</PackageIconUrl>
  <PackageProjectUrl>http://numl.net</PackageProjectUrl>
  <PackageLicenseUrl>https://raw.githubusercontent.com/sethjuarez/numl/master/LICENSE.md</PackageLicenseUrl>
  <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
  <RepositoryType>git</RepositoryType>
  <RepositoryUrl>https://raw.githubusercontent.com/sethjuarez/numl</RepositoryUrl>
  <!-- owners is not supported in MSBuild -->
</PropertyGroup>
```

Non è disponibile nessuna opzione equivalente per l'elemento `owners` in MSBuild. In `summary` è possibile usare la proprietà `<Description>` di MSBuild, anche se il valore di `summary` non viene migrato automaticamente a tale proprietà, poiché tale proprietà è mappata all'elemento [`description`](#-other-common-root-level-options).

## <a name="scripts"></a>script

```json
{
  "scripts": {
    "precompile": "generateCode.cmd",
    "postpublish": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
  }
}
```

Gli equivalenti in MSBuild sono i [target](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets):

```xml
<Target Name="MyPreCompileTarget" BeforeTargets="Build">
  <Exec Command="generateCode.cmd" />
</Target>

<Target Name="MyPostCompileTarget" AfterTargets="Publish">
  <Exec Command="obfuscate.cmd" />
  <Exec Command="removeTempFiles.cmd" />
</Target>
```


## <a name="runtimeoptions"></a>runtimeOptions

```json
{
  "runtimeOptions": {
    "configProperties": {
      "System.GC.Server": true,
      "System.GC.Concurrent": true,
      "System.GC.RetainVM": true,
      "System.Threading.ThreadPool.MinThreads": 4,
      "System.Threading.ThreadPool.MaxThreads": 25
    }
  }
}
```

Tutte le impostazioni in questo gruppo, ad eccezione della proprietà "System.GC.Server", vengono inserite in un file denominato *runtimeconfig.template.json* nella cartella del progetto, con le opzioni elevate all'oggetto radice durante il processo di migrazione:

```json
{
  "configProperties": {
    "System.GC.Concurrent": true,
    "System.GC.RetainVM": true,
    "System.Threading.ThreadPool.MinThreads": 4,
    "System.Threading.ThreadPool.MaxThreads": 25
  }
}
```

La proprietà "System.GC.Server" viene migrata nel file csproj:
```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
</PropertyGroup>
```

È possibile tuttavia impostare tutti questi valori nel file csproj e anche nelle proprietà di MSBuild:
```xml
<PropertyGroup>
  <ServerGarbageCollection>true</ServerGarbageCollection>
  <ConcurrentGarbageCollection>true</ConcurrentGarbageCollection>
  <RetainVMGarbageCollection>true</RetainVMGarbageCollection>
  <ThreadPoolMinThreads>4</ThreadPoolMinThreads>
  <ThreadPoolMaxThreads>25</ThreadPoolMaxThreads>
</PropertyGroup>
```

## <a name="shared"></a>shared
```json
{
  "shared": "shared/**/*.cs"
}
```

Non supportato in csproj. È invece necessario creare e includere i file di contenuto nel file *.nuspec*. Per altre informazioni, vedere [Including content files](https://docs.microsoft.com/nuget/schema/nuspec#including-content-files) (Includere i file di contenuto).

## <a name="files"></a>file

In *project.json*, la compilazione e la creazione di pacchetti possono essere estese per compilare e incorporare da cartelle diverse.
In MSBuild, questa operazione viene eseguita tramite [items](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-items). L'esempio seguente illustra una conversione comune:

```json
{
  "buildOptions": {
    "compile": {
      "copyToOutput": "notes.txt",
      "include": "../Shared/*.cs",
      "exclude": "../Shared/Not/*.cs"
    },
    "embed": {
      "include": "../Shared/*.resx"
    }
  },
  "packOptions": {
    "include": "Views/",
    "mappings": {
      "some/path/in/project.txt": "in/package.txt"
    }
  },
  "publishOptions": {
    "include": [
      "files/",
      "publishnotes.txt"
    ]
  }
}
```

```xml
<ItemGroup>
  <Compile Include="..\Shared\*.cs" Exclude="..\Shared\Not\*.cs" />
  <EmbeddedResource Include="..\Shared\*.resx" />
  <Content Include="Views\**\*" PackagePath="%(Identity)" />
  <None Include="some/path/in/project.txt" Pack="true" PackagePath="in/package.txt" />
  
  <None Include="notes.txt" CopyToOutputDirectory="Always" />
  <!-- CopyToOutputDirectory = { Always, PreserveNewest, Never } -->

  <Content Include="files\**\*" CopyToPublishDirectory="PreserveNewest" />
  <None Include="publishnotes.txt" CopyToPublishDirectory="Always" />
  <!-- CopyToPublishDirectory = { Always, PreserveNewest, Never } -->
</ItemGroup>
```

> [!NOTE]
> Molti dei modelli di glob predefiniti vengono aggiunti automaticamente da .NET Core SDK.
> Per altre informazioni, vedere [Default Compile Item Values](https://aka.ms/sdkimplicititems) (Valori predefiniti degli elementi di compilazione).

Tutti gli elementi `ItemGroup` di MSBuild supportano `Include`, `Exclude` e `Remove`.

Il layout del pacchetto all'interno di .nupkg può essere modificato con `PackagePath="path"`.

Ad eccezione di `Content`, la maggior parte dei gruppi di elementi richiedono in modo esplicito l'aggiunta di `Pack="true"` nel pacchetto. `Content` verrà incluso nella cartella *content* in un pacchetto poiché la proprietà `<IncludeContentInPack>` di MSBuild è impostata su `true` per impostazione predefinita. Per altre informazioni, vedere [Including content in a package](https://docs.microsoft.com/nuget/schema/msbuild-targets#including-content-in-a-package) (Includere contenuto in un pacchetto).

`PackagePath="%(Identity)"` è un modo breve di impostare il percorso di un pacchetto sul percorso del file relativo al progetto.

## <a name="testrunner"></a>testRunner

### <a name="xunit"></a>xUnit

```json
{
  "testRunner": "xunit",
  "dependencies": {
    "dotnet-test-xunit": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="xunit" Version="2.2.0-*" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-*" />
</ItemGroup>
```

### <a name="mstest"></a>MSTest

```json
{
  "testRunner": "mstest",
  "dependencies": {
    "dotnet-test-mstest": "<any>"
  }
}
```

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-*" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.12-*" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.11-*" />
</ItemGroup>
```

## <a name="see-also"></a>Vedere anche
[project.json reference](project-json.md) (Riferimento a project.json)

[High-level overview of changes in CLI](../tools/cli-msbuild-architecture.md) (Panoramica generale sulle modifiche nell'interfaccia della riga di comando)

