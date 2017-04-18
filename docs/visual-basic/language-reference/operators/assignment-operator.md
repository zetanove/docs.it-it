---
title: = Operatore (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Assign
- vb.=
dev_langs:
- VB
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
caps.latest.revision: 16
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
ms.openlocfilehash: 47b69a908f12ec36daf2848da6ee4b04895fd3a4
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>Operatore = (Visual Basic)
Assegna un valore a una variabile o proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
variableorproperty = value  
```  
  
## <a name="parts"></a>Parti  
 `variableorproperty`  
 Qualsiasi variabile modificabile o qualsiasi proprietà.  
  
 `value`  
 Qualsiasi valore letterale, costante o espressione.  
  
## <a name="remarks"></a>Note  
 L'elemento a sinistra del segno di uguale (`=`) può essere una semplice variabile scalare, una proprietà o un elemento della matrice. La variabile o proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md). Il `=` operatore assegna il valore alla sua destra alla variabile o proprietà alla sua sinistra.  
  
> [!NOTE]
>  Il `=` operatore viene utilizzato anche come un operatore di confronto. Per informazioni dettagliate, vedere [operatori di confronto](../../../visual-basic/language-reference/operators/comparison-operators.md).  
  
## <a name="overloading"></a>Overload  
 Il `=` operatore può essere sottoposto a overload solo come operatore di confronto relazionale, non come un operatore di assegnazione. Per ulteriori informazioni, vedere [routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato l'operatore di assegnazione. Il valore a destra viene assegnato alla variabile a sinistra.  
  
 [!code-vb[9 VbVbalrOperators](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/assignment-operator_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [/ = (Operatore)](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [* = (Operatore)](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [+ = Operatore](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [-= Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [Operatore / = (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\= Operatore](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [^ = (Operatore)](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [Istruzioni](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Operatori di confronto](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Sola lettura](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [Inferenza del tipo di variabile locale](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)

