---
title: Comando dotnet-pack - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-pack consente di creare pacchetti NuGet per il progetto .NET Core.
keywords: dotnet-pack, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8dbbb3f7-b817-4161-a6c8-a3489d05e051
ms.translationtype: Human Translation
ms.sourcegitcommit: 14c2e01ab0c30c9f1cbfdcc53ea85fe51a4d8c2e
ms.openlocfilehash: 5a2ea69825fa336b1d8ce2283e214d02c16347e3
ms.contentlocale: it-it
ms.lasthandoff: 05/01/2017

---

# <a name="dotnet-pack"></a>dotnet-pack

## <a name="name"></a>Nome

`dotnet-pack`: comprime il codice in un pacchetto NuGet.

## <a name="synopsis"></a>Riepilogo

`dotnet pack [<PROJECT>] [-o|--output] [--no-build] [--include-symbols] [--include-source] [-c|--configuration] [--version-suffix <VERSION_SUFFIX>] [-s|--serviceable] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet pack` consente di compilare il progetto e creare pacchetti NuGet. Il risultato di questo comando è un pacchetto NuGet. Se l'opzione `--include-symbols` è presente, viene creato un altro pacchetto contenente i simboli di debug. 

Le dipendenze NuGet del progetto compresso vengono aggiunte al file con estensione *nuspec*, in modo da poter essere risolte durante l'installazione del pacchetto. I riferimenti da progetto a progetto non sono inseriti all'interno del progetto. Attualmente è necessario disporre di un pacchetto per ogni progetto se sono presenti dipendenze da progetto a progetto.

Per impostazione predefinita, `dotnet pack` compila prima il progetto. Se si vuole evitare questo comportamento, passare l'opzione `--no-build`. Questo può essere utile negli scenari di compilazione di integrazione continua (CI, Continuous Integration), in cui si sa che il codice è stato compilato in precedenza.

È possibile aggiungere proprietà MSBuild al comando `dotnet pack` per il processo di compressione. Per altre informazioni, vedere [NuGet metadata properties](csproj.md#nuget-metadata-properties) (Proprietà dei metadati NuGet) e [MSBuild Command-Line Reference](/visualstudio/msbuild/msbuild-command-line-reference) (Informazioni di riferimento sulla riga di comando di MSBuild).

## <a name="arguments"></a>Argomenti

`PROJECT` 
    
Progetto da comprimere. Può essere un percorso a un [file csproj](csproj.md) o a una directory. Se omesso, per impostazione predefinita viene usata la directory corrente. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-o|--output <OUTPUT_DIRECTORY>`

Inserisce i pacchetti compilati nella directory specificata. 

`--no-build`

Non compila il progetto prima della compressione. 

`--include-symbols`

Genera i simboli `nupkg`. 

`--include-source`

Include i file di origine nel pacchetto NuGet. I file di origine sono inclusi nella cartella `src` del pacchetto `nupkg`. 

`-c|--configuration <CONFIGURATION>`

Configurazione da usare durante la compilazione del progetto. Se non è specificata, per impostazione predefinita viene usata `Debug`.

`--version-suffix <VERSION_SUFFIX>`

Definisce il valore della proprietà MSBuild `$(VersionSuffix)` nel progetto.

`-s|--serviceable`

Imposta il flag utilizzabile dai servizi nel pacchetto. Per altre informazioni, vedere [.NET Blog: .NET 4.5.1 Supports Microsoft Security Updates for .NET NuGet Libraries](https://aka.ms/nupkgservicing) (Blog .NET: .NET 4.5.1 supporta gli aggiornamenti della sicurezza Microsoft per le librerie NuGet di .NET).

`--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Comprimere il progetto nella directory corrente:

`dotnet pack`

Comprimere il progetto `app1`:

`dotnet pack ~/projects/app1/project.csproj`
    
Comprimere il progetto nella directory corrente e inserire i pacchetti risultanti nella cartella `nupkgs`:

`dotnet pack --output nupkgs`

Comprimere il progetto nella directory corrente e inserirlo nella cartella `nupkgs`, ignorando il passaggio relativo alla compilazione:

`dotnet pack --no-build --output nupkgs`

Con il suffisso della versione del progetto configurato come `<VersionSuffix>$(VersionSuffix)</VersionSuffix>` nel file con estensione *csproj*, comprimere il progetto corrente e aggiornare la versione del pacchetto risultante con il suffisso specificato:

`dotnet pack --version-suffix "ci-1234"`

Impostare la versione del pacchetto su `2.1.0` con la proprietà MSBuild `PackageVersion`:

`dotnet pack /p:PackageVersion=2.1.0`

