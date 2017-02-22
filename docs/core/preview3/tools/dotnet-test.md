---
title: Comando dotnet-test | Microsoft Docs
description: Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto.
keywords: dotnet-test, interfaccia della riga di comando, comando dell&quot;interfaccia della riga di comando, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 02/08/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 4bf0aef4-148a-41c6-bb95-0a9e1af8762e
translationtype: Human Translation
ms.sourcegitcommit: 02f39bc959a56ab0fc2cfa57ce13f300a8a46107
ms.openlocfilehash: 204ebdb5a945dcd0c9277f1d95c113e829303b32

---

#<a name="dotnet-test-net-core-tools-rc4"></a>dotnet-test (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core, vedere l'argomento [dotnet-test](../../tools/dotnet-test.md).

## <a name="name"></a>Nome

`dotnet-test` - Driver di test .NET

## <a name="synopsis"></a>Riepilogo

`dotnet test [project] [--help] 
    [--settings] [--list-tests] [--filter] 
    [--test-adapter-path] [--logger] 
    [--configuration] [--framework] [--output] [--diag]
    [--no-build] [--verbosity]`

## <a name="description"></a>Descrizione

Il comando `dotnet test` viene usato per eseguire unit test in un determinato progetto. Gli unit test sono progetti della libreria di classi con dipendenze dal framework di unit test (ad esempio, NUnit o xUnit) e dal Test Runner dotnet per tale framework di unit test. Sono disponibili come pacchetti NuGet e vengono ripristinati come dipendenze ordinarie per il progetto.

Anche i progetti di test devono specificare il test runner. Quest'ultimo viene specificato usando un normale elemento `<PackageReference>`, come illustrato nel file di progetto di esempio seguente:

[!code-xml[Modello di base XUnit](../../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="options"></a>Opzioni

`[project]`
    
Specifica un percorso del progetto di test. Se omesso, per impostazione predefinita sarà la directory corrente.

`-h|--help`

Stampa una breve guida per il comando.

`-s|--settings <SETTINGS_FILE>`

Impostazioni da usare durante l'esecuzione di test. 

`-t|--list-tests`

Elenca tutti i test individuati nel progetto corrente. 

`--filter <EXPRESSION>`

Filtra i test nel progetto corrente usando l'espressione specificata. Per altre informazioni sul supporto dei filtri, vedere [Running selective unit tests in Visual Studio using TestCaseFilter](https://aka.ms/vstest-filtering) (Esecuzione di unit test selettivi in Visual Studio con TestCaseFilter).

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

Usa gli adattatori di test personalizzati dal percorso specificato nell'esecuzione del test. 

`-l|--logger <LoggerUri/FriendlyName>`

Specifica un logger per i risultati di test. 

`-c|--configuration <Debug|Release>`

Configurazione in cui eseguire la compilazione. Il valore predefinito è `Debug` ma la configurazione del progetto potrebbe eseguire l'override di questa impostazione predefinita dell'SDK.

`-f|--framework <FRAMEWORK>`

Cerca i file binari di test per un framework specifico.

`-o|--output <OUTPUT_DIRECTORY>`

Directory in cui trovare i file binari da eseguire.

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

Abilita la modalità di diagnostica per la piattaforma di test e scrive messaggi di diagnostica nel file specificato. 

`--no-build` 

Non compila il progetto di test prima di eseguirlo.

`-v|--verbosity [quiet|minimal|normal|diagnostic]`

Imposta il livello di dettaglio del comando. È possibile specificare i livelli di dettaglio seguenti: q[uiet], m[inimal], n[ormal], d[etailed] e diag[nostic]. 

## <a name="examples"></a>Esempi

Eseguire i test nel progetto nella directory corrente:

`dotnet test` 

Eseguire i test nel progetto test1:

`dotnet test ~/projects/test1/test1.csproj` 

## <a name="see-also"></a>Vedere anche

[Framework](../../../standard/frameworks.md)

[Catalogo RID (Runtime IDentifier)](../../rid-catalog.md)



<!--HONumber=Feb17_HO2-->


