---
title: Comando dotnet-pack | .NET Core SDK
description: Il comando dotnet-pack consente di creare pacchetti NuGet per il progetto .NET Core.
keywords: dotnet-pack, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: mairaw
manager: wpickett
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 8b4b8cef-f56c-4a10-aa01-fde8bfaae53e
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 5aca8db50bf80606ff94562a6014c396b0ef770e

---

#<a name="dotnet-pack"></a>dotnet-pack

## <a name="name"></a>Nome

`dotnet-pack`: comprime il codice in un pacchetto NuGet

## <a name="synopsis"></a>Riepilogo

`dotnet pack [--help] [--output]  
    [--no-build] [--include-symbols]
    [--include-source] [--servicable]
    [--configuration]  [--version-suffix]
    [project]`  

## <a name="description"></a>Descrizione

Il comando `dotnet pack` consente di compilare il progetto e creare pacchetti NuGet. Il risultato di questo comando è un pacchetto NuGet. Se l'opzione `--include-symbols` è presente, verrà creato un altro pacchetto contenente i simboli di debug. 

Le dipendenze NuGet del progetto compresse vengono aggiunte al file NUSPEC, in modo che possano essere risolte durante l'installazione del pacchetto. I riferimenti da progetto a progetto non sono inseriti all'interno del progetto. Attualmente è necessario disporre di un pacchetto per ogni progetto se sono presenti dipendenze da progetto a progetto.

`dotnet pack` per impostazione predefinita compila innanzitutto il progetto. Per evitare questo passaggio, passare l'opzione `--no-build`. Può essere utile negli scenari di compilazione di integrazione continua (CI, Continuous Integration), in cui ad esempio si sa che il codice è stato appena compilato. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`[project]` 
    
Progetto da comprimere. Può essere un percorso a un [file csproj](csproj.md) o a una directory. Se omesso, per impostazione predefinita sarà la directory corrente. 

`-o|--output <OUTPUT_DIRECTORY>`

Inserisce i pacchetti compilati nella directory specificata. 

`--no-build`

Non compila il progetto prima della compressione. 

`--include-source`

Include i file di origine nel pacchetto NuGet. I file di origine sono inclusi nella cartella `src` del pacchetto nupkg. 

`--include-symbols`

Generare il pacchetto nupkg dei simboli. 

`-c|--configuration <Debug|Release>`

Configurazione da usare durante la compilazione del progetto. Se non è specificata, per impostazione predefinita sarà `Debug`.

`--version-suffix`

Aggiorna l'asterisco nel suffisso della versione del pacchetto `-*` con una stringa specificata.

## <a name="examples"></a>Esempi

Comprimere il progetto nella directory corrente:

`dotnet pack`

Comprimere il progetto app1:

`dotnet pack ~/projects/app1/project.csproj`
    
Comprimere il progetto nella directory corrente e inserire i pacchetti risultanti nella cartella specificata:

`dotnet pack --output nupkgs`

Comprimere il progetto nella directory corrente e inserirlo nella cartella specificata, ignorando il passaggio relativo alla compilazione:

`dotnet pack --no-build --output nupkgs`

Comprimere il progetto corrente e aggiornare la versione dei pacchetti risultante con il suffisso specificato. Ad esempio, la versione `1.0.0-*` verrà aggiornata in `1.0.0-ci-1234`.

`dotnet pack --version-suffix "ci-1234"`



<!--HONumber=Nov16_HO3-->


