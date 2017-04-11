---
title: Strumenti dell&quot;interfaccia della riga di comando di .NET Core | Microsoft Docs
description: "Panoramica degli strumenti e delle funzionalità dell&quot;interfaccia della riga di comando."
keywords: interfaccia della riga di comando, strumenti dell&quot;interfaccia della riga di comando, .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/20/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 7c5eee9f-d873-4224-8f5f-ed83df329a59
translationtype: Human Translation
ms.sourcegitcommit: d97a1501ad25b683cbb5d7fbd8bd1b137f7f4046
ms.openlocfilehash: 978dd62d655d0168b5a9c1c9732bc69ca9b256eb
ms.lasthandoff: 04/10/2017

---

# <a name="net-core-command-line-interface-cli-tools"></a>Strumenti dell'interfaccia della riga di comando di .NET Core

L'interfaccia della riga di comando di .NET Core è una nuova toolchain multipiattaforma per lo sviluppo di applicazioni .NET. È un elemento di base su cui possono essere costruiti altri strumenti di livello più elevato, come gli ambienti di sviluppo integrato (IDE, Integrated Development Environment), gli editor e gli agenti di orchestrazione della compilazione.

## <a name="installation"></a>Installazione

È possibile usare programmi di installazione nativi o script della shell di installazione:

* I programmi di installazione nativi sono destinati essenzialmente ai computer degli sviluppatori e si avvalgono del meccanismo di installazione nativo di ogni piattaforma supportata, ad esempio i pacchetti DEB in Ubuntu o i bundle MSI in Windows. Questi programmi installano e configurano l'ambiente in modo da poter essere immediatamente usato dallo sviluppatore ma richiedono privilegi amministrativi sul computer. È possibile visualizzare le istruzioni di installazione nel sito Web [.NET Core installation guide](https://aka.ms/dotnetcoregs) (Guida all'installazione di .NET Core).
* Gli script vengono usati principalmente per configurare i server di compilazione o quando si vuole installare gli strumenti senza privilegi amministrativi. Con l'installazione degli script non vengono installati nel computer anche i prerequisiti, che devono essere installati manualmente. Per altre informazioni, vedere l'[argomento di riferimento sugli script di installazione](dotnet-install-script.md). Per informazioni su come configurare l'interfaccia della riga di comando nel server di compilazione di integrazione continua (CI, Continuous Integration), vedere [Uso di .NET Core SDK e dei relativi strumenti in integrazione continua](using-ci-with-cli.md).

