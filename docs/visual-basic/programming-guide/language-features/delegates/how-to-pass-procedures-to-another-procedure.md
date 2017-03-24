---
title: 'Procedura: passare una routine a un&quot;altra routine in Visual Basic | Documenti di Microsoft'
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
- AddressOf operator
- delegates [Visual Basic], passing procedures
ms.assetid: 5adbba15-5a1d-413f-ab3e-3ff6cc0a4669
caps.latest.revision: 9
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 9865e2d7d3786d289add3fa63b3db777317facdf
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-pass-procedures-to-another-procedure-in-visual-basic"></a>Procedura: passare una routine a un'altra routine in Visual Basic
In questo esempio viene illustrato come utilizzare i delegati per passare una routine a un'altra routine.  
  
 Un delegato è un tipo che è possibile utilizzare come qualsiasi altro tipo in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Il `AddressOf` operatore restituisce un oggetto delegato quando viene applicato a un nome di procedura.  
  
 L'esempio include una procedura con un parametro del delegato che può accettare un riferimento a un'altra routine, ottenuto con la `AddressOf` operatore.  
  
### <a name="create-the-delegate-and-matching-procedures"></a>Creare il delegato e le procedure corrispondenti  
  
1.  Crea un delegato denominato `MathOperator`.  
  
     [!code-vb[VbVbalrDelegates n.&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_1.vb)]  
  
2.  Creare una routine denominata `AddNumbers` con parametri e valore restituito che corrispondono a quelle di `MathOperator`, in modo che le firme corrispondono.  
  
     [!code-vb[VbVbalrDelegates n.&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_2.vb)]  
  
3.  Creare una routine denominata `SubtractNumbers` con una firma corrispondente `MathOperator`.  
  
     [!code-vb[VbVbalrDelegates n.&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_3.vb)]  
  
4.  Creare una routine denominata `DelegateTest` che accetta un delegato come parametro.  
  
     Questa routine può accettare un riferimento a `AddNumbers` o `SubtractNumbers`, in quanto le relative firme corrispondono il `MathOperator` firma.  
  
     [!code-vb[VbVbalrDelegates n.&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_4.vb)]  
  
5.  Creare una routine denominata `Test` che chiama `DelegateTest` una volta con il delegato per `AddNumbers` come parametro e di nuovo con il delegato per `SubtractNumbers` come parametro.  
  
     [!code-vb[VbVbalrDelegates n.&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-pass-procedures-to-another-procedure_5.vb)]  
  
     Quando `Test` viene chiamato, viene innanzitutto visualizzato il risultato di `AddNumbers` applicata a `5` e `3`, ovvero 8. Quindi il risultato di `SubtractNumbers` su `9` e `3` viene visualizzato, ovvero 6.  
  
## <a name="see-also"></a>Vedere anche  
 [Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [AddressOf (operatore)](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegate (istruzione)](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Procedura: Richiamare un metodo delegato](../../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
