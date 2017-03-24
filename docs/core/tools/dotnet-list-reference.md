---
title: Comando dotnet-list reference | Microsoft Docs
description: Il comando dotnet-list reference offre un&quot;opzione utile per visualizzare un elenco dei riferimenti da progetto a progetto.
keywords: dotnet-list, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 8f954a0c-03f8-4fbc-a529-b313ab12c623
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: e95aa43bfed78d72ef1ea5f3883ae64e06ffaa99
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-list-reference"></a>dotnet-list reference

## <a name="name"></a>Nome

`dotnet-list reference`: visualizza un elenco dei riferimenti da progetto a progetto.

## <a name="synopsis"></a>Riepilogo

```
dotnet list [project] reference
dotnet list reference [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet list reference` offre un'opzione utile per visualizzare un elenco dei riferimenti al progetto per un progetto specificato.

## <a name="arguments"></a>Argomenti

`project`

File di progetto per il quale visualizzare l'elenco dei riferimenti. Se non specificato, il comando ne cercherà uno nella directory corrente.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

## <a name="examples"></a>Esempi

Visualizzare l'elenco dei riferimenti al progetto per il progetto specificato:

`dotnet list app/app.csproj reference`

Visualizzare l'elenco dei riferimenti al progetto per il progetto nella directory corrente:

`dotnet list reference`

