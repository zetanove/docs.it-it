---
title: Comando dotnet-restore | Microsoft Docs
description: Informazioni sul ripristino delle dipendenze e degli strumenti specifici per il progetto tramite il comando dotnet-restore.
keywords: dotnet-restore, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fd7a5769-afbe-4838-bbaf-3ae0cfcbb914
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 594956488dee39903feba44e10d6bb81801412a4

---

#<a name="dotnet-restore-net-core-tools-rc4"></a>dotnet-restore (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [dotnet-restore](../../tools/dotnet-restore.md).

## <a name="name"></a>Nome

`dotnet-restore`: ripristina le dipendenze e gli strumenti di un progetto.

## <a name="synopsis"></a>Riepilogo

`dotnet restore [root] [--help] [--source]  
    [--packages] [--disable-parallel] [--configfile] 
    [--no-cache] [--ignore-failed-sources] [--no-dependencies]`

## <a name="description"></a>Descrizione

Il comando `dotnet restore` usa NuGet per ripristinare le dipendenze e gli strumenti specifici del progetto definiti nel file di progetto. Per impostazione predefinita, il ripristino delle dipendenze e degli strumenti viene eseguito in parallelo.

Per ripristinare le dipendenze, NuGet necessita dei feed in cui si trovano i pacchetti. I feed in genere vengono forniti tramite il file di configurazione NuGet.config. Un feed predefinito è presente durante l'installazione degli strumenti dell'interfaccia della riga di comando. È possibile specificare più feed creando un file NuGet.config nella directory del progetto. È possibile specificare i feed anche tramite chiamata sul prompt dei comandi. 

Per le dipendenze è possibile specificare dove vengono inseriti i pacchetti ripristinati durante l'operazione di ripristino, usando l'argomento `--packages`. Se il percorso non è specificato, viene usata la cache predefinita dei pacchetti NuGet. Si trova nella directory `.nuget/packages` nella directory home dell'utente in tutti i sistemi operativi (ad esempio, */home/user1* in Linux or *C:\Users\user1* in Windows).

Per gli strumenti specifici del progetto, `dotnet restore` ripristina innanzitutto il pacchetto in cui viene compresso lo strumento e quindi ripristina le dipendenze dello strumento come specificato nel file di progetto.

## <a name="options"></a>Opzioni

`[root]` 
    
Percorso facoltativo del file di progetto da ripristinare. 

`-h|--help`

Stampa una breve guida per il comando.

`-s|--source <SOURCE>`

Specifica un'origine dei pacchetti NuGet da usare durante l'operazione di ripristino. Questa impostazione sostituisce tutte le origini specificate nel file NuGet.config. È possibile specificare più origini, selezionando questa opzione più volte.

`--packages <PACKAGES_DIRECTORY]`

Specifica la directory in cui inserire i pacchetti ripristinati. 

`--disable-parallel`

Disabilita il ripristino di più progetti in parallelo. 

`--configfile <FILE>`

File di configurazione NuGet (NuGet.config) da usare per l'operazione di ripristino.

`--no-cache`

Specifica di non memorizzare nella cache pacchetti e richieste HTTP.

` --ignore-failed-sources`

Segnala le origini con esito negativo solo se sono presenti pacchetti che soddisfano il requisito di versione.

`--no-dependencies`

Quando si ripristina un progetto con riferimenti P2P, non vengono ripristinati i riferimenti, ma solo il progetto radice. 

## <a name="examples"></a>Esempi

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente:

`dotnet restore` 

Ripristinare le dipendenze e gli strumenti per il progetto `app1` che si trova nel percorso specificato:

`dotnet restore ~/projects/app1/app1.csproj`
    
Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente usando il percorso di file specificato come origine di fallback:

`dotnet restore -f c:\packages\mypackages` 

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente usando i due percorsi di file specificati come origini di fallback:

`dotnet restore -f c:\packages\mypackages -f c:\packages\myotherpackages` 

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente e includere solo gli errori nell'output:

`dotnet restore --verbosity Error`



<!--HONumber=Feb17_HO2-->


