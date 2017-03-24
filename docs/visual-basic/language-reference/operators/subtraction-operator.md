---
title: '- Operatore (Visual Basic) | Documenti di Microsoft'
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Negate
- vb.-
dev_langs:
- VB
helpviewer_keywords:
- '- operator [Visual Basic]'
- operators [Visual Basic], subtraction
- operators [Visual Basic], difference
- negation operator
- operators [Visual Basic], arithmetic
- subtraction operator, syntax
- arithmetic operators, subtraction
- difference operator
- math operators
- operators [Visual Basic], negation
- minus operator [Visual Basic]
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
caps.latest.revision: 14
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
ms.openlocfilehash: 7f45094da7bc61687d9c767d25858aa214bf1978
ms.lasthandoff: 03/13/2017

---
# <a name="--operator-visual-basic"></a>Operatore - (Visual Basic)
Restituisce la differenza tra due espressioni numeriche o il valore negativo di un'espressione numerica.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      expression1 – expression2  
- or -  
– expression1  
```  
  
## <a name="parts"></a>Parti  
 `expression1`  
 Obbligatorio. Qualsiasi espressione numerica.  
  
 `expression2`  
 Obbligatorio solo se il `–` operatore viene calcolato un valore negativo. Qualsiasi espressione numerica.  
  
## <a name="result"></a>Risultato  
 Il risultato è la differenza tra `expression1` e `expression2`, o il valore negato di `expression1`.  
  
 Il tipo di dati del risultato è un tipo numerico appropriato per i tipi di dati di `expression1` e `expression2`. Vedere le tabelle "Calcoli su numeri Integer" in [dati tipi di operatore restituisce un risultato](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## <a name="supported-types"></a>Tipi supportati  
 Tutti i tipi numerici. Sono inclusi i tipi a virgola mobile e senza segno e `Decimal`.  
  
## <a name="remarks"></a>Note  
 Nel primo utilizzo illustrato nella sintassi precedente, il `–` operatore è il *binario* operatore di sottrazione aritmetica per comprendere la differenza tra due espressioni numeriche.  
  
 Nel secondo utilizzo illustrato nella sintassi precedente, il `–` operatore è il *unario* operatore di negazione per il valore negativo di un'espressione. In questo senso, la negazione consiste nell'inversione del segno di `expression1` in modo che il risultato è positivo se `expression1` è negativo.  
  
 Se un'espressione restituisce [nulla](../../../visual-basic/language-reference/nothing.md), `–` operatore considera come zero.  
  
> [!NOTE]
>  Il `–` operatore può essere *overload*, il che significa che una classe o struttura possibile ridefinire il comportamento quando un operando specifica il tipo di classe o struttura. Se il codice utilizza l'operatore su una classe o una struttura, assicurarsi comprendere il comportamento ridefinito. Per ulteriori informazioni, vedere [routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata la `–` operatore per calcolare e restituire la differenza tra due numeri, quindi per negare un numero.  
  
 [!code-vb[VbVbalrOperators&#10;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/subtraction-operator_1.vb)]  
  
 Dopo l'esecuzione di queste istruzioni, `binaryResult` contiene il valore 124,45 e `unaryResult` 334,90.  
  
## <a name="see-also"></a>Vedere anche  
 [-= Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)
 [operatori aritmetici](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Precedenza tra operatori in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operatori aritmetici in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)

