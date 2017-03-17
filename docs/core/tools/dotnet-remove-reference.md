---
title: Comando dotnet-remove reference | Microsoft Docs
description: Il comando dotnet-remove reference offre un&quot;opzione utile per rimuovere riferimenti da progetto a progetto.
keywords: dotnet-remove, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 889c6b7e-a313-40b1-9fd3-6a6f4c52f1d0
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 1f1a364b703c6b83a9b21ee420d62411bf9cd3ec
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-remove-reference"></a>dotnet-remove reference

## <a name="name"></a>Nome

`dotnet-remove reference`: rimuove i riferimenti da progetto a progetto.

## <a name="synopsis"></a>Riepilogo

```
dotnet remove [project] reference [-f|--framework] <project_references>
dotnet remove reference [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet remove reference` offre un'opzione utile per rimuovere i riferimenti al progetto da un progetto.

## <a name="arguments"></a>Argomenti

`project`

File di progetto da usare. Se non specificato, il comando ne cercherà uno nella directory corrente.

`project_references`

Riferimenti da progetto a progetto da rimuovere. È possibile specificare uno o più progetti. I criteri GLOB sono supportati nei terminali basati su Unix/Linux.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-f|--framework <FRAMEWORK>`

Rimuove il riferimento solo quando la destinazione è un framework specifico.

## <a name="examples"></a>Esempi

Rimuovere un riferimento al progetto dal progetto specificato:

`dotnet remove app/app.csproj reference lib/lib.csproj`

Rimuovere più riferimenti al progetto dal progetto nella directory corrente:

`dotnet remove reference lib1/lib1.csproj lib2/lib2.csproj`

Rimuovere più riferimenti al progetto usando il criterio GLOB:

`dotnet remove app/app.csproj reference **/*.csproj`
