---
title: Comando dotnet-remove package - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-remove package offre un&quot;opzione utile per rimuovere il riferimento al pacchetto NuGet in un progetto.
keywords: dotnet-remove, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2fcc8d37-16b3-4581-8038-832160e72d36
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: a321610540534a63bd12a8f878950b75e882c3d4
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-remove-package"></a>dotnet-remove package

## <a name="name"></a>Nome

`dotnet-remove package`: rimuove il riferimento al pacchetto da un file di progetto.

## <a name="synopsis"></a>Riepilogo

`dotnet remove [<PROJECT>] package <PACKAGE_NAME> [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet remove package` offre un'opzione utile per rimuovere un riferimento al pacchetto NuGet da un progetto.

## <a name="arguments"></a>Argomenti

`PROJECT`

Specifica il file di progetto. Se non specificato, il comando ne cercherà uno nella directory corrente.

`PACKAGE_NAME`

Riferimento al pacchetto da rimuovere.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

## <a name="examples"></a>Esempi

Rimuove il pacchetto NuGet `Newtonsoft.Json` da un progetto nella directory corrente:

`dotnet remove package Newtonsoft.Json`
