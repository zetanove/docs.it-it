---
title: Prerequisiti per .NET Core in Mac | Microsoft Docs
description: Versioni macOS supportate e dipendenze .NET Core necessarie per lo sviluppo, la distribuzione e l&quot;esecuzione di applicazioni .NET Core su computer macOS.
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 03/16/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: ff143583ba62fc1d82561e739a75107e50ebee88
ms.openlocfilehash: da75f5fd56b7ce66b2c46ef488e6e26c55a63ee2
ms.lasthandoff: 03/20/2017

---

# <a name="prerequisites-for-net-core-on-mac"></a>Prerequisiti per .NET Core in Mac

Questo articolo illustra le versioni macOS supportate e le dipendenze .NET Core necessarie per lo sviluppo, la distribuzione e l'esecuzione di applicazioni .NET Core su computer macOS. Le versioni del sistema operativo e le dipendenze indicate di seguito sono valide per le tre modalità di sviluppo di app .NET Core in ambiente Mac: tramite la [riga di comando con l'editor preferito](tutorials/using-with-xplat-cli.md), con [Visual Studio Code (VS Code)](https://code.visualstudio.com/) e con [Visual Studio per Mac](https://www.visualstudio.com/vs/visual-studio-mac/).

## <a name="supported-macos-versions"></a>Versioni macOS supportate

.NET Core è supportato dalle versioni di macOS seguenti:

* macOS 10.12 "Sierra"
* macOS 10.11 "El Capitan"

Per l'elenco completo dei sistemi operativi supportati, vedere le [note sulla versione di .NET Core](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md).

## <a name="net-core-dependencies"></a>Dipendenze .NET Core

Per l'esecuzione di .NET Core in macOS è necessario OpenSSL. È possibile ottenere facilmente OpenSSL tramite il sistema di gestione pacchetti [Homebrew ("brew")](http://brew.sh/) per macOS. Dopo aver installato *brew*, installare OpenSSL eseguendo i comandi seguenti da un prompt (dei comandi) Terminal:

```Terminal
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

Dopo aver installato OpenSSL, ottenere il [programma di installazione di .NET Core SDK per Mac](https://go.microsoft.com/fwlink/?linkid=843444) ufficiale. La versione più recente è .NET Core 1.1.1. Per le versioni con supporto a lungo termine e per download aggiuntivi, visitare la pagina [.NET Downloads: All downloads](https://www.microsoft.com/net/download/core) (Download .NET: Tutti i download). In caso di problemi con l'installazione in macOS, vedere [Known issues & workarounds](https://github.com/dotnet/core/blob/master/cli/known-issues.md) (Problemi noti e soluzioni alternative).

## <a name="visual-studio-for-mac"></a>Visual Studio per Mac

Per lo sviluppo di .NET Core in macOS con Visual Studio per Mac sono previsti i requisiti seguenti:

* Versione supportata del sistema operativo macOS
* Openssl
* .NET core SDK per Mac
* [Visual Studio per Mac](https://www.visualstudio.com/vs/visual-studio-mac/)

