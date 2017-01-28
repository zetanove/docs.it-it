---
title: Comando dotnet-msbuild | .NET Core SDK
description: Il comando dotnet-msmsbuild consente di accedere alla riga di comando MSmsbuild
keywords: dotnet-msmsbuild, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: mairaw
manager: wpickett
ms.date: 10/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: ffdc40ba-ef33-463e-aa35-b0af1fe615a2
translationtype: Human Translation
ms.sourcegitcommit: cde9d9577246a9025d646ce2a6d574a18512146e
ms.openlocfilehash: 51a3afdcf591b8147790d78471c6fee63ceb7f2d

---

#<a name="dotnet-msbuild"></a>dotnet-msbuild

## <a name="name"></a>Nome 
dotnet-msbuild: consente di creare un progetto e tutte le relative dipendenze 

## <a name="synopsis"></a>Riepilogo

`dotnet msbuild <msbuild_arguments>`

## <a name="description"></a>Descrizione
Il comando `dotnet msbuild` consente di accedere a un'istanza completamente funzionante di MSBuild 

Il comando ha le stesse funzionalità del client della riga di comando MSBuild esistente. Le opzioni sono uguali. È possibile usare la [documentazione esistente](https://msdn.microsoft.com/en-us/library/ms164311.aspx) per acquisire familiarità con i riferimenti ai comandi. 

## <a name="examples"></a>Esempi

Compilare un progetto e le relative dipendenze:

`dotnet msbuild`

Compilare un progetto e le relative dipendenze usando la configurazione per il rilascio:

`dotnet msbuild /p:Configuration=Release`

Eseguire la destinazione di pubblicazione e pubblicare per il RID `osx.10.11-x64`:

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`



<!--HONumber=Nov16_HO3-->


