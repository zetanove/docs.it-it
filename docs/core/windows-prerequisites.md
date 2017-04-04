---
title: Prerequisiti per .NET Core in Windows | Documentazione Microsoft
description: Informazioni sulle dipendenze per sviluppare ed eseguire applicazioni .NET Core in computer Windows.
keywords: .NET Core, Windows, prerequisiti, dipendenze, Visual Studio
author: mairaw
ms.author: mairaw
ms.date: 03/07/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: ff143583ba62fc1d82561e739a75107e50ebee88
ms.openlocfilehash: 13947fd81940c1ccb606cb4cd765dc230fe95c0f
ms.lasthandoff: 03/20/2017

---

# <a name="prerequisites-for-net-core-on-windows"></a>Prerequisiti per .NET Core in Windows

Questo articolo descrive le dipendenze e i prerequisiti per distribuire ed eseguire applicazioni .NET Core in computer Windows e svilupparle con Visual Studio.

## <a name="supported-windows-versions"></a>Versioni di Windows supportate

.NET Core è supportato nelle versioni di Windows seguenti:

* Windows 7 SP1
* Windows 8,1
* Windows 10
* Windows Server 2008 R2 SP1 (Full Server o Server Core)
* Windows Server 2012 SP1 (Full Server o Server Core)
* Windows Server 2012 R2 SP1 (Full Server o Server Core)
* Windows Server 2016 (Full Server, Server Core o Nano Server)

Per l'elenco completo dei sistemi operativi supportati, vedere le [note sulla versione di .NET Core](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md).

## <a name="net-core-dependencies"></a>Dipendenze .NET Core

.NET Core richiede Visual C++ Redistributable per l'esecuzione in versioni di Windows precedenti a Windows 10 e Windows Server 2016. Questa dipendenza viene installata automaticamente se si usa il programma di installazione di .NET Core. È invece necessario installare manualmente [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145) se si esegue l'installazione di .NET Core tramite [script](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-install-script) o si distribuisce un'applicazione .NET Core autonoma.

> [!NOTE]
> <em>Solo per i computer Windows 7 e Windows Server 2008:</em><br>
> Verificare che l'installazione di Windows sia aggiornata e includa l'hotfix [KB2533623](https://support.microsoft.com/en-us/kb/2533623) installato tramite Windows Update.

## <a name="prerequisites-with-visual-studio-2017"></a>Prerequisiti con Visual Studio 2017

È possibile usare l'editor preferito per sviluppare applicazioni .NET Core con .NET Core SDK. Se si vuole tuttavia sviluppare applicazioni .NET Core in Windows in un ambiente di sviluppo integrato, è possibile usare [Visual Studio 2017](#visual-studio-2017).

> [!IMPORTANT]
> Anche se è possibile usare Visual Studio 2015 con una versione di anteprima degli strumenti di .NET Core, questi progetti saranno basati su *project.json*, che ora è deprecato. Visual Studio 2017 usa file di progetto basati su MSBuild. Per altre informazioni sulle modifiche del formato, vedere [High-level overview of changes](./tools/cli-msbuild-architecture.md) (Panoramica generale delle modifiche).

Per usare Visual Studio 2017 per lo sviluppo di app .NET Core, è necessario avere l'ultima versione di Visual Studio installata con il set di strumenti di **sviluppo multipiattaforma di .NET Core** selezionato (nella sezione **Altri set di strumenti**).
![Screenshot dell'installazione di Visual Studio 2017 con il carico di lavoro "Sviluppo multipiattaforma .NET Core" selezionato](./media/windows-prerequisites/vs_workloads.jpg)

Ci sono edizioni diverse di Visual Studio 2017. Per iniziare, è possibile scaricare [Visual Studio Community 2017](https://www.visualstudio.com/downloads/) gratuitamente.  Per altre informazioni sul processo di installazione di Visual Studio, vedere [Install Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio) (Installare Visual Studio 2017).

Per verificare di avere a disposizione la versione più recente di Visual Studio 2017, seguire questa procedura:
 +
 +*Dal menu**?**scegliere**Informazioni su Microsoft Visual Studio**. +* Nella finestra di dialogo **Informazioni su Microsoft Visual Studio** il numero di versione deve essere 15.0.26228.4 o superiore.

Nelle [note sulla versione ](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes) è possibile trovare altre informazioni sulle modifiche in Visual Studio 2017.

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546
