---
title: Comando dotnet-nuget-locals | Microsoft Docs
description: Il comando dotnet-nuget-locals cancella o elenca risorse NuGet locali quali cache delle richieste HTTP, cache temporanea o cartella globale dei pacchetti a livello di computer.
keywords: dotnet-nuget-locals, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: karann-msft
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8440229e-317e-4dc1-9463-cba5fdb12c3b
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 3d8ca57c3c9c25a59b98552784b057182c9100a3
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-nuget-locals"></a>dotnet-nuget-locals

## <a name="name"></a>Nome

`dotnet-nuget-locals`: cancella o elenca risorse NuGet locali quali cache delle richieste HTTP, cache temporanea o cartella globale dei pacchetti a livello di computer. 

## <a name="synopsis"></a>Riepilogo

```
dotnet nuget locals <cache_location> [(-c|--clear)|(-l|--list)] [--force-english-output]
dotnet nuget locals [-h|--help]
```

dove `<cache_location>` è uno dei valori seguenti: `all`, `http-cache`, `packages-cache`, `global-packages` o `temp`.

## <a name="description"></a>Descrizione

Il comando `dotnet nuget locals` cancella o elenca risorse NuGet locali quali cache delle richieste HTTP, cache temporanea o cartella globale dei pacchetti a livello di computer.

## <a name="arguments"></a>Argomenti

`all`

Indica che l'operazione specificata deve essere applicata a tutti i tipi di cache, ovvero alla cache delle richieste HTTP, alla cache globale dei pacchetti e alla cache temporanea.

`http-cache`

Indica che l'operazione specificata deve essere applicata soltanto alla cache delle richieste HTTP. Le altre posizioni di cache non sono interessate.

`global-packages`

Indica che l'operazione specificata deve essere applicata soltanto alla cache globale dei pacchetti. Le altre posizioni di cache non sono interessate.

`temp`

Indica che l'operazione specificata deve essere applicata soltanto alla cache temporanea. Le altre posizioni di cache non sono interessate.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-c|--clear`

L'opzione "clear" viene usata per eseguire un'operazione di cancellazione sul tipo di cache specificato. Il contenuto delle directory della cache viene eliminato in modo ricorsivo. Affinché l'operazione abbia esito positivo, l'utente/gruppo che la esegue deve disporre delle autorizzazioni per i file presenti nelle directory della cache. In caso contrario, viene visualizzato un messaggio di errore con l'indicazione delle cartelle e/o dei file che non sono stati cancellati.

`-l|--list`

L'opzione "list" viene usata per visualizzare la posizione del tipo di cache specificato. 

`--force-english-output`

Forza la visualizzazione in inglese dell'output della riga di comando.

## <a name="examples"></a>Esempi

Visualizza i percorsi di tutte le directory locali della cache, ovvero directory della cache HTTP, directory della cache globale dei pacchetti e directory della cache temporanea.

`dotnet nuget locals –l all`

Visualizza il percorso della directory locale della cache HTTP:

`dotnet nuget locals --list http-cache`

Cancella tutti i file presenti in tutte le directory locali della cache, ovvero directory della cache HTTP, directory della cache globale dei pacchetti e directory della cache temporanea.

`dotnet nuget locals --clear all`

Cancella tutti i file presenti nella directory locale della cache globale dei pacchetti:

`dotnet nuget locals -c global-packages`

Cancella tutti i file presenti nella directory locale della cache temporanea:

`dotnet nuget locals -c temp`

## <a name="troubleshooting"></a>Risoluzione dei problemi

Per informazioni sui problemi e sugli errori più comuni relativi all'uso del comando `dotnet-nuget-locals`, vedere [Managing the NuGet cache](https://docs.microsoft.com/nuget/consume-packages/managing-the-nuget-cache) (Gestione della cache NuGet).

