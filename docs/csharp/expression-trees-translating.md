---
title: Traduzione degli alberi delle espressioni
description: Traduzione degli alberi delle espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b453c591-acc6-4e08-8175-97e5bc65958e
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 01cc83bc46d2cbe6beaaa5c3212b18bb8608ec82
ms.lasthandoff: 03/13/2017

---

# <a name="translating-expression-trees"></a>Traduzione degli alberi delle espressioni

[Precedente -- Creazione di espressioni](expression-trees-building.md)

In questa sezione finale si apprenderà come visitare ogni nodo in un albero delle espressioni, compilando una copia di tale albero delle espressioni modificato. Queste sono le tecniche che verranno usate in due scenari importanti. La prima consiste nel comprendere gli algoritmi espressi da un albero delle espressioni in modo che possa essere traslato in un altro ambiente. La seconda si applica quando si desidera modificare l'algoritmo creato. È possibile aggiungere la registrazione, intercettare chiamate al metodo e tenerne traccia, oltre ad altri scopi.

## <a name="translating-is-visiting"></a>Traslare è sinonimo di visitare

Il codice compilato per traslare un albero delle espressioni è un'estensione di tutto questo, utile per visitare tutti i nodi in un albero. Quando si trasla un albero delle espressioni, tutti i nodi vengono visitati e durante la visita viene compilato il nuovo albero. Il nuovo albero può contenere riferimenti ai nodi originali o ai nuovi nodi posizionati nell'albero.

Vediamo questo aspetto praticamente visitando un albero delle espressioni e creando un nuovo albero con alcuni nodi di sostituzione. In questo esempio, sostituiamo qualsiasi costante con una costante dieci volte maggiore.
In alternativa, possiamo lasciare l'albero delle espressioni intatto. Invece di leggere il valore della costante e sostituirla con una nuova costante, eseguiremo una sostituzione del nodo della costante con un nuovo nodo che esegue la moltiplicazione.

In questo caso, dopo aver trovato il nodo di una costante, creare un nuovo nodo di moltiplicazione i cui figli rappresentino la costante originale e la costante `10`:

```csharp
private static Expression ReplaceNodes(Expression original)
{
    if (original.NodeType == ExpressionType.Constant)
    {
        return Expression.Multiply(original, Expression.Constant(10));
    }
    else if (original.NodeType == ExpressionType.Add)
    {
        var binaryExpression = (BinaryExpression)original;
        return Expression.Add(
            ReplaceNodes(binaryExpression.Left),
            ReplaceNodes(binaryExpression.Right));
    }
    return original;
}
```

Sostituendo il nodo originale con il sostituto, viene formato un nuovo albero che contiene le modifiche. Possiamo verificarlo tramite la compilazione e l'esecuzione dell'albero sostituito.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
var sum = ReplaceNodes(addition);
var executableFunc = Expression.Lambda(sum);

var func = (Func<int>)executableFunc.Compile();
var answer = func();
Console.WriteLine(answer);
```

La creazione di un nuovo albero è una combinazione tra la visita ai nodi nell'albero esistente e la creazione e l'inserimento di nuovi nodi nell'albero.

Questo esempio illustra l'importanza dell'immutabilità degli alberi delle espressioni. Si noti che il nuovo albero creato in precedenza contiene una combinazione di nodi appena creati e nodi dall'albero esistente. Questa combinazione è sicura, poiché i nodi dell'albero esistente non possono essere modificati. Ciò può comportare una notevole efficienza della memoria.
Gli stessi nodi possono essere usati in uno o più alberi delle espressioni. Dal momento che i nodi non possono essere modificati, lo stesso nodo può essere riutilizzato secondo necessità.

## <a name="traversing-and-executing-an-addition"></a>Attraversamento ed esecuzione di un'addizione

Esamineremo ora questi aspetti creando un secondo visitatore che percorre l'albero dei nodi di addizione e calcola il risultato. È possibile realizzare tale operazione apportando un paio di modifiche al visitatore che abbiamo visto fino a questo momento. In questa nuova versione, il visitatore restituisce la somma parziale dell'operazione di addizione fino a questo punto. Per un'espressione costante, la somma corrisponde semplicemente al valore dell'espressione costante. Per un'espressione di addizione, il risultato è la somma degli operandi sinistro e destro, dopo l'attraversamento degli alberi.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var three= Expression.Constant(3, typeof(int));
var four = Expression.Constant(4, typeof(int));
var addition = Expression.Add(one, two);
var add2 = Expression.Add(three, four);
var sum = Expression.Add(addition, add2);

// Declare the delegate, so we can call it 
// from itself recursively:
Func<Expression, int> aggregate = null;
// Aggregate, return constants, or the sum of the left and right operand.
// Major simplification: Assume every binary expression is an addition.
aggregate = (exp) =>
    exp.NodeType == ExpressionType.Constant ?
    (int)((ConstantExpression)exp).Value :
    aggregate(((BinaryExpression)exp).Left) + aggregate(((BinaryExpression)exp).Right);

var theSum = aggregate(sum);
Console.WriteLine(theSum);
```

