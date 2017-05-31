---
title: Comando dotnet-restore - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Informazioni sul ripristino delle dipendenze e degli strumenti specifici per il progetto tramite il comando dotnet-restore.
keywords: dotnet-restore, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/24/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fd7a5769-afbe-4838-bbaf-3ae0cfcbb914
ms.translationtype: Human Translation
ms.sourcegitcommit: 602c173ff8d114a76c5598cd0826485ac32a2e72
ms.openlocfilehash: fd4fd6ef2e8482a2b961ccbca1f5227d80c8be53
ms.contentlocale: it-it
ms.lasthandoff: 03/29/2017

---

# <a name="dotnet-restore"></a>dotnet-restore

## <a name="name"></a>Nome

`dotnet-restore`: ripristina le dipendenze e gli strumenti di un progetto.

## <a name="synopsis"></a>Riepilogo

`dotnet restore [<ROOT>] [-s|--source] [-r|--runtime] [--packages] [--disable-parallel] [--configfile] [--no-cache] [--ignore-failed-sources] [--no-dependencies] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet restore` usa NuGet per ripristinare le dipendenze e gli strumenti specifici del progetto definiti nel file di progetto. Per impostazione predefinita, il ripristino delle dipendenze e degli strumenti viene eseguito in parallelo.

Per ripristinare le dipendenze, NuGet necessita dei feed in cui si trovano i pacchetti. I feed vengono forniti in genere tramite il file di configurazione *NuGet.config*. Durante l'installazione degli strumenti dell'interfaccia della riga di comando, viene fornito un file di configurazione predefinito. È possibile specificare più feed creando un file *NuGet.config* nella directory del progetto. È inoltre possibile specificare feed aggiuntivi per ogni chiamata a un prompt dei comandi. 

Per le dipendenze è possibile specificare dove vengono inseriti i pacchetti ripristinati durante l'operazione di ripristino usando l'argomento `--packages`. Se questa destinazione non viene specificata, viene usata la cache predefinita dei pacchetti NuGet che si trova nella directory `.nuget/packages` della directory home dell'utente in tutti i sistemi operativi (ad esempio, */home/user1* in Linux or *C:\Users\user1* in Windows).

Per gli strumenti specifici del progetto, `dotnet restore` ripristina innanzitutto il pacchetto in cui viene compresso lo strumento e quindi ripristina le dipendenze dello strumento come specificato nel file di progetto.

Il funzionamento del comando `dotnet restore` può essere modificato da alcune impostazioni del file *NuGet.Config*, se è presente. Se ad esempio si imposta `globalPackagesFolder` in *NuGet.Config* i pacchetti NuGet ripristinati vengono posizionati nella cartella specificata. Questo approccio rappresenta un'alternativa all'impostazione dell'opzione `--packages` per il comando `dotnet restore`. Per altre informazioni, vedere [NuGet.Config reference](https://docs.microsoft.com/nuget/schema/nuget-config-file) (Informazioni di riferimento su NuGet.Config).

## <a name="arguments"></a>Argomenti

`ROOT` 
    
Percorso facoltativo del file di progetto da ripristinare.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-s|--source <SOURCE>`

Specifica un'origine dei pacchetti NuGet da usare durante l'operazione di ripristino. Questa impostazione esegue l'override di tutte le origini specificate nel file *NuGet.config*. È possibile specificare più origini, selezionando questa opzione più volte.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Specifica un runtime per il ripristino dei pacchetti. Questo runtime viene usato per ripristinare i pacchetti di runtime non esplicitamente elencati nel tag `<RuntimeIdentifiers>` del file *csproj*. Per un elenco degli identificatori di runtime (RID, Runtime Identifier), vedere il [catalogo RID](../rid-catalog.md). Specificare più origini selezionando questa opzione più volte.

`--packages <PACKAGES_DIRECTORY>`

Specifica la directory per i pacchetti ripristinati. 

`--disable-parallel`

Disabilita il ripristino di più progetti in parallelo. 

`--configfile <FILE>`

File di configurazione NuGet (*NuGet.config*) da usare per l'operazione di ripristino.

`--no-cache`

Specifica di non memorizzare nella cache pacchetti e richieste HTTP.

`--ignore-failed-sources`

Segnala le origini con esito negativo solo se sono presenti pacchetti che soddisfano il requisito di versione.

`--no-dependencies`

Durante il ripristino di un progetto con riferimenti da progetto a progetto, ripristinare il progetto radice e non i riferimenti.

`--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente:

`dotnet restore` 

Ripristinare le dipendenze e gli strumenti per il progetto `app1` che si trova nel percorso specificato:

`dotnet restore ~/projects/app1/app1.csproj`
    
Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente usando il percorso di file specificato come origine:

`dotnet restore -s c:\packages\mypackages` 

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente usando i due percorsi di file specificati come origini:

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages` 

Ripristinare le dipendenze e gli strumenti per il progetto nella directory corrente e mostrare solo un output minimo:

`dotnet restore --verbosity minimal`

