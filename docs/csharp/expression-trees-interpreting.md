---
title: Interpretazione di espressioni
description: Interpretazione di espressioni
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: adf73dde-1e52-4df3-9929-2e0670e28e16
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 07352a2807c08ad19b8d5a47c5a42a0e1c455ab6
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---

# <a name="interpreting-expressions"></a>Interpretazione di espressioni

[Precedente -- Esecuzione di espressioni](expression-trees-execution.md)

Scriviamo ora del codice per esaminare la struttura di un *albero delle espressioni*. Ogni nodo in un albero delle espressioni sarà un oggetto di una classe derivata da `Expression`.

Tale progettazione rende la visita di tutti i nodi in un albero delle espressioni un'operazione ricorsiva relativamente semplice. Come strategia generale, iniziare in corrispondenza del nodo radice e determinare di quale tipo di nodo si tratti.

Se il tipo di nodo contiene elementi figlio, visitare in modo ricorsivo gli elementi figlio. In ogni nodo figlio, ripetere il processo usato in corrispondenza del nodo radice: determinare il tipo e, se il tipo contiene elementi figlio, visitare ognuno di essi.

## <a name="examining-an-expression-with-no-children"></a>Analisi di un'espressione senza elementi figlio
Iniziare visitando ogni nodo in un albero delle espressioni molto semplice.
Ecco il codice che crea un'espressione costante e ne esamina quindi le proprietà:

```csharp
var constant = Expression.Constant(24, typeof(int));

Console.WriteLine($"This is a/an {constant.NodeType} expression type");
Console.WriteLine($"The type of the constant value is {constant.Type}");
Console.WriteLine($"The value of the constant value is {constant.Value}");
```

Questo comporterà il risultato seguente:

```
This is an Constant expression type
The type of the constant value is System.Int32
The value of the constant value is 24
```

A questo punto, iniziare a scrivere il codice che esamina l'espressione e scrivere alcune proprietà importanti su di esso. Di seguito è riportato il codice:

## <a name="examining-a-simple-addition-expression"></a>Analisi di un'espressione di addizione semplice

Iniziamo con l'esempio di addizione presentato nella parte introduttiva di questa sezione.

```csharp
Expression<Func<int>> sum = () => 1 + 2;
```

> Non si usa `var` per dichiarare questo albero delle espressioni e ciò non è possibile perché il lato destro dell'assegnazione è tipizzato in modo implicito. Per comprendere meglio questo meccanismo, leggere [qui](implicitly-typed-lambda-expressions.md).

Il nodo radice è una `LambdaExpression`. Per ottenere la parte di codice di interesse a destra dell'operatore `=>`, è necessario trovare uno degli elementi figlio della `LambdaExpression`. È possibile farlo con tutte le espressioni in questa sezione. Il nodo padre consente di trovare il tipo restituito della `LambdaExpression`.

Per esaminare ogni nodo in questa espressione, è necessario visitare in modo ricorsivo un certo numero di nodi. Ecco una semplice prima implementazione:

```csharp
Expression<Func<int, int, int>> addition = (a, b) => a + b;

Console.WriteLine($"This expression is a {addition.NodeType} expression type");
Console.WriteLine($"The name of the lambda is {((addition.Name == null) ? "<null>" : addition.Name)}");
Console.WriteLine($"The return type is {addition.ReturnType.ToString()}");
Console.WriteLine($"The expression has {addition.Parameters.Count} arguments. They are:");
foreach(var argumentExpression in addition.Parameters)
{
    Console.WriteLine($"\tParameter Type: {argumentExpression.Type.ToString()}, Name: {argumentExpression.Name}");
}

var additionBody = (BinaryExpression)addition.Body;
Console.WriteLine($"The body is a {additionBody.NodeType} expression");
Console.WriteLine($"The left side is a {additionBody.Left.NodeType} expression");
var left = (ParameterExpression)additionBody.Left;
Console.WriteLine($"\tParameter Type: {left.Type.ToString()}, Name: {left.Name}");
Console.WriteLine($"The right side is a {additionBody.Right.NodeType} expression");
var right= (ParameterExpression)additionBody.Right;
Console.WriteLine($"\tParameter Type: {right.Type.ToString()}, Name: {right.Name}");
```

