---
title: 'Procedura: modificare strutture ad albero di espressione (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: d1309fff-28bd-4d8e-a2cf-75725999e8f2
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
ms.openlocfilehash: fb4e818eed7d6547e091c914d40b3ce87af59512
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-modify-expression-trees-visual-basic"></a>Procedura: modificare strutture ad albero di espressione (Visual Basic)
In questo argomento viene illustrato come modificare un albero delle espressioni. Gli alberi delle espressioni non sono modificabili, il che significa che non può essere modificati direttamente. Per modificare un albero delle espressioni, è necessario creare una copia di una struttura esistente e quando si crea la copia, apportare le modifiche necessarie. È possibile utilizzare la <xref:System.Linq.Expressions.ExpressionVisitor>classe per attraversare una struttura esistente e copiare ogni nodo visitato.</xref:System.Linq.Expressions.ExpressionVisitor>  
  
### <a name="to-modify-an-expression-tree"></a>Per modificare un albero delle espressioni  
  
1.  Creare un nuovo **applicazione Console** progetto.  
  
2.  Aggiungere un `Imports` istruzione per il file per il `System.Linq.Expressions` dello spazio dei nomi.  
  
3.  Aggiungere la `AndAlsoModifier` classe al progetto.  
  
    ```vb  
    Public Class AndAlsoModifier  
        Inherits ExpressionVisitor  
  
        Public Function Modify(ByVal expr As Expression) As Expression  
            Return Visit(expr)  
        End Function  
  
        Protected Overrides Function VisitBinary(ByVal b As BinaryExpression) As Expression  
            If b.NodeType = ExpressionType.AndAlso Then  
                Dim left = Me.Visit(b.Left)  
                Dim right = Me.Visit(b.Right)  
  
                ' Make this binary expression an OrElse operation instead   
                ' of an AndAlso operation.  
                Return Expression.MakeBinary(ExpressionType.OrElse, left, right, _  
                                             b.IsLiftedToNull, b.Method)  
            End If  
  
            Return MyBase.VisitBinary(b)  
        End Function  
    End Class  
    ```  
  
     Questa classe eredita la <xref:System.Linq.Expressions.ExpressionVisitor>classe ed è specializzata per modificare le espressioni che rappresentano condizionale `AND` operations.</xref:System.Linq.Expressions.ExpressionVisitor> Queste operazioni vengono modificate da un'istruzione condizionale `AND` a un'istruzione condizionale `OR`. A tale scopo, la classe esegue l'override di <xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A>metodo del tipo di base, poiché condizionale `AND` le espressioni sono rappresentate come espressioni binarie.</xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> Nel `VisitBinary` (metodo), se l'espressione che viene passato al metodo rappresenta un'istruzione condizionale `AND` operazione, il codice costruisce una nuova espressione che contiene il condizionale `OR` operatore anziché condizionale `AND` operatore. Se l'espressione che viene passato a `VisitBinary` non rappresenta un'istruzione condizionale `AND` operazione, il metodo rinvia all'implementazione della classe base. I metodi della classe base costruiscono nodi sono come le strutture ad albero dell'espressione viene passati, ma i nodi dispongono delle strutture sub sostituite con le strutture ad albero dell'espressione che sono generati in modo ricorsivo dal visitatore.  
  
4.  Aggiungere un `Imports` istruzione per il file per il `System.Linq.Expressions` dello spazio dei nomi.  
  
5.  Aggiungere codice per il `Main` metodo nel file Module1. vb per creare una struttura ad albero dell'espressione e passarla al metodo a cui verrà modificato in modo.  
  
    ```vb  
    Dim expr As Expression(Of Func(Of String, Boolean)) = _  
        Function(name) name.Length > 10 AndAlso name.StartsWith("G")  
  
    Console.WriteLine(expr)  
  
    Dim modifier As New AndAlsoModifier()  
    Dim modifiedExpr = modifier.Modify(CType(expr, Expression))  
  
    Console.WriteLine(modifiedExpr)  
  
    ' This code produces the following output:  
    ' name => ((name.Length > 10) && name.StartsWith("G"))  
    ' name => ((name.Length > 10) || name.StartsWith("G"))  
    ```  
  
     Il codice crea un'espressione che contiene un'istruzione condizionale `AND` operazione. Viene quindi creata un'istanza del `AndAlsoModifier` classe e viene passata l'espressione per il `Modify` metodo di questa classe. Per mostrare le modifiche restituite originale e le strutture ad albero dell'espressione modificata.  
  
6.  Compilare l'applicazione ed eseguirla.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: eseguire alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [Alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)
