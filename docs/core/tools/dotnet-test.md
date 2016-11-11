---
title: Comando dotnet-test | .NET Core SDK
description: Il comando &quot;dotnet test&quot; viene usato per eseguire unit test in un determinato progetto.
keywords: dotnet-test, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: mairaw
manager: wpickett
ms.date: 10/07/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3a0fa917-eb0a-4d7e-9217-d06e65455675
translationtype: Human Translation
ms.sourcegitcommit: c6ee3f5663d0a3f62914e8de474cca4d15340c9d
ms.openlocfilehash: b12861f0ce3c40bf4db51994ea5d4a92b8ef0162

---

#<a name="dotnettest"></a>dotnet-test

## <a name="name"></a>Nome

`dotnet-test` esegue unit test con il Test Runner configurato

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


<!--HONumber=Nov16_HO1-->


