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
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: e83c8ad302590bcd77129c3ff325e498da751e69

---

#<a name="dotnetpack"></a>dotnet-pack

## <a name="name"></a>Nome

`dotnet-pack`: comprime il codice in un pacchetto NuGet

## <a name="synopsis"></a>Riepilogo

`dotnet pack [--help] [--output]  
    [--no-build] [--build-base-path]  
    [--configuration]  [--version-suffix]
    [project]`  

## <a name="description"></a>Descrizione

Il comando `dotnet pack` consente di compilare il progetto e creare pacchetti NuGet. Il risultato di questa operazione sono due pacchetti con l'estensione `nupkg`. Un pacchetto contiene il codice e l'altro contiene i simboli di debug. 

Le dipendenze NuGet del progetto compresse vengono aggiunte al file NUSPEC, in modo che possano essere risolte durante l'installazione del pacchetto. I riferimenti da progetto a progetto non sono inseriti all'interno del progetto. Attualmente è necessario disporre di un pacchetto per ogni progetto se sono presenti dipendenze da progetto a progetto.

`dotnet pack` per impostazione predefinita compila innanzitutto il progetto. Per evitare questo passaggio, passare l'opzione `--no-build`. Può essere utile negli scenari di compilazione di integrazione continua (CI, Continuous Integration), in cui ad esempio si sa che il codice è stato appena compilato. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`[project]` 
    
Progetto da comprimere. Può essere un percorso di un file [project.json](project-json.md) o di una directory. Se omesso, per impostazione predefinita sarà la directory corrente. 

`-o|--output <OUTPUT_DIRECTORY>`

Inserisce i pacchetti compilati nella directory specificata. 

`--no-build`

Non compila il progetto prima della compressione. 

`--build-base-path`

Inserisce gli elementi di compilazione temporanei nella directory specificata. Per impostazione predefinita, vengono collocati nella directory `obj` all'interno della directory corrente. 

`-c|--configuration <Debug|Release>`

Configurazione da usare durante la compilazione del progetto. Se non è specificata, per impostazione predefinita sarà `Debug`.

`--version-suffix`

Aggiorna l'asterisco nel suffisso della versione del pacchetto `-*` con una stringa specificata.

## <a name="examples"></a>Esempi

Comprimere il progetto nella directory corrente:

`dotnet pack`

Comprimere il progetto app1:

`dotnet pack ~/projects/app1/project.json`
    
Comprimere il progetto nella directory corrente e inserire i pacchetti risultanti nella cartella specificata:

`dotnet pack --output nupkgs`

Comprimere il progetto nella directory corrente e inserirlo nella cartella specificata, ignorando il passaggio relativo alla compilazione:

`dotnet pack --no-build --output nupkgs`

Comprimere il progetto corrente e aggiornare la versione dei pacchetti risultante con il suffisso specificato. Ad esempio, la versione `1.0.0-*` verrà aggiornata in `1.0.0-ci-1234`.

`dotnet pack --version-suffix "ci-1234"`


<!--HONumber=Nov16_HO1-->


