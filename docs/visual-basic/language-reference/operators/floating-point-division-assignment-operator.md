---
title: Operatore / = (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb./=
dev_langs:
- VB
helpviewer_keywords:
- assignment statements, compound
- statements [Visual Basic], compound assignment
- /= operator [Visual Basic]
- operator /=
- compound assignment statements
ms.assetid: a1e22d0e-8380-4761-9da1-84fb51c34821
caps.latest.revision: 23
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ab0a007f039d3dbda989bb605cb80fcf5fc7460a
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>Operatore /= (Visual Basic)
Divide il valore di una variabile o proprietà per il valore di un'espressione e assegna il risultato a virgola mobile e la variabile o proprietà.  
  
## <a name="syntax"></a>Sintassi  
  
```  
variableorproperty /= expression  
```  
  
## <a name="parts"></a>Parti  
 `variableorproperty`  
 Obbligatorio. Qualsiasi variabile numerica o proprietà.  
  
 `expression`  
 Obbligatorio. Qualsiasi espressione numerica.  
  
## <a name="remarks"></a>Note  
 L'elemento sul lato sinistro del `/=` operatore può essere una semplice variabile scalare, una proprietà o un elemento della matrice. La variabile o proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 Il `/=` operatore divide innanzitutto il valore della variabile o proprietà (sul lato sinistro dell'operatore) per il valore dell'espressione (sul lato destro dell'operatore). L'operatore quindi assegna il risultato dell'operazione a virgola mobile per la variabile o proprietà.  
  
 Questa istruzione assegna un `Double` valore alla variabile o proprietà a sinistra. If `Option Strict` is `On`, `variableorproperty` must be a `Double`. Se `Option Strict` è `Off`, Visual Basic esegue una conversione implicita e assegna il valore risultante a `variableorproperty`, con un messaggio di errore in fase di esecuzione. Per ulteriori informazioni, vedere [conversioni di ampliamento e restrizione](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) e [istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
## <a name="overloading"></a>Overload  
 Il [/ (operatore) (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) può essere *overload*, il che significa che una classe o struttura possibile ridefinire il comportamento quando un operando specifica il tipo di classe o struttura. L'overload di `/` operatore influisce sul comportamento di `/=` operatore. Se il codice utilizza `/=` in una classe o struttura che esegue l'overload `/`, assicurarsi di comprendere il comportamento ridefinito. Per ulteriori informazioni, vedere [routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `/=` operatore per dividere una `Integer` variabile da un secondo e di assegnare il quoziente alla prima variabile.  
  
 [!code-vb[VbVbalrOperators n.&17;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/floating-point-division-assignment-operator_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [/ Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)   
 [\\= Operatore](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [Operatori di assegnazione](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Aritmetici (operatori)](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Precedenza tra operatori in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Istruzioni](../../../visual-basic/programming-guide/language-features/statements.md)

