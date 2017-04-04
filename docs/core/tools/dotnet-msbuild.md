---
title: Comando dotnet-msbuild - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-msbuild consente di accedere alla riga di comando di MSBuild.
keywords: dotnet-msmsbuild, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/15/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 069909ab3890b75502602f57fc15df19bc7dd614
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>Nome

`dotnet-msbuild`: consente di compilare un progetto e tutte le relative dipendenze.

## <a name="synopsis"></a>Riepilogo

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>Descrizione

Il comando `dotnet msbuild` consente di accedere a un'istanza completamente funzionante di MSBuild.

Il comando ha le stesse funzionalità del client della riga di comando di MSBuild esistente. Le opzioni sono uguali. Usare [Riferimenti alla riga di comando di MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference) per ottenere informazioni sulle opzioni disponibili. 

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet msbuild`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet msbuild /p:Configuration=Release`

Eseguire la destinazione di pubblicazione e pubblicare per il RID `osx.10.11-x64`:

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`
