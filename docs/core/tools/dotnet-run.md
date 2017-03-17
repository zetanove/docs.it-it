---
title: Comando dotnet-run | Microsoft Docs
description: Il comando dotnet-run offre un modo pratico per eseguire l&quot;applicazione dal codice sorgente.
keywords: dotnet-run, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 40d4e60f-9900-4a48-b03c-0bae06792d91
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 60bb9160e43788539b0dc6bcf1372bb925e9ba22
ms.lasthandoff: 03/07/2017

---

#<a name="dotnet-run"></a>dotnet-run

## <a name="name"></a>Nome 

`dotnet-run`: esegue il codice sorgente "sul posto" senza compilazioni esplicite o comandi di avvio.

## <a name="synopsis"></a>Riepilogo

```
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

## <a name="description"></a>Descrizione

Il comando `dotnet run` offre un modo pratico per eseguire l'applicazione dal codice sorgente con un solo comando. Questo comando è utile per lo sviluppo iterativo veloce nella riga di comando. Poiché il comando dipende da [`dotnet build`](dotnet-build.md) per la compilazione del codice, tutti i requisiti per la compilazione, ad esempio il ripristino del progetto, si applicano anche a `dotnet run`. 

I file di output vengono scritti nel percorso predefinito, ovvero `bin/<configuration>/<target>`. Ad esempio, se si ha un'applicazione `netcoreapp1.0` e si esegue `dotnet run`, l'output verrà inserito in `bin/Debug/netcoreapp1.0`. I file vengono sovrascritti in base alle esigenze. I file temporanei vengono inseriti nella directory `obj`. 

Nel caso in cui il progetto abbia più framework specificati, `dotnet run` visualizzerà un errore a meno che non venga usata l'opzione `--framework` per specificare i framework per i quali eseguire l'applicazione.

Il comando `dotnet run` deve essere usato nel contesto di progetti e non di assembly di compilazione. Se invece si sta tentando di eseguire il file DLL di un'applicazione portabile, usare [dotnet](dotnet.md) senza comandi, come nell'esempio seguente:
 
`dotnet myapp.dll`

Per altre informazioni sul driver `dotnet`, vedere l'argomento [.NET Core Command Line Tools (CLI)](index.md) (Strumenti dell'interfaccia della riga di comando di .NET Core).

Per eseguire l'applicazione, il comando `dotnet run` risolve le dipendenze dell'applicazione esterne al runtime condiviso dalla cache NuGet. Per tutte queste ragioni, non è consigliabile usare questo comando per eseguire applicazioni in produzione. In alternativa, [creare una distribuzione](../deploying/index.md) usando il comando [`dotnet publish`](dotnet-publish.md) e usarla in produzione. 

## <a name="options"></a>Opzioni

`--`

Delimita gli argomenti a `dotnet run` dagli argomenti per l'applicazione in esecuzione. Tutti gli argomenti dopo questo verranno passati all'applicazione in esecuzione. 

`-h|--help`

Stampa una breve guida per il comando.

`-c|--configuration {Debug|Release}`

Configurazione da usare per la compilazione del progetto. Il valore predefinito è `Debug`.

`-f|--framework <FRAMEWORK_IDENTIFIER>`

Compila ed esegue l'app usando il framework specificato. Il framework deve essere specificato nel file di progetto.

`-p|--project <PATH>`

Specifica il percorso del file di progetto da eseguire. Può essere un percorso a un file [csproj](csproj.md) o a una directory contenente un file [csproj](csproj.md). Se non specificato, per impostazione predefinita sarà la directory corrente. 

## <a name="examples"></a>Esempi

Eseguire il progetto nella directory corrente:

`dotnet run` 

Eseguire il progetto specificato:

`dotnet run --project /projects/proj1/proj1.csproj`

Eseguire il progetto nella directory corrente (l'argomento `--help` in questo esempio viene passato all'applicazione in esecuzione, poiché è stato usato l'argomento `--`):

`dotnet run --configuration Release -- --help`
