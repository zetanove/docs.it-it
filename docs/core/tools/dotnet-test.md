---
title: Comando dotnet-test | Microsoft Docs
description: Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto.
keywords: dotnet-test, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 3a0fa917-eb0a-4d7e-9217-d06e65455675
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 871a6f736272309f6fae74b06f437c7271df2321

---

#<a name="dotnet-test"></a>dotnet-test

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 2 di .NET Core. Per gli strumenti di .NET Core versione RC4, vedere l'argomento [dotnet-test (strumenti di .NET Core RC4)](../preview3/tools/dotnet-test.md).

## <a name="name"></a>Nome

`dotnet-test`: esegue unit test con il Test Runner configurato.

## <a name="synopsis"></a>Riepilogo

`dotnet test [project] [--help] 
    [--parentProcessId] [--port] [--configuration]   
    [--output] [--build-base-path] [--framework] [--runtime]
    [--no-build]`  

## <a name="description"></a>Descrizione

Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto. Gli unit test sono progetti della libreria di classi con dipendenze dal framework di unit test (ad esempio, NUnit o xUnit) e dal Test Runner dotnet per tale framework di unit test. Sono disponibili come pacchetti NuGet e vengono ripristinati come dipendenze ordinarie per il progetto.

Per i progetti di test è inoltre necessario specificare una proprietà del Test Runner nel file project.json tramite il nodo "testRunner". Questo valore deve contenere il nome del framework di unit test.

Il file project.json di esempio seguente mostra le proprietà necessarie:

```json
{
  "version": "1.0.0-*",
  "buildOptions": {
    "debugType": "portable"
  },
  "dependencies": {
    "System.Runtime.Serialization.Primitives": "4.1.1",
    "xunit": "2.1.0",
    "dotnet-test-xunit": "1.0.0-rc2-192208-24"
  },
  "testRunner": "xunit",
  "frameworks": {
    "netcoreapp1.0": {
      "dependencies": {
        "Microsoft.NETCore.App": {
          "type": "platform",
          "version": "1.0.0"
        }
      },
      "imports": [
        "dotnet5.4",
        "portable-net451+win8"
      ]
    }
  }
}
```

`dotnet test` supporta due modalità di esecuzione:

1. Console: in modalità console `dotnet test` esegue completamente qualsiasi comando passato e restituisce i risultati. Ogni volta che `dotnet test` viene richiamato senza passare la porta --port, viene eseguito in modalità console e ciò comporterà a sua volta l'esecuzione del Test Runner in modalità console.
2. Fase di progettazione: usata nel contesto di altri strumenti, ad esempio editor o ambienti di sviluppo integrato (IDE, Integrated Development Environment). Per altre informazioni su questa modalità, vedere il documento sul [protocollo dotnet-test](test-protocol.md). 

## <a name="options"></a>Opzioni

`[project]`
    
Specifica un percorso del progetto di test. Se omesso, per impostazione predefinita sarà la directory corrente.

`-?|-h|--help`

Stampa una breve guida per il comando.

`--parentProcessId`

Usato dagli ambienti di sviluppo integrato per specificare il relativo ID processo. Se il processo padre viene interrotto, anche il test si interromperà.

`--port`

Usato dagli ambienti di sviluppo integrato per specificare un numero di porta per l'ascolto di una connessione.

`-c|--configuration <Debug|Release>`

Configurazione in cui eseguire la compilazione. Il valore predefinito è `Release`. 

`-o|--output [OUTPUT_DIRECTORY]`

Directory in cui trovare i file binari da eseguire.

`-b|--build-base-path <OUTPUT_DIRECTORY>`

Directory in cui inserire gli output temporanei.

`-f|--framework [FRAMEWORK]`

Cerca i file binari di test per un framework specifico.

`-r|--runtime [RUNTIME_IDENTIFIER]`

Cerca i file binari di test per il runtime specificato.

`--no-build` 

Non compila il progetto di test prima di eseguirlo. 

## <a name="examples"></a>Esempi

Eseguire i test nel progetto nella directory corrente:

`dotnet test` 

Eseguire i test nel progetto test1:

`dotnet test /projects/test1/project.json` 

## <a name="see-also"></a>Vedere anche

[Protocollo di comunicazione dotnet-test](test-protocol.md)

[Framework](../../standard/frameworks.md)

[Catalogo RID (Runtime IDentifier)](../rid-catalog.md)


<!--HONumber=Feb17_HO2-->