Useremo qui il codice, ma i concetti sono molto intuitivi.
Questo codice visita gli elementi figlio in una prima ricerca profondità. Quando incontra un nodo della costante, il visitatore restituisce il valore della costante. Dopo che il visitatore ha visitato entrambi gli elementi figlio, verrà calcolata la somma per essi, per questo sottoalbero. A questo punto, il nodo di addizione può calcolare la somma.
Dopo aver visitato tutti i noti dell'albero delle espressioni, verrà calcolata la somma. È possibile tracciare l'esecuzione eseguendo l'esempio nel debugger.

Semplifichiamo il tracciamento dell'analisi dei nodi e delle modalità di calcolo della somma tramite l'attraversamento dell'albero. Di seguito è riportata una versione aggiornata del metodo Aggregate che include una certa quantità di informazioni di tracciamento:

```csharp
private static int Aggregate(Expression exp)
{
    if (exp.NodeType == ExpressionType.Constant)
    {
        var constantExp = (ConstantExpression)exp;
        Console.Error.WriteLine($"Found Constant: {constantExp.Value}");
        return (int)constantExp.Value;
    }
    else if (exp.NodeType == ExpressionType.Add)
    {
        var addExp = (BinaryExpression)exp;
        Console.Error.WriteLine("Found Addition Expression");
        Console.Error.WriteLine("Computing Left node");
        var leftOperand = Aggregate(addExp.Left);
        Console.Error.WriteLine($"Left is: {leftOperand}");
        Console.Error.WriteLine("Computing Right node");
        var rightOperand = Aggregate(addExp.Right);
        Console.Error.WriteLine($"Right is: {rightOperand}");
        var sum = leftOperand + rightOperand;
        Console.Error.WriteLine($"Computed sum: {sum}");
        return sum;
    }
    else throw new NotSupportedException("Haven't written this yet");
}

```

L'esecuzione del metodo sulla stessa espressione produce l'output seguente:

```
10
Found Addition Expression
Computing Left node
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Constant: 2
Right is: 2
Computed sum: 3
Left is: 3
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 10
10
```

Tracciare l'output e procedere con il codice in alto. È possibile comprendere in che modo il codice visiti ogni nodo e calcoli la somma attraversando l'albero e trovando la somma.

Esaminiamo ora un'esecuzione diversa, con l'espressione rappresentata da `sum1`:

```csharp
Expression<Func<int> sum1 = () => 1 + (2 + (3 + 4));
```

Di seguito è riportato l'output dell'analisi di questa espressione:

```
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 2
Left is: 2
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 9
Right is: 9
Computed sum: 10
10
```

Mentre la risposta finale è la stesso, l'attraversamento dell'albero è completamente diverso. I nodi vengono attraversati in un ordine diverso, perché l'albero è stato costruita con diverse operazioni che si verificano prima.

## <a name="learning-more"></a>Ulteriori informazioni

Questo esempio illustra un piccolo sottoinsieme del codice creato per attraversare e interpretare gli algoritmi rappresentati da un albero delle espressioni. Per una descrizione completa di tutte le operazioni necessarie per compilare una libreria generica che trasla gli alberi delle espressioni in un'altra lingua, vedere [questa serie](http://blogs.msdn.com/b/mattwar/archive/2008/11/18/linq-links.aspx) di Matt Warren. La serie spiega in dettaglio come traslare il codice di un albero delle espressioni.

Mi auguro che abbiamo percepito la vera potenza degli alberi delle espressioni.
È possibile esaminare un set di codice, apportare modifiche a tale codice ed eseguire la versione modificata. Dal momento che gli alberi delle espressioni sono immutabili, è possibile creare nuovi alberi usando i componenti degli alberi esistenti. Questa operazione riduce la quantità di memoria necessaria per creare alberi delle espressioni modificati.

[Successivo -- Conclusioni](expression-trees-summary.md)

