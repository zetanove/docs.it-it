---
title: Prerequisiti di .NET Core
description: Prerequisiti di .NET Core
keywords: .NET, .NET Core
author: billwagner
manager: wpickett
ms.date: 09/15/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: 130b94a745b0e3222e205d8af26194239130ec9c
ms.openlocfilehash: 2e6483b3f1b8b9e1f36a0f4f7377319871fd5674

---

# <a name="prerequisites-for-windows-development"></a>Prerequisiti per lo sviluppo su Windows

Per lo sviluppo di .NET Core in Windows con Visual Studio sono necessari gli elementi seguenti:

* Una versione supportata del client o del sistema operativo Windows.
* Visual Studio 2015 Update 3.3 o versioni successive
* Estensione NuGet Manager per Visual Studio
* .NET Core Tooling Preview 2

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

Per sviluppare app .NET Core è necessario Visual Studio 2015. È possibile scaricare [Visual Studio Community 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs) gratuitamente. 

Verificare di eseguire [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx):

* Dal menu **Guida** scegliere **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio).
* Nella finestra di dialogo **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio) il numero di versione sarà 14.0.25424.00 o successivo e dovrebbe includere la dicitura "Update 3".
* Se non si dispone di tale aggiornamento, è necessario scaricare e installare [Visual Studio 2015 Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).
* Se si dispone dell'aggiornamento ma il numero di versione è precedente a 14.0.25424.00, è necessario scaricare e installare [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx).

Per altre informazioni sulle modifiche apportate in Update 3, vedere le [note sulla versione di .NET Core](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).

## <a name="nuget-manager-extension-for-visual-studio"></a>Estensione NuGet Manager per Visual Studio

NuGet è lo strumento di gestione dei pacchetti per la piattaforma di sviluppo Microsoft, incluso .NET Core. Per creare .NET Core è necessario [NuGet 3.5.0](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) o versione successiva.

## <a name="net-core-tools-for-visual-studio-2015"></a>Strumenti .NET Core per Visual Studio 2015

Scaricare e installare l'[SDK ][.NET Core 1.0.1 - VS 2015 Tooling Preview 2]. 

Il pacchetto .NET Core Tooling installa .NET Core, i modelli di progetto e altri strumenti per Visual Studio 2015.

> [!NOTE]
Attualmente non è possibile scaricare un programma di installazione offline per l'[SDK ][.NET Core 1.0.1 - VS 2015 Tooling Preview 2]. È invece necessario scaricare l'[SDK] del [normale programma di avvio automatico] ed eseguirlo con un'opzione della riga di comando, ad esempio `/layout c:\path`, per ottenere un layout offline. Questo layout può essere usato in seguito come programma di installazione offline. È sufficiente avviare il file eseguibile dal percorso locale. Si noti che, poiché si tratta di un layout completo, questa procedura scarica tutti i pacchetti per tutte le lingue supportate, per un totale di circa 1 GB.

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546



<!--HONumber=Nov16_HO3-->


