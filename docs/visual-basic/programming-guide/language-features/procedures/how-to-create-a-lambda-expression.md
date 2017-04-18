---
title: 'Procedura: creare un&quot;espressione Lambda (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5e105e87b1e63218f2c3c2204350257c139b5837
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-lambda-expression-visual-basic"></a>Procedura: creare un'espressione lambda (Visual Basic)
Oggetto *espressione lambda* è una funzione o subroutine che non dispone di un nome. Un'espressione lambda può essere utilizzata ogni volta che un tipo delegato è valido.  
  
### <a name="to-create-a-single-line-lambda-expression-function"></a>Per creare una funzione di espressione lambda a riga singola  
  
1.  In qualsiasi situazione in cui può essere utilizzato un tipo delegato, digitare la parola chiave `Function`, come nell'esempio seguente:  
  
     `Dim add1 =`   `Function`  
  
2.  Tra parentesi, direttamente dopo `Function`, digitare i parametri della funzione. Si noti che non si specifica un nome dopo `Function`.  
  
     `Dim add1 = Function`   `(num As Integer)`  
  
3.  Dopo l'elenco di parametri, digitare una singola espressione come corpo della funzione. Il valore che restituisce l'espressione è il valore restituito dalla funzione. Non si utilizza un `As` clausola per specificare il tipo restituito.  
  
     [!code-vb[VbVbalrLambdas n.&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_1.vb)]  
  
     L'espressione lambda viene chiamata passando un argomento integer.  
  
     [!code-vb[VbVbalrLambdas n.&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_2.vb)]  
  
4.  In alternativa, lo stesso risultato avviene nell'esempio seguente:  
  
     [!code-vb[VbVbalrLambdas n.&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_3.vb)]  
  
### <a name="to-create-a-single-line-lambda-expression-subroutine"></a>Per creare una subroutine di espressione lambda a riga singola  
  
1.  In qualsiasi situazione in cui può essere utilizzato un tipo delegato, digitare la parola chiave `Sub`, come illustrato nell'esempio seguente.  
  
     `Dim add1 =`   `Sub`  
  
2.  Tra parentesi, direttamente dopo `Sub`, digitare i parametri della subroutine. Si noti che non si specifica un nome dopo `Sub`.  
  
     `Dim add1 = Sub`   `(msg As String)`  
  
3.  Dopo l'elenco di parametri, digitare una singola istruzione come corpo della subroutine.  
  
     [!code-vb[VbVbalrLambdas n.&17;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_4.vb)]  
  
     L'espressione lambda viene chiamata passando un argomento stringa.  
  
     [!code-vb[VbVbalrLambdas&#18;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_5.vb)]  
  
### <a name="to-create-a-multiline-lambda-expression-function"></a>Per creare una funzione di espressione lambda su più righe  
  
1.  In qualsiasi situazione in cui può essere utilizzato un tipo delegato, digitare la parola chiave `Function`, come illustrato nell'esempio seguente.  
  
     `Dim add1 =`   `Function`  
  
2.  Tra parentesi, direttamente dopo `Function`, digitare i parametri della funzione. Si noti che non si specifica un nome dopo `Function`.  
  
     `Dim add1 = Function`   `(index As Integer)`  
  
3.  Premere INVIO. Il `End Function` istruzione viene aggiunto automaticamente.  
  
4.  All'interno del corpo della funzione, aggiungere il codice seguente per creare un'espressione e restituire il valore. Non si utilizza un `As` clausola per specificare il tipo restituito.  
  
     [!code-vb[&#19; VbVbalrLambdas](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_6.vb)]  
  
     L'espressione lambda viene chiamata passando un argomento integer.  
  
     [!code-vb[VbVbalrLambdas&#20;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_7.vb)]  
  
### <a name="to-create-a-multiline-lambda-expression-subroutine"></a>Per creare una subroutine di espressione lambda su più righe  
  
1.  In qualsiasi situazione in cui può essere utilizzato un tipo delegato, digitare la parola chiave `Sub`, come illustrato nell'esempio seguente:  
  
     `Dim add1 =`   `Sub`  
  
2.  Tra parentesi, direttamente dopo `Sub`, digitare i parametri della subroutine. Si noti che non si specifica un nome dopo `Sub`.  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3.  Premere INVIO. Il `End Sub` istruzione viene aggiunto automaticamente.  
  
4.  All'interno del corpo della funzione, aggiungere il seguente codice da eseguire quando viene richiamata la subroutine.  
  
     [!code-vb[VbVbalrLambdas numero&21;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_8.vb)]  
  
     L'espressione lambda viene chiamata passando un argomento stringa.  
  
     [!code-vb[VbVbalrLambdas&#22;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_9.vb)]  
  
## <a name="example"></a>Esempio  
 È un utilizzo comune delle espressioni lambda per definire una funzione che può essere passata come argomento per un parametro il cui tipo è `Delegate`. Nell'esempio seguente, il <xref:System.Diagnostics.Process.GetProcesses%2A>metodo restituisce una matrice di processi in esecuzione nel computer locale.</xref:System.Diagnostics.Process.GetProcesses%2A> Il <xref:System.Linq.Enumerable.Where%2A>metodo la <xref:System.Linq.Enumerable>classe richiede un `Boolean` come argomento del delegato.</xref:System.Linq.Enumerable> </xref:System.Linq.Enumerable.Where%2A> L'espressione lambda nell'esempio viene utilizzata a tale scopo. Restituisce `True` per ogni processo che ha un solo thread e quelli selezionati in `filteredList`.  
  
 [!code-vb[VbVbalrLambdas&#10;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_10.vb)]  
  
 Nell'esempio precedente è equivalente al codice seguente, scritto in [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] sintassi:  
  
 [!code-vb[VbVbalrLambdas&#11;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_11.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 [Espressioni lambda](./lambda-expressions.md)   
 [Istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Procedura: passare una routine a un'altra routine in Visual Basic](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Delegate (istruzione)](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
