---
title: Comando dotnet-nuget-delete | Microsoft Docs
description: Il comando dotnet-nuget-delete rimuove dall&quot;elenco o elimina un pacchetto dal server.
keywords: dotnet-nuget-delete, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: karann-msft
ms.author: mairaw
ms.date: 11/11/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 6ddffde4-c789-4e90-990e-d35f6a6565d4
translationtype: Human Translation
ms.sourcegitcommit: 2ad428dcda9ef213a8487c35a48b33929259abba
ms.openlocfilehash: 787b1427b1064943570cbc361042ab2f20d11088
ms.lasthandoff: 01/21/2017

---

#<a name="dotnet-nuget-delete"></a>dotnet-nuget-delete

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>Nome 
`dotnet-nuget-delete`: rimuove dall'elenco o elimina un pacchetto dal server. 

## <a name="synopsis"></a>Riepilogo

`dotnet nuget delete [<package_name> <package_version>] 
    [--help] [--source] [--non-interactive] 
    [--api-key] [--force-english-output] [--verbosity] [--config-file]`

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

`--verbosity <LEVEL>`

Visualizza la quantità di dettagli nell'output. Il livello può essere `normal`, `quiet` o `detailed`.

`--config-file <FILE>`

File di configurazione NuGet usato in modo specifico per questo comando, a sostituzione di altri file di configurazione individuati dal processo di individuazione e concatenazione dei file di configurazione standard. Il percorso può essere assoluto o relativo.
Per altre informazioni sui file di configurazione, vedere [Configuring NuGet Behavior](https://docs.microsoft.com/nuget/consume-packages/configuring-nuget-behavior) (Configurazione del comportamento di NuGet).

## <a name="examples"></a>Esempi

Elimina la versione 1.0 del pacchetto MyPackage:

`dotnet nuget delete MyPackage 1.0` 

Elimina la versione 1.0 del pacchetto MyPackage, senza richiedere all'utente credenziali o altro input:

`dotnet nuget delete MyPackage 1.0 --non-interactive`

Elimina la versione 1.0 del pacchetto MyPackage, specificando un file di configurazione personalizzato *./config/My.Config*:

`dotnet nuget delete MyPackage 1.0 --config-file ./config/My.Config`

Elimina la versione 1.0 del pacchetto MyPackage con il massimo livello di dettaglio:

`dotnet nuget delete MyPackage 1.0 --verbosity detailed`

