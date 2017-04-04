---
title: Comando dotnet-clean - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-clean consente di pulire la directory corrente.
keywords: dotnet-clean, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: eff65fa1-bab4-4421-8260-d0a284b690b2
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 0bdd8b9ab133ca92e414618412d95d8136d6234a
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-clean"></a>dotnet-clean

## <a name="name"></a>Nome

`dotnet-clean`: pulisce l'output di un progetto. 

## <a name="synopsis"></a>Riepilogo

`dotnet clean [<PROJECT>] [-o|--output] [-f|--framework] [-c|--configuration] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet clean` pulisce l'output della compilazione precedente. Viene implementato come una [destinazione di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets). Per questo motivo, il progetto viene valutato quando tale comando viene eseguito. Vengono puliti solo gli output creati durante la compilazione. Vengono pulite sia la cartella intermedia (*obj*) sia quella dell'output finale (*bin*).

## <a name="arguments"></a>Argomenti

`PROJECT`

Progetto MSBuild da pulire. Se non viene specificato un file di progetto, MSBuild cerca nella directory di lavoro corrente un file con estensione che termina con *proj* e usa tale file.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui vengono inseriti gli output di compilazione. Se al momento della compilazione del progetto è stato specificato il framework, specificare l'opzione `-f|--framework <FRAMEWORK>` con l'opzione della directory di output.

`-f|--framework <FRAMEWORK>`

[Framework](../../standard/frameworks.md) specificato in fase di compilazione. Il framework deve essere definito nel [file di progetto](csproj.md). Se il framework è stato specificato in fase di compilazione, è necessario specificarlo al momento della pulizia.

`-c|--configuration <CONFIGURATION>`

Definisce la configurazione. Se omessa, il valore predefinito è `Debug`. Se è stata specificata durante la fase di compilazione, questa proprietà è necessaria soltanto al momento della pulizia.

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I livelli consentiti sono q[uiet], m[inimal], n[ormal], d[etailed] e diag[nostic].

## <a name="examples"></a>Esempi

Pulire una compilazione predefinita del progetto:

`dotnet clean`

Pulire un progetto compilato con la configurazione di tipo Versione:

`dotnet clean --configuration Release`

