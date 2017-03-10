---
title: "- Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Negate"
  - "vb.-"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "- operator [Visual Basic]"
  - "operators [Visual Basic], subtraction"
  - "operators [Visual Basic], difference"
  - "negation operator"
  - "operators [Visual Basic], arithmetic"
  - "subtraction operator, syntax"
  - "arithmetic operators, subtraction"
  - "difference operator"
  - "math operators"
  - "operators [Visual Basic], negation"
  - "minus operator [Visual Basic]"
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# - Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Restituisce la differenza tra due espressioni numeriche o il valore negativo di un'espressione numerica.  
  
## Sintassi  
  
```  
  
      expression1 – expression2  
- or -  
– expression1  
```  
  
## Parti  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
 `expression2`  
 Obbligatoria, a meno che con l'operatore `–` non venga calcolato un valore negativo.  Qualsiasi espressione numerica.  
  
## Risultato  
 Il risultato è la differenza tra `expression1` ed `expression2` o il valore negato di `expression1`.  
  
 Il tipo di dati del risultato è un tipo numerico appropriato in base ai tipi di dati di `expression1` ed `expression2`.  Per informazioni, vedere le tabelle "Operazioni aritmetiche su valori integer" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## Tipi supportati  
 Tutti i tipi numerici.  Sono inclusi i tipi non firmati e a virgola mobile e `Decimal`.  
  
## Note  
 Nel primo utilizzo illustrato nella sintassi precedente, l'operatore `–` è l'operatore *binario* di sottrazione aritmetica che consente di calcolare la differenza tra due espressioni numeriche.  
  
 Nel secondo utilizzo illustrato nella sintassi precedente, l'operatore `–` è l'operatore di negazione *unario* che consente di calcolare il valore negativo di un'espressione.  In questo caso, la negazione consiste nell'inversione del segno di `expression1`, in modo che il risultato sia positivo se `expression1` è negativa.  
  
 Se una delle espressioni restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), l'operatore `–` la considererà uguale a zero.  
  
> [!NOTE]
>  L'operatore `–` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `–` viene utilizzato per calcolare e restituire la differenza tra due numeri e quindi per negare un numero.  
  
 [!code-vb[VbVbalrOperators#10](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/subtraction-operator_1.vb)]  
  
 Dopo l'esecuzione di tali istruzioni, `binaryResult` conterrà il valore 124,45 e `unaryResult` –334,90.  
  
## Vedere anche  
 [\-\= Operator](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)