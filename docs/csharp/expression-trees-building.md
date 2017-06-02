---
title: Compilazione di alberi delle espressioni
description: Compilazione di alberi delle espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 542754a9-7f40-4293-b299-b9f80241902c
ms.translationtype: Human Translation
ms.sourcegitcommit: 890c058bd09893c2adb185e1d8107246eef2e20a
ms.openlocfilehash: 5cce6b538e27f654c1f4fec732a9c69372f8c9ad
ms.contentlocale: it-it
ms.lasthandoff: 04/12/2017

---

# <a name="building-expression-trees"></a>Compilazione di alberi delle espressioni

[Precedente -- Interpretazione di espressioni](expression-trees-interpreting.md)

Tutti gli alberi delle espressioni visti finora sono stati creati dal compilatore C#. È stato sufficiente creare un'espressione lambda assegnata a una variabile tipizzata come un'espressione `Expression<Func<T>>` o di tipo simile. Questo tuttavia non è l'unico modo per creare un albero delle espressioni. In molti scenari potrebbe essere necessario compilare un'espressione in memoria in fase di esecuzione. 

La compilazione di alberi delle espressioni è complicata dal fatto che gli alberi delle espressioni non sono modificabili. Ciò significa che l'albero deve essere compilato dalle foglie alla radice. Ciò si riflette nelle API usate per compilare gli alberi delle espressioni: i metodi usati per compilare un nodo accettano tutti gli elementi figlio come argomenti. I seguenti esempi illustrano le tecniche.

## <a name="creating-nodes"></a>Creazione di nodi

Iniziamo con un esempio relativamente semplicemente, usando l'espressione di addizione già impiegata nelle sezioni seguenti:

```csharp
Expression<Func<int>> sum = () => 1 + 2;
```

Per costruire l'albero delle espressioni, è necessario creare i nodi foglia.
I nodi foglia sono costanti, e per costruirli è pertanto possibile usare il metodo `Expression.Constant`:

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
```

Successivamente, viene creata creato l'espressione di addizione:

```csharp
var addition = Expression.Add(one, two);
```

Dopo aver creato l'espressione di addizione, è possibile creare l'espressione lambda:

```csharp
var lamdba = Expression.Lambda(addition);
```

Si tratta di un'espressione LambdaExpression molto semplice, perché non contiene argomenti.
Più avanti in questa sezione verrà illustrato come eseguire il mapping degli argomenti ai parametri e compilare espressioni più complesse.

Per le espressioni semplici come questa, è possibile combinare tutte le chiamate in un'unica istruzione:

```csharp
var lambda = Expression.Lambda(
    Expression.Add(
        Expression.Constant(1, typeof(int)),
        Expression.Constant(2, typeof(int))
    )
);
```

## <a name="building-a-tree"></a>Compilazione di una struttura ad albero

Vengono illustrate le nozioni di base per la compilazione di un albero delle espressioni in memoria. Strutture ad albero più complesse implicano in genere più tipi di nodo e più nodi dell'albero. L'esempio seguente mostra due tipi di nodo che vengono in genere compilati quando si creano alberi delle espressioni: i nodi argomento e i nodi di chiamata al metodo.

Di seguito viene compilato un albero delle espressioni per creare questa espressione:

```csharp
Expression<Func<double, double, double>> distanceCalc =
    (x, y) => Math.Sqrt(x * x + y * y);
```
 
Si inizia creando espressioni per i parametri per `x` e `y`:

```csharp
var xParameter = Expression.Parameter(typeof(double), "x");
var yParameter = Expression.Parameter(typeof(double), "y");
```

Per creare le espressioni di addizione e moltiplicazione seguire il modello illustrato in precedenza:

```csharp
var xSquared = Expression.Multiply(xParameter, xParameter);
var ySquared = Expression.Multiply(yParameter, yParameter);
var sum = Expression.Add(xSquared, ySquared);
```

Quindi è necessario creare un'espressione di chiamata al metodo per la chiamata a `Math.Sqrt`.

```csharp
var sqrtMethod = typeof(Math).GetMethod("Sqrt", new[] { typeof(double) });
var distance = Expression.Call(sqrtMethod, sum);
```

Infine, inserire la chiamata al metodo in un'espressione lambda e verificare che gli argomenti nell'espressione lambda siano stati definiti:

```csharp
var distanceLambda = Expression.Lambda(
    distance,
    xParameter,
    yParameter);
