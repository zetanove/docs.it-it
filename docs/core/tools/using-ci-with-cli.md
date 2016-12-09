---
title: Uso di .NET Core SDK e dei relativi strumenti in integrazione continua
description: Uso di .NET Core SDK e dei relativi strumenti in integrazione continua
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 5fb15297-a276-417f-8c4f-267281357769
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 0fda867f1d29caaca716ad27baf6e43146cb99df

---

# <a name="using-net-core-sdk-and-tools-in-continuous-integration-ci"></a>Uso di .NET Core SDK e dei relativi strumenti in integrazione continua

## <a name="overview"></a>Panoramica
Questo documento descrive l'uso di .NET Core SDK e dei relativi strumenti sul server di compilazione. Su un server di compilazione di integrazione continua è in genere opportuno automatizzare l'installazione. In teoria, l'automazione non dovrebbe richiedere privilegi amministrativi, se possibile. 

Per le soluzioni di integrazione continua SaaS, sono disponibili diverse opzioni. In questo documento verranno presentate due opzioni molto comuni, [TravisCI](https://travis-ci.org/) e [AppVeyor](https://www.appveyor.com/). Esistono, naturalmente, molti altri servizi, ma i meccanismi di installazione e uso sono in genere simili.

## <a name="installation-options-for-ci-build-servers"></a>Opzioni di installazione per i server di compilazione di integrazione continua

## <a name="using-the-native-installers"></a>Uso di programmi di installazione nativi
Se l'uso di programmi di installazione nativi che richiedono privilegi amministrativi non rappresenta un problema, è possibile usare questi programmi per ogni piattaforma per configurare il server di compilazione. Questo approccio, soprattutto nel caso dei server di compilazione Linux, offre il vantaggio dell'installazione automatica delle dipendenze necessarie per l'esecuzione dell'SDK. I programmi di installazione nativi installano anche una versione dell'SDK a livello di sistema. Se si preferisce non usare questa opzione, è consigliabile leggere la sezione [Uso dello script di installazione](#using-the-installer-script) più avanti in questo documento. 

Questo approccio è semplice. Per Linux, è possibile scegliere di usare un sistema di gestione pacchetti basato su feed, ad esempio `apt-get` per Ubuntu o `yum` per CentOS, oppure i pacchetti stessi (ovvero DEB o RPM). Nel primo caso è necessario configurare il feed che contiene i pacchetti.

Per le piattaforme Windows, è possibile usare il file MSI. 

Tutti i file binari sono reperibili nella [pagina introduttiva a .NET Core](https://aka.ms/dotnetcoregs) che contiene riferimenti alle ultime versioni stabili. Se si desiderano versioni più recenti (e potenzialmente instabili) oppure l'ultima versione, è possibile usare i collegamenti dal [repository dell'interfaccia della riga di comando](https://github.com/dotnet/cli). 

## <a name="using-the-installer-script"></a>Uso dello script di installazione
Lo script di installazione consente l'installazione senza privilegi di amministratore nel server di compilazione e offre inoltre un meccanismo di automazione molto semplice. Lo script scarica i file ZIP/tarball necessari, li decomprime e aggiunge anche il percorso di installazione locale alla variabile PATH, in modo che gli strumenti possano essere chiamati immediatamente dopo l'installazione. 

Lo script di installazione può essere facilmente automatizzato all'inizio della compilazione per recuperare e installare la versione necessaria dell'SDK. Per "versione necessaria" si intende la versione richiesta dall'applicazione compilata. È possibile scegliere il percorso di installazione in modo da poter installare l'SDK in locale e quindi pulire i dati al termine della compilazione. Ciò consente di aggiungere incapsulamento e atomicità al processo di compilazione. 

Per informazioni di riferimento sullo script di installazione, vedere il documento relativo a [dotnet-install](dotnet-install-script.md). 

### <a name="dealing-with-the-dependencies"></a>Gestione delle dipendenze
Se si usa lo script di installazione, le dipendenze native non vengono installate automaticamente ed è quindi necessario installarle se nel sistema operativo non sono presenti. L'elenco dei prerequisiti è incluso nel [repository dell'interfaccia della riga di comando](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md). 

## <a name="ci-services-setup-examples"></a>Esempi di configurazione dei servizi di integrazione continua
Le sezioni seguenti mostrano esempi di configurazioni tramite le offerte SaaS di integrazione continua indicate in precedenza. 

### <a name="travisci"></a>TravisCI

Il servizio [travis-ci](https://travis-ci.org/) può essere configurato per l'installazione di .NET Core SDK con il linguaggio `csharp` e la chiave `dotnet`.

È sufficiente usare:

```yaml
dotnet: 1.0.0-preview2-003121
```

Travis può eseguire sia un processo `osx` (OS X 10.11) sia un processo `linux` (Ubuntu 14.04) in una matrice di compilazione. Per altre informazioni, vedere l'[esempio .travis.yml](https://github.com/dotnet/docs/blob/master/.travis.yml).

### <a name="appveyor"></a>AppVeyor

Per il servizio [appveyor.com ci](https://www.appveyor.com/), .NET Core SDK preview2 è installato nell'immagine del processo di compilazione `Visual Studio 2015`.

È sufficiente usare:

```yaml
os: Visual Studio 2015
```

È possibile installare una versione specifica di .NET Core SDK. Per altre informazioni, vedere l'[esempio appveyor.yml](https://github.com/dotnet/docs/blob/master/appveyor.yml). 

Nell'esempio, i file binari di .NET Core SDK vengono scaricati, decompressi in una sottodirectory e aggiunti alla variabile di ambiente `PATH`.

È possibile aggiungere una matrice di compilazione per eseguire test di integrazione con più versioni di .NET Core SDK.

```yaml
environment:
  matrix:
    - CLI_VERSION: 1.0.0-preview2-003121
    - CLI_VERSION: Latest

install:
  # .NET Core SDK binaries
  - ps: $url = "https://dotnetcli.blob.core.windows.net/dotnet/preview/Binaries/$($env:CLI_VERSION)/dotnet-dev-win-x64.$($env:CLI_VERSION.ToLower()).zip"
  # follow normal installation from binaries
```




<!--HONumber=Nov16_HO3-->


