---
title: Comando dotnet-msbuild | Microsoft Docs
description: Il comando dotnet-msbuild consente di accedere alla riga di comando di MSBuild.
keywords: dotnet-msmsbuild, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: a000e49a8672affe5b3bb9bd8a5f7e8095ab0aa9
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>Nome

`dotnet-msbuild`: consente di compilare un progetto e tutte le relative dipendenze.

## <a name="synopsis"></a>Riepilogo

```
dotnet msbuild <msbuild_arguments>
dotnet msbuild [-h]
```

## <a name="description"></a>Descrizione

Il comando `dotnet msbuild` consente di accedere a un'istanza completamente funzionante di MSBuild 

Il comando ha le stesse funzionalità del client della riga di comando di MSBuild esistente. Le opzioni sono uguali. Per acquisire familiarità con le opzioni, vedere [Riferimenti alla riga di comando di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference). 

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet msbuild`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet msbuild /p:Configuration=Release`

Eseguire la destinazione di pubblicazione e pubblicare per il RID `osx.10.11-x64`:

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`
