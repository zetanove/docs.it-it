---
title: Informazioni di riferimento di csproj | Microsoft Docs
description: Informazioni sulle differenze tra i file csproj esistenti e .NET Core
keywords: informazioni di riferimento, csproj, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: dfa7cc0f7005269b4e2560c8bbc8b049ed02cc1a

---

# <a name="additions-to-the-csproj-format-for-net-core"></a>Aggiunte al formato csproj per .NET Core

[!INCLUDE[preview-warning](../../../includes/warning.md)]

Questo documento descrive le modifiche aggiunte ai file csproj come parte del passaggio da `project.json` a `csproj` e [MSBuild](https://github.com/Microsoft/MSBuild). Per altre informazioni sulla sintassi generale dei file di progetto e informazioni di riferimento, vedere la documentazione del [file di progetto MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-project-file-schema-reference).  

## <a name="additions"></a>Aggiornamenti

### <a name="packagereference"></a>PackageReference
Specifica una dipendenza NuGet nel progetto. L'attributo `Include` specifica l'ID del pacchetto. 

```xml
<PackageReference Include="<package-id>">
    <Version></Version>
    <PrivateAssets></PrivateAssets>
    <IncludeAssets></IncludeAssets>
    <ExcludeAssets></ExcludeAssets>
</PackageReference>
```

#### <a name="version"></a>Versione
`<Version>` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

#### <a name="includeassets"></a>IncludeAssets
L'elemento figlio `<IncludeAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` devono essere utilizzate. 

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib sono disponibili per la compilazione.
* Runtime: vengono distribuiti i contenuti della cartella runtime.
* ContentFiles: vengono usati i contenuti della cartella contentfiles.
* Build: vengono usate le proprietà/destinazioni nella cartella build.
* Native: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* Analyzers: vengono usati gli analizzatori.

In alternativa, l'elemento può contenere:

* None: nessuno degli asset viene usato.
* All: vengono usati tutti gli asset.

#### <a name="excludeassets"></a>ExcludeAssets
L'elemento figlio `<ExcludeAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` non devono essere utilizzate.

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib sono disponibili per la compilazione.
* Runtime: vengono distribuiti i contenuti della cartella runtime.
* ContentFiles: vengono usati i contenuti della cartella contentfiles.
* Build: vengono usate le proprietà/destinazioni nella cartella build.
* Native: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* Analyzers: vengono usati gli analizzatori.

In alternativa, l'elemento può contenere:

* None: nessuno degli asset viene usato.
* All: vengono usati tutti gli asset.

#### <a name="privateassets"></a>PrivateAssets
L'elemento figlio `<PrivateAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` devono essere utilizzate. Specifica, inoltre, che tali risorse non devono essere trasmesse al progetto successivo. 

> [!NOTE]
> Questo è un nuovo termine per l'elemento `SuppressParent` di project.json/xproj. 

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib sono disponibili per la compilazione.
* Runtime: vengono distribuiti i contenuti della cartella runtime.
* ContentFiles: vengono usati i contenuti della cartella contentfiles.
* Build: vengono usate le proprietà/destinazioni nella cartella build.
* Native: i contenuti degli asset nativi vengono copiati nella cartella di output per il runtime.
* Analyzers: vengono usati gli analizzatori.

In alternativa, l'elemento può contenere:

* None: nessuno degli asset viene usato.
* All: vengono usati tutti gli asset.

### <a name="dotnetclitoolreference"></a>DotnetCliToolReference
L'elemento `<DotnetCliToolReference>` specifica lo strumento dell'interfaccia della riga di comando che l'utente vuole ripristinare nel contesto del progetto. Si tratta di una sostituzione per il nodo `tools` in `project.json`. 

#### <a name="version"></a>Versione
`<Version>` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

### <a name="runtimeidentifiers"></a>Identificatori di runtime
L'elemento `<RuntimeIdentifiers>` consente di specificare un elenco delimitato da punto e virgola di [identificatori di runtime (RID)](../../rid-catalog.md) per il progetto. I RID consentono di pubblicare distribuzioni autonome. 


<!--HONumber=Jan17_HO3-->


