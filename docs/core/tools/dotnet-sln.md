---
title: Comando dotnet-sln | Microsoft Docs
description: Il comando dotnet-sln rappresenta un&quot;opzione comoda per aggiungere, rimuovere ed elencare i progetti in un file di soluzione.
keywords: dotnet-sln, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: e5a72d3e-c14b-4b0a-a978-c5e54a0988c6
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 84c2a9cab36dcfa76f90d75c83f4988ba441b0a8
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-sln"></a>dotnet-sln

## <a name="name"></a>Nome

`dotnet-sln`: consente di modificare un file di soluzione .NET Core.

## <a name="synopsis"></a>Riepilogo

```
dotnet sln [<solution_name>] add <project> <project>
dotnet sln [<solution_name>] add **/**
dotnet sln [<solution_name>] remove <project> <project>
dotnet sln [<solution_name>] remove **/**
dotnet sln [<solution_name>] list
dotnet sln [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet sln` offre un modo comodo per aggiungere, rimuovere ed elencare i progetti in un file di soluzione.

## <a name="commands"></a>Comandi:

`add <project>`

`add **/*`

Aggiunge uno o più progetti più al file di soluzione. I criteri GLOB sono supportati nei terminali basati su Unix/Linux.

`remove <project>`

`remove **/*`

Rimuove uno o più progetti più dal file di soluzione. I criteri GLOB sono supportati nei terminali basati su Unix/Linux.

`list`

Elenca tutti i progetti in un file di soluzione.

## <a name="arguments"></a>Argomenti

`solution_name`

File di soluzione da usare. Se non specificato, il comando ne cercherà uno nella directory corrente. Se sono presenti più file di soluzione nella directory, è necessario specificarne uno.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

## <a name="examples"></a>Esempi

Aggiungere un progetto a una soluzione:

`dotnet sln todo.sln add todo-app/todo-app.csproj`

Aggiungere un progetto alla soluzione nella directory corrente:

`dotnet sln add todo-app.csproj`

Rimuovere un progetto da una soluzione:

`dotnet sln todo.sln remove todo-app/todo-app.csproj`

Aggiungere più progetti a una soluzione usando criteri GLOB:

`dotnet sln add **/**/*.fsproj`

