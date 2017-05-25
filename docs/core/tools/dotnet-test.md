---
title: Comando dotnet-test - Interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto.
keywords: dotnet-test, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 03/25/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 4bf0aef4-148a-41c6-bb95-0a9e1af8762e
ms.translationtype: Human Translation
ms.sourcegitcommit: ae036cfcad341ffc859336a7ab2a49feec145715
ms.openlocfilehash: 734cf337fdd0d33f6c2b6d929b795b2307135550
ms.contentlocale: it-it
ms.lasthandoff: 05/18/2017

---

#<a name="dotnet-test"></a>dotnet-test

## <a name="name"></a>Nome

`dotnet-test`: driver di test .NET usato per eseguire gli unit test.

## <a name="synopsis"></a>Riepilogo

`dotnet test [<PROJECT>] [-s|--settings] [-t|--list-tests] [--filter] [-a|--test-adapter-path] [-l|--logger] [-c|--configuration] [-f|--framework] [-o|--output] [-d|--diag] [--no-build] [-v|--verbosity] [-h|--help]`

## <a name="description"></a>Descrizione

Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto. Gli unit test sono progetti dell'applicazione console con dipendenze nel framework di unit test (ad esempio MSText, NUnit o xUnit) e nel Test Runner dotnet per il framework di unit test. Sono disponibili come pacchetti NuGet e vengono ripristinati come dipendenze ordinarie per il progetto.

Anche i progetti di test devono specificare il Test Runner. Quest'ultimo viene specificato usando un normale elemento `<PackageReference>`, come illustrato nel file di progetto di esempio seguente:

[!code-xml[Modello di base XUnit](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="options"></a>Opzioni

`PROJECT`
    
Specifica un percorso del progetto di test. Se omesso, per impostazione predefinita sarà la directory corrente.

`-h|--help`

Stampa una breve guida per il comando.

`-s|--settings <SETTINGS_FILE>`

Impostazioni da usare durante l'esecuzione di test. 

`-t|--list-tests`

Elenca tutti i test individuati nel progetto corrente. 

`--filter <EXPRESSION>`

Filtra i test nel progetto corrente usando l'espressione specificata. Per altre informazioni, vedere la sezione [Dettagli dell'opzione filter](#filter-option-details). Per altre informazioni e per esempi sull'uso del filtro degli unit test selettivi, vedere [Esecuzione di unit test selettivi](../testing/selective-unit-tests.md).

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

Usa gli adattatori di test personalizzati dal percorso specificato nell'esecuzione del test. 

`-l|--logger <LoggerUri/FriendlyName>`

Specifica un logger per i risultati di test. 

`-c|--configuration <CONFIGURATION>`

Configurazione in cui eseguire la compilazione. Il valore predefinito è `Debug`, ma la configurazione del progetto può eseguire l'override di questa impostazione predefinita dell'SDK.

`-f|--framework <FRAMEWORK>`

Cerca i file binari di test per un [framework](../../standard/frameworks.md) specifico.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui trovare i file binari da eseguire.

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

Abilita la modalità di diagnostica per la piattaforma di test e scrive messaggi di diagnostica nel file specificato. 

`--no-build` 

Non compila il progetto di test prima di eseguirlo.

`-v|--verbosity <LEVEL>`

Imposta il livello di dettaglio del comando. I valori consentiti sono `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` e `diag[nostic]`.

## <a name="examples"></a>Esempi

Eseguire i test nel progetto nella directory corrente:

`dotnet test` 

Eseguire i test nel progetto `test1`:

`dotnet test ~/projects/test1/test1.csproj`

## <a name="filter-option-details"></a>Dettagli dell'opzione filter

`--filter <EXPRESSION>`

`<Expression>` ha il formato `<property><operator><value>[|&<Expression>]`.

`<property>` è un attributo di `Test Case`. La tabella seguente elenca le proprietà supportate da framework diffusi per unit test:

| Framework di test | Proprietà supportate                                                                                      |
| :------------: | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>Nome</li><li>ClassName</li><li>Priorità</li><li>TestCategory</li></ul> |
| Xunit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>Tratti</li></ul>                                   |

`<operator>` descrive la relazione tra la proprietà e il valore:

| Operatore | Funzione        |
| :------: | --------------- |
| `=`      | Corrispondenza esatta     |
| `!=`     | Corrispondenza non esatta |
| `~`      | Contiene        |

`<value>` è una stringa. Per tutte le ricerche non viene fatta distinzione tra maiuscole e minuscole.

Un'espressione senza `<operator>` viene considerata automaticamente come un'operazione `contains` sulla proprietà `FullyQualifiedName`. Ad esempio, `dotnet test --filter xyz` è uguale a `dotnet test --filter FullyQualifiedName~xyz`.

Le espressioni possono essere unite con operatori condizionali:

| Operatore | Funzione |
| :------: | :------: |
| `|`      | OR       |
| `&`      | AND      |

È possibile racchiudere le espressioni tra parentesi quando si usano gli operatori condizionali (ad esempio, `(Name~TestMethod1) | (Name~TestMethod2)`).

Per altre informazioni e per esempi sull'uso del filtro degli unit test selettivi, vedere [Running selective unit tests](../testing/selective-unit-tests.md) (Esecuzione di unit test selettivi).

## <a name="see-also"></a>Vedere anche

[Framework e destinazioni](../../standard/frameworks.md)   
[Catalogo dei RID (Runtime IDentifier) di .NET Core](../rid-catalog.md)

