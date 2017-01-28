---
title: Comando dotnet-run | .NET Core SDK
description: Il comando dotnet-run offre un modo pratico per eseguire l&quot;applicazione dal codice sorgente.
keywords: dotnet-run, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 495ff50b-cb30-4d30-8f20-beb3d5e7c31f
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 6f95125640e7341426c3a019771a6b8595d10e73

---

#<a name="dotnet-run"></a>dotnet-run

## <a name="name"></a>Nome 

dotnet-run: esegue il codice sorgente "sul posto" senza compilazioni esplicite o senza avviare i comandi

## <a name="synopsis"></a>Riepilogo

`dotnet run [--help] [--framework] [--configuration]
    [--project] [[--] [application arguments]]`

## <a name="description"></a>Descrizione
Il comando `dotnet run` offre un modo pratico per eseguire l'applicazione dal codice sorgente con un solo comando. Compila il codice sorgente, genera un programma di output e quindi lo esegue. Questo comando è utile per lo sviluppo iterativo veloce e può essere usato anche per eseguire un programma con distribuzione di origine, ad esempio un sito Web.

Questo comando usa la [compilazione dotnet](dotnet-build.md) per compilare gli input di origine in un assembly .NET prima di avviare il programma. I requisiti per questo comando e per la gestione degli input di origine vengono tutti ereditati dal comando di compilazione. Per altre informazioni su tali requisiti, vedere la documentazione relativa al comando di compilazione.

I file di output vengono scritti nella cartella figlio *bin*, che verrà creata se non esiste già. I file verranno sovrascritti in base alle esigenze. I file temporanei vengono scritti nella cartella figlio *obj*.  

Nel caso in cui il progetto abbia più framework specificati, `dotnet run` selezionerà prima i framework .NET Core. Se non sono presenti, verrà generato un errore. Per specificare altri framework, usare l'argomento `--framework`.

Il comando `dotnet run` deve essere usato nel contesto di progetti e non di assembly di compilazione. Se invece si sta tentando di eseguire il file DLL di un'applicazione portabile, usare [dotnet](dotnet.md) senza comandi, come nell'esempio seguente:
 
`dotnet myapp.dll`

Per altre informazioni sul driver `dotnet`, vedere l'argomento [.NET Core Command Line Tools (CLI)](index.md) (Strumenti dell'interfaccia della riga di comando di .NET Core).

## <a name="options"></a>Opzioni

`--`

Delimita gli argomenti a `dotnet run` dagli argomenti per l'applicazione in esecuzione. Tutti gli argomenti dopo questo verranno passati all'applicazione in esecuzione. 

`-h|--help`

Stampa una breve guida per il comando.

`-f`, `--framework <FRAMEWORK_IDENTIFIER>`

Esegue l'applicazione per un determinato identificatore del framework (FID, Framework Identifier). 

`-c`, `--configuration <Debug|Release>`

Configurazione da usare durante la pubblicazione. Il valore predefinito è `Debug`.

`-p`, `--project [PATH]`

Specifica il progetto da eseguire. Può essere un percorso a un file [csproj](csproj.md) o a una directory contenente un file [csproj](csproj.md). Se non specificato, per impostazione predefinita sarà la directory corrente. 

## <a name="examples"></a>Esempi

Eseguire il progetto nella directory corrente: `dotnet run` 

Eseguire il progetto specificato:

`dotnet run --project /projects/proj1/proj1.csproj`

Eseguire il progetto nella directory corrente (l'argomento `--help` in questo esempio viene passato all'applicazione in esecuzione, poiché è stato usato l'argomento `--`):

`dotnet run --configuration Release -- --help`


<!--HONumber=Nov16_HO3-->


