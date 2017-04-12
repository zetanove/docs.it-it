---
title: 'Procedura: eseguire alberi delle espressioni (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 9dfb5ab3-f48f-417e-975f-f8f6f1cdc18d
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e12c45b417310f097d597561b2652ee793a4b2c0
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-execute-expression-trees-visual-basic"></a>Procedura: eseguire alberi delle espressioni (Visual Basic)
In questo argomento viene illustrato come eseguire una struttura ad albero dell'espressione. L'esecuzione di una struttura ad albero dell'espressione potrebbe restituire un valore, o può eseguire solo un'azione, ad esempio si chiama un metodo.  
  
 Solo gli alberi delle espressioni che rappresentano le espressioni lambda possono essere eseguite. Gli alberi delle espressioni che rappresentano le espressioni lambda sono di tipo <xref:System.Linq.Expressions.LambdaExpression>o <xref:System.Linq.Expressions.Expression%601>.</xref:System.Linq.Expressions.Expression%601> </xref:System.Linq.Expressions.LambdaExpression> Per eseguire tali alberi delle espressioni, chiamare il <xref:System.Linq.Expressions.LambdaExpression.Compile%2A>per creare un delegato eseguibile e quindi richiamare il delegato.</xref:System.Linq.Expressions.LambdaExpression.Compile%2A>  
  
> [!NOTE]
>  Se non è noto il tipo del delegato, ovvero l'espressione lambda è di tipo <xref:System.Linq.Expressions.LambdaExpression>e non <xref:System.Linq.Expressions.Expression%601>, è necessario chiamare il <xref:System.Delegate.DynamicInvoke%2A>metodo sul delegato anziché richiamarlo direttamente.</xref:System.Delegate.DynamicInvoke%2A> </xref:System.Linq.Expressions.Expression%601> </xref:System.Linq.Expressions.LambdaExpression>  
  
 Se una struttura ad albero dell'espressione non rappresenta un'espressione lambda, è possibile creare una nuova espressione lambda che utilizza l'albero delle espressioni originale come corpo, chiamando il <xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29>(metodo).</xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29> Quindi, è possibile eseguire l'espressione lambda come descritto in precedenza in questa sezione.  
  
## <a name="example"></a>Esempio  
 Esempio di codice seguente viene illustrato come eseguire una struttura ad albero dell'espressione che rappresenta l'elevamento di un numero a una potenza creando un'espressione lambda e dell'esecuzione. Il risultato, che rappresenta il numero elevato alla potenza, viene visualizzato.  
  
```vb  
' The expression tree to execute.  
Dim be As BinaryExpression = Expression.Power(Expression.Constant(2.0R), Expression.Constant(3.0R))  
  
' Create a lambda expression.  
Dim le As Expression(Of Func(Of Double)) = Expression.Lambda(Of Func(Of Double))(be)  
  
' Compile the lambda expression.  
Dim compiledExpression As Func(Of Double) = le.Compile()  
  
' Execute the lambda expression.  
Dim result As Double = compiledExpression()  
  
' Display the result.  
MsgBox(result)  
  
' This code produces the following output:  
' 8  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Aggiungere un riferimento a System.Core.dll progetto se non è già fatto riferimento.  
  
-   Includere lo spazio dei nomi System.Linq.Expressions.  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [Procedura: modificare strutture ad albero di espressione (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)
