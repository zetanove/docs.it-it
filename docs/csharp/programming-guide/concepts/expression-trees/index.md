---
title: Alberi delle espressioni (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 87195c8936aba485919d6c717fcbfaa1b282bddc
ms.lasthandoff: 03/31/2017

---
# <a name="expression-trees-c"></a>Alberi delle espressioni (C#)
Gli alberi delle espressioni rappresentano codice in una struttura dei dati simile a un albero, dove ogni nodo è un'espressione, ad esempio una chiamata al metodo o un'operazione binaria come `x < y`.  
  
 È possibile compilare ed eseguire codice rappresentato dagli alberi delle espressioni. In questo modo è possibile modificare dinamicamente codice eseguibile, eseguire query LINQ in vari database e creare query dinamiche. Per altre informazioni sugli alberi delle espressioni in LINQ, vedere [How to: Use Expression Trees to Build Dynamic Queries (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md) (Procedura: Usare alberi delle espressioni per creare query dinamiche (C#)).  
  
 Gli alberi delle espressioni sono anche usati in Dynamic Language Runtime (DLR) per fornire interoperabilità tra linguaggi dinamici e .NET Framework e per consentire ai writer dei compilatori di creare alberi delle espressioni invece di codice MSIL (Microsoft Intermediate Language). Per altre informazioni su DLR, vedere [Dynamic Language Runtime Overview](https://msdn.microsoft.com/library/dd233052) (Panoramica su Dynamic Language Runtime).  
  
 È possibile creare un albero delle espressioni tramite il compilatore di C# o di Visual Basic in base a un'espressione lambda anonima oppure manualmente tramite lo spazio dei nomi <xref:System.Linq.Expressions>.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Creazione di alberi delle espressioni da espressioni lambda  
 Quando un'espressione lambda viene assegnata a una variabile di tipo <xref:System.Linq.Expressions.Expression%601>, il compilatore genera codice per compilare un albero delle espressioni che rappresenti l'espressione lambda.  
  
 Il compilatore di C# può generare alberi delle espressioni solo da espressioni lambda, o lambda su una sola riga. Non possono analizzare espressioni lambda dell'istruzione (o le espressioni lambda a più righe). Per altre informazioni sulle espressioni lambda in C#, vedere [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Gli esempi di codice seguenti illustrano in che modo il compilatore di C# crea un albero delle espressioni che rappresenta l'espressione lambda `num => num < 5`.  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>Creazione di alberi delle espressioni tramite l'API  
 Per creare alberi delle espressioni tramite l'API, usare la classe <xref:System.Linq.Expressions.Expression>. Questa classe contiene metodi factory statici che creano nodi degli alberi delle espressioni di tipi specifici, come ad esempio <xref:System.Linq.Expressions.ParameterExpression>, che rappresenta una variabile o un parametro, o <xref:System.Linq.Expressions.MethodCallExpression>, che rappresenta una chiamata al metodo. Anche <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression>, e gli altri tipi specifici per espressione sono definiti nello spazio dei nomi <xref:System.Linq.Expressions>. Questi tipi derivano dal tipo astratto <xref:System.Linq.Expressions.Expression>.  
  
 L'esempio di codice seguente illustra come creare un albero delle espressioni che rappresenti l'espressione lambda `num => num < 5` usando l'API.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for   
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 In .NET Framework 4 o nelle versioni successive l'API degli alberi delle espressioni supporta anche assegnazioni ed espressioni del flusso di controllo quali cicli, blocchi condizionali e blocchi `try-catch`. Tramite l'API è possibile creare alberi delle espressioni più complessi rispetto a quelli che è possibile creare da espressioni lambda con il compilatore di C#. L'esempio seguente illustra come creare un albero delle espressioni che calcola il fattoriale di un numero.  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.   
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

Per altre informazioni, vedere l'articolo [Generating Dynamic Methods with Expression Trees in Visual Studio 2010](http://go.microsoft.com/fwlink/p/?LinkId=169513) (Generazione di metodi dinamici con alberi delle espressioni in Visual Studio 2010), valido anche per le versioni successive di Visual Studio.
  
## <a name="parsing-expression-trees"></a>Analisi degli alberi delle espressioni  
 L'esempio di codice seguente illustra come scomporre nei vari componenti l'albero delle espressioni che rappresenta l'espressione lambda `num => num < 5`.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>Non modificabilità degli alberi delle espressioni  
 Gli alberi delle espressioni devono essere non modificabili. Ciò significa che per modificare un albero delle espressioni è necessario costruirne uno nuovo copiando quello esistente e sostituendone i nodi. È possibile usare un visitatore dell'albero delle espressioni per attraversare l'albero delle espressioni esistente. Per altre informazioni, vedere [How to: Modify Expression Trees (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md) (Procedura: Modificare alberi delle espressioni (C#)).  
  
## <a name="compiling-expression-trees"></a>Compilazione degli alberi delle espressioni  
 Il tipo <xref:System.Linq.Expressions.Expression%601> specifica il metodo <xref:System.Linq.Expressions.Expression%601.Compile%2A> che compila il codice rappresentato da un albero dell'espressione in un delegato eseguibile.  
  
 L'esempio di codice seguente illustra come compilare un albero delle espressioni ed eseguire il codice risultante.  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 Per altre informazioni, vedere [How to: Execute Expression Trees (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md) (Procedura: Eseguire alberi delle espressioni (C#)).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Expressions>   
 [How to: Execute Expression Trees (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)  (Procedura: Eseguire alberi delle espressioni (C#))  
 [How to: Modify Expression Trees (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)  (Procedura: Modificare alberi delle espressioni (C#))  
 [Espressioni lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)   
 [Dynamic Language Runtime Overview](https://msdn.microsoft.com/library/dd233052)  (Panoramica su Dynamic Language Runtime)  
 [Programming Concepts (C#)](../../../../csharp/programming-guide/concepts/index.md) (Concetti di programmazione (C#))
