---
title: Comando dotnet-build | Microsoft Docs
description: Il comando dotnet-build consente di compilare un progetto e tutte le relative dipendenze.
keywords: dotnet-build, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e1a2bc4-a919-4a86-8f33-a9b218b1fcb3
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 17c2db54f871795c370a6475c21e36736a6b46c3
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-build"></a>dotnet-build

## <a name="name"></a>Nome

`dotnet-build`: consente di compilare un progetto e tutte le relative dipendenze.

## <a name="synopsis"></a>Riepilogo

```
dotnet build [project] [-o|--output] [-f|--framework] [-c|--configuration] [-r|--runtime] [--version-suffix] [--no-incremental] [--no-dependencies] [-v|--verbosity]
dotnet build [--help]
```

## <a name="description"></a>Descrizione
Il comando `dotnet build` compila il progetto e le relative dipendenze in un set di file binari. I file binari sono i file di simboli usati per il debug (con estensione `*.pdb`) e il codice del progetto in Intermediate Language (IL) con estensione `*.dll`. Verrà anche prodotto un file JSON che elenca le dipendenze dell'applicazione con estensione `*.deps.json`. Verrà infine prodotto anche un file `runtime.config.json`. Questo file specifica il runtine condiviso e la versione in cui verrà eseguito il codice compilato. 

Se il progetto ha dipendenze di terze parti, ad esempio librerie di NuGet, queste dipendenze verranno risolte dalla cache NuGet e non saranno disponibili con l'output compilato del progetto. Per queste ragioni, il prodotto di `dotnet build` non è pronto per essere trasferito in un altro computer per essere eseguito. Ciò si differenzia dal comportamento di .NET Framework in cui la compilazione di un progetto eseguibile (un'applicazione) produce un output che è possibile eseguire in qualsiasi computer in cui è installato .NET Framework. Per ottenere un'esperienza simile in .NET Core, è necessario usare il comando [dotnet publish](dotnet-publish.md). Altre informazioni sono disponibili nel documento [Distribuzione di applicazioni .NET Core](../deploying/index.md). 

Per la compilazione è necessario un file *assets.json*, ovvero un file che elenca tutte le dipendenze dell'applicazione. È quindi necessario eseguire [`dotnet restore`](dotnet-restore.md) prima della compilazione del progetto. La mancanza del file assets è indicata dall'incapacità degli strumenti di risolvere gli assembly di riferimento generando errori. 

Poiché `dotnet build` usa MSBuild per compilare il progetto, sono supportate le compilazioni parallele e le compilazioni incrementali. Per altre informazioni su questi argomenti, vedere la [documentazione di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild). 

In aggiunta alle relative opzioni, il comando `dotnet build` accetterà anche le opzioni MSBuild, ad esempio `/p` per l'impostazione delle proprietà o `/l` per la definizione di un logger. Per altre informazioni su queste opzioni, vedere la documentazione del comando [`dotnet msbuild`](dotnet-msbuild.md). Se si vuole sapere quando 

La proprietà `<OutputType>` nel file di progetto determina se il progetto è eseguibile o meno. L'esempio seguente descrive un progetto che produce codice eseguibile: 


```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Per produrre una libreria, è sufficiente omettere la proprietà. La differenza principale nell'output è rappresentata dal fatto che il file DLL IL di una libreria non contiene alcun punto di ingresso e non è possibile eseguirla. 

## <a name="arguments"></a>Argomenti

`project`

File di progetto da compilare.
Se non viene specificato un file di progetto, MSBuild cerca nella directory di lavoro corrente un file con estensione che termina con `proj` e usa il file.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui inserire i file binari compilati. È necessario definire anche `--framework` quando si specifica questa opzione.

`-f|--framework <FRAMEWORK>`

Esegue la compilazione per un framework specifico. Il framework deve essere definito nel [file di progetto](csproj.md).

`-c|--configuration [Debug|Release]`

Definisce una configurazione in cui eseguire la compilazione. Se omessa, il valore predefinito è `Debug`.

`-r|--runtime [RUNTIME_IDENTIFIER]`

Runtime di destinazione per cui eseguire la compilazione. Per un elenco degli identificatori di runtime (RID, Runtime Identifier) che è possibile usare, vedere il [catalogo RID](../rid-catalog.md).

`--version-suffix [VERSION_SUFFIX]`

Definisce l'elemento che deve sostituire `*` nel campo relativo alla versione del file di progetto. Il formato rispetta le linee guida della versione NuGet.

`--no-incremental`

Contrassegna la compilazione come non sicura per la compilazione incrementale. Disattiva la compilazione incrementale e impone una ricompilazione pulita del grafico delle dipendenze del progetto.

`--no-dependencies`

Ignora i riferimenti da progetto a progetto e compila solo il progetto radice specificato per la compilazione.

`-v|--verbosity`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet build`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet build --configuration Release`

Compilare un progetto e le relative dipendenze per un runtime specifico ( in questo esempio, Ubuntu 16.04):

`dotnet build --runtime ubuntu.16.04-x64`
