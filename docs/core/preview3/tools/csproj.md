---
title: Informazioni di riferimento di csproj | Microsoft Docs
description: Informazioni sulle differenze tra i file csproj esistenti e .NET Core
keywords: informazioni di riferimento, csproj, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 07/02/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: 0402707f98af8b716b041ba1260162cd227918cc
ms.openlocfilehash: 98f6ced2a199bdbe2f91f46e48ffd3ac52438cf8

---

# <a name="additions-to-the-csproj-format-for-net-core"></a>Aggiunte al formato csproj per .NET Core

[!INCLUDE[preview-warning](../../../includes/warning.md)]

Questo documento descrive le modifiche aggiunte ai file csproj come parte del passaggio da `project.json` a `csproj` e [MSBuild](https://github.com/Microsoft/MSBuild). Per altre informazioni sulla sintassi generale dei file di progetto e informazioni di riferimento, vedere la documentazione del [file di progetto MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference).  

## <a name="additions"></a>Aggiornamenti

* Elemento PackageReference che specifica una dipendenza NuGet nel progetto. L'attributo `Include` specifica l'ID del pacchetto. 

```xml
<PackageReference Include="<package-id>" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

## <a name="version"></a>Versione
`Version` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

## <a name="includeassets"></a>IncludeAssets
L'attributo `IncludeAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` devono essere usati. 

L'attributo può contenere uno o più dei valori seguenti:

* `Compile`: i contenuti della cartella lib sono disponibili per la compilazione.
* `Runtime`: vengono distribuiti i contenuti della cartella runtime.
* `ContentFiles`: vengono usati i contenuti della cartella contentfiles.
* `Build`: vengono usate le proprietà/destinazioni nella cartella build.
* `Native`: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* `Analyzers`: vengono usati gli analizzatori.

In alternativa, l'attributo può contenere:

* `None`: nessuno degli asset viene usato.
* `All`: vengono usati tutti gli asset.

## <a name="excludeassets"></a>ExcludeAssets
L'attributo `ExcludeAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` non devono essere usati.

L'attributo può contenere uno o più dei valori seguenti:

* `Compile`: i contenuti della cartella lib sono disponibili per la compilazione.
* `Runtime`: vengono distribuiti i contenuti della cartella runtime.
* `ContentFiles`: vengono usati i contenuti della cartella contentfiles.
* `Build`: vengono usate le proprietà/destinazioni nella cartella build.
* `Native`: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* `Analyzers`: vengono usati gli analizzatori.

In alternativa, l'elemento può contenere:

* `None`: nessuno degli asset viene usato.
* `All`: vengono usati tutti gli asset.

## <a name="privateassets"></a>PrivateAssets
L'attributo `PrivateAssets` specifica quali asset appartenenti al pacchetto specificato dall'elemento `<PackageReference>` devono essere usati. Specifica, inoltre, che tali asset non devono essere trasmessi al progetto successivo. 

> [!NOTE]
> Questo è un nuovo termine per l'elemento `SuppressParent` di project.json/xproj. 

L'attributo può contenere uno o più dei valori seguenti:

* `Compile`: i contenuti della cartella lib sono disponibili per la compilazione.
* `Runtime`: vengono distribuiti i contenuti della cartella runtime.
* `ContentFiles`: vengono usati i contenuti della cartella contentfiles.
* `Build`: vengono usate le proprietà/destinazioni nella cartella build.
* `Native`: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* `Analyzers`: vengono usati gli analizzatori.

In alternativa, l'attributo può contenere:

* `None`: nessuno degli asset viene usato.
* `All`: vengono usati tutti gli asset.

* L'elemento `<DotnetCliToolReference>` DotnetCliToolReference specifica lo strumento dell'interfaccia della riga di comando che l'utente vuole ripristinare nel contesto del progetto. Si tratta di una sostituzione per il nodo `tools` in `project.json`. 

```xml
<DotnetCliToolReference Include="<package-id>" Version="" />
```

## <a name="version"></a>Versione
`Version` specifica la versione del pacchetto da ripristinare. L'attributo rispetta le regole dello schema di numerazione delle versioni NuGet.

* RuntimeIdentifiers L'elemento `<RuntimeIdentifiers>` consente di specificare un elenco delimitato da punto e virgola di [identificatori di runtime (RID)](../../rid-catalog.md) per il progetto. I RID consentono di pubblicare distribuzioni autonome. 

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```


* RuntimeIdentifier L'elemento `<RuntieIdentifier>` consente di specificare un solo [identificatore di runtime (RID)](../../rid-catalog.md) per il progetto. I RID consentono di pubblicare una distribuzione autonoma. 

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```


* PackageTargetFallback L'elemento `<PackageTargetFallback>` consente di specificare un set di destinazioni compatibili da usare durante il ripristino di pacchetti. È progettato per consentire ai pacchetti che usano il TxM dotnet di interagire con pacchetti che non dichiarano un TxM dotnet. Se il progetto usa il TxM dotnet, anche tutti i pacchetti da cui si dipende devono avere un TxM dotnet, a meno che non si aggiunga `<PackageTargetFallback>` al progetto per consentire alle piattaforme non dotnet di essere compatibili con dotnet. 

L'esempio seguente include i fallback per tutte le destinazioni nel progetto: 

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

L'esempio seguente specifica i fallback solo per la destinazione `netcoreapp1.0`:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp1.0'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="nuget-metadata-properties"></a>Proprietà dei metadati NuGet
Con il passaggio a MSbuild, i metadati di input usati per la creazione di un pacchetto NuGet sono stati spostati da file project.json a csproj. Gli input sono proprietà di MSBuild. L'elenco seguente include le proprietà usate come input per il processo di creazione del pacchetto quando si usa il comando `dotnet pack` o la destinazione di MSBuild `Pack` che fa parte dell'SDK. 

* IsPackable
* PackageVersion
* PackageId
* Titolo
* Autori
* Descrizione
* Copyright
* PackageRequireLicenseAcceptance
* PackageLicenseUrl
* PackageProjectUrl
* PackageIconUrl
* PackageReleaseNotes
* PackageTags
* PackageOutputPath
* IncludeSymbols
* IncludeSource
* PackageTypes
* IsTool
* RepositoryUrl
* RepositoryType
* NoPackageAnalysis
* MinClientVersion
* IncludeBuildOutput
* IncludeContentInPack
* BuildOutputTargetFolder
* ContentTargetFolders
* NuspecFile
* NuspecBasePath
* NuspecProperties


<!--HONumber=Feb17_HO2-->