Questo esempio dà l'output seguente:

```
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 arguments. They are:
        Parameter Type: System.Int32, Name: a
        Parameter Type: System.Int32, Name: b
The body is a/an Add expression
The left side is a Parameter expression
        Parameter Type: System.Int32, Name: a
The right side is a Parameter expression
        Parameter Type: System.Int32, Name: b
```

Nell'esempio di codice riportato sopra è possibile rilevare numerose ripetizioni.
Procediamo alla pulizia e alla creazione di un visitatore del nodo dell'espressione per un utilizzo più generico. Questo richiederà la scrittura di un algoritmo ricorsivo. Qualsiasi nodo potrebbe essere di un tipo con elementi figlio.
Qualsiasi nodo con elementi figlio richiede la visita di tali elementi figlio e la determinazione del tipo di nodo. Ecco la versione pulita che usa la ricorsione per visitare le operazioni di addizione:

```csharp
// Base Visitor class:
public abstract class Visitor
{
    private readonly Expression node;

    protected Visitor(Expression node)
    {
        this.node = node;
    }

    public abstract void Visit(string prefix);

    public ExpressionType NodeType => this.node.NodeType;
    public static Visitor CreateFromExpression(Expression node)
    {
        switch(node.NodeType)
        {
            case ExpressionType.Constant:
                return new ConstantVisitor((ConstantExpression)node);
            case ExpressionType.Lambda:
                return new LambdaVisitor((LambdaExpression)node);
            case ExpressionType.Parameter:
                return new ParameterVisitor((ParameterExpression)node);
            case ExpressionType.Add:
                return new BinaryVisitor((BinaryExpression)node);
            default:
                Console.Error.WriteLine($"Node not processed yet: {node.NodeType}");
                return default(Visitor);
        }
    }
}

// Lambda Visitor
public class LambdaVisitor : Visitor
{
    private readonly LambdaExpression node;
    public LambdaVisitor(LambdaExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression type");
        Console.WriteLine($"{prefix}The name of the lambda is {((node.Name == null) ? "<null>" : node.Name)}");
        Console.WriteLine($"{prefix}The return type is {node.ReturnType.ToString()}");
        Console.WriteLine($"{prefix}The expression has {node.Parameters.Count} argument(s). They are:");
        // Visit each parameter:
        foreach (var argumentExpression in node.Parameters)
        {
            var argumentVisitor = Visitor.CreateFromExpression(argumentExpression);
            argumentVisitor.Visit(prefix + "\t");
        }
        Console.WriteLine($"{prefix}The expression body is:");
        // Visit the body:
        var bodyVisitor = Visitor.CreateFromExpression(node.Body);
        bodyVisitor.Visit(prefix + "\t");
    }
}

// Binary Expression Visitor:
public class BinaryVisitor : Visitor
{
    private readonly BinaryExpression node;
    public BinaryVisitor(BinaryExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This binary expression is a {NodeType} expression");
        var left = Visitor.CreateFromExpression(node.Left);
        Console.WriteLine($"{prefix}The Left argument is:");
        left.Visit(prefix + "\t");
        var right = Visitor.CreateFromExpression(node.Right);
        Console.WriteLine($"{prefix}The Right argument is:");
        right.Visit(prefix + "\t");
    }
}

// Parameter visitor:
public class ParameterVisitor : Visitor
{
    private readonly ParameterExpression node;
    public ParameterVisitor(ParameterExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}Type: {node.Type.ToString()}, Name: {node.Name}, ByRef: {node.IsByRef}");
    }
}

// Constant visitor:
public class ConstantVisitor : Visitor
{
    private readonly ConstantExpression node;
    public ConstantVisitor(ConstantExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}The type of the constant value is {node.Type}");
        Console.WriteLine($"{prefix}The value of the constant value is {node.Value}");
    }
}
```

