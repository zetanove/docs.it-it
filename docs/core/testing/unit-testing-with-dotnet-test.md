---
title: Eseguire unit test in .NET Core usando il test dotnet
description: Eseguire unit test in .NET Core usando il test dotnet
keywords: .NET, .NET Core
author: ardalis
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdcdb812-6f13-4f20-9e90-0c0977937142
translationtype: Human Translation
ms.sourcegitcommit: 5687fc7ded899a478d1972ffea10a1e37d40124b
ms.openlocfilehash: f1f08f550d7484869e67fe705dc789ca5dae8e2f
ms.lasthandoff: 01/18/2017

---

# <a name="unit-testing-in-net-core-using-dotnet-test"></a>Eseguire unit test in .NET Core usando il test dotnet

Di [Steve Smith](http://ardalis.com) e [Bill Wagner](https://github.com/BillWagner)

[Visualizzare o scaricare codice di esempio](https://github.com/dotnet/docs/tree/master/samples/core/getting-started/unit-testing-using-dotnet-test)

> [!NOTE]
> Le informazioni contenute in questo argomento sono valide per .NET Core 1.0.

## <a name="creating-the-projects"></a>Creazione dei progetti

[Writing Libraries with Cross Platform Tools](../tutorials/libraries.md) (Scrittura di librerie con strumenti multipiattaforma) contiene informazioni sull'organizzazione di soluzioni multiprogetto per l'origine e i test. Questo articolo segue tali convenzioni. La struttura del progetto finale avrà un aspetto simile al seguente:

```
/unit-testing-using-dotnet-test
|__global.json
|__/src
   |__/PrimeService
      |__Source Files
      |__project.json
|__/test
   |__/PrimeService.Tests
      |__Test Files
      |__project.json
```

Nella directory radice è necessario creare un file `global.json` contenente i nomi delle directory `src` e `test`:

```json
{
    "projects": [
        "src",
        "test"
    ]
}
```

### <a name="creating-the-source-project"></a>Creazione del progetto di origine

Successivamente nella directory `src` creare la directory `PrimeService`.
Passare alla directory ed eseguire `dotnet new -t lib` per creare il progetto di origine.


Rinominare `Library.cs` in `PrimeService.cs`. Per usare lo sviluppo basato su test (TDD), si creerà un'implementazione con esito negativo della classe `PrimeService`:

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

Passare quindi alla directory "test" e creare la directory `PrimeServices.Tests`.
Passare alla directory `PrimeServices.Tests` e creare un nuovo progetto tramite `dotnet new -t xunittest`. `dotnet new -t xunittest` crea un progetto di test che usa xUnit come libreria di test. 

Il modello generato ha configurato il Test Runner alla radice di `project.json`:

```json
{
  "version": "1.0.0-*",
  "testRunner": "xunit",
  // ...
}
```

Il modello imposta anche il nodo framework per l'uso di `netcoreapp1.0` e include le importazioni necessarie per fare in modo che xUnit.net funzioni con .NET Core RTM:

```json
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dotnet54",
        "portable-net45+win8" 
      ]
    }
  }
```

Per creare ed eseguire unit test, il progetto di test richiede altri pacchetti.
`dotnet new` ha aggiunto xUnit e l'utilità di esecuzione di xUnit. È necessario aggiungere il pacchetto PrimeService come altra dipendenza al progetto:

```json
"dependencies": {
  "xunit":"2.1.0",
  "dotnet-test-xunit": "1.0.0-rc2-192208-24",
  "PrimeService": {
    "target": "project"
  }
}
```

Si noti che il progetto `PrimeService` non include informazioni sul percorso directory. Poiché la struttura di progetto è stata creata per corrispondere all'organizzazione prevista di `src` e `test`, come indicato dal file `global.json`, il sistema di compilazione troverà il percorso corretto per il progetto. Aggiungere l'elemento `"target": "project"` per indicare a NuGet di cercare nelle directory di progetto e non nel feed NuGet. Senza questa chiave, è possibile scaricare un pacchetto con lo stesso nome della libreria interna.

È possibile visualizzare l'intero file nel [repository degli esempi](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/project.json) su GitHub.

Dopo aver preparato questa struttura iniziale, è possibile scrivere il primo test.
Dopo aver verificato il primo unit test, tutto è configurato e dovrebbe funzionare senza problemi quando si aggiungono funzionalità e test.

## <a name="creating-the-first-test"></a>Creazione del primo test

L'approccio TDD richiede che venga scritto un test con esito negativo, quindi che venga superato e infine ripetuto il processo. Verrà quindi scritto un test con esito negativo. Rimuovere `program.cs` dalla directory `PrimeService.Tests` e creare un nuovo file di C# con il contenuto seguente:

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
Il Test Runner xUnit include il punto d'ingresso del programma per eseguire i test dalla console. `dotnet test` avvia il Test Runner e fornisce al Test Runner un argomento della riga di comando che indica l'assembly contenente i test.

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
Esistono alcuni altri casi semplici per i numeri primi: 0, -1. È possibile aggiungerli come nuovi test, con l'attributo `[Fact]`, ma questa operazione risulta rapidamente noiosa. Esistono altri attributi xUnit che consentono di scrivere una suite di test analoghi.  Un oggetto `Theory` rappresenta una suite di test che eseguono lo stesso codice, ma hanno argomenti di input diversi.
È possibile usare l'attributo `[InlineData]` per specificare i valori per tali input. 
 
 Anziché creare nuovi test, usare questi due attributi per creare una singola teoria che verifica alcuni valori minori di 2, ovvero il numero primo più basso:

```cs
[Theory]
[InlineData(-1)]
[InlineData(0)]
[InlineData(1)]
public void ReturnFalseGivenValuesLessThan2(int value)
{
    var result = _primeService.IsPrime(value);

    Assert.False(result, $"{value} should not be prime");
}
```

Se si esegue `dotnet test`, si noterà che i due test hanno esito negativo.
È possibile superarli modificando il servizio. È necessario modificate la clausola `if` all'inizio del metodo:

```cs
if(candidate < 2)
```

Ora tutti i test verranno superati.

Continuare a eseguire l'iterazione aggiungendo altri test, altre teorie e altro codice nella libreria principale. Si otterrà rapidamente la [versione completa dei test](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/test/PrimeService.Tests/PrimeServie_IsPrimeShould.cs) e l'[implementazione completa della libreria](https://github.com/dotnet/docs/blob/master/samples/core/getting-started/unit-testing-using-dotnet-test/src/PrimeService/PrimeService.cs).

È stata compilata una piccola libreria e un set di unit test per tale libreria.
Questa soluzione è stata strutturata in modo che l'aggiunta di nuovi pacchetti e test sia semplice e permetta all'utente di concentrarsi sul problema in questione. Gli strumenti verranno eseguiti automaticamente.
   
   > [!TIP]
   > Nella piattaforma Windows è possibile usare MSTest. Per altre informazioni, vedere il [documento sull'uso di MSTest in Windows](./using-mstest-on-windows.md).

