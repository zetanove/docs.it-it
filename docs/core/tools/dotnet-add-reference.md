---
title: Comando dotnet-add - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-add reference offre un&quot;opzione utile per aggiungere riferimenti da progetto a progetto.
keywords: dotnet-add, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e2a3efd-443c-4f23-a1b1-a662a5387879
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 1b342f0aea19c01d7bdae94552019f4c171fd1a2
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-add-reference"></a>dotnet-add reference

## <a name="name"></a>Nome

`dotnet-add reference`: aggiunge riferimenti da progetto a progetto.

## <a name="synopsis"></a>Riepilogo

`dotnet add [<PROJECT>] reference [-f|--framework] <PROJECT_REFERENCES> [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet add reference` offre un'opzione utile per aggiungere i riferimenti al progetto in un progetto. Dopo l'esecuzione del comando, al file di progetto vengono aggiunti gli elementi [`<ProjectReference>`](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-items).

```xml
<ItemGroup>
  <ProjectReference Include="app.csproj" />
  <ProjectReference Include="..\lib2\lib2.csproj" />
  <ProjectReference Include="..\lib1\lib1.csproj" />
</ItemGroup>
```

## <a name="arguments"></a>Argomenti

`PROJECT`

Specifica il file di progetto. Se non specificato, il comando ne cercherà uno nella directory corrente.

`PROJECT_REFERENCES`

Riferimenti da progetto a progetto da aggiungere. Specificare uno o più progetti. I [criteri GLOB](https://en.wikipedia.org/wiki/Glob_(programming)) sono supportati nei sistemi basati su Unix/Linux.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-f|--framework <FRAMEWORK>`

Aggiunge riferimenti al progetto solo quando la destinazione è un [framework](../../standard/frameworks.md) specifico.

## <a name="examples"></a>Esempi

Aggiungere un riferimento al progetto:

`dotnet add app/app.csproj reference lib/lib.csproj`

Aggiungere più riferimenti al progetto:

`dotnet add reference lib1/lib1.csproj lib2/lib2.csproj`

Aggiungere più riferimenti al progetto usando un criterio GLOB in Linux/Unix:

`dotnet add app/app.csproj reference **/*.csproj`