Questo algoritmo è la base di un algoritmo che può visitare qualsiasi `LambdaExpression` arbitraria. Vi sono molte mancanze, in particolare perché il codice creato cerca soltanto un esempio molto ridotto dei possibili set di nodi dell'albero delle espressioni che potrebbe rilevare. È tuttavia possibile ricavare una certa quantità di informazioni utili dal risultato prodotto. Il caso predefinito nel metodo `Visitor.CreateFromExpression` visualizza un messaggio nella console di errore quando viene rilevato un nuovo tipo di nodo. In questo modo, si sa di dover aggiungere un nuovo tipo di espressione.

Quando si esegue questo visitatore nell'espressione di addizione precedente, si ottiene l'output seguente:

```
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: b, ByRef: False
```

Ora che è stata creata un'implementazione del visitatore più generale, è possibile visitare ed elaborare più tipi diversi di espressioni.

## <a name="examining-an-addition-expression-with-many-levels"></a>Analisi di un'espressione di addizione con molti livelli

Procediamo con un esempio più complesso, limitando comunque i tipi di nodo alla sola addizione:

```csharp
Expression<Func<int>> sum = () => 1 + 2 + 3 + 4;
```

Prima di procedere all'esecuzione sull'algoritmo visitatore, provare a pensare quale potrebbe essere l'output. Tenere presente che l'operatore `+` è un *operatore binario*: deve avere due figli, che rappresentano gli operandi sinistro e destro. Sono possibili diversi modi per costruire un albero che può essere corretto:

```csharp
Expression<Func<int>> sum1 = () => 1 + (2 + (3 + 4));
Expression<Func<int>> sum2 = () => ((1 + 2) + 3) + 4;

Expression<Func<int>> sum3 = () => (1 + 2) + (3 + 4);
Expression<Func<int>> sum4 = () => 1 + ((2 + 3) + 4);
Expression<Func<int>> sum5 = () => (1 + (2 + 3)) + 4;
```

Si può visualizzare la separazione in due possibili risposte per evidenziare quella più efficace. La prima possibilità rappresenta le espressioni *associative all'operando destro*. La seconda rappresenta le espressioni *associative all'operando sinistro*.
Il vantaggio di entrambi i formati è che il formato si adatta a qualsiasi numero arbitrario di espressioni di addizione. 

Se si esegue questa espressione tramite il visitatore, verrà visualizzato questo output, che verifica che l'espressione di addizione semplice è *associativa all'operando sinistro*. 

Per eseguire questo esempio e visualizzare l'albero delle espressioni completo, è stato necessario apportare una modifica all'albero delle espressioni di origine. Quando l'albero delle espressioni contiene tutte le costanti, l'albero risultante contiene semplicemente il valore costante di `10`. Il compilatore esegue tutta l'addizione e riduce l'espressione alla sua forma più semplice. La semplice aggiunta di una variabile nell'espressione è sufficiente per visualizzare l'albero originale:

```csharp
Expression<Func<int, int>> sum = (a) => 1 + a + 3 + 4;
```

Creare un visitatore per questa somma ed eseguire il visitatore per visualizzare l'output seguente:

```
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This binary expression is a Add expression
                        The Left argument is:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                        The Right argument is:
                                This is an Parameter expression type
                                Type: System.Int32, Name: a, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
        The Right argument is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 4
```

È anche possibile eseguire uno qualsiasi degli altri esempi tramite il codice del visitatore e vedere quali alberi rappresenta. Di seguito è riportato un esempio dell'espressione `sum3` precedente (con un parametro aggiuntivo per impedire che il compilatore elabori la costante):

```csharp
Expression<Func<int, int, int>> sum3 = (a, b) => (1 + a) + (3 + b);
```

