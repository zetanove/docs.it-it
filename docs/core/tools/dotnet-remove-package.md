---
title: Comando dotnet-remove package | Microsoft Docs
description: Il comando dotnet-remove package offre un&quot;opzione utile per rimuovere il riferimento al pacchetto NuGet in un progetto.
keywords: dotnet-remove, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 2fcc8d37-16b3-4581-8038-832160e72d36
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 87c80ad193df9cc3e0feabc41bb58f1d8dda23cd
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-remove-package"></a>dotnet-remove package

## <a name="name"></a>Nome

`dotnet-remove package`: rimuove il riferimento al pacchetto da un file di progetto.

## <a name="synopsis"></a>Riepilogo

```
dotnet remove [project] package <package_name>
dotnet remove package [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet remove package` offre un'opzione utile per rimuovere un riferimento al pacchetto NuGet da un progetto.

## <a name="arguments"></a>Argomenti

`project`

File di progetto da usare. Se non specificato, il comando ne cercherà uno nella directory corrente.

`package_name`

Riferimento al pacchetto da rimuovere.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

## <a name="examples"></a>Esempi

Rimuove il pacchetto NuGet `Newtonsoft.Json` da un progetto nella directory corrente:

`dotnet remove package Newtonsoft.Json`
