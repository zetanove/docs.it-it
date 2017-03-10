---
title: Strumenti dell&quot;interfaccia della riga di comando di .NET Core | Microsoft Docs
description: "Una panoramica dell&quot;interfaccia della riga di comando e delle relative funzionalità principali"
keywords: interfaccia della riga di comando, strumenti dell&quot;interfaccia della riga di comando, .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 7c5eee9f-d873-4224-8f5f-ed83df329a59
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 4e3137d8506342662d145481d5e9fde1d53b9ba3
ms.lasthandoff: 03/07/2017

---

# <a name="net-core-command-line-interface-tools-net-core-sdk-10-tools"></a>Strumenti dell'interfaccia della riga di comando di .NET Core (strumenti di .NET Core SDK 1.0)

L'interfaccia della riga di comando di .NET Core è un nuova toolchain di base multipiattaforma per lo sviluppo di applicazioni .NET Core. È una toolchain "di base" perché corrisponde al livello primario su cui possono essere costruiti gli altri strumenti di livello più alto, ad esempio gli ambienti di sviluppo integrato (IDE, Integrated Development Environment), gli editor e gli agenti di orchestrazione della compilazione. 

È inoltre multipiattaforma per impostazione predefinita e ha la stessa superficie su ciascuna delle piattaforme supportate. Ciò significa che, una volta appresa la modalità di funzionamento degli strumenti, è possibile usare l'interfaccia della riga di comando allo stesso modo da qualsiasi piattaforma supportata. 

## <a name="installation"></a>Installazione
Come per qualsiasi strumento, è innanzitutto necessario eseguire l'installazione nel computer. A seconda dello scenario, per installare l'interfaccia della riga di comando è possibile usare programmi nativi oppure lo script della shell di installazione.

I programmi di installazione nativi sono principalmente destinati ai computer degli sviluppatori. L'interfaccia della riga di comando viene distribuita mediante il meccanismo di installazione nativo di ogni piattaforma supportata, ad esempio i pacchetti DEB in Ubuntu o i bundle MSI in Windows. Questi programmi di installazione installano e configurano l'ambiente in base alle esigenze per consentire all'utente di usare l'interfaccia della riga di comando immediatamente dopo l'installazione. Tuttavia, richiedono anche privilegi amministrativi sul computer. È possibile visualizzare le istruzioni di installazione nella [pagina introduttiva di .NET Core](https://aka.ms/dotnetcoregs).

Al contrario, gli script di installazione non richiedono privilegi amministrativi. Tuttavia, non installano tutti i prerequisiti nel computer ed è quindi necessario eseguire questa operazione manualmente. Gli script sono progettati principalmente per configurare i server di compilazione o possono essere usati quando si desidera installare gli strumenti senza privilegi amministrativi (tenendo conto della precedente precisazione relativa ai prerequisiti). È possibile trovare altre informazioni nell'[ argomento di riferimento dello script di installazione](dotnet-install-script.md). Se si è interessati alla procedura per configurare l'interfaccia della riga di comando nel server di compilazione di integrazione continua, è possibile vedere l'argomento sull'uso dell'[interfaccia della riga di comando con server di integrazione continua](using-ci-with-cli.md). 