Di seguito è riportato l'output dal visitatore:

```
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 1
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: b, ByRef: False
```

Si noti che le parentesi non fanno parte dell'output. Non sono presenti nodi nell'albero delle espressioni che rappresentano le parentesi nell'espressione di input. La struttura dell'albero delle espressioni contiene tutte le informazioni necessarie per comunicare la precedenza.

## <a name="extending-from-this-sample"></a>Estensione da questo esempio

L'esempio riguarda solo gli alberi delle espressioni più elementari. Il codice in questa sezione gestisce solo interi costanti e l'operatore `+` binario. Come esempio finale, aggiorniamo il visitatore per gestire un'espressione più complessa. Facciamolo funzionare in questo modo:

```csharp
Expression<Func<int, int>> factorial = (n) =>
    n == 0 ? 
    1 : 
    Enumerable.Range(1, n).Aggregate((product, factor) => product * factor);
```

Questo codice rappresenta una possibile implementazione per funzione matematica *fattoriale*. Il modo in cui è stato scritto questo codice consente di evidenziare due limitazioni della creazione degli alberi delle espressioni tramite l'assegnazione di espressioni lambda alle espressioni. In primo luogo, non sono consentite espressioni lambda dell'istruzione. Non è quindi possibile usare cicli, blocchi, istruzioni if / else e altre strutture di controllo comuni in C#. Si è limitati all'uso delle espressioni. In secondo luogo, non è possibile chiamare in modo ricorsivo la stessa espressione.
Ciò sarebbe possibile se fosse già un delegato, ma non può essere chiamata nella sua forma di albero delle espressioni. Nella sezione relativa alla [creazione di alberi delle espressioni](expression-trees-building.md) verranno illustrate le tecniche per superare queste limitazioni.


