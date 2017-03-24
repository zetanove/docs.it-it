---
title: Usare MSTest con .NET Core | Microsoft Docs
description: Come usare MSTest con .NET Core
keywords: MSTest, .NET, .NET Core
author: ncarandini
ms.author: wiwagn
ms.date: 02/10/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ed447641-3e85-4e50-b7ed-004630048a3e
translationtype: Human Translation
ms.sourcegitcommit: 195664ae6409be02ca132900d9c513a7b412acd4
ms.openlocfilehash: 4ffc7dd4e11820a3c50ca83847a7ab418bf2faf3
ms.lasthandoff: 03/07/2017

---

# <a name="unit-testing-with-mstest-and-net-core"></a>Unit testing con MSTest e .NET Core

## <a name="creating-the-projects"></a>Creazione dei progetti

[Writing Libraries with Cross Platform Tools](../tutorials/libraries.md) (Scrittura di librerie con strumenti multipiattaforma) contiene informazioni sull'organizzazione di soluzioni multiprogetto per l'origine e i test. Questo articolo segue tali convenzioni. La struttura del progetto finale avrà un aspetto simile al seguente:

```
/unit-testing-using-mstest
|__/PrimeService
   |__Source Files
   |__PrimeService.csproj
|__/PrimeService.Tests
   |__Test Files
   |__PrimeService.csproj
```

### <a name="creating-the-source-project"></a>Creazione del progetto di origine

Aprire una finestra della shell. Iniziare nella directory *unit-testing-using-mstest*, creare la directory *PrimeService*.
Rendere *PrimeService* la directory corrente ed eseguire `dotnet new classlib` per creare il progetto di origine.

Assegnare il nome *PrimeService.cs* al file *Class1.cs*. Per usare lo sviluppo basato su test (TDD), si creerà un'implementazione con esito negativo della classe `PrimeService`:

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

Ritornare successivamente alla directory *unit-testing-using-mstest* e creare la directory *PrimeServices.Tests*.
Rendere *PrimeService.Tests* la directory corrente e creare un nuovo progetto usando `dotnet new mstest`. Ciò crea un progetto di test che usa MStest come libreria test. 

Il modello generato ha configurato il Test Runner nel file *PrimeServiceTests.csproj*:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.0.0-preview-20170123-02" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.10-rc2" />
  <PackageReference Include="MSTest.TestFramework" Version="1.0.8-rc2" />
</ItemGroup>
```

Per creare ed eseguire unit test, il progetto di test richiede altri pacchetti.
`dotnet new` ha aggiunto l'SDK MSTest, il framework di test MSTest e il Runner MSTest. È necessario aggiungere il pacchetto PrimeService allo stesso modo di un'altra dipendenza al progetto. È possibile eseguire questa operazione usando l'interfaccia della riga di comando di `dotnet`:

```
dotnet add reference ../PrimeService/PrimeService.csproj
```

Oppure è possibile modificare manualmente il file *PrimeService.Tests.csproj*.
Subito sotto il primo nodo `<ItemGroup>` aggiungere un altro nodo `<ItemGroup>` con un riferimento al progetto della libreria:

```xml
  <ItemGroup>
    <ProjectReference Include="..\PrimeService\PrimeService.csproj" />
  </ItemGroup>
```

È possibile visualizzare l'intero file nel [repository degli esempi](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService.Tests.csproj) su GitHub.

Dopo aver preparato questa struttura iniziale, è possibile scrivere il primo test.
Dopo aver verificato il primo unit test, tutto è configurato e dovrebbe funzionare senza problemi quando si aggiungono funzionalità e test.

## <a name="creating-the-first-test"></a>Creazione del primo test

Prima di compilare la libreria o i test, è necessario eseguire `dotnet restore` in entrambe le directory *PrimeService* e *PrimeService.Tests*. Questo comando ripristina tutti i pacchetti NuGet necessari a ogni progetto.

L'approccio TDD richiede che venga scritto un test con esito negativo, quindi che venga superato e infine ripetuto il processo. Verrà quindi scritto un test con esito negativo. Rimuovere *UnitTest1.cs* dalla directory *PrimeService.Tests* e creare un nuovo file C# denominato *PrimeService_IsPrimeShould.cs* con il contenuto seguente:

```cs
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestClass]
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;
        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [TestMethod]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.IsFalse(result, $"1 should not be prime");
        }
    }
}
```

Gli attributi `[TestClass]` indicano una classe che contiene unit test. L'attributo `[TestMethod]` identifica un metodo come un singolo test. 

Salvare questo file, quindi eseguire `dotnet build` per compilare il progetto di test.
Se non è già stato compilato il progetto `PrimeService`, il sistema di compilazione lo rileverà e compilerà il progetto, in quanto è una dipendenza del progetto di test.

Eseguire ora `dotnet test` per eseguire i test dalla console.
Il Test Runner MSTest include il punto d'ingresso del programma per eseguire i test dalla console. `dotnet test` avvia il Test Runner e indica al Test Runner un argomento della riga di comando che specifica l'assembly contenente i test.

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

Nella directory *PrimeService.Tests* eseguire di nuovo `dotnet test`. Il comando `dotnet test` esegue prima una compilazione del progetto Prime.Services e quindi del progetto PrimeService.Tests. Dopo la compilazione di entrambi i progetti, verrà eseguito il test singolo. Procede.

## <a name="adding-more-features"></a>Aggiunta di altre funzionalità

Ora che il test è stato superato, è necessario scriverne altri.
Esistono alcuni altri casi semplici per i numeri primi: 0, -1. È possibile aggiungerli come nuovi test, con l'attributo `[TestMethod]`, ma questa operazione risulta rapidamente noiosa. Sono disponibili altri attributi di MSTest che consentono di scrivere una suite di test analoghi.  Un oggetto `DataTestMethod` rappresenta una suite di test che eseguono lo stesso codice, ma hanno argomenti di input diversi.
È possibile usare l'attributo `[DataRow]` per specificare i valori per tali input. 
 
 Anziché creare nuovi test, usare questi due attributi per creare un metodo singolo di test dei dati che verifica alcuni valori minori di 2, ovvero il numero primo più basso:

[!code-csharp[Sample_TestCode](../../../samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs#Sample_TestCode "Primi test")]

Se si esegue `dotnet test`, si noterà che i due test hanno esito negativo.
È possibile superarli modificando il servizio. È necessario modificate la clausola `if` all'inizio del metodo:

```cs
if(candidate < 2)
```

Ora tutti i test verranno superati.

Continuare a eseguire l'iterazione aggiungendo altri test, altre teorie e altro codice nella libreria principale. Si otterrà rapidamente la [versione completa dei test](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs) e l'[implementazione completa della libreria](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-mstest/PrimeService/PrimeService.cs).

È stata compilata una piccola libreria e un set di unit test per tale libreria.
Questa soluzione è stata strutturata in modo che l'aggiunta di nuovi pacchetti e test sia semplice e permetta all'utente di concentrarsi sul problema in questione. Gli strumenti verranno eseguiti automaticamente.
