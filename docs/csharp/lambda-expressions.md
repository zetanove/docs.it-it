---
title: Espressioni lambda
description: Informazioni sull&quot;uso delle espressioni lambda, vale a dire blocchi di codice eseguibile che possono essere passati come argomenti.
keywords: .NET, .NET Core, espressioni lambda, lambda, delegati
ms-author: ronpet
author: rpetrusha
ms.date: 11/22/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b6a0539a-8ce5-4da7-adcf-44be345a2714
ms.translationtype: Human Translation
ms.sourcegitcommit: 81f31f1abc9db14b6b899564d67ca6e90d269ad7
ms.openlocfilehash: bbb524e50d74207227420d073afd5758d3d5aaa7
ms.contentlocale: it-it
ms.lasthandoff: 04/11/2017

---

# <a name="lambda-expressions"></a>Espressioni lambda #

Un'*espressione lambda* è un blocco di codice costituito da espressioni o da istruzioni che viene trattato come oggetto. Tale blocco può essere passato come argomento ai metodi e può anche essere restituito dalle chiamate al metodo. Le espressioni lambda sono spesso usate per eseguire le attività seguenti:

- Passaggio del codice da eseguire a metodi asincroni, ad esempio @System.Threading.Tasks.Task.Run(System. Action).

- Scrittura di [espressioni di query LINQ](linq/index.md).

- Creazione di [alberi delle espressioni](expression-trees-building.md).

Le espressioni lambda sono codice che può essere rappresentato come delegato o come albero delle espressioni che viene compilato in un delegato. Il tipo di delegato specifico di un'espressione lambda dipende dai parametri dell'espressione e dal valore restituito. Le espressioni lambda che non restituiscono un valore corrispondano a un delegato `Action` specifico, che dipende dal relativo numero di parametri. Le espressioni lambda che restituiscono un valore corrispondano a un delegato `Func` specifico, che dipende dal relativo numero di parametri. Ad esempio, se un'espressione lambda con due parametri non restituisce un valore, corrisponde a un delegato @System.Action% 602. Ad esempio, se un'espressione lambda con due parametri non restituisce un valore, corrisponde a un delegato @System.Func% 602.

Un'espressione lambda usa `=>`, vale a dire l'[operatore di dichiarazione lambda](language-reference/operators/lambda-operator.md), per separare l'elenco di parametri dell'espressione lambda dal codice eseguibile. Per creare un'espressione lambda, specificare gli eventuali parametri di input a sinistra dell'operatore lambda e inserire il blocco di espressioni o di istruzioni dall'altra parte. Ad esempio, l'espressione lambda `x => x * x` a riga singola specifica un parametro denominato `x` e restituisce il valore di `x` al quadrato. È possibile assegnare questa espressione a un tipo di delegato, come illustrato nell'esempio riportato di seguito:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/lambda1.cs#1)]

Oppure è possibile passarla direttamente come argomento del metodo:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/lambda2.cs#2)]

## <a name="expression-lambdas"></a>Espressioni lambda ##

 Un'espressione lambda con un'espressione a destra dell'operatore => è denominata *espressione lambda*. Queste espressioni vengono usate spesso nella costruzione di [alberi delle espressioni](expression-trees.md). Un'espressione lambda dell'espressione restituisce il risultato dell'espressione e ha il formato di base seguente:

```csharp
(input parameters) => expression
```

Le parentesi sono facoltative solo se l'espressione lambda ha un parametro di input; in caso contrario sono obbligatorie. Specificare zero parametri di input con parentesi vuote:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#1)]

Due o più parametri di input vengono separati da virgole e racchiusi tra parentesi:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#2)]

Il compilatore usa solitamente l'inferenza del tipo per determinare i tipi di parametro. Talvolta è tuttavia difficile o impossibile per il compilatore dedurre i tipi di input. In tal caso, è possibile specificare i tipi in modo esplicito come illustrato nell'esempio seguente:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/expression3.cs#3)]

