---
title: Informazioni di riferimento su csproj | .NET Core SDK
description: Informazioni sulle differenze tra i file csproj esistenti e .NET Core
keywords: informazioni di riferimento, csproj, .NET Core
author: blackdwarf
ms.author: mairaw
manager: wpickett
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: af32bc592762d7e8cb4e3b180656d9c3464df4a5

---

<a name="additions-to-csproj-format-for-net-core"></a>Aggiunte al formato di file csproj per .NET Core
----------------------------------------

# <a name="overview"></a>Panoramica 
Questo documento descrive le modifiche aggiunte ai file csproj come parte del passaggio da project.json a csproj e [MSBuild](https://github.com/Microsoft/MSBuild). Questo documento descrive **solo gli elementi differenziali dei file csproj non principali**. Per altre informazioni sui riferimenti e la sintassi generale del file di progetto, consultare la documentazione del [file di progetto MSBuild](). 

> **Nota:** questo documento verrà ampliato, è quindi opportuno consultarlo per verificare la presenza di aggiornamenti. 

# <a name="additions"></a>Aggiornamenti

## <a name="packagereference"></a>PackageReference
Specifica una dipendenza NuGet nel progetto. L'attributo `Include` specifica l'ID del pacchetto. 

```xml
<PackageReference Include="<package-id>">
    <Version></Version>
    <PrivateAssets></PrivateAssets>
    <IncludeAssets></IncludeAssets>
    <ExcludeAssets></ExcludeAssets>
</PackageReference>
```

### <a name="version"></a>Versione
`<Version>` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

### <a name="includeassets"></a>IncludeAssets
L'elemento figlio `<IncludeAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` devono essere utilizzate. 

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib disponibili per la compilazione
* Runtime: i contenuti della cartella runtime distribuita
* ContentFiles: i contenuti della cartella contentfiles usata
* Build: le proprietà/destinazioni nella cartella build usate
* Native: i contenuti degli asset nativi copiati nella cartella di output per il runtime
* Analyzers: gli analizzatori usati

In alternativa, l'elemento può contenere:

* None: nessuno degli elementi usati
* All: tutti gli elementi usati

### <a name="excludeassets"></a>ExcludeAssets
L'elemento figlio `<ExcluseAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` non devono essere utilizzate.

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib disponibili per la compilazione
* Runtime: i contenuti della cartella runtime distribuita
* ContentFiles: i contenuti della cartella contentfiles usata
* Build: le proprietà/destinazioni nella cartella build usate
* Native: i contenuti degli asset nativi copiati nella cartella di output per il runtime
* Analyzers: gli analizzatori usati

In alternativa, l'elemento può contenere:

* None: nessuno degli elementi usati
* All: tutti gli elementi usati

### <a name="privateassets"></a>PrivateAssets
L'elemento figlio `<PrivateAssets>` specifica quali risorse appartenenti al pacchetto specificato dall'elemento padre `<PackageReference>` devono essere utilizzate. Specifica, inoltre, che tali risorse non devono essere trasmesse al progetto successivo. 

> **Nota:** si tratta di un nuovo termine per l'elemento `SupressParent` di project.json/xproj. 

L'elemento può contenere uno o più dei valori seguenti:

* Compile: i contenuti della cartella lib disponibili per la compilazione
* Runtime: i contenuti della cartella runtime distribuita
* ContentFiles: i contenuti della cartella contentfiles usata
* Build: le proprietà/destinazioni nella cartella build usate
* Native: i contenuti degli asset nativi copiati nella cartella di output per il runtime
* Analyzers: gli analizzatori usati

In alternativa, l'elemento può contenere:

* None: nessuno degli elementi usati
* All: tutti gli elementi usati

## <a name="dotnetclitoolreference"></a>DotnetCliToolReference
L'elemento `<DotnetCliToolReference>` specifica lo strumento dell'interfaccia della riga di comando che l'utente vuole ripristinare nel contesto del progetto. Si tratta di una sostituzione per il nodo `tools` in `project.json`. 

### <a name="version"></a>Versione
`<Version>` specifica la versione del pacchetto da ripristinare. L'elemento rispetta le regole dello schema di numerazione delle versioni NuGet.

## <a name="runtimeidentifiers"></a>Identificatori di runtime
L'elemento `<RuntimeIdentifiers>` consente di specificare un elenco delimitato da punto e virgola di [identificatori di runtime](../../rid-catalog.md) per il progetto. In questo modo, è possibile eseguire la pubblicazione di distribuzioni autonome. 




<!--HONumber=Nov16_HO3-->


