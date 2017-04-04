---
title: Comando dotnet-run - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando dotnet-run offre un modo pratico per eseguire l&quot;applicazione dal codice sorgente.
keywords: dotnet-run, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/22/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 40d4e60f-9900-4a48-b03c-0bae06792d91
translationtype: Human Translation
ms.sourcegitcommit: dff752a9d31ec92b113dae9eed20cd72faf57c84
ms.openlocfilehash: 49e6738a90663645f761bb7748a723624ad8fdc6
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-run"></a>dotnet-run

## <a name="name"></a>Nome 

`dotnet-run`: esegue il codice sorgente senza comandi espliciti di compilazione o avvio.

## <a name="synopsis"></a>Riepilogo

`dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet run` offre un modo pratico per eseguire l'applicazione dal codice sorgente con un solo comando. Questo comando è utile per lo sviluppo iterativo veloce dalla riga di comando. Il comando dipende dal comando [`dotnet build`](dotnet-build.md) per compilare il codice. I requisiti per la compilazione, ad esempio il ripristino preliminare del progetto, si applicano anche a `dotnet run`. 

I file di output vengono scritti nel percorso predefinito, ovvero `bin/<configuration>/<target>`. Se ad esempio si ha un'applicazione `netcoreapp1.0` e si esegue `dotnet run`, l'output viene inserito in `bin/Debug/netcoreapp1.0`. I file vengono sovrascritti in base alle esigenze. I file temporanei vengono inseriti nella directory `obj`. 

Se il progetto specifica più framework, l'esecuzione di `dotnet run` genera un errore a meno che non venga usata l'opzione `-f|--framework <FRAMEWORK>` per specificare il framework.

Il comando `dotnet run` viene usato nel contesto dei progetti e non di assembly di compilazione. Se in alternativa si prova a eseguire la DLL di un'applicazione dipendente da framework, è necessario usare [dotnet](dotnet.md) senza un comando. Ad esempio, per eseguire `myapp.dll`, usare:
 
```
dotnet myapp.dll
```

Per altre informazioni sul driver `dotnet`, vedere l'argomento [Strumenti dell'interfaccia della riga di comando di .NET Core](index.md).

Per eseguire l'applicazione, il comando `dotnet run` risolve le dipendenze dell'applicazione esterne al runtime condiviso dalla cache NuGet. È consigliabile non per usare `dotnet run` per eseguire le applicazioni nell'ambiente di produzione perché questo comando usa dipendenze memorizzate nella cache. In alternativa, [creare una distribuzione](../deploying/index.md) usando il comando [`dotnet publish`](dotnet-publish.md) e distribuire l'output pubblicato. 

## <a name="options"></a>Opzioni

`--`

Delimita gli argomenti a `dotnet run` dagli argomenti per l'applicazione in esecuzione. Tutti gli argomenti dopo questo vengono passati all'applicazione in esecuzione. 

`-h|--help`

Stampa una breve guida per il comando.

`-c|--configuration <CONFIGURATION>`

Configurazione da usare per la compilazione del progetto. Il valore predefinito è `Debug`.

`-f|--framework <FRAMEWORK>`

Compila ed esegue l'app usando il [framework](../../standard/frameworks.md) specificato. Il framework deve essere specificato nel file di progetto.

`-p|--project <PATH/PROJECT.csproj>`

Specifica il percorso e il nome del file di progetto. Vedere la nota. Se non specificato, per impostazione predefinita il percorso corrisponde alla directory corrente.

> [!NOTE]
> Usare il percorso e il nome del file di progetto con l'opzione `-p|--project`. Una regressione nell'interfaccia della riga di comando impedisce di specificare un percorso di cartella in questo momento. Per altre informazioni e per tenere traccia di questo problema, vedere [dotnet run -p, can not start a project (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992) (dotnet run -p, non è possibile avviare un progetto (dotnet/cli #5992)).

## <a name="examples"></a>Esempi

Eseguire il progetto nella directory corrente:

`dotnet run` 

Eseguire il progetto specificato:

`dotnet run --project /projects/proj1/proj1.csproj`

Eseguire il progetto nella directory corrente. L'argomento `--help` in questo esempio viene passato all'applicazione perché viene usato l'argomento `--`:

`dotnet run --configuration Release -- --help`