Si noti che nell'esempio precedente il corpo di un'espressione lambda dell'espressione può essere costituito da una chiamata al metodo. Se si creano tuttavia alberi delle espressioni valutati al di fuori di .NET Framework, ad esempio in SQL Server o in Entity Framework, non è consigliabile usare chiamate al metodo nelle espressioni lambda. I metodi non avranno infatti alcun significato all'esterno del contesto del runtime .NET. Se si sceglie comunque di usare le chiamate al metodo, testarle attentamente per assicurarsi che possano essere risolte correttamente.

## <a name="statement-lambdas"></a>Espressioni lambda dell'istruzione ##

Un'espressione lambda dell'istruzione è simile a un'espressione lambda dell'espressione con la differenza che l'istruzione o le istruzioni sono racchiuse tra parentesi graffe:

```csharp
(input parameters) => { statement; }
```

Il corpo di un'espressione lambda dell'istruzione può essere costituito da un numero qualsiasi di istruzioni, sebbene in pratica generalmente non ce ne siano più di due o tre.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/statement1.cs#1)]

Le espressioni lambda dell'istruzione, come i metodi anonimi, non possono essere utilizzate per creare alberi delle espressioni.

## <a name="async-lambdas"></a>Espressioni lambda asincrone ##

Usando le parole chiave [async](language-reference/keywords/async.md) e [await](language-reference/keywords/await.md) è facile creare istruzioni ed espressioni lambda che includono l'elaborazione asincrona. Nell'esempio viene chiamato un metodo `ShowSquares` eseguito in modo asincrono.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/async1.cs#1)]

