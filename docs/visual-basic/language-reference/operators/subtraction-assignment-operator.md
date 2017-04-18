---
title: -= Operatore (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.-=
dev_langs:
- VB
helpviewer_keywords:
- -= operator [Visual Basic]
- assignment statements, compound
- statements [Visual Basic], compound assignment
- operator -=
- compound assignment statements
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
caps.latest.revision: 19
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
ms.openlocfilehash: f640bd288c677954bae189c2e86ef096e7a73a2b
ms.lasthandoff: 03/13/2017

---
# <a name="--operator-visual-basic"></a>Operatore -= (Visual Basic)
Sottrae il valore di un'espressione dal valore di una variabile o proprietà e assegna il risultato alla variabile o proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
variableorproperty -= expression  
```  
  
## <a name="parts"></a>Parti  
 `variableorproperty`  
 Obbligatorio. Qualsiasi variabile numerica o proprietà.  
  
 `expression`  
 Obbligatorio. Qualsiasi espressione numerica.  
  
## <a name="remarks"></a>Note  
 L'elemento sul lato sinistro del `-=` operatore può essere una semplice variabile scalare, una proprietà o un elemento della matrice. La variabile o proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 Il `-=` operatore sottrae prima il valore dell'espressione (sul lato destro dell'operatore) dal valore della variabile o proprietà (sul lato sinistro dell'operatore). L'operatore quindi assegna il risultato dell'operazione per la variabile o proprietà.  
  
## <a name="overloading"></a>Overload  
 Il [-operatore (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-operator.md) può essere *overload*, il che significa che una classe o struttura possibile ridefinire il comportamento quando un operando specifica il tipo di classe o struttura. L'overload di `-` operatore influisce sul comportamento di `-=` operatore. Se il codice utilizza `-=` in una classe o struttura che esegue l'overload `-`, assicurarsi di comprendere il comportamento ridefinito. Per ulteriori informazioni, vedere [routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `-=` operatore per sottrarre uno `Integer` da un'altra variabile e assegnare il risultato alla variabile di quest'ultimo.  
  
 [!code-vb[VbVbalrOperators&#11;](codesnippet/VisualBasic/subtraction-assignment-operator_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [-Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-operator.md)   
 [Operatori di assegnazione](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Aritmetici (operatori)](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Precedenza tra operatori in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Istruzioni](../../../visual-basic/programming-guide/language-features/statements.md)

