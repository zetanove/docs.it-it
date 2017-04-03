---
title: 'Procedura: Eseguire alberi delle espressioni (C#) | Documentazione Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: get-started-article
dev_langs:
- CSharp
ms.assetid: b8c40db5-2464-4bb9-9001-8c2bc7f006c5
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 0e7d061644aa6c0f36b7a193ded5485000ad0309
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-execute-expression-trees-c"></a>Procedura: Eseguire alberi delle espressioni (C#)
In questo argomento viene illustrato come eseguire un albero delle espressioni. L'esecuzione di un albero delle espressioni può restituire un valore o può eseguire solo un'azione, ad esempio la chiamata a un metodo.  
  
 Possono essere eseguite solo gli alberi delle espressioni che rappresentano espressioni lambda. Gli alberi delle espressioni che rappresentano espressioni lambda sono di tipo <xref:System.Linq.Expressions.LambdaExpression> o <xref:System.Linq.Expressions.Expression%601>. Per eseguire questi alberi delle espressioni, chiamare il metodo <xref:System.Linq.Expressions.LambdaExpression.Compile%2A> per creare un delegato eseguibile e quindi richiamare il delegato.  
  
> [!NOTE]
>  Se il tipo di delegato non è noto, ovvero l'espressione lambda è di tipo <xref:System.Linq.Expressions.LambdaExpression> e non <xref:System.Linq.Expressions.Expression%601>, è necessario chiamare il metodo <xref:System.Delegate.DynamicInvoke%2A> sul delegato anziché chiamarlo direttamente.  
  
 Se un albero delle espressioni non rappresenta un'espressione lambda, è possibile creare una nuova espressione lambda che usa l'albero delle espressioni originale come corpo, chiamando il metodo <xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29>. Sarà quindi possibile eseguire l'espressione lambda come descritto precedentemente in questa sezione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene descritto come eseguire un albero delle espressioni che rappresenta l'elevamento di un numero a una potenza mediante la creazione e l'esecuzione di un'espressione lambda. Verrà visualizzato il risultato che rappresenta il numero elevato a potenza.  
  
```csharp  
// The expression tree to execute.  
BinaryExpression be = Expression.Power(Expression.Constant(2D), Expression.Constant(3D));  
  
// Create a lambda expression.  
Expression<Func<double>> le = Expression.Lambda<Func<double>>(be);  
  
// Compile the lambda expression.  
Func<double> compiledExpression = le.Compile();  
  
// Execute the lambda expression.  
double result = compiledExpression();  
  
// Display the result.  
Console.WriteLine(result);  
  
// This code produces the following output:  
// 8  
```  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Aggiungere un riferimento di progetto a System.Core.dll, se non è già presente.  
  
-   Includere lo spazio dei nomi System.Linq.Expressions.  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)   
 [Procedura: Modificare alberi delle espressioni (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)
