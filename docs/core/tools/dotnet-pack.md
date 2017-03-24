---
title: Comando dotnet-pack | Microsoft Docs
description: Il comando dotnet-pack consente di creare pacchetti NuGet per il progetto .NET Core.
keywords: dotnet-pack, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8dbbb3f7-b817-4161-a6c8-a3489d05e051
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 88289a09a22bf20ec9089ec6a74269cd682a305b
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-pack"></a>dotnet-pack

## <a name="name"></a>Nome

`dotnet-pack`: comprime il codice in un pacchetto NuGet.

## <a name="synopsis"></a>Riepilogo

```
dotnet pack [project] [-o|--output] [--no-build] [--include-symbols] [--include-source] [-c|--configuration] [--version-suffix] [-s|--serviceable] [-v|--verbosity]
dotnet pack [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet pack` consente di compilare il progetto e creare pacchetti NuGet. Il risultato di questo comando è un pacchetto NuGet. Se l'opzione `--include-symbols` è presente, verrà creato un altro pacchetto contenente i simboli di debug. 

Le dipendenze NuGet del progetto compresse vengono aggiunte al file `nuspec` in modo che possano essere risolte durante l'installazione del pacchetto. I riferimenti da progetto a progetto non sono inseriti all'interno del progetto. Attualmente è necessario disporre di un pacchetto per ogni progetto se sono presenti dipendenze da progetto a progetto.

`dotnet pack` per impostazione predefinita compila innanzitutto il progetto. Per evitare questo passaggio, passare l'opzione `--no-build`. Può essere utile negli scenari di compilazione di integrazione continua (CI, Continuous Integration), in cui ad esempio si sa che il codice è stato appena compilato. 

## <a name="arguments"></a>Argomenti

`project` 
    
Progetto da comprimere. Può essere un percorso a un [file csproj](csproj.md) o a una directory. Se omesso, per impostazione predefinita sarà la directory corrente. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-o|--output <OUTPUT_DIRECTORY>`

Inserisce i pacchetti compilati nella directory specificata. 

`--no-build`

Non compila il progetto prima della compressione. 

`--include-symbols`

Genera il pacchetto nupkg dei simboli. 

`--include-source`

Include i file di origine nel pacchetto NuGet. I file di origine sono inclusi nella cartella `src` del pacchetto `nupkg`. 

`-c|--configuration <Debug|Release>`

Configurazione da usare durante la compilazione del progetto. Se non è specificata, per impostazione predefinita sarà `Debug`.

`--version-suffix <VERSION_SUFFIX>`

Definisce il valore della proprietà MSBuild $(VersionSuffix) nel progetto.

`-s|--serviceable`

Imposta il flag utilizzabile dai servizi nel pacchetto. Per altre informazioni, vedere https://aka.ms/nupkgservicing.

`--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Comprimere il progetto nella directory corrente:

`dotnet pack`

Comprimere il progetto app1:

`dotnet pack ~/projects/app1/project.csproj`
    
Comprimere il progetto nella directory corrente e inserire i pacchetti risultanti nella cartella specificata:

`dotnet pack --output nupkgs`

Comprimere il progetto nella directory corrente e inserirlo nella cartella specificata, ignorando il passaggio relativo alla compilazione:

`dotnet pack --no-build --output nupkgs`

Comprimere il progetto corrente e aggiornare la versione del pacchetto risultante con il suffisso specificato. Il suffisso della versione del progetto è configurato come `<VersionSuffix>$(VersionSuffix)</VersionSuffix>` nel file *.csproj*.

`dotnet pack --version-suffix "ci-1234"`
