---
title: Comando dotnet-add reference | Microsoft Docs
description: Il comando dotnet-add reference offre un&quot;opzione utile per aggiungere riferimenti da progetto a progetto.
keywords: dotnet-add, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: spboyer
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5e2a3efd-443c-4f23-a1b1-a662a5387879
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 7d23377244cfe60730b50bd247209de6e90bec70
ms.lasthandoff: 03/07/2017

---
# <a name="dotnet-add-reference"></a>dotnet-add reference

## <a name="name"></a>Nome

`dotnet-add reference`: aggiunge riferimenti da progetto a progetto.

## <a name="synopsis"></a>Riepilogo

```
dotnet add [project] reference [-f|--framework] <project_references>
dotnet add reference [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet add reference` offre un'opzione utile per aggiungere i riferimenti al progetto in un progetto. Dopo l'esecuzione del comando, vengono aggiunti al file di progetto i frammenti [`<ProjectReference>`](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-items).

```xml
<ItemGroup>
  <ProjectReference Include="app.csproj" />
  <ProjectReference Include="..\lib2\lib2.csproj" />
  <ProjectReference Include="..\lib1\lib1.csproj" />
</ItemGroup>
```

## <a name="arguments"></a>Argomenti

`project`

File di progetto da usare. Se non specificato, il comando ne cercherà uno nella directory corrente.

`project_references`

Riferimenti da progetto a progetto da aggiungere. È possibile specificare uno o più progetti. Il criterio GLOB è supportato nei terminali basati su Unix/Linux.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.

`-f|--framework <FRAMEWORK>`

Aggiunge riferimenti al progetto solo quando la destinazione è un framework specifico.

## <a name="examples"></a>Esempi

Aggiungere un riferimento al progetto:

`dotnet add app/app.csproj reference lib/lib.csproj`

Aggiungere più riferimenti al progetto:

`dotnet add reference lib1/lib1.csproj lib2/lib2.csproj`

Aggiungere più riferimenti al progetto usando il criterio GLOB in Linux/Unix:

`dotnet add app/app.csproj reference **/*.csproj`
