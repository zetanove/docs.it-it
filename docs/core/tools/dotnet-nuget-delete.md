---
title: Comando dotnet-nuget-delete | Microsoft Docs
description: Il comando dotnet-nuget-delete rimuove dall&quot;elenco o elimina un pacchetto dal server.
keywords: dotnet-nuget-delete, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: karann-msft
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 6ddffde4-c789-4e90-990e-d35f6a6565d4
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 2ce157e3f32f3e899245e38bb4520b17be3e0b32
ms.lasthandoff: 03/07/2017

---
#<a name="dotnet-nuget-delete"></a>dotnet-nuget-delete

## <a name="name"></a>Nome

`dotnet-nuget-delete`: rimuove dall'elenco o elimina un pacchetto dal server. 

## <a name="synopsis"></a>Riepilogo

```
dotnet nuget delete [<package_name> <package_version>] [-s|--source] [--non-interactive] [-k|--api-key] [--force-english-output]
dotnet nuget delete [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet nuget delete` rimuove dall'elenco o elimina un pacchetto dal server. Per NuGet.org, l'azione è rimuovere il pacchetto dall'elenco.

## <a name="options"></a>Opzioni

`-h|--help`

Stampa una breve guida per il comando.  

`-s|--source <SOURCE>`

Specifica l'URL del server. Gli URL supportati per nuget.org includono `http://www.nuget.org`, `http://www.nuget.org/api/v3` e `http://www.nuget.org/api/v2/package`. Per i feed privati, sostituire il nome host (ad esempio, `%hostname%/api/v3`).

`--non-interactive`

Non richiede input o conferme dell'utente.

`-k|--api-key <API_KEY>`

Chiave API per il server.

`--force-english-output`

Forza la visualizzazione in inglese dell'output della riga di comando.

## <a name="examples"></a>Esempi

Elimina la versione 1.0 del pacchetto MyPackage:

`dotnet nuget delete MyPackage 1.0` 

Elimina la versione 1.0 del pacchetto MyPackage, senza richiedere all'utente credenziali o altro input:

`dotnet nuget delete MyPackage 1.0 --non-interactive`

