---
title: Comando dotnet-build - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-build consente di compilare un progetto e tutte le relative dipendenze.
keywords: dotnet-build, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e1a2bc4-a919-4a86-8f33-a9b218b1fcb3
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: e5deac8a7b8faac97ccf8b801f274a2c03268d64
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-build"></a>dotnet-build

## <a name="name"></a>Nome

`dotnet-build`: consente di compilare un progetto e tutte le relative dipendenze.

## <a name="synopsis"></a>Riepilogo

`dotnet build [<PROJECT>] [-o|--output] [-f|--framework] [-c|--configuration] [-r|--runtime] [--version-suffix] [--no-incremental] [--no-dependencies] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet build` compila il progetto e le relative dipendenze in un set di file binari. I file binari includono il codice del progetto in Intermediate Language (IL) con estensione *dll* e i file di simboli usati per il debug con estensione *pdb*. Viene generato un file JSON di dipendenze (*\*.deps.json*) con l'elenco delle dipendenze dell'applicazione. Viene generato un file *\*.runtimeconfig.json* che specifica il runtime condiviso e la relativa versione per l'applicazione.

Se il progetto ha dipendenze di terze parti, ad esempio librerie di NuGet, queste dipendenze vengono risolte dalla cache NuGet e non sono disponibili con l'output compilato del progetto. Per queste ragioni, il prodotto di `dotnet build` non è pronto per essere trasferito in un altro computer per l'esecuzione. Questo comportamento si differenzia da quello di .NET Framework in cui la compilazione di un progetto eseguibile (un'applicazione) genera un output che è possibile eseguire in qualsiasi computer in cui è installato .NET Framework. Per ottenere un'esperienza simile in .NET Core, è necessario usare il comando [dotnet publish](dotnet-publish.md). Per altre informazioni, vedere [Distribuzione di applicazioni .NET Core](../deploying/index.md). 

Per la compilazione è necessario il file *project.assets.json*, che elenca le dipendenze dell'applicazione. Il file viene creato quando si esegue [`dotnet restore`](dotnet-restore.md) prima di compilare il progetto. Senza il file di asset sul posto, gli strumenti non sono in grado di risolvere gli assembly di riferimento, generando così errori.

`dotnet build` usa MSBuild per compilare il progetto e quindi supporta le compilazioni parallele e incrementali. Per altre informazioni, vedere [Compilazioni incrementali](https://docs.microsoft.com/visualstudio/msbuild/incremental-builds). 

In aggiunta alle proprie opzioni, il comando `dotnet build` accetta anche le opzioni di MSBuild, ad esempio `/p` per l'impostazione delle proprietà o `/l` per la definizione di un logger. Altre informazioni su queste opzioni sono disponibili in [Riferimenti alla riga di comando di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference). 

La proprietà `<OutputType>` nel file di progetto determina se il progetto è eseguibile o meno. L'esempio seguente descrive un progetto che produce codice eseguibile:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Per generare una libreria, omettere la proprietà `<OutputType>`. La differenza principale nell'output di compilazione è che la DLL di linguaggio intermedio per una libreria non contiene punti di ingresso e non può essere eseguita. 

## <a name="arguments"></a>Argomenti

`PROJECT`

File di progetto da compilare. Se non viene specificato un file di progetto, MSBuild cerca nella directory di lavoro corrente un file con estensione che termina con *proj* e usa tale file.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui inserire i file binari compilati. È necessario definire anche `--framework` quando si specifica questa opzione.

`-f|--framework <FRAMEWORK>`

Esegue la compilazione per un [framework](../../standard/frameworks.md) specifico. Il framework deve essere definito nel [file di progetto](csproj.md).

`-c|--configuration <CONFIGURATION>`

Definisce la configurazione di compilazione. Se omessa, la configurazione di compilazione predefinita è `Debug`. Usare `Release` per creare una configurazione per il rilascio.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Specifica il runtime di destinazione. Per un elenco degli identificatori di runtime (RID, Runtime Identifier), vedere il [catalogo RID](../rid-catalog.md).

`--version-suffix <VERSION_SUFFIX>`

Definisce il suffisso di versione per un asterisco (`*`) nel campo del file di progetto relativo alla versione. Il formato rispetta le linee guida della versione NuGet.

`--no-incremental`

Contrassegna la compilazione come non sicura per la compilazione incrementale. Disattiva la compilazione incrementale e impone una ricompilazione pulita del grafico delle dipendenze del progetto.

`--no-dependencies`

Ignora i riferimenti da progetto a progetto e compila solo il progetto radice specificato per la compilazione.

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet build`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet build --configuration Release`

Compilare un progetto e le relative dipendenze per un runtime specifico ( in questo esempio, Ubuntu 16.04):

`dotnet build --runtime ubuntu.16.04-x64`