```

In questo esempio più complesso, vengono illustrate altre due tecniche spesso necessarie per creare alberi delle espressioni.

Innanzitutto è necessario creare gli oggetti che rappresentano i parametri o le variabili locali prima di usarli. Dopo aver creato questi oggetti, è possibile inserirli nell'albero delle espressioni secondo necessità.

È quindi necessario usare un sottoinsieme dell'API Reflection per creare un oggetto `MethodInfo`, così da poter creare un albero delle espressioni per accedere a tale metodo. È necessario limitarsi al sottoinsieme delle API Reflection disponibili nella piattaforma .NET Core. Anche queste tecniche possono essere estese ad altri alberi delle espressioni.

## <a name="building-code-in-depth"></a>Compilazione di codice complesso

Non ci sono limiti alle possibilità di creare usando queste API. Tuttavia, più complicato è l'albero delle espressioni che si vuole compilare, più difficile sarà da gestire e leggere il codice. 

Viene ora creato un albero delle espressioni che è l'equivalente di questo codice:

```csharp
Func<int, int> factorialFunc = (n) =>
{
    var res = 1;
    while (n > 1)
    {
        res = res * n;
        n--;
    }
    return res;
};
```

Si noti che non è stato compilato l'albero delle espressioni, ma il delegato. Usando la classe `Expression` non è possibile compilare espressioni lambda dell'istruzione. Ecco il codice necessario per compilare la stessa funzionalità. È complicato dal fatto che non esiste un'API per compilare un ciclo `while`, ed è invece necessario creare un ciclo contenente un test condizionale e una destinazione dell'etichetta per uscire dal ciclo. 

```csharp
var nArgument = Expression.Parameter(typeof(int), "n");
var result = Expression.Variable(typeof(int), "result");

// Creating a label that represents the return value
LabelTarget label = Expression.Label(typeof(int));

var initializeResult = Expression.Assign(result, Expression.Constant(1));

// This is the inner block that performs the multiplication,
// and decrements the value of 'n'
var block = Expression.Block(
    Expression.Assign(result,
        Expression.Multiply(result, nArgument)),
    Expression.PostDecrementAssign(nArgument)
);

// Creating a method body.
BlockExpression body = Expression.Block(
    new[] { result },
    initializeResult,
    Expression.Loop(
        Expression.IfThenElse(
            Expression.GreaterThan(nArgument, Expression.Constant(1)),
            block,
            Expression.Break(label, result)
        ),
        label
    )
);
```

Il codice per creare l'albero delle espressioni per la funzione fattoriale è più lungo, più complesso, e include numerose etichette e istruzioni di interruzione che è preferibile evitare nelle quotidiane attività di codifica. 

Per questa sezione è stato anche aggiornato il codice visitatore, per visitare ogni nodo in questo albero delle espressioni e scrivere le informazioni relative ai nodi creati in questo esempio. È possibile [visualizzare o scaricare il codice di esempio](https://github.com/dotnet/docs/tree/master/samples/csharp/expression-trees) dal repository GitHub dotnet/docs. Provare a compilare ed eseguire da soli gli esempi. Per istruzioni sul download, vedere [Esempi ed esercitazioni](../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="examining-the-apis"></a>Analisi delle API

Le API dell'albero delle espressioni sono tra le più difficili da esplorare .NET Core. La loro finalità è piuttosto complessa: consentono di scrivere codice che genera codice in fase di esecuzione. Sono intrinsecamente complicate perché devono offrire un equilibrio tra la capacità di supportare tutte le strutture di controllo disponibili nel linguaggio C# e mantenere l'area di superficie delle API di dimensioni ridotte. Questo equilibrio fa sì che molte strutture di controllo siano rappresentate non dai propri costrutti in C#, ma da costrutti che rappresentano la logica sottostante generata dal compilatore a partire da quei costrutti di livello superiore. 

Inoltre, attualmente sono disponibili espressioni in C# che non possono essere compilate direttamente usando metodi della classe `Expression`. In generale, questi saranno gli operati e le espressioni più recenti aggiunte in C# 5 e C# 6. Ad esempio, non è possibile compilare espressioni `async` e non è possibile creare direttamente il nuovo operatore `?.`.

[Successivo -- Conversione di espressioni](expression-trees-translating.md)