In questa espressione si incontrano i nodi di tutti questi tipi:
1. Uguale (espressione binaria)
2. Per (espressione binaria)
3. Condizionale (l'espressione ? : )
4. Espressione per chiamata al metodo (chiamata `Range()` e `Aggregate()`)

Un modo per modificare l'algoritmo visitatore consiste nel continuare a eseguirlo e scrivere il tipo di nodo ogni volta che si raggiunge la clausola `default`. Dopo alcune iterazioni, si osserverà ognuno dei nodi potenziali. Si dispone quindi di tutto il necessario. Il risultato è simile al seguente:

```csharp
public static Visitor CreateFromExpression(Expression node)
{
    switch(node.NodeType)
    {
        case ExpressionType.Constant:
            return new ConstantVisitor((ConstantExpression)node);
        case ExpressionType.Lambda:
            return new LambdaVisitor((LambdaExpression)node);
        case ExpressionType.Parameter:
            return new ParameterVisitor((ParameterExpression)node);
        case ExpressionType.Add:
        case ExpressionType.Equal:
        case ExpressionType.Multiply:
            return new BinaryVisitor((BinaryExpression)node);
        case ExpressionType.Conditional:
            return new ConditionalVisitor((ConditionalExpression)node);
        case ExpressionType.Call:
            return new MethodCallVisitor((MethodCallExpression)node);
        default:
            Console.Error.WriteLine($"Node not processed yet: {node.NodeType}");
            return default(Visitor);
    }
}
```

Il ConditionalVisitor e il MethodCallVisitor elaborano questi due nodi:

```csharp
public class ConditionalVisitor : Visitor
{
    private readonly ConditionalExpression node;
    public ConditionalVisitor(ConditionalExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        var testVisitor = Visitor.CreateFromExpression(node.Test);
        Console.WriteLine($"{prefix}The Test for this expression is:");
        testVisitor.Visit(prefix + "\t");
        var trueVisitor = Visitor.CreateFromExpression(node.IfTrue);
        Console.WriteLine($"{prefix}The True clause for this expression is:");
        trueVisitor.Visit(prefix + "\t");
        var falseVisitor = Visitor.CreateFromExpression(node.IfFalse);
        Console.WriteLine($"{prefix}The False clause for this expression is:");
        falseVisitor.Visit(prefix + "\t");
    }
}

public class MethodCallVisitor : Visitor
{
    private readonly MethodCallExpression node;
    public MethodCallVisitor(MethodCallExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        if (node.Object == null)
            Console.WriteLine($"{prefix}This is a static method call");
        else
        {
            Console.WriteLine($"{prefix}The receiver (this) is:");
            var receiverVisitor = Visitor.CreateFromExpression(node.Object);
            receiverVisitor.Visit(prefix + "\t");
        }

        var methodInfo = node.Method;
        Console.WriteLine($"{prefix}The method name is {methodInfo.DeclaringType}.{methodInfo.Name}");
        // There is more here, like generic arguments, and so on.
        Console.WriteLine($"{prefix}The Arguments are:");
        foreach(var arg in node.Arguments)
        {
            var argVisitor = Visitor.CreateFromExpression(arg);
            argVisitor.Visit(prefix + "\t");
        }
    }
}
```

L'output per l'albero delle espressioni sarà:

```
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: n, ByRef: False
The expression body is:
        This expression is a Conditional expression
        The Test for this expression is:
                This binary expression is a Equal expression
                The Left argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: n, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 0
        The True clause for this expression is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 1
        The False clause for this expression is:
                This expression is a Call expression
                This is a static method call
                The method name is System.Linq.Enumerable.Aggregate
                The Arguments are:
                        This expression is a Call expression
                        This is a static method call
                        The method name is System.Linq.Enumerable.Range
                        The Arguments are:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                                This is an Parameter expression type
                                Type: System.Int32, Name: n, ByRef: False
                        This expression is a Lambda expression type
                        The name of the lambda is <null>
                        The return type is System.Int32
                        The expression has 2 arguments. They are:
                                This is an Parameter expression type
                                Type: System.Int32, Name: product, ByRef: False
                                This is an Parameter expression type
                                Type: System.Int32, Name: factor, ByRef: False
                        The expression body is:
                                This binary expression is a Multiply expression
                                The Left argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: product, ByRef: False
                                The Right argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: factor, ByRef: False
```

## <a name="extending-the-sample-library"></a>Estensione della libreria degli esempi

Gli esempi in questa sezione illustrano le tecniche principali per visitare ed esaminare i nodi in un albero delle espressioni. Sono state tralasciate molte azioni che potrebbero essere necessarie in modo da concentrarsi sulle attività di base relative alla visita e all'accesso ai nodi in un albero delle espressioni. 

In primo luogo, i visitatori gestiscono solo le costanti che sono valori interi. I valori costanti potrebbero essere di qualsiasi altro tipo numerico e il linguaggio C# supporta le conversioni e le promozioni tra tali tipi. Una versione più affidabile di questo codice rispecchierebbe tutte queste funzionalità.

Anche nell'ultimo esempio viene riconosciuto un sottoinsieme dei possibili tipi di nodo.
È comunque possibile inserire molte espressioni che ne determinerebbero l'esito negativo.
Un'implementazione completa è inclusa nella libreria standard di .NET con il nome [ExpressionVisitor](https://docs.microsoft.com/dotnet/core/api/System.Linq.Expressions.ExpressionVisitor) ed è in grado di gestire tutti i possibili tipi di nodo.

Infine, la libreria usata in questo articolo è stata creata per la formazione e dimostrazione. Non è ottimizzata. È stata scritta per rendere le strutture usate molto chiare e per evidenziare le tecniche applicate per visitare i nodi e analizzarne il contenuto. Un'implementazione di produzione presterebbe maggiore attenzione alle prestazioni di quanto è stato fatto qui.

Anche con queste limitazioni, sarà possibile iniziare a scrivere algoritmi e leggere e comprendere gli alberi delle espressioni.

[Successivo -- Creazione di espressioni](expression-trees-building.md)

