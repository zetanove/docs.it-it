---
title: Comando dotnet-migrate - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-migrate consente di eseguire la migrazione di un progetto e di tutte le relative dipendenze.
keywords: dotnet-migrate, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0da07253-5ae1-42e9-9455-bffee9950952
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: bde4df1c9e84e103c75b0ccc32d7e970b7708b53
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-migrate"></a>dotnet-migrate

## <a name="name"></a>Nome

`dotnet-migrate`: esegue la migrazione di un progetto .NET Core Preview 2 a un progetto .NET Core SDK 1.0.

## <a name="synopsis"></a>Riepilogo

`dotnet migrate [<SOLUTION_FILE|PROJECT_DIR>] [-t|--template-file] [-v|--sdk-package-version] [-x|--xproj-file] [-s|--skip-project-references] [-r|--report-file] [--format-report-file-json] [--skip-backup] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet migrate` esegue la migrazione di un progetto basato su *project.json* Preview 2 valido a un progetto *csproj* .NET Core SDK 1.0 valido. 

Per impostazione predefinita, il comando esegue la migrazione del progetto radice e dei riferimenti del progetto presenti nel progetto radice. Questo comportamento viene disabilitato usando l'opzione `--skip-project-references` in fase di esecuzione. 

È possibile eseguire la migrazione in uno degli scenari seguenti:

* Un singolo progetto, specificando il file *project.json* di cui eseguire la migrazione.
* Tutte le directory specificate nel file *global.json*, passando un percorso del file *global.json*.
* Un file *solution.sln*, dove vengono migrati i progetti a cui viene fatto riferimento nella soluzione.
* Tutte le sottodirectory della directory specificata, in modo ricorsivo.

Il comando `dotnet migrate` mantiene il file *project.json* di cui è stata eseguita la migrazione all'interno di una directory `backup`, che verrà creata se non esiste già. Questo comportamento viene sottoposto a override tramite l'opzione `--skip-backup`. 

Per impostazione predefinita, l'operazione di migrazione restituisce lo stato del processo di migrazione all'output standard (STDOUT). Se si usa l'opzione `--report-file <REPORT_FILE>`, l'output viene salvato nel file specificato. 

Il comando `dotnet migrate` supporta solo progetti basati su *project.json* Preview 2 validi. Questo significa che non è possibile usare questo comando per eseguire la migrazione di progetti basati su DNX o *project.json* Preview 1 direttamente a progetti MSBuild/csproj. È prima necessario eseguire manualmente la migrazione del progetto a un progetto basato su *project.json* Preview 2 e quindi usare il comando `dotnet migrate` per eseguire la migrazione del progetto.

## <a name="arguments"></a>Argomenti

`PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR`

Percorso a uno degli elementi seguenti:

* File *project.json* di cui eseguire la migrazione.
* File *global.json*. Verrà eseguita la migrazione delle cartelle specificate in *global.json*.
* File *solution.sln*. Verrà eseguita la migrazione dei progetti a cui viene fatto riferimento nella soluzione.
* Directory di cui eseguire la migrazione. Verranno cercati in modo ricorsivo i file *project.json* di cui eseguire la migrazione.

Se non è specificata alcuna opzione, verrà impostata automaticamente la directory corrente.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-t|--template-file <TEMPLATE_FILE>`

File csproj modello da usare per la migrazione. Per impostazione predefinita, viene usato lo stesso modello di quello eliminato da `dotnet new console`. 

`-v|--sdk-package-version <VERSION>`

Versione del pacchetto SDK a cui viene fatto riferimento nell'app di cui è stata eseguita la migrazione. Il valore predefinito è la versione dell'SDK in `dotnet new`.

`-x|--xproj-file <FILE>`

Percorso del file xproj da usare. Obbligatorio quando è presente più di un progetto xproj nella directory di un progetto.

`-s|--skip-project-references [Debug|Release]`

Ignora la migrazione dei riferimenti del progetto. Per impostazione predefinita, i riferimenti al progetto vengono migrati in modo ricorsivo.

`-r|--report-file <REPORT_FILE>`

Report di migrazione dell'output a un file oltre che alla console.

`--format-report-file-json <REPORT_FILE>`

File di report di migrazione dell'output come JSON anziché messaggi utente.

`--skip-backup`

Dopo l'esito positivo della migrazione, ignorare lo spostamento di *project.json*, *global.json* e *\*.xproj* in una directory `backup`.

## <a name="examples"></a>Esempi

Eseguire la migrazione di un progetto nella directory corrente e in tutte le relative dipendenze da progetto a progetto:

`dotnet migrate`

Eseguire la migrazione di tutti i progetti inclusi nel file *global.json*:

`dotnet migrate path/to/global.json`

Eseguire solo la migrazione del progetto corrente e non delle dipendenze da progetto a progetto. Usare una versione specifica dell'SDK:

`dotnet migrate -s -v 1.0.0-preview4`
