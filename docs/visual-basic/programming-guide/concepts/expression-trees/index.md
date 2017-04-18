---
title: Alberi delle espressioni (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 8bbbb02d-7ffc-476b-8c25-118d82bf5d46
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: 7e33ed084c560470a486ebbb25035a59ddc18565
ms.openlocfilehash: 5f22d535ea6fb55ccadba4476e2e61f32b7a64f2
ms.lasthandoff: 03/31/2017

---
# <a name="expression-trees-visual-basic"></a>Alberi delle espressioni (Visual Basic)
Gli alberi delle espressioni rappresentano codice in una struttura dei dati simile a un albero, dove ogni nodo è un'espressione, ad esempio una chiamata al metodo o un'operazione binaria come `x < y`.  
  
 È possibile compilare ed eseguire codice rappresentato dagli alberi delle espressioni. In questo modo è possibile modificare dinamicamente codice eseguibile, eseguire query LINQ in vari database e creare query dinamiche. Per altre informazioni sugli alberi delle espressioni in LINQ, vedere [How to: Use Expression Trees to Build Dynamic Queries (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md) (Procedura: Usare alberi delle espressioni per creare query dinamiche (Visual Basic)).  
  
 Gli alberi delle espressioni sono anche usati in Dynamic Language Runtime (DLR) per fornire interoperabilità tra linguaggi dinamici e .NET Framework e per consentire ai writer dei compilatori di creare alberi delle espressioni invece di codice MSIL (Microsoft Intermediate Language). Per altre informazioni su DLR, vedere [Dynamic Language Runtime Overview](https://msdn.microsoft.com/library/dd233052) (Panoramica su Dynamic Language Runtime).  
  
 È possibile creare un albero delle espressioni tramite il compilatore di C# o di Visual Basic in base a un'espressione lambda anonima oppure manualmente tramite lo spazio dei nomi <xref:System.Linq.Expressions>.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Creazione di alberi delle espressioni da espressioni lambda  
 Quando un'espressione lambda viene assegnata a una variabile di tipo <xref:System.Linq.Expressions.Expression%601>, il compilatore genera codice per compilare un albero delle espressioni che rappresenti l'espressione lambda.  
  
 Il compilatore di Visual Basic può generare alberi delle espressioni solo da espressioni lambda, o lambda su una sola riga. Non possono analizzare espressioni lambda dell'istruzione (o le espressioni lambda a più righe). Per altre informazioni sulle espressioni lambda in Visual Basic, vedere [Espressioni lambda](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 Gli esempi di codice seguenti illustrano in che modo il compilatore di Visual Basic crea un albero delle espressioni che rappresenta l'espressione lambda `Function(num) num < 5`.  
  
```vb  
Dim lambda As Expression(Of Func(Of Integer, Boolean)) =  
    Function(num) num < 5  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>Creazione di alberi delle espressioni tramite l'API  
 Per creare alberi delle espressioni tramite l'API, usare la classe <xref:System.Linq.Expressions.Expression>. Questa classe contiene metodi factory statici che creano nodi degli alberi delle espressioni di tipi specifici, come ad esempio <xref:System.Linq.Expressions.ParameterExpression>, che rappresenta una variabile o un parametro, o <xref:System.Linq.Expressions.MethodCallExpression>, che rappresenta una chiamata al metodo. Anche <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression>, e gli altri tipi specifici per espressione sono definiti nello spazio dei nomi <xref:System.Linq.Expressions>. Questi tipi derivano dal tipo astratto <xref:System.Linq.Expressions.Expression>.  
  
 L'esempio di codice seguente illustra come creare un albero delle espressioni che rappresenti l'espressione lambda `Function(num) num < 5` usando l'API.  
  
```vb  
' Import the following namespace to your project: System.Linq.Expressions  
  
' Manually build the expression tree for the lambda expression num => num < 5.  
Dim numParam As ParameterExpression = Expression.Parameter(GetType(Integer), "num")  
Dim five As ConstantExpression = Expression.Constant(5, GetType(Integer))  
Dim numLessThanFive As BinaryExpression = Expression.LessThan(numParam, five)  
Dim lambda1 As Expression(Of Func(Of Integer, Boolean)) =  
  Expression.Lambda(Of Func(Of Integer, Boolean))(  
        numLessThanFive,  
        New ParameterExpression() {numParam})  
```  
  
 In .NET Framework 4 o nelle versioni successive l'API degli alberi delle espressioni supporta anche assegnazioni ed espressioni del flusso di controllo quali cicli, blocchi condizionali e blocchi `try-catch`. Tramite l'API è possibile creare alberi delle espressioni più complessi rispetto a quelli che è possibile creare da espressioni lambda tramite il compilatore di Visual Basic. L'esempio seguente illustra come creare un albero delle espressioni che calcola il fattoriale di un numero.  
  
```vb  
' Creating a parameter expression.  
Dim value As ParameterExpression =  
    Expression.Parameter(GetType(Integer), "value")  
  
' Creating an expression to hold a local variable.   
Dim result As ParameterExpression =  
    Expression.Parameter(GetType(Integer), "result")  
  
' Creating a label to jump to from a loop.  
Dim label As LabelTarget = Expression.Label(GetType(Integer))  
  
' Creating a method body.  
Dim block As BlockExpression = Expression.Block(  
    New ParameterExpression() {result},  
    Expression.Assign(result, Expression.Constant(1)),  
    Expression.Loop(  
        Expression.IfThenElse(  
            Expression.GreaterThan(value, Expression.Constant(1)),  
            Expression.MultiplyAssign(result,  
                Expression.PostDecrementAssign(value)),  
            Expression.Break(label, result)  
        ),  
        label  
    )  
)  
  
' Compile an expression tree and return a delegate.  
Dim factorial As Integer =  
    Expression.Lambda(Of Func(Of Integer, Integer))(block, value).Compile()(5)  
  
Console.WriteLine(factorial)  
' Prints 120.  
```

Per altre informazioni, vedere l'articolo [Generating Dynamic Methods with Expression Trees in Visual Studio 2010](http://go.microsoft.com/fwlink/p/?LinkId=169513) (Generazione di metodi dinamici con alberi delle espressioni in Visual Studio 2010), valido anche per le versioni successive di Visual Studio.
  
## <a name="parsing-expression-trees"></a>Analisi degli alberi delle espressioni  
 L'esempio di codice seguente illustra come scomporre nei vari componenti l'albero delle espressioni che rappresenta l'espressione lambda `Function(num) num < 5`.  
  
```vb  
' Import the following namespace to your project: System.Linq.Expressions  
  
' Create an expression tree.  
Dim exprTree As Expression(Of Func(Of Integer, Boolean)) = Function(num) num < 5  
  
' Decompose the expression tree.  
Dim param As ParameterExpression = exprTree.Parameters(0)  
Dim operation As BinaryExpression = exprTree.Body  
Dim left As ParameterExpression = operation.Left  
Dim right As ConstantExpression = operation.Right  
  
Console.WriteLine(String.Format("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value))  
  
' This code produces the following output:  
'  
' Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>Non modificabilità degli alberi delle espressioni  
 Gli alberi delle espressioni devono essere non modificabili. Ciò significa che per modificare un albero delle espressioni è necessario costruirne uno nuovo copiando quello esistente e sostituendone i nodi. È possibile usare un visitatore dell'albero delle espressioni per attraversare l'albero delle espressioni esistente. Per altre informazioni, vedere [How to: Modify Expression Trees (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md) (Procedura: Modificare alberi delle espressioni (Visual Basic)).  
  
## <a name="compiling-expression-trees"></a>Compilazione degli alberi delle espressioni  
 Il tipo <xref:System.Linq.Expressions.Expression%601> specifica il metodo <xref:System.Linq.Expressions.Expression%601.Compile%2A> che compila il codice rappresentato da un albero dell'espressione in un delegato eseguibile.  
  
 L'esempio di codice seguente illustra come compilare un albero delle espressioni ed eseguire il codice risultante.  
  
```vb  
' Creating an expression tree.  
Dim expr As Expression(Of Func(Of Integer, Boolean)) =  
    Function(num) num < 5  
  
' Compiling the expression tree into a delegate.  
Dim result As Func(Of Integer, Boolean) = expr.Compile()  
  
' Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4))  
  
' Prints True.  
  
' You can also use simplified syntax  
' to compile and run an expression tree.  
' The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4))  
  
' Also prints True.  
```  
  
 Per altre informazioni, vedere [How to: Execute Expression Trees (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md) (Procedura: Eseguire alberi delle espressioni (Visual Basic)).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Expressions>   
 [How to: Execute Expression Trees (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)  (Procedura: Eseguire alberi delle espressioni (Visual Basic))  
 [How to: Modify Expression Trees (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)  (Procedura: Modificare alberi delle espressioni (Visual Basic)).  
 [Espressioni lambda](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Dynamic Language Runtime Overview](https://msdn.microsoft.com/library/dd233052)  (Panoramica su Dynamic Language Runtime)  
 [Programming Concepts (Visual Basic)](../../../../visual-basic/programming-guide/concepts/index.md) (Concetti di programmazione (Visual Basic))