Per altre informazioni su come creare e usare i metodi asincroni, vedere [Programmazione asincrona con async e await (C#)](programming-guide/concepts/async/index.md).

## <a name="lambda-expressions-and-tuples"></a>Espressioni lambda e tuple ##

A partire da C# 7.0, il linguaggio C# offre supporto predefinito delle tuple. È possibile specificare una tupla come argomento di un'espressione lambda e l'espressione lambda può restituire una tupla. In alcuni casi, il compilatore C# usa l'inferenza del tipo per determinare i tipi di componenti della tupla. 

Per definire una tupla, è necessario racchiudere tra parentesi un elenco di componenti delimitato da virgole. L'esempio riportato sotto usa una tupla con 5 componenti per passare una sequenza di numeri a un'espressione lambda, la quale raddoppia ogni valore e restituisce una tupla con 5 componenti che contiene il risultato delle moltiplicazioni.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/tuples1.cs#1)]

In genere, i campi di una tupla sono denominati `Item1`, `Item2` e così via. È possibile tuttavia definire una tupla usando i componenti denominati, come illustra l'esempio seguente.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/tuples2.cs#1)]

Per altre informazioni sul supporto delle tuple in C#, vedere [C# Tuple types](tuples.md) (Tipi di tupla in C#).

## <a name="lambdas-with-the-standard-query-operators"></a>Espressioni lambda con operatori query standard ##

LINQ to Objects e altre implementazioni hanno un parametro di input il cui tipo è uno della famiglia @System.Func%601 di delegati generici. Questi delegati usano parametri di tipo per definire il numero e il tipo di parametri di input e il tipo restituito del delegato. I delegati `Func` sono molto utili per incapsulare le espressioni definite dall'utente applicate a ogni elemento in un set di dati di origine. Considerare ad esempio il delegato @System.Func%601, la cui sintassi è la seguente:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#1)]

È possibile creare un'istanza del delegato come un codice simile al seguente

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#2)]

dove `int` è un parametro di input e `bool` è il valore restituito. Il valore restituito è sempre specificato nell'ultimo parametro di tipo. Quando viene richiamato, il delegato `Func` seguente restituisce true o false per indicare se il parametro di input è uguale a 5:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#3)]

È anche possibile specificare un'espressione lambda quando il tipo di argomento è @System.Linq.Expressions.Expression%601, ad esempio negli operatori query standard definiti nel tipo @System.Linq.Queryable. Quando si specifica un argomento @System.Linq.Expressions.Expression%601, l'espressione lambda viene compilata per un albero delle espressioni. Nell'esempio seguente viene usato l'operatore di query standard [System.Linq.Enumerable.Count](xref:System.Linq.Enumerable.Count%60%601(System.Collections.Generic.IEnumerable{%60%600})).

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#4)]

Il compilatore è in grado di dedurre il tipo del parametro di input oppure è possibile specificarlo in modo esplicito. Questa espressione lambda particolare conta i numeri interi (`n`) che divisi per due danno un resto di 1.

L'esempio seguente crea una sequenza contenente tutti gli elementi presenti nella matrice `numbers` che si trovano a sinistra di 9, vale a dire il primo numero della sequenza che non soddisfa la condizione.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#5)]

In questo esempio viene illustrato come specificare più parametri di input racchiudendoli tra parentesi. Il metodo restituisce tutti gli elementi presenti nella matrice di numeri finché non viene rilevato un numero il cui valore è inferiore alla relativa posizione all'interno della matrice.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/query1.cs#6)]

## <a name="type-inference-in-lambda-expressions"></a>Inferenza del tipo nelle espressioni lambda ##

Quando si scrivono espressioni lambda, spesso non occorre specificare un tipo per i parametri di input, in quanto il compilatore può dedurlo in base al corpo dell'espressione lambda, ai tipi di parametro e ad altri fattori, come descritto nelle specifiche del linguaggio C#. Per la maggior parte degli operatori di query standard, il primo input è il tipo degli elementi nella sequenza di origine. Pertanto, se si esegue una query su un oggetto `IEnumerable<Customer>`, si deduce che la variabile di input sia un oggetto `Customer`, ovvero che si dispone dell'accesso ai relativi metodi e proprietà:

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/infer1.cs#1)]

Di seguito sono riportate le regole generali per l'inferenza del tipo nelle espressioni lambda:

- L'espressione lambda deve contenere lo stesso numero di parametri del tipo delegato.

- Ogni argomento di input nell'espressione lambda deve essere convertibile in modo implicito nel parametro del delegato corrispondente.

- Il valore restituito dell'espressione lambda, se presente, deve essere convertibile in modo implicito nel tipo restituito del delegato.

Si noti che le espressioni lambda non hanno un tipo poiché Common Type System non ha alcun concetto intrinseco di "espressione lambda". In alcuni casi, tuttavia, può essere utile fare riferimento in modo informale al "tipo" di un'espressione lambda. In questi casi, per tipo si intende il tipo delegato o il tipo @System.Linq.Expressions.Expression in cui viene convertita l'espressione lambda.

## <a name="variable-scope-in-lambda-expressions"></a>Ambito delle variabili nelle espressioni lambda ##

Le espressioni lambda possono fare riferimento alle *variabili esterne* (vedere [Metodi anonimi](programming-guide/statements-expressions-operators/anonymous-methods.md)) presenti nell'ambito del metodo che definisce la funzione lambda oppure nell'ambito del tipo che contiene l'espressione lambda. Le variabili acquisite in questo modo vengono archiviate per poter essere utilizzate nell'espressione lambda anche se le variabili diventano esterne all'ambito e vengono sottoposte a Garbage Collection. Una variabile esterna deve essere assegnata prima di poter essere utilizzata in un'espressione lambda. Nell'esempio seguente vengono illustrate queste regole.

[!code-csharp[csSnippets.Lambdas](../../samples/snippets/csharp/concepts/lambda-expressions/scope.cs#1)]

 Le regole seguenti si applicano all'ambito delle variabili nelle espressioni lambda:

- Una variabile acquisita non sarà sottoposta a Garbage Collection finché il delegato a cui fa riferimento non diventa idoneo per il Garbage Collection.

- Le variabili introdotte all'interno di un'espressione lambda non sono visibili nel metodo esterno.

- Un'espressione lambda non può acquisire direttamente un parametro `ref` o `out` da un metodo contenitore.

- Un'istruzione return in un'espressione lambda non causa la restituzione del metodo contenitore.

- Un'espressione lambda non può contenere un'istruzione `goto` , `break` o `continue` , inclusa nella funzione lambda se la destinazione dell'istruzione jump è esterna al blocco. È altresì errato inserire all'esterno del blocco della funzione lambda un'istruzione jump se la destinazione è interna al blocco.

## <a name="see-also"></a>Vedere anche ##

[LINQ (Language Integrated Query)](../standard/using-linq.md)   
[Metodi anonimi](programming-guide/statements-expressions-operators/anonymous-methods.md)   
[Alberi delle espressioni](expression-trees.md)