Per impostazione predefinita, l'interfaccia della riga di comando viene installata in modalità side-by-side (SxS). Pertanto, in un unico computer possono coesistere più versioni degli strumenti dell'interfaccia della riga di comando. La procedura per determinare la versione usata in un computer in cui sono installate più versioni è illustrata nella sezione [Driver](#driver).

## <a name="cli-commands"></a>Comandi dell'interfaccia della riga di comando

Per impostazione predefinita vengono installati i comandi seguenti:

### <a name="basic-commands"></a>Comandi di base

* [new](dotnet-new.md)
* [restore](dotnet-restore.md)
* [build](dotnet-build.md)
* [publish](dotnet-publish.md)
* [run](dotnet-run.md)
* [test](dotnet-test.md)
* [vstest](dotnet-vstest.md)
* [pack](dotnet-pack.md)
* [migrate](dotnet-migrate.md)
* [clean](dotnet-clean.md)
* [sln](dotnet-sln.md)

### <a name="project-modification-commands"></a>Comandi di modifica dei progetti

* [add package](dotnet-add-package.md)
* [add reference](dotnet-add-reference.md)
* [remove package](dotnet-remove-package.md)
* [remove reference](dotnet-remove-reference.md)
* [list reference](dotnet-list-reference.md)

### <a name="advanced-commands"></a>Comandi avanzati

* [nuget delete](dotnet-nuget-delete.md)
* [nuget locals](dotnet-nuget-locals.md)
* [nuget push](dotnet-nuget-push.md)
* [msbuild](dotnet-msbuild.md)
* [dotnet install script](dotnet-install-script.md)

L'interfaccia della riga di comando adotta un modello di estendibilità che consente di specificare altri strumenti per i progetti. Per altre informazioni, vedere l'argomento [Modello di estendibilità dell'interfaccia della riga di comando di .NET Core](extensibility.md).

## <a name="command-structure"></a>Struttura dei comandi

La struttura dei comandi dell'interfaccia della riga di comando è composta dal [driver ("dotnet")](#driver), dal [comando (o "verbo")](#command-verb) e, in alcuni casi, dagli [argomenti](#arguments) e dalle [opzioni](#options). Questo modello può essere osservato nella maggior parte delle operazioni eseguite dalla riga di comando, inclusa la creazione di una nuova app console e la relativa esecuzione dalla riga di comando, come illustrato dai comandi seguenti quando vengono eseguiti da una directory denominata *my_app*:

```console
dotnet new console
dotnet restore
dotnet build --output /build_output
dotnet /build_output/my_app.dll
```

### <a name="driver"></a>Driver

Il driver, denominato [dotnet](dotnet.md), ha due compiti: eseguire un'[app dipendente dal framework](../deploying/index.md) ed eseguire un comando. `dotnet` non è accompagnato da un comando solo quando viene usato per avviare un'applicazione.

Per eseguire un'applicazione dipendente dal framework, specificare l'app dopo il driver, ad esempio `dotnet /path/to/my_app.dll`. Se si esegue il comando dalla cartella in cui si trova la DLL dell'app, è sufficiente eseguire `dotnet my_app.dll`.

Nel momento in cui si fornisce un comando al driver, `dotnet.exe` avvia il processo di esecuzione del comando dell'interfaccia della riga di comando. Come prima operazione, il driver determina la versione degli strumenti da usare. Se la versione non è specificata nelle opzioni di comando, il driver usa la versione più recente disponibile. Per specificare una versione diversa dall'ultima versione installata, usare l'opzione `--fx-version <VERSION>` (vedere l'articolo di riferimento sul [comando dotnet](dotnet.md)). Dopo aver determinato la versione dell'SDK, il driver esegue il comando.

### <a name="command-verb"></a>Comando ("verbo")

Il comando (o "verbo") è semplicemente un comando che esegue un'azione. Ad esempio, `dotnet build` compila il codice, mentre `dotnet publish` pubblica il codice. I comandi vengono implementati come un'applicazione console usando una convenzione `dotnet-{verb}`. 

### <a name="arguments"></a>Argomenti

Gli argomenti passati alla riga di comando sono gli argomenti per il comando richiamato. Quando si esegue `dotnet publish my_app.csproj`, ad esempio, l'argomento `my_app.csproj` indica il progetto da pubblicare e viene passato al comando `publish`.

### <a name="options"></a>Opzioni

Le opzioni passate alla riga di comando sono le opzioni per il comando richiamato. Quando si esegue `dotnet publish --output /build_output`, ad esempio, l'opzione `--output` e il relativo valore vengono passati al comando `publish`. 

## <a name="migration-from-projectjson"></a>Migrazione da project.json

Se si sono usati gli strumenti della Preview 2 per generare progetti basati su *project.json*, consultare l'argomento [dotnet migrate](dotnet-migrate.md) per informazioni sulla migrazione del progetto in MSBuild/*.csproj* per l'uso con gli strumenti di rilascio. Per i progetti .NET Core creati prima del rilascio degli strumenti della Preview 2, aggiornare manualmente il progetto seguendo le istruzioni disponibili in [Migrazione da DNX all'interfaccia della riga di comando di .NET Core (project.json)](../migration/from-dnx.md) e usare `dotnet migrate` o aggiornare direttamente i progetti.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Repository GitHub dotnet/CLI](https://github.com/dotnet/cli/)
* [.NET Core installation guide](https://aka.ms/dotnetcoregs) (Guida all'installazione di .NET Core)

