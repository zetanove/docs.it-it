---
title: Prerequisiti di .NET Core (strumenti dell&quot;anteprima 3)
description: Prerequisiti di .NET Core (strumenti dell&quot;anteprima 3)
keywords: .NET, .NET Core
author: billwagner
ms.author: wiwagn
ms.date: 09/15/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: 07b62bd7163193eff8dc8f61fda7a45a924bba2b
ms.openlocfilehash: ee4ccba7c06f0a7f67e3fe59c885febf895235fd

---

# <a name="prerequisites-for-windows-development-preview-3-tooling"></a>Prerequisiti per lo sviluppo su Windows (strumenti dell'anteprima 3)

Per lo sviluppo di .NET Core in Windows con Visual Studio sono necessari gli elementi seguenti:

* Una versione supportata del client o del sistema operativo Windows.
* Visual Studio 2017 RC o versione successiva
* Strumenti dell'anteprima 3 di .NET Core

## <a name="supported-windows-versions"></a>Versioni di Windows supportate

.NET Core è supportato dalle versioni di Windows seguenti:

* Windows 7 SP1
* Windows 8,1
* Windows 10
* Windows Server 2008 R2 SP1 (Full Server o Server Core)
* Windows Server 2012 SP1 (Full Server o Server Core)
* Windows Server 2012 R2 SP1 (Full Server o Server Core)
* Windows Server 2016 (Full Server, Server Core o Nano Server)

Per l'elenco completo dei [sistemi operativi supportati](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md#rtm-platform-support), vedere le [note sulla versione di .NET Core](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md).

## <a name="net-core-dependencies"></a>Dipendenze .NET Core

Per l'esecuzione di .NET Core in Windows è necessario VC++ Redistributable, che viene installato dal programma di installazione di .NET Core. Se si installa .NET Core tramite lo script del programma di installazione (`dotnet-install.ps1`), è necessario installare VC++ Redistributable in modo manuale. 

La versione di Visual C++ Redistributable varia in base alla versione di Windows.

* Windows 10
    * [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)
* Windows 7+ (non Windows 10)
    * Verificare che l'installazione di Windows sia aggiornata e includa l'hotfix [KB2533623](https://support.microsoft.com/en-us/kb/2533623) installato tramite Windows Update.
    * [Aggiornamento Universal CRT](https://www.microsoft.com/en-us/download/details.aspx?id=48234). Per altre informazioni su Universal CRT, vedere [questo post di blog](https://blogs.msdn.microsoft.com/vcblog/2015/03/03/introducing-the-universal-crt/).

## <a name="visual-studio"></a>Visual Studio

È possibile sviluppare applicazioni .NET Core con qualsiasi editor usando gli strumenti da riga di comando di .NET Core, ma se si vuole usare Visual Studio e l'anteprima 3 degli strumenti di .NET Core, è necessario Visual Studio 2017 RC o versione successiva. È possibile scaricare gratuitamente [Visual Studio Community 2017 RC](https://www.visualstudio.com/vs/visual-studio-2017-rc/). 

Verificare di eseguire Visual Studio 2017 RC:

* Dal menu **Guida** scegliere **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio).
* Nella finestra di dialogo **Informazioni su Microsoft Visual Studio** il numero di versione sarà 15.0.25831.1 o successivo.

Per altre informazioni sulle modifiche apportate in Visual Studio 2017 RC, vedere le [note sulla versione](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes).

Assicurarsi che durante l'installazione sia stato installato il carico di lavoro ".NET Core e Docker (anteprima)". In caso contrario, è possibile eseguire nuovamente l'installazione e selezionarlo.



<!--HONumber=Nov16_HO3-->


