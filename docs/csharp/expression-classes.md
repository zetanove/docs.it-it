---
title: Tipi di framework che supportano alberi delle espressioni
description: Tipi di framework che supportano alberi delle espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: e9c85021-0d36-48af-91b7-aaaa66f22654
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 64b3b7999b6ff01bdf28cb7902ba50087d191cb4
ms.lasthandoff: 03/13/2017

---

# <a name="framework-types-supporting-expression-trees"></a>Tipi di framework che supportano alberi delle espressioni

[Precedente -- Expression Trees Explained (Nozioni di base sugli alberi delle espressioni)](expression-trees-explained.md)

In .NET Core Framework esiste un lungo elenco di classi che funzionano con gli alberi delle espressioni.
È possibile visualizzare l'elenco completo [qui](https://docs.microsoft.com/dotnet/core/api/System.Linq.Expressions).
Anziché rivedere l'elenco completo, cerchiamo di comprendere come sono state progettate le classi del framework.

Nella progettazione del linguaggio, un'espressione è un corpo di codice che valuta e restituisce un valore. Le espressioni possono essere molto semplici: l'espressione costante `1` restituisce il valore costante 1. Possono essere più complicate: l'espressione `(-B + Math.Sqrt(B*B + 4 * A * C)) / (2 * A)` restituisce una radice di un'equazione quadratica (nel caso in cui l'equazione abbia una soluzione).  

## <a name="it-all-starts-with-systemlinqexpression"></a>Tutto inizia con System.Linq.Expression

Una delle difficoltà legate all'uso degli alberi delle espressioni è che molti tipi diversi di espressioni sono validi in molte posizioni nei programmi. Si consideri un'espressione di assegnazione. Il lato destro di un'assegnazione può essere un valore costante, una variabile, un'espressione per chiamata al metodo o altro. Tale flessibilità del linguaggio significa che possono insorgere molti tipi di espressioni diverse in qualsiasi punto nei nodi di un albero quando si attraversa un albero delle espressioni. Pertanto, quando è possibile usare il tipo di espressione di base questo è il modo più semplice per lavorare. È talvolta necessario, tuttavia, ottenere maggiori informazioni.
La classe Expression di base contiene una proprietà `NodeType` per questo scopo.
Restituisce un `ExpressionType` che costituisce un'enumerazione dei tipi di espressioni possibili.
Quando si conosce il tipo di nodo, è possibile eseguirne il cast al tipo ed eseguire azioni specifiche conoscendo il tipo del nodo dell'espressione. È possibile eseguire la ricerca di determinati tipi di nodo e quindi usare le proprietà specifiche di quel tipo di espressione.

Ad esempio, questo codice stamperà il nome di una variabile per un'espressione di accesso alle variabili. È stata seguita la procedura di verifica del tipo di nodo, quindi è stato eseguito il cast a un'espressione di accesso alle variabili e infine sono state verificate le proprietà del tipo di espressione specifica:

```csharp
Expression<Func<int, int>> addFive = (num) => num + 5;

if (addFive.NodeType == ExpressionType.Lambda)
{
    var lambdaExp = (LambdaExpression)addFive;

    var parameter = lambdaExp.Parameters.First();

    Console.WriteLine(parameter.Name);
    Console.WriteLine(parameter.Type);
}
```

## <a name="creating-expression-trees"></a>Creazione dell'albero delle espressioni

La classe `System.Linq.Expression` contiene anche molti metodi statici per creare espressioni. Questi metodi creano un nodo di espressione usando gli argomenti specificati per i relativi elementi figlio. In questo modo, si compila un'espressione dai relativi nodi foglia. Ad esempio, questo codice compila un'espressione di aggiunta:

```csharp
// Addition is an add expression for "1 + 2"
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
```

In questo semplice esempio si vede che nella creazione e nell'uso degli alberi delle espressioni sono coinvolti molti tipi. Tale complessità è necessaria per offrire le funzionalità di vocabolario avanzate del linguaggio C#.

## <a name="navigating-the-apis"></a>Esplorazione delle API
Sono disponibili tipi di nodo Expression che eseguono il mapping a quasi tutti gli elementi della sintassi del linguaggio C#. Ogni tipo offre metodi specifici per il tipo di elemento di linguaggio. Vi sono molti elementi da tenere presenti contemporaneamente. Anziché tentare di memorizzare tutti gli elementi, ecco le tecniche consigliate per lavorare con gli alberi delle espressioni:
1. Esaminare i membri dell'enumerazione `ExpressionType` per determinare i possibili nodi da esaminare. Questo è estremamente utile quando si intende analizzare e comprendere un albero delle espressioni.
2. Esaminare i membri statici della classe `Expression` per compilare un'espressione. Tali metodi possono compilare qualsiasi tipo di espressione da un set dei relativi nodi figlio.
3. Esaminare la classe `ExpressionVisitor` per compilare un albero delle espressioni modificato.

Esaminando ognuna di queste aree, si otterranno maggiori informazioni. Si troverà quanto necessario iniziando con uno di questi tre passaggi.
 
 [Successivo -- Esecuzione di alberi delle espressioni](expression-trees-execution.md)
 

