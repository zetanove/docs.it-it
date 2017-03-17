---
title: Comando dotnet-migrate | Microsoft Docs
description: Il comando dotnet-migrate consente di eseguire la migrazione di un progetto e di tutte le relative dipendenze.
keywords: dotnet-migrate, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0da07253-5ae1-42e9-9455-bffee9950952
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: b7da4df5319e7c17900b9c093347e8a17045a6a3
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-migrate"></a>dotnet-migrate

## <a name="name"></a>Nome 
dotnet-migrate: esegue la migrazione di un progetto .NET Core Preview 2 in un progetto .NET Core SDK 1.0.

## <a name="synopsis"></a>Riepilogo

```
dotnet migrate [-t|--template-file] [-v|--sdk-package-version] [-x|--xproj-file] [-s|--skip-project-references] [-r|--report-file] [--format-report-file-json] [--skip-backup] [<arguments>]
dotnet migrate [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet migrate` eseguirà la migrazione di un progetto basato su *project.json* Preview 2 valido in un progetto *csproj* .NET Core SDK 1.0 valido. 

Per impostazione predefinita, il comando eseguirà la migrazione del progetto radice e dei riferimenti del progetto contenuti dal progetto radice. Questo comportamento può essere disabilitato usando l'opzione `--skip-project-references` in fase di esecuzione. 

È possibile eseguire la migrazione in uno degli scenari seguenti:

* In un singolo progetto specificando il file *project.json* di cui eseguire la migrazione
* In tutte le directory specificate nel file *global.json* passando un percorso al file *global.json*
* In tutte le sottodirectory della directory specificata in modo ricorsivo 

Il comando migrate mantiene il file *project.json* di cui è stata eseguita la migrazione all'interno di una directory `backup` che verrà creata se non è già esistente. Questo comportamento può essere sostituito con l'opzione `--skip-backup`. 

Per impostazione predefinita, l'operazione di migrazione restituirà lo stato del processo di migrazione all'output standard (STDOUT). Se si usa l'opzione `--report-file`, tale output verrà salvato anche in un file specificato. 

Il comando `dotnet migrate` supporta solo file *project.json* Preview 2 validi. Per questa ragione non è possibile usare il comando per eseguire la migrazione di file *project.json* DNX o Preview 1 direttamente in csproj. È necessario innanzitutto eseguire la migrazione dei file in file project.json Preview 2 e quindi in file csproj. In futuro, verrà aggiunto il supporto per i progetti dell'anteprima 1. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-t|--template-file <TEMPLATE_FILE>`

File csproj modello da usare per la migrazione. Per impostazione predefinita, verrà usato lo stesso modello di quello eliminato da `dotnet new console`. 

`-v|--sdk-package-version <VERSION>`

Versione del pacchetto SDK a cui verrà fatto riferimento nell'app di cui è stata eseguita la migrazione. Il valore predefinito è la versione dell'SDK in dotnet.

`-x|--xproj-file <FILE>`

Percorso del file xproj da usare. Obbligatorio quando è presente più di un progetto xproj nella directory di un progetto.

`-s|--skip-project-references [Debug|Release]`

Ignora la migrazione dei riferimenti del progetto. Per impostazione predefinita, i riferimenti al progetto vengono migrati in modo ricorsivo.

`-r|--report-file <REPORT_FILE>`

Report di migrazione dell'output a un file oltre che alla console.

`--format-report-file-json <REPORT_FILE>`

File di report di migrazione dell'output come json anziché messaggi utente.

`--skip-backup`

Ignora lo spostamento di project.json, global.json e \*.xproj`backup` a una directory dopo l'esito positivo della migrazione.

## <a name="examples"></a>Esempi

Eseguire la migrazione di un progetto alla directory corrente e a tutte le relative dipendenze da progetto e progetto:

`dotnet migrate`

Eseguire la migrazione di tutti i progetti a cui punta il file *global.json*:

`dotnet migrate path/to/global.json`

Eseguire solo la migrazione del progetto corrente e non delle dipendenze da progetto a progetto e usare una specifica versione dell'SDK:

`dotnet migrate -s -v 1.0.0-preview4`
