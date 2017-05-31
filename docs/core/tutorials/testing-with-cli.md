---
title: Organizzazione e test di progetti con la riga di comando di .NET Core | Microsoft Docs
description: Questa esercitazione illustra come organizzare e testare i progetti .NET Core dalla riga di comando.
keywords: .NET, .NET Core, unit test, .NET CLI, xUnit
author: cartermp
ms.author: mairaw
ms.date: 05/16/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 52ff1be3-d92e-4477-9c84-8c1771e87ab5
ms.translationtype: Human Translation
ms.sourcegitcommit: 6edd52bc56a03138fe16048fa06cad00a2af4847
ms.openlocfilehash: 1e6e987777678ade860f108aed05bba926a6d4fd
ms.contentlocale: it-it
ms.lasthandoff: 05/16/2017

---

# <a name="organizing-and-testing-projects-with-the-net-core-command-line"></a>Organizzazione e test di progetti con la riga di comando di .NET Core

Questa esercitazione segue [Introduzione all'uso di .NET Core su Windows/Linux/macOS dalla riga di comando](using-with-xplat-cli.md) e va oltre la creazione di una semplice app console, illustrando lo sviluppo di applicazioni più avanzate e organizzate. L'esercitazione indica come usare le cartelle per organizzare il codice, quindi illustra come estendere un'applicazione console con il framework di testo [xUnit](https://xunit.github.io/).

## <a name="using-folders-to-organize-code"></a>Uso di cartelle per organizzare il codice

È possibile introdurre nuovi tipi in un'app console aggiungendo all'app i file contenenti i tipi. Se ad esempio si aggiungono al progetto file contenenti i tipi `AccountInformation` e `MonthlyReportRecords`, la struttura del progetto resta semplice e facile da esplorare:

```
/MyProject
|__AccountInformation.cs
|__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

Tuttavia questa soluzione funziona solo quando le dimensioni del progetto sono relativamente piccole. Si supponga di aggiungere 20 tipi al progetto. La navigazione e la manutenzione diventano più complicate per la presenza di molti file nella directory radice del progetto.

Per organizzare il progetto, creare una nuova cartella per l'archiviazione dei file dei tipi e denominarla *Models*. Inserire i file dei tipi nella cartella *Models*:

```
/MyProject
|__/Models
   |__AccountInformation.cs
   |__MonthlyReportRecords.cs
|__MyProject.csproj
|__Program.cs
```

La navigazione e la manutenzione risultano più facili nei progetti che raggruppano i file in cartelle mediante codice. Nella sezione successiva viene creato un esempio più complesso con cartelle e unit test.

## <a name="organizing-and-testing-using-the-newtypes-pets-sample"></a>Organizzare ed eseguire test con l'esempio NewTypes Pets

### <a name="building-the-sample"></a>Compilare l'esempio

Nelle fasi successive è possibile seguire [il progetto di esempio NewTypes Pets](https://github.com/dotnet/docs/tree/master/samples/core/console-apps/NewTypesMsBuild) o creare file e cartelle personalizzati. I tipi sono organizzati mediante codice in una struttura di cartelle che consente l'aggiunta di più tipi in un secondo momento. A loro volta i test sono inseriti mediante codice in cartelle che consentono l'aggiunta di altri test in un secondo momento.

L'esempio contiene due tipi `Dog` e `Cat` e definisce l'implementazione dell'interfaccia comune `IPet`. Per il progetto `NewTypes` l'obiettivo è l'organizzazione dei tipi associati agli animali domestici in una cartella *Pets*. Se in seguito viene aggiunto un altro set di tipi, ad esempio *WildAnimals*, questi vengono inseriti nella cartella *NewTypes* allo stesso livello della cartella *Pets*. La cartella *WildAnimals* può contenere tipi corrispondenti ad animali non domestici, ad esempio i tipi `Squirrel` e `Rabbit`. In questo modo mano a mano che vengono aggiunti dei tipi il progetto mantiene un'organizzazione ottimale. 

Creare la seguente struttura di cartelle con il contenuto di file indicato:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
```

*IPet.cs*:

[!code-csharp[Interfaccia IPet](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/IPet.cs)]

*Dog.cs*:

[!code-csharp[Classe Dog](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/Dog.cs)]

*Cat.cs*:

[!code-csharp[Classe Cat](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Pets/Cat.cs)]

*Program.cs*:

[!code-csharp[Principale](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/Program.cs)]

*NewTypes.csproj*:

[!code-xml[File csproj NewTypes](../../../samples/core/console-apps/NewTypesMsBuild/src/NewTypes/NewTypes.csproj)]

Eseguire i seguenti comandi:

```console
dotnet restore
dotnet run
```

L'output è il seguente:

```console
Woof!
Meow!
```

Esercizio facoltativo: aggiungere un nuovo tipo di animale domestico, ad esempio `Bird`, estendendo il progetto. Fare in modo che il metodo `TalkToOwner` corrispondente all'uccellino restituisca `Tweet!` al proprietario. Eseguire nuovamente l'app. L'output includerà `Tweet!`.

### <a name="testing-the-sample"></a>Test dell'esempio

Il progetto `NewTypes` è attivo ed è stato organizzato inserendo i tipi associati agli animali da compagnia in una cartella. Creare il progetto di test e iniziare a creare test con il framework di test [xUnit](https://xunit.github.io/). Gli unit test consentono di verificare automaticamente che i tipi di animali domestici funzionino correttamente.

Creare una cartella *test* contenente una sottocartella *NewTypesTests*. Al prompt dei comandi della cartella *NewTypesTests* eseguire `dotnet new xunit`. Questa operazione produce due file: *NewTypesTests.csproj* e *UnitTest1.cs*.

Il progetto di test non può verificare i tipi in `NewTypes` e richiede un riferimento al progetto `NewTypes`. Per aggiungere un riferimento al progetto usare il comando [`dotnet add reference`](../tools/dotnet-add-reference.md):

```
dotnet add reference ../../src/NewTypes/NewTypes.csproj
```

In alternativa è possibile aggiungere manualmente il riferimento al progetto aggiungendo un nodo `<ItemGroup>` al file *NewTypesTests.csproj*:

```xml
<ItemGroup>
  <ProjectReference Include="../../src/NewTypes/NewTypes.csproj" />
</ItemGroup>
```

*NewTypesTests.csproj*:

[!code-xml[File csproj NewTypesTests](../../../samples/core/console-apps/NewTypesMsBuild/test/NewTypesTests/NewTypesTests.csproj)]

Il file *NewTypesTests.csproj* contiene quanto segue:

* Riferimento pacchetto a `Microsoft.NET.Test.Sdk`, l'infrastruttura di test .NET
* Riferimento pacchetto a `xunit`, l'infrastruttura di test xUnit
* Riferimento pacchetto a `xunit.runner.visualstudio`, il Test Runner
* Riferimento progetto a `NewTypes`, il codice da sottoporre ai test

Cambiare il nome *UnitTest1.cs* in *PetTests.cs* e sostituire il codice del file con il codice seguente:

```csharp
using System;
using Xunit;
using Pets;

public class PetTests
{
    [Fact]
    public void DogTalkToOwnerReturnsWoof()
    {
        string expected = "Woof!";
        string actual = new Dog().TalkToOwner();
        
        Assert.NotEqual(expected, actual);
    }
    
    [Fact]
    public void CatTalkToOwnerReturnsMeow()
    {
        string expected = "Meow!";
        string actual = new Cat().TalkToOwner();
        
        Assert.NotEqual(expected, actual);
    }
}
```

Esercizio facoltativo: se in precedenza è stato aggiunto un tipo `Bird` che restituisce `Tweet!` al proprietario, aggiungere al file *PetTests.cs* un metodo di test `BirdTalkToOwnerReturnsTweet` per verificare che il metodo `TalkToOwner` funzioni correttamente per il tipo `Bird`.

> [!NOTE]
> Anche se si prevede che i valori `expected` e `actual` siano uguali, le asserzioni iniziali con le verifiche `Assert.NotEqual` specificano che sono *not equal* (diversi). Inizialmente creare sempre i test in modo che diano esito negativo almeno una volta, per verificare la struttura del codice. Questo è un passaggio importante nella metodologia di design basato su test (TDD, Test-Driven Design). Dopo aver verificato che i test hanno dato esito negativo, modificare le asserzioni per fare in modo che diano esito positivo.

Di seguito viene riportata la struttura completa del progetto:

```
/NewTypes
|__/src
   |__/NewTypes
      |__/Pets
         |__Dog.cs
         |__Cat.cs
         |__IPet.cs
      |__Program.cs
      |__NewTypes.csproj
|__/test
   |__NewTypesTests
      |__PetTests.cs
      |__NewTypesTests.csproj
```

Iniziare nella directory *test/NewTypesTests*. Ripristinare il progetto di test con il comando [`dotnet restore`](../tools/dotnet-restore.md). Eseguire i test con il comando [`dotnet test`](../tools/dotnet-test.md). Questo comando avvia il Test Runner specificato nel file di progetto.
 
Come previsto, i test hanno esito negativo e la console visualizza il seguente output:
 
```
Test run for C:\NewTypesMsBuild\test\NewTypesTests\bin\Debug\netcoreapp1.1\NewTypesTests.dll(.NETCoreApp,Version=v1.1)
Microsoft (R) Test Execution Command Line Tool Version 15.0.0.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:00.7271827]   Discovering: NewTypesTests
[xUnit.net 00:00:00.8258687]   Discovered:  NewTypesTests
[xUnit.net 00:00:00.8663545]   Starting:    NewTypesTests
[xUnit.net 00:00:01.0109236]     PetTests.CatTalkToOwnerReturnsMeow [FAIL]
[xUnit.net 00:00:01.0119107]       Assert.NotEqual() Failure
[xUnit.net 00:00:01.0120278]       Expected: Not "Meow!"
[xUnit.net 00:00:01.0120968]       Actual:   "Meow!"
[xUnit.net 00:00:01.0130500]       Stack Trace:
[xUnit.net 00:00:01.0141240]         C:\NewTypesMsBuild\test\NewTypesTests\PetTests.cs(22,0): at PetTests.CatTalkToOwnerReturnsMeow()
[xUnit.net 00:00:01.0272364]     PetTests.DogTalkToOwnerReturnsWoof [FAIL]
[xUnit.net 00:00:01.0273649]       Assert.NotEqual() Failure
[xUnit.net 00:00:01.0274166]       Expected: Not "Woof!"
[xUnit.net 00:00:01.0274690]       Actual:   "Woof!"
[xUnit.net 00:00:01.0275264]       Stack Trace:
[xUnit.net 00:00:01.0275960]         C:\NewTypesMsBuild\test\NewTypesTests\PetTests.cs(13,0): at PetTests.DogTalkToOwnerReturnsWoof()
[xUnit.net 00:00:01.0294509]   Finished:    NewTypesTests
Failed   PetTests.CatTalkToOwnerReturnsMeow
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Meow!"
Actual:   "Meow!"
Stack Trace:
   at PetTests.CatTalkToOwnerReturnsMeow() in C:\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 22
Failed   PetTests.DogTalkToOwnerReturnsWoof
Error Message:
 Assert.NotEqual() Failure
Expected: Not "Woof!"
Actual:   "Woof!"
Stack Trace:
   at PetTests.DogTalkToOwnerReturnsWoof() in C:\NewTypesMsBuild\test\NewTypesTests\PetTests.cs:line 13

Total tests: 2. Passed: 0. Failed: 2. Skipped: 0.
Test Run Failed.
Test execution time: 2.1371 Seconds
```

Modificare le asserzioni dei test da `Assert.NotEqual` a `Assert.Equal`:

[!code-csharp[Classe PetTests](../../../samples/core/console-apps/NewTypesMsBuild/test/NewTypesTests/PetTests.cs)]

Eseguire nuovamente i test con il comando `dotnet test`. Si ottiene il seguente output:

```
Microsoft (R) Test Execution Command Line Tool Version 15.0.0.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:01.3882374]   Discovering: NewTypesTests
[xUnit.net 00:00:01.4767970]   Discovered:  NewTypesTests
[xUnit.net 00:00:01.5157667]   Starting:    NewTypesTests
[xUnit.net 00:00:01.6408870]   Finished:    NewTypesTests

Total tests: 2. Passed: 2. Failed: 0. Skipped: 0.
Test Run Successful.
Test execution time: 1.6634 Seconds
```

I test hanno esito positivo. I metodi dei tipi di animali da compagnia restituiscono i valori corretti nei messaggi trasmessi al proprietario.

Si sono apprese tecniche per l'organizzazione e il test di progetti con xUnit. Continuare con queste tecniche applicandole nei propri progetti. *Buona codifica!*
