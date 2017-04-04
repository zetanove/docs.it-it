---
title: Comando dotnet-publish - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-publish consente di pubblicare il progetto .NET Core in una directory.
keywords: dotnet-publish, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: f2ef275a-7c5e-430a-8c30-65f52af62771
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 48bfe6c77ee6c5d905069f47da5512ac63a24b2a
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-publish"></a>dotnet-publish

## <a name="name"></a>Nome

`dotnet-publish`: inserisce l'applicazione e le relative dipendenze in una cartella per la distribuzione in un sistema host.

## <a name="synopsis"></a>Riepilogo

`dotnet publish [<PROJECT>] [-f|--framework] [-r|--runtime] [-o|--output] [-c|--configuration] [--version-suffix] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

`dotnet publish` compila l'applicazione, legge le relative dipendenze specificate nel file di progetto e pubblica il set di file risultante in una directory. L'output conterrà quanto segue:

* Codice Intermediate Language (IL) in un assembly con un'estensione `*.dll`.
* File *\*.deps.json* contenente tutte le dipendenze del progetto.
* File *\*.runtime.config.json* che specifica il runtime condiviso previsto dall'applicazione e altre opzioni di configurazione per il runtime, ad esempio il tipo di Garbage Collection.
* Dipendenze dell'applicazione. Questi dati vengono copiati dalla cache NuGet nella cartella di output.

L'output del comando `dotnet publish` è pronto per la distribuzione in un sistema host (ad esempio un server, un computer PC o Mac o un laptop) per l'esecuzione. Questa è l'unica modalità supportata ufficialmente per preparare l'applicazione per la distribuzione. A seconda del tipo di distribuzione specificato dal progetto, nel sistema host il runtime condiviso di .NET Core può essere installato o meno. Per altre informazioni, vedere [Distribuzione di applicazioni .NET Core](../deploying/index.md). Per la struttura di directory di un'applicazione pubblicata, vedere [Directory structure](https://docs.microsoft.com/en-us/aspnet/core/hosting/directory-structure) (Struttura di directory).

## <a name="arguments"></a>Argomenti

`PROJECT` 

Progetto da pubblicare che, se non specificato, corrisponde per impostazione predefinita alla directory corrente. 

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-f|--framework <FRAMEWORK>`

Pubblica l'applicazione per il [framework di destinazione](../../standard/frameworks.md) specificato. È necessario specificare il framework di destinazione nel file di progetto.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Pubblica l'applicazione per un determinato runtime. Viene usato durante la creazione di una [distribuzione indipendente (SCD, Self-Contained Deployment)](../deploying/index.md#self-contained-deployments-scd). Per un elenco degli identificatori di runtime (RID, Runtime Identifier), vedere il [catalogo RID](../rid-catalog.md). L'impostazione predefinita prevede la pubblicazione di una [distribuzione dipendente da framework (FDD, Framework-Dependent Deployment)](../deploying/index.md#framework-dependent-deployments-fdd).

`-o|--output <OUTPUT_DIRECTORY>`

Specifica il percorso della directory di output. Se non specificato, il percorso predefinito sarà *./bin/[configuration]/[framework]/* per una distribuzione dipendente da framework o *./bin/[configuration]/[framework]/[runtime]* per una distribuzione indipendente.

`-c|--configuration <CONFIGURATION>`

Configurazione da usare durante la compilazione del progetto. Il valore predefinito è `Debug`.

`--version-suffix <VERSION_SUFFIX>`

Definisce il suffisso di versione che sostituirà l'asterisco (`*`) nel campo del file di progetto relativo alla versione.

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Pubblicare il progetto nella directory corrente:

`dotnet publish`

Pubblicare l'applicazione usando il file di progetto specificato:

`dotnet publish ~/projects/app1/app1.csproj`
    
Pubblicare il progetto nella directory corrente usando il framework `netcoreapp1.1`:

`dotnet publish --framework netcoreapp1.1`
    
Pubblicare l'applicazione corrente usando il framework `netcoreapp1.1` e il runtime per `OS X 10.10`. Questo identificatore di runtime deve essere elencato nel file di progetto.

`dotnet publish --framework netcoreapp1.1 --runtime osx.10.11-x64`

## <a name="see-also"></a>Vedere anche

* [Framework di destinazione](../../standard/frameworks.md)
* [Catalogo RID (Runtime IDentifier)](../rid-catalog.md)
