---
title: "Modello di estendibilità dell&quot;interfaccia della riga di comando di .NET Core"
description: "Modello di estendibilità dell&quot;interfaccia della riga di comando di .NET Core"
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 1bebd25a-120f-48d3-8c25-c89965afcbcd
translationtype: Human Translation
ms.sourcegitcommit: aeb199a9aeb1584570ad2a2942e2f22c75a59616
ms.openlocfilehash: 4223f296224c9b62c88b72f0f643c8b8b6fc9f6b

---

# <a name="net-core-cli-extensibility-model"></a>Modello di estendibilità dell'interfaccia della riga di comando di .NET Core 

## <a name="overview"></a>Panoramica
Questo documento analizza i principali metodi per estendere gli strumenti dell'interfaccia della riga di comando e illustra gli scenari relativi a ciascuno di essi. Viene indicato come utilizzare gli strumenti e vengono fornite brevi note riguardanti la compilazione di entrambi i tipi di strumenti. 

## <a name="how-to-extend-cli-tools"></a>Come estendere gli strumenti dell'interfaccia della riga di comando
Gli strumenti dell'interfaccia della riga di comando possono essere estesi in due modi principali:

1. Tramite pacchetti NuGet in base al progetto
2. Tramite il PATH di sistema

I due meccanismi di estendibilità sopra indicati non sono mutualmente esclusivi: è possibile usarli entrambi o usarne uno soltanto. La scelta dipende in larga misura dall'obiettivo che si intende raggiungere con l'estensione.

## <a name="per-project-based-extensibility"></a>Estendibilità in base al progetto
Gli strumenti in base al progetto sono [applicazioni console portabili](../deploying/index.md) distribuite come pacchetti NuGet. Gli strumenti sono disponibili solo nel contesto del progetto che fa riferimento ad essi e per il quale vengono ripristinati. La chiamata all'esterno del contesto del progetto, ad esempio all'esterno della directory contenente il progetto, avrà esito negativo perché non sarà possibile trovare il comando.

Questi strumenti sono perfetti anche per i server di compilazione, dal momento che non è necessario nulla al di fuori di `project.json`. Il processo di compilazione esegue il ripristino del progetto compilato e gli strumenti saranno disponibili. Rientrano in questa categoria anche i progetti in un particolare linguaggio, ad esempio F#. In definitiva, ogni progetto può essere scritto soltanto in uno specifico linguaggio. 

Questo modello di estendibilità, infine, fornisce il supporto per la creazione di strumenti che devono accedere all'output compilato del progetto. Ad esempio, rientrano in questa categoria diversi strumenti di visualizzazione Razor presenti in applicazioni MVC [ASP.NET](https://www.asp.net/). 

### <a name="consuming-per-project-tools"></a>Utilizzo di strumenti in base al progetto
Per l'utilizzo di questi strumenti, è necessario aggiungere un nodo `tools` al file `project.json`. All'interno del nodo `tools` viene fatto riferimento al pacchetto in cui si trovano gli strumenti. Dopo l'esecuzione di `dotnet restore`, viene eseguito il ripristino dello strumento e delle relative dipendenze. 

Per gli strumenti che devono caricare l'output di compilazione del progetto per l'esecuzione, è in genere presente un'altra dipendenza elencata sotto le normali dipendenze del file di progetto. Questo significa che gli strumenti che caricano il codice del progetto sono costituiti da due componenti: 

1. L'invoker principale "tools"
2. Qualsiasi numero di altri strumenti contenenti la logica da utilizzare 

Perché due componenti? È necessario che gli strumenti che devono caricare l'output di compilazione di un progetto dispongano di un grafico delle dipendenze unificato con il progetto a cui stanno lavorando. Aggiungendo il componente "dipendenza", si consente a NuGet di risolvere queste dipendenze come grafico unificato. L'invoker è presente perché è necessario prendere in considerazione sia la posizione che i framework dello strumento di dipendenza. L'invoker può accettare tutti gli argomenti di reindirizzamento (`-c`, `-o`, `-b`) specificati dall'utente ed è in grado di trovare lo strumento di dipendenza. È inoltre in grado di implementare qualsiasi criterio per i casi in cui sono presenti più strumenti di dipendenza per più framework. In altri termini, è in grado di eseguire tutti i criteri, di eseguirne uno soltanto e così via. In generale, la logica può essere condivisa tra questi due strumenti in tutti i modi necessari. 

