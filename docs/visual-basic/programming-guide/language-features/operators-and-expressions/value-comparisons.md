---
title: "Value Comparisons (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "variables [Visual Basic], comparing values"
  - "Visual Basic code, operators"
  - "Visual Basic code, expressions"
  - "comparison operators, comparing expressions"
  - "numeric expressions"
  - "operators [Visual Basic], comparison"
  - "expressions [Visual Basic], comparing"
ms.assetid: 60da0c76-9458-4afc-97e9-44a7939c064c
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Value Comparisons (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli operatori di confronto consentono di creare espressioni che confrontano i valori delle variabili numeriche.  Queste espressioni restituiscono un valore di tipo `Boolean` basato sull'esito del confronto, che può essere true o false.  I seguenti sono esempi di questo tipo di espressioni.  
  
 `45 > 26`  
  
 `26 > 45`  
  
 La prima espressione viene valutata `True`, in quanto 45 è maggiore di 26.  Nel secondo esempio viene valutata `False`, in quanto 26 è minore di 45.  
  
 In questo modo è possibile confrontare anche espressioni numeriche.  Le espressioni confrontate possono essere a loro volta espressioni complesse, come nell'esempio seguente:  
  
 `x / 45 * (y +17) >= System.Math.Sqrt(z) / (p - (x * 16))`  
  
 L'espressione complessa precedente comprende valori letterali, variabili e chiamate di funzioni.  Vengono valutate le espressioni su entrambi i lati dell'operatore di confronto, quindi i valori risultanti vengono confrontati utilizzando l'operatore di confronto `>=`.  Se il valore dell'espressione di sinistra è maggiore di o uguale al valore dell'espressione di destra, tutta l'espressione restituisce `True`; in caso contrario restituisce `False`.  
  
 Le espressioni di confronto dei valori normalmente vengono utilizzate nelle costruzioni `If...Then`, come indicato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#84](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_1.vb)]  
  
 Il segno `=` è un operatore di confronto oltre che un operatore di assegnazione.  Se utilizzato come operatore di confronto, esso consente di valutare se il valore di sinistra è uguale al valore di destra, come indicato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#85](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_2.vb)]  
  
 È possibile utilizzare un'espressione di confronto anche in tutti i casi in cui sia richiesto un valore di tipo `Boolean`, come in un'istruzione `If`, `While`, `Loop` o `ElseIf` o durante l'assegnazione o il passaggio di un valore a una variabile `Boolean`.  Nell'esempio seguente, il valore restituito dall'espressione di confronto viene assegnato a una variabile `Boolean`.  
  
 [!code-vb[VbVbalrOperators#86](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/value-comparisons_3.vb)]  
  
## Vedere anche  
 [Boolean Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [Operators and Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [How to: Calculate Numeric Values](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)   
 [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)