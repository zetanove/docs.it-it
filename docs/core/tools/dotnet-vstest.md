---
title: Comando dotnet-vstest | Microsoft Docs
description: Il comando dotnet-vstest consente di compilare un progetto e tutte le relative dipendenze.
keywords: dotnet-vstest, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: guardrex
ms.author: mairaw
ms.date: 03/09/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0e36c070-2242-41d3-96f1-aea0aca48d4d
translationtype: Human Translation
ms.sourcegitcommit: 4a1f0c88fb1ccd6694f8d4f5687431646adbe000
ms.openlocfilehash: 27b96e74ae1abc83ba527cb799db33bec7af35bf
ms.lasthandoff: 03/22/2017

---

# <a name="dotnet-vstest"></a>dotnet-vstest

## <a name="name"></a>Nome

`dotnet-vstest`: esegue test dai file specificati.

## <a name="synopsis"></a>Riepilogo

`dotnet vstest [<TEST_FILE_NAMES>] [--Settings|/Settings] [--Tests|/Tests] [--TestAdapterPath|/TestAdapterPath] [--Platform|/Platform] [--Framework|/Framework] [--Parallel|/Parallel] [--TestCaseFilter|/TestCaseFilter] [--logger|/logger] [-lt|--ListTests|/lt|/ListTests] [--ParentProcessId|/ParentProcessId] [--Port|/Port] [--Diag|/Diag] [[--] <args>...]] [-?|--Help|/?|/Help]`

## <a name="description"></a>Descrizione

Il comando `dotnet-vstest` esegue l'applicazione della riga di comando `VSTest.Console` per eseguire unit test automatici e test sull'applicazione UI codificata.

## <a name="arguments"></a>Argomenti

`TEST_FILE_NAMES`

Eseguire i test dagli assembly specificati. Per separare più nomi di assembly di test, usare gli spazi.

## <a name="options"></a>Opzioni

`--Settings|/Settings:<Settings File>`

Impostazioni da usare durante l'esecuzione di test.

`--Tests|/Tests:<Test Names>`

Esegue test con nomi corrispondenti ai valori specificati. Se si specificano più valori, separarli con virgole.

`--TestAdapterPath|/TestAdapterPath`

Durante l'esecuzione dei test, vengono usati adattatori di test personalizzati da un percorso specificato (se presenti).

`--Platform|/Platform:<Platform type>`

Architettura della piattaforma di destinazione usata per l'esecuzione dei test. I valori validi sono `x86`, `x64` e `ARM`.

`--Framework|/Framework:<Framework Version>`

Versione di .NET Framework di destinazione usata per l'esecuzione dei test. Esempi di valori validi sono `.NETFramework,Version=v4.6`, `.NETCoreApp,Version=v1.0` e così via. Altri valori supportati sono `Framework35`, `Framework40`, `Framework45` e `FrameworkCore10`.

`--Parallel|/Parallel`

Esegue test in parallelo. Per impostazione predefinita, tutti i core presenti nel computer sono disponibili per l'uso. Impostare un numero esplicito di core con un file di impostazioni.

`--TestCaseFilter|/TestCaseFilter:<Expression>`

Esegue test corrispondenti all'espressione specificata. `<Expression>` è in formato `<property>Operator<value>[|&<Expression>]`, dove Operator è `=`, `!=` o `~`.  L'operatore `~` usa la semantica 'contains' ed è applicabile per le proprietà stringa come `DisplayName`. Per raggruppare le sottoespressioni vengono usate le parentesi `()`.

`-?|--Help|/?|/Help`

Stampa una breve guida per il comando.

`--logger|/logger:<Logger Uri/FriendlyName>`

Specifica un logger per i risultati dei test.  

* Per pubblicare i risultati dei test in Team Foundation Server, usare il provider di logger `TfsPublisher`:

  ```
  /logger:TfsPublisher;
      Collection=<team project collection url>;
      BuildName=<build name>;
      TeamProject=<team project name>
      [;Platform=<Defaults to "Any CPU">]
      [;Flavor=<Defaults to "Debug">]
      [;RunTitle=<title>]
  ```

* Per registrare i risultati in un file di risultati dei test di Visual Studio (con estensione trx), usare il provider di logger `trx`. Questa opzione crea un file nella directory dei risultati dei test con nome di file di log specificato. Se `LogFileName` non è specificato, viene creato un nome di file univoco per contenere i risultati dei test.

  ```
  /logger:trx [;LogFileName=<Defaults to unique file name>]
  ```

`-lt|--ListTests|/lt|/ListTests:<File Name>`

Elenca i test individuati dal contenitore di test specificato.

`--ParentProcessId|/ParentProcessId:<ParentProcessId>`

ID del processo padre responsabile dell'avvio del processo corrente.

`--Port|/Port:<Port>`

Specifica la porta per la connessione socket e la ricezione dei messaggi di evento.

`--Diag|/Diag:<Path to log file>`

Abilita i log dettagliati per la piattaforma di test. I log vengono scritti nel file specificato.

`args`

Specifica argomenti aggiuntivi da passare all'adattatore. Gli argomenti sono specificati come coppie nome-valore nel formato `<n>=<v>`, dove `<n>` è il nome dell'argomento e `<v>` è il valore dell'argomento. Per separare più argomenti usare uno spazio.

## <a name="examples"></a>Esempi

Eseguire test in `mytestproject.dll`:

`dotnet vstest mytestproject.dll`

Eseguire test in `mytestproject.dll` e `myothertestproject.exe`:

`dotnet vstest mytestproject.dll myothertestproject.exe`

Eseguire test `TestMethod1`:

`dotnet vstest /Tests:TestMethod1`

Eseguire test `TestMethod1` e `TestMethod2`:

`dotnet vstest /Tests:TestMethod1,TestMethod2`