Di seguito è riportato un esempio di aggiunta di un semplice strumento "tools" a un semplice progetto. Si consideri un comando di esempio denominato `dotnet-api-search` che consente di cercare nei pacchetti NuGet l'API specificata. Di seguito è riportato un file `project.json` di un'applicazione console che usa tale strumento:

```json
{
    "version": "1.0.0",
    "compilationOptions": {
        "emitEntryPoint": true
    },
    "dependencies": {
        "Microsoft.NETCore.App": {
            "type": "platform",
            "version": "1.0.0"
        }
    },
    "tools": {
        "dotnet-api-search": {
            "version": "1.0.0",
            "imports": ["dnxcore50"]
        }
    },
    "frameworks": {
        "netcoreapp1.0": {}
    }
}
```

Il nodo `tools` è strutturato in modo analogo al nodo `dependencies` e richiede l'ID pacchetto del pacchetto contenente almeno lo strumento e la relativa versione. Nell'esempio precedente è presente un'altra istruzione, `imports`. Tale istruzione influenza il processo di ripristino dello strumento e specifica che quest'ultimo, oltre che con qualsiasi framework usato come destinazione, è compatibile anche con la destinazione `dnxcore50`. Per altre informazioni, vedere l'[argomento di riferimento di project.json](project-json.md).

### <a name="building-tools"></a>Compilazione degli strumenti
Come affermato in precedenza, gli strumenti sono essenzialmente applicazioni console portabili. La compilazione di uno strumento è analoga a quella di qualsiasi applicazione console. Dopo la compilazione, usare il comando [`dotnet pack`](dotnet-pack.md) per creare un pacchetto NuGet (nupkg) contenente il codice, informazioni sulle relative dipendenze e così via. Il nome del pacchetto è a scelta dell'autore, ma è necessario che l'applicazione in esso contenuta, l'effettivo file binario dello strumento, sia conforme alla convenzione di `dotnet-<command>` per consentire a `dotnet` di richiamare il pacchetto. 

Poiché gli strumenti sono applicazioni portabili, l'utente che utilizza lo strumento deve disporre della versione delle librerie .NET Core in base a cui tale strumento è stato creato. Solo in questo modo è possibile eseguire lo strumento. Qualsiasi altra dipendenza usata dallo strumento e non contenuta nelle librerie .NET Core viene ripristinata e posizionata nella cache NuGet. Di conseguenza, l'intero strumento viene eseguito usando gli assembly delle librerie .NET Core oltre agli assembly della cache NuGet. 

Gli strumenti di questo tipo hanno un grafico delle dipendenze completamente separato da quello del progetto che li usa. Il processo di ripristino ripristinerà innanzitutto le dipendenze del progetto e quindi ciascuno degli strumenti e le relative dipendenze. 

