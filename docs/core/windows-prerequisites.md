---
title: Prerequisiti per .NET Core in Windows | Documentazione Microsoft
description: Informazioni sulle dipendenze per sviluppare ed eseguire applicazioni .NET Core in computer Windows.
keywords: .NET Core, Windows, prerequisiti, dipendenze, Visual Studio
author: mairaw
ms.author: mairaw
ms.date: 01/05/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
translationtype: Human Translation
ms.sourcegitcommit: a8019c9fc25ef458aa555743e61cd83a3beb11ed
ms.openlocfilehash: b5c088da7d1155414a08995ae0d72154af891190
ms.lasthandoff: 01/24/2017

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

Per l'elenco completo dei [sistemi operativi supportati](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md#rtm-platform-support), vedere le [note sulla versione di .NET Core 1.0.0](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0.md).

## <a name="net-core-dependencies"></a>Dipendenze .NET Core

.NET Core richiede Visual C++ Redistributable per l'esecuzione in versioni di Windows precedenti a Windows 10 e Windows Server 2016. Questa dipendenza viene installata automaticamente se si usa il programma di installazione di .NET Core. È invece necessario installare manualmente [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145) se si esegue l'installazione di .NET Core tramite [script](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-install-script) o si distribuisce un'applicazione .NET Core autonoma.

> [!NOTE]
> <em>Solo per i computer Windows 7 e Windows Server 2008:</em><br>
> Verificare che l'installazione di Windows sia aggiornata e includa l'hotfix [KB2533623](https://support.microsoft.com/en-us/kb/2533623) installato tramite Windows Update.

## <a name="prerequisites-with-visual-studio"></a>Prerequisiti con Visual Studio

È possibile usare l'editor preferito per sviluppare applicazioni .NET Core con .NET Core SDK. Per sviluppare applicazioni .NET Core in Windows con Visual Studio, tuttavia, è possibile usare due versioni:

* [Visual Studio 2015](#visual-studio-2015)
* [Visual Studio 2017 RC](#visual-studio-2017-rc)

I progetti creati con Visual Studio 2015 saranno basati su project.json per impostazione predefinita, mentre i progetti creati con Visual Studio 2017 RC saranno sempre basati su MSBuild. Per altre informazioni sulle modifiche del formato, vedere [High-level overview of changes](./preview3/tools/layering.md) (Panoramica generale delle modifiche).

### <a name="visual-studio-2015"></a>Visual Studio 2015

Per usare Visual Studio 2015 per sviluppare app .NET Core, è necessario:

* Visual Studio 2015 Update 3.3 o versione successiva.

   Esistono [edizioni](https://www.visualstudio.com/vs/compare) diverse di Visual Studio 2015. Per iniziare, è possibile scaricare [Visual Studio Community 2015](https://www.visualstudio.com/downloads/) gratuitamente. 

   Per verificare di avere a disposizione [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx), seguire questa procedura:

   * Dal menu **Guida** scegliere **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio).
   * Nella finestra di dialogo **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio) il numero di versione sarà 14.0.25424.00 o successivo e dovrebbe includere la dicitura "Update 3".
   * Se non si dispone di tale aggiornamento, è necessario scaricare e installare [Visual Studio 2015 Update 3](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).
   * Se si dispone dell'aggiornamento ma il numero di versione è precedente a 14.0.25424.00, è necessario scaricare e installare [Visual Studio 2015 Update 3.3](https://msdn.microsoft.com/library/mt752379.aspx).

   Per altre informazioni sulle modifiche apportate in Update 3, vedere le [note sulla versione di .NET Core](https://www.visualstudio.com/news/releasenotes/vs2015-update3-vs).

* Estensione NuGet Manager per Visual Studio

   NuGet è lo strumento di gestione dei pacchetti per la piattaforma di sviluppo Microsoft, incluso .NET Core. Per creare app .NET Core, è necessario [NuGet 3.5.0-beta](https://dist.nuget.org/visualstudio-2015-vsix/v3.5.0-beta/NuGet.Tools.vsix) o versione successiva.

* .NET Core Tooling Preview 2

   Scaricare e installare [.NET Core 1.0.1 - VS 2015 Tooling Preview 2][sdk]. 

   Il pacchetto .NET Core Tooling installa .NET Core, i modelli di progetto e altri strumenti per Visual Studio 2015.

   > [!NOTE]
   > Attualmente non è possibile scaricare un programma di installazione offline per [.NET Core 1.0.1 - VS 2015 Tooling Preview 2][sdk]. È invece necessario scaricare il [normale programma di avvio automatico][sdk] ed eseguirlo con un'opzione della riga di comando, ad esempio `/layout c:\path`, per ottenere un layout offline. Questo layout può essere usato in seguito come programma di installazione offline. È sufficiente avviare il file eseguibile dal percorso locale. Si noti che, poiché si tratta di un layout completo, questa procedura scarica tutti i pacchetti per tutte le lingue supportate, per un totale di circa 1 GB.

### <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

Se si vuole usare Visual Studio 2017 RC per lo sviluppo di app .NET Core, è necessario disporre dell'ultima versione di Visual Studio RC installata, con il carico di lavoro ".NET Core e Docker (Preview)" selezionato. 

Esistono edizioni diverse di Visual Studio 2017 RC. Per iniziare, è possibile scaricare gratuitamente [Visual Studio Community 2017 RC](https://www.visualstudio.com/vs/visual-studio-2017-rc/#downloadvs).  Per altre informazioni sul processo di installazione di Visual Studio, vedere [Install Visual Studio 2017 RC](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio) (Installare Visual Studio 2017 RC).

Per verificare di avere a disposizione la versione più recente di Visual Studio 2017 RC, seguire questa procedura:

* Dal menu **Guida** scegliere **About Microsoft Visual Studio** (Informazioni su Microsoft Visual Studio).
* Nella finestra di dialogo **Informazioni su Microsoft Visual Studio** il numero di versione deve essere 15.0.26020.0 o successivo.

Per altre informazioni sulle modifiche apportate in Visual Studio 2017 RC, vedere le [note sulla versione](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes).

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546