Per impostazione predefinita, l'interfaccia della riga di comando viene installata in modalità side-by-side (SxS). Ciò significa che più versioni degli strumenti dell'interfaccia della riga di comando possono coesistere in un determinato momento su un singolo computer. Il modo in cui viene identificata la versione corretta è illustrato più dettagliatamente nella sezione [Driver](#driver). 

### <a name="what-commands-come-in-the-box"></a>Comandi predefiniti
Per impostazione predefinita vengono installati i comandi seguenti:

* [new](dotnet-new.md)
* [migrate](dotnet-migrate.md)
* [restore](dotnet-restore.md)
* [run](dotnet-run.md)
* [build](dotnet-build.md)
* [test](dotnet-test.md)
* [publish](dotnet-publish.md)
* [pack](dotnet-pack.md)

È inoltre possibile importare altri comandi in base al progetto e aggiungere comandi personalizzati. Questa operazione è illustrata in dettaglio nella sezione [Estendibilità](#extensibility). 

## <a name="working-with-the-cli"></a>Uso dell'interfaccia della riga di comando

Prima di approfondire l'argomento con dettagli specifici, è possibile esaminare una panoramica generale del funzionamento dell'interfaccia della riga di comando. Nell'esempio seguente sono inclusi alcuni comandi dell'installazione standard dell'interfaccia della riga di comando per inizializzare una nuova applicazione console semplice, ripristinare le dipendenze, compilare l'applicazione e quindi eseguirla. 

```console
dotnet new console
dotnet restore
dotnet build --output /stuff
dotnet /stuff/new.dll
```

Come si può notare nell'esempio precedente, gli strumenti dell'interfaccia della riga di comando vengono usati in base a un modello specifico. All'interno di questo modello, è possibile identificare tre parti principali di ogni comando:

1. [Il driver ("dotnet")](#driver)
2. [Il comando, o "verbo"](#the-verb)
3. [Gli argomenti del comando](#the-arguments)

### <a name="driver"></a>Driver
Il driver, denominato [dotnet](dotnet.md), è la prima parte del comando che viene richiamato. Il driver ha due compiti:

1. Eseguire le applicazioni portabili
2. Eseguire il verbo

L'operazione eseguita dipende dalle informazioni specificate sulla riga di comando. Nel primo caso, si specifica la DLL di un'applicazione portabile che `dotnet` esegue in modo simile al seguente: `dotnet /path/to/your.dll`. 

Nel secondo caso, il driver prova a richiamare il comando specificato. Viene così avviato il processo di esecuzione del comando dell'interfaccia della riga di comando. Innanzitutto, il driver determina la versione degli strumenti desiderata. È possibile specificare la versione nel file [global.json](global-json.md) usando la proprietà `version`. Se non è disponibile, il driver individua la versione più recente degli strumenti installata nel disco e usa tale versione. Una volta determinata la versione, il driver esegue il comando. 

### <a name="the-verb"></a>Verbo
Il verbo è semplicemente un comando che esegue un'azione. `dotnet build` compila il codice. `dotnet publish` pubblica il codice. Il verbo viene implementato come applicazione console, che per convenzione è denominata nel modo seguente: `dotnet-{verb}`. Tutta la logica viene implementata nell'applicazione console che rappresenta il verbo. 

### <a name="the-arguments"></a>Argomenti
Gli argomenti passati alla riga di comando sono gli argomenti relativi all'effettivo verbo o comando richiamato. Ad esempio, quando si digita `dotnet publish --output publishedapp`, l'argomento `--output` viene passato al comando `publish`. 

## <a name="types-of-application-portability"></a>Tipi di portabilità delle applicazioni
L'interfaccia della riga di comando consente la portabilità delle applicazioni in due modi principali:

1. Installazione di applicazioni completamente portabili che possono essere eseguite ovunque sia installato .NET Core
2. Distribuzioni autonome

Altre informazioni su entrambe le modalità di distribuzione sono disponibili nell'argomento [Distribuzione di applicazioni .NET Core](../deploying/index.md). 

## <a name="migration-from-projectjson"></a>Migrazione da project.json
Se si usano gli strumenti dell'anteprima 2 e i progetti *project.json*, è possibile vedere la documentazione sul comando [dotnet migrate](dotnet-migrate.md) per acquisire familiarità con il comando e su come eseguire la migrazione del progetto. 

> [!NOTE]
> Il comando `dotnet migrate` non esegue attualmente la migrazione dei file *project.json* precedenti all'anteprima 2. 

## <a name="extensibility"></a>Estendibilità
Naturalmente, non ogni singolo strumento che è possibile usare nel flusso di lavoro farà parte degli strumenti dell'interfaccia della riga di comando. Tuttavia, l'interfaccia della riga di comando di .NET Core ha un modello di estendibilità che consente di specificare altri strumenti per i progetti. Per altre informazioni, vedere l'argomento [Modello di estendibilità dell'interfaccia della riga di comando di .NET Core](extensibility.md).

## <a name="summary"></a>Riepilogo
In questa breve panoramica sono state illustrate le funzionalità più importanti dell'interfaccia della riga di comando. Altre informazioni sono disponibili negli argomenti concettuali e di riferimento pubblicati su questo sito. È anche possibile usare altre risorse:
* Repository GitHub [dotnet/CLI](https://github.com/dotnet/cli/)
* [Istruzioni introduttive](https://aka.ms/dotnetcoregs/)

