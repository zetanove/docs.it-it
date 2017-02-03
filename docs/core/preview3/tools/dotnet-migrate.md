---
title: Comando dotnet-migrate | Microsoft Docs
description: Il comando dotnet-migrate consente di eseguire la migrazione di un progetto e di tutte le relative dipendenze.
keywords: dotnet-migrate, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 11/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0da07253-5ae1-42e9-9455-bffee9950952
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: 8d83b3f013ecdc1fbf92598a81dfe3a7a2d17054

---

#<a name="dotnet-migrate"></a>dotnet-migrate

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>Nome 
dotnet-migrate: consente di eseguire la migrazione di un progetto .Net Core dall'anteprima 2 all'anteprima 4

## <a name="synopsis"></a>Riepilogo

`dotnet migrate [--help] [--template-file]  
    [--sdk-package-version] [--xproj-file]  
    [--skip-project-references]  [--report-file] [--format-report-file-json]
    [--skip-backup]
    [<arguments>]`

## <a name="description"></a>Descrizione
Il comando `dotnet migrate` eseguirà la migrazione di un progetto valido dell'anteprima 2 basato su `project.json` a un progetto `csproj` valido dell'anteprima 4. Per impostazione predefinita, il comando eseguirà la migrazione del progetto radice e dei riferimenti del progetto contenuti dal progetto radice. Questo comportamento può essere disabilitato usando l'opzione `--skip-project-references` in fase di esecuzione. 

È possibile eseguire la migrazione in uno degli scenari seguenti:

* In un singolo progetto, specificando il file `project.json` per eseguire la migrazione
* In tutte le directory specificate nel file `global.json`, mediante il passaggio in un percorso del file `global.json`
* In tutte le sottodirectory della directory specificata in modo ricorsivo 

Il comando migrate mantiene il file `project.json` di cui è stata eseguita la migrazione all'interno di una directory `backup` che verrà creata se non è già esistente. Questo comportamento può essere sostituito con l'opzione `--skip-backup`. 

Per impostazione predefinita, l'operazione di migrazione restituirà lo stato del processo di migrazione all'output standard (STDOUT). Se si usa l'opzione `--report-file`, tale output verrà salvato anche in un file specificato. 

A partire dall'anteprima 4, il comando `dotnet migrate` supporta solo file `project.json` validi dell'anteprima 2. Ciò significa che non è possibile usarlo per eseguire la migrazione di file `project.json` DNX o dell'anteprima 1 direttamente in csproj. È necessario innanzitutto eseguire la migrazione di tali file ai file project.json dell'anteprima 2 e quindi ai file csproj. In futuro, verrà aggiunto il supporto per i progetti dell'anteprima 1. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-t|--template-file <TEMPLATE_FILE>`

File csproj modello da usare per la migrazione. Per impostazione predefinita, verrà usato lo stesso modello di quello eliminato da `dotnet new`. 

`-v|--sdk-package-version <VERSION>`

Versione del pacchetto SDK a cui verrà fatto riferimento nell'app di cui è stata eseguita la migrazione. Il valore predefinito è la versione dell'SDK in dotnet.

`-x|--xproj-file <FILE>`

Percorso del file xproj da usare. Obbligatorio quando è presente più di un progetto xproj nella directory di un progetto.

`-s|--skip-project-references [Debug|Release]`

Ignora la migrazione dei riferimenti del progetto. Per impostazione predefinita, i riferimenti del progetto vengono migrati in modo ricorsivo.

`-r|--report-file <REPORT_FILE>`

Report di migrazione dell'output a un file oltre che alla console.

`--format-report-file-json <REPORT_FILE>`

File di report di migrazione dell'output come json anziché messaggi utente.

`--skip-backup`

Ignora lo spostamento di project.json, global.json e \*.xproj`backup` a una directory dopo l'esito positivo della migrazione.

## <a name="examples"></a>Esempi

Eseguire la migrazione di un progetto alla directory corrente e a tutte le relative dipendenze da progetto e progetto:

`dotnet migrate`

Eseguire la migrazione di tutti i progetti a cui punta il file `global.json`:

`dotnet migrate path/to/global.json`

Eseguire solo la migrazione del progetto corrente e non delle dipendenze da progetto a progetto e usare una specifica versione dell'SDK:

`dotnet migrate -s -v 1.0.0-preview4`


<!--HONumber=Jan17_HO3-->