Esempi più dettagliati e differenti combinazioni sono disponibili in [.NET Core CLI repo](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestProjects) (Archivio .NET Core dell'interfaccia della riga di comando). Nello stesso archivio è possibile vedere anche l'[implementazione degli strumenti usati](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages). 

La compilazione di strumenti che caricano gli output di compilazione dei progetti è leggermente diversa. Come illustrato in precedenza, per questi tipi di strumenti sono presenti due componenti:

1. Uno strumento dispatcher richiamato dall'utente
2. Una dipendenza specifica del framework contenente la logica riguardante l'individuazione degli output di compilazione e l'utilizzo degli stessi

Un esempio fondamentale sono i comandi [Entity Framework (EF)](https://github.com/aspnet/EntityFramework) nonché il comando [`dotnet test`](dotnet-test.md). In entrambi i casi è presente uno strumento a cui viene fatto riferimento nel nodo `tools` del file `project.json` e che agisce da dispatcher principale. L'utente richiama questo strumento dalla riga di comando. Il secondo componente è la dipendenza indicata nelle dipendenze principali del progetto, sia quelle radice che quelle specifiche del framework. Questo pacchetto contiene la logica effettiva dello strumento. Il pacchetto è una dipendenza normale e pertanto verrà ripristinato come parte del processo di ripristino del progetto. 

A differenza dei precedenti tipi di strumenti, questi strumenti sono parte effettiva del grafico del progetto che li utilizza. Il motivo è che questi strumenti devono accedere al codice del progetto e potenzialmente a tutte le relative dipendenze. Gli strumenti EF (Entity Framework), ad esempio, devono poter accedere perché devono analizzare gli assembly per individuare il codice di cui hanno bisogno, ad esempio le migrazioni.  

Un altro motivo dell'esistenza di questa soluzione a due componenti è la necessità di creare un modello di chiamata più "pulito". La maggior parte dei comandi dell'interfaccia della riga di comando che eliminano determinati elementi dal disco, ad esempio `dotnet build` o `dotnet publish`, consentono agli utenti di reindirizzare gli output a un percorso differente usando l'argomento `--output`, `--build-base-path` o `--configuration`. Ad esempio, per consentire agli strumenti EF di individuare l'output di compilazione del progetto, è necessario fornire gli stessi argomenti con gli stessi valori a *entrambi* i driver `dotnet` nonché al comando `ef`. Con il modello di chiamata, gli utenti passano gli argomenti allo strumento dispatcher, che può quindi usarli per individuare il file binario necessario contenente la logica nelle directory di output. 

Un esempio chiaro di questo approccio è disponibile in [.NET Core CLI repo](https://github.com/dotnet/cli) (Archivio .NET Core dell'interfaccia della riga di comando):

* [File project.json di esempio](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/TestAssets/DesktopTestProjects/AppWithDirectDependencyDesktopAndPortable/project.json)
* [Implementazione del dispatcher](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages/dotnet-dependency-tool-invoker)
* [Implementazione della dipendenza specifica del framework](https://github.com/dotnet/cli/tree/rel/1.0.0-preview2/TestAssets/TestPackages/dotnet-desktop-and-portable)


### <a name="path-based-extensibility"></a>Estendibilità basata su PATH
L'estendibilità basata sul PATH viene in genere usata per i computer di sviluppo in cui è necessario disporre di uno strumento in grado di coprire concettualmente più di un singolo progetto. Il principale svantaggio di questo meccanismo di estensione è che è vincolato al computer in cui è presente lo strumento. Se si vuole usare questo meccanismo in un altro computer, è necessario eseguire un'attività di distribuzione.

Questo modello di estendibilità del set di strumenti dell'interfaccia della riga di comando è molto semplice. Come illustrato in [.NET Core CLI overview](index.md) (Panoramica sull'interfaccia della riga di comando di .NET Core), il driver `dotnet` può eseguire qualsiasi comando denominato in base alla convenzione `dotnet-<command>`. La logica di risoluzione predefinita testerà prima diverse posizioni e alla fine sceglierà il percorso specificato dal PATH di sistema. Se il comando richiesto è presente nel PATH di sistema ed è un file binario che è possibile richiamare, il driver `dotnet` lo richiamerà. 

Il file binario può essere un qualsiasi file eseguibile dal sistema operativo. Nei sistemi Unix può trattarsi di qualsiasi file con il bit eseguibile impostato tramite `chmod +x`. Nei sistemi Windows può trattarsi di qualsiasi file eseguibile da Windows. 

Di seguito è riportata un'implementazione molto semplice di un comando `dotnet clean`. Per implementare il comando verrà usato `bash`. Il comando eliminerà semplicemente le directory `bin/` e `obj/` nella directory corrente. Se gli viene passato l'argomento `--lock`, il comando eliminerà anche il file `project.lock.json`. Il comando è riportato di seguito per intero. 

```bash
#!/bin/bash

# Delete the bin and obj dirs
rm -rf bin/ obj/

LOCK_FILE=$1
if [[ "$LOCK_FILE" = "--lock" ]]; then
    rm project.lock.json
fi


echo "Cleaning complete..."
```

Nei sistemi MacOS è possibile salvare lo script come `dotnet-clean` e impostarne il bit eseguibile con `chmod +x dotnet-clean`. È quindi possibile creare un collegamento simbolico in `/usr/local/bin` usando il comando `ln -s dotnet-clean /usr/local/bin/`. In questo modo sarà possibile richiamare il comando Clean usando la sintassi `dotnet clean`. È possibile testare questo scenario creando un'app, eseguendo `dotnet build` su tale app e quindi eseguendo `dotnet clean`. 

## <a name="conclusion"></a>Conclusione
Gli strumenti dell'interfaccia della riga di comando di .NET Core offrono due approcci diversi all'estendibilità. Gli strumenti in base al progetto sono contenuti nel contesto del progetto stesso, ma consentono una facile installazione mediante il ripristino. Gli strumenti basati su PATH sono ottimi per scopi di carattere generale e validi per più progetti. Sono utilizzabili su un singolo computer. 



<!--HONumber=Nov16_HO3-->


