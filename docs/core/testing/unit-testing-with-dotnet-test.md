---
title: Unit Testing in .NET Core con il test dotnet | Microsoft Docs
description: Eseguire unit test in .NET Core usando il test dotnet
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 002/02/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdcdb812-6f13-4f20-9e90-0c0977937142
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: cd860241f5f20b6a4f1ccfec60e0c9cd5079152a
ms.lasthandoff: 03/07/2017

---

# <a name="unit-testing-in-net-core-using-dotnet-test"></a>Eseguire unit test in .NET Core usando il test dotnet

Di [Steve Smith](http://ardalis.com) e [Bill Wagner](https://github.com/BillWagner)

[Visualizzare o scaricare codice di esempio](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-using-dotnet-test)

## <a name="creating-the-projects"></a>Creazione dei progetti

[Writing Libraries with Cross Platform Tools](../tutorials/libraries.md) (Scrittura di librerie con strumenti multipiattaforma) contiene informazioni sull'organizzazione di soluzioni multiprogetto per l'origine e i test. Questo articolo segue tali convenzioni. La struttura del progetto finale avrà un aspetto simile al seguente:

```
/unit-testing-using-dotnet-test
|__/PrimeService
   |__Source Files
   |__PrimeService.csproj
|__/PrimeService.Tests
   |__Test Files
   |__PrimeService.csproj
```

### <a name="creating-the-source-project"></a>Creazione del progetto di origine

Iniziare nella directory `unit-testing-using-dotnet-test`, creare la directory `PrimeService`.
Passare alla directory ed eseguire `dotnet new classib` per creare il progetto di origine.


Rinominare `Class1.cs` in `PrimeService.cs`. Per usare lo sviluppo basato su test (TDD), si creerà un'implementazione con esito negativo della classe `PrimeService`:

```cs
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate) 
        {
            throw new NotImplementedException("Please create a test first");
        } 
    }
}

```

### <a name="creating-the-test-project"></a>Creazione del progetto di test

Successivamente ritornare alla directory 'unit-testing-using-dotnet-test' e creare la directory `PrimeServices.Tests`.
Passare alla directory `PrimeService.Tests` e creare un nuovo progetto tramite `dotnet new xunit`. `dotnet xunit` crea un progetto di test che usa xUnit come libreria di test. 

Il modello generato ha configurato il Test Runner nel file PrimeServiceTests.csproj:

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-preview-20170125-04" />
    <PackageReference Include="xunit" Version="2.2.0-beta5-build3474" />
    <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0-beta5-build1225" />
  </ItemGroup>
```

Per creare ed eseguire unit test, il progetto di test richiede altri pacchetti.
`dotnet new` ha aggiunto xUnit e il Runner di xUnit. È necessario aggiungere il pacchetto PrimeService allo stesso modo di un'altra dipendenza al progetto. È possibile eseguire questa operazione usando l'interfaccia della riga di comando di `dotnet`:

```
dotnet add reference ../PrimeService/PrimeService.csproj
```

Oppure è possibile modificare direttamente il file `PrimeService.Tests.csproj`.
Subito sotto il primo nodo `<ItemGroup>` aggiungere un altro nodo `<ItemGroup>` con un riferimento al progetto della libreria:

```xml
  <ItemGroup>
    <ProjectReference Include="..\PrimeService\PrimeService.csproj" />
  </ItemGroup>
```

È possibile visualizzare l'intero file nel [repository degli esempi](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService.Tests.csproj) su GitHub.

Dopo aver preparato questa struttura iniziale, è possibile scrivere il primo test.
Dopo aver verificato il primo unit test, tutto è configurato e dovrebbe funzionare senza problemi quando si aggiungono funzionalità e test.

## <a name="creating-the-first-test"></a>Creazione del primo test

Prima di compilare la libreria o i test, è necessario eseguire `dotnet restore` in entrambe le directory `PrimeService` e `PrimeService.Tests`. Questo comando ripristina tutti i pacchetti NuGet necessari a ogni progetto.

L'approccio TDD richiede che venga scritto un test con esito negativo, quindi che venga superato e infine ripetuto il processo. Verrà quindi scritto un test con esito negativo. Rimuovere `UnitTest1.cs` dalla directory `PrimeService.Tests` e creare un nuovo file C# denominato `PrimeService_IsPrimeShould.cs` con il contenuto seguente:

```cs
namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;
         public PrimeService_IsPrimeShould()
         {
             _primeService = new PrimeService();
         }

        [Fact]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.False(result, $"1 should not be prime");
        }
    }
}
```

L'attributo `[Fact]` identifica un metodo come un singolo test. 

Salvare questo file, quindi eseguire `dotnet build` per compilare il progetto di test.
Se non è già stato compilato il progetto `PrimeService`, il sistema di compilazione lo rileverà e compilerà il progetto, in quanto è una dipendenza del progetto di test.

Eseguire ora `dotnet test` per eseguire i test dalla console.
Il Test Runner di xUnit include il punto d'ingresso del programma per eseguire i test dalla console. `dotnet test` avvia il Test Runner e fornisce al Test Runner un argomento della riga di comando che indica l'assembly contenente i test.

Il test ha esito negativo. Non è stata ancora creata l'implementazione.
Scrivere il codice più semplice per superare il test:

```cs
public bool IsPrime(int candidate) 
{
    if(candidate == 1) 
    { 
        return false;
    } 
    throw new NotImplementedException("Please create a test first");
} 
```

### <a name="adding-more-features"></a>Aggiunta di altre funzionalità

Ora che il test è stato superato, è necessario scriverne altri.
Esistono alcuni altri casi semplici per i numeri primi: 0, -1. È possibile aggiungerli come nuovi test, con l'attributo `[Fact]`, ma questa operazione risulta rapidamente noiosa. Sono disponibili altri attributi xUnit che consentono di scrivere una suite di test analoghi.  Un oggetto `Theory` rappresenta una suite di test che eseguono lo stesso codice, ma hanno argomenti di input diversi.
È possibile usare l'attributo `[InlineData]` per specificare i valori per tali input. 
 
 Anziché creare nuovi test, usare questi due attributi per creare una singola teoria che verifica alcuni valori minori di 2, ovvero il numero primo più basso:

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-dotnet-test/PrimeService.Tests/PrimeService_IsPrimeShould.cs#Sample_TestCode "Primi test")]
```

Run `dotnet test` and you'll see that two of these tests fail.
You can make them pass by changing the service. You need to change
the `if` clause at the beginning of the method:

```cs
if(candidate < 2)
```

Ora tutti i test verranno superati.

Continuare a eseguire l'iterazione aggiungendo altri test, altre teorie e altro codice nella libreria principale. Si otterrà rapidamente la [versione completa dei test](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/PrimeService_IsPrimeShould.cs) e l'[implementazione completa della libreria](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/src/PrimeService/PrimeService.cs).

È stata compilata una piccola libreria e un set di unit test per tale libreria.
Questa soluzione è stata strutturata in modo che l'aggiunta di nuovi pacchetti e test sia semplice e permetta all'utente di concentrarsi sul problema in questione. Gli strumenti verranno eseguiti automaticamente.

