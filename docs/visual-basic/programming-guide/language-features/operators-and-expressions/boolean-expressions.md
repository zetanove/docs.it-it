---
title: "Boolean Expressions (Visual Basic) | Microsoft Docs"
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
  - "short-circuiting"
  - "Boolean expressions"
  - "logical operators, Boolean expressions"
  - "expressions [Visual Basic], Boolean"
  - "expression evaluation, Boolean expressions"
  - "operators [Visual Basic], short-circuiting"
  - "Visual Basic code, operators"
  - "short-circuit evaluation"
  - "logical operators, short-circuiting"
  - "operators [Visual Basic], Boolean"
  - "Visual Basic code, expressions"
ms.assetid: d3d90406-55c8-4404-8143-50fd7f0d0d1a
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Boolean Expressions (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Un'*espressione booleana* è un'espressione che restituisce un valore del [tipo di dati Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md):`True` o `False`.  Le espressioni `Boolean` possono presentarsi in diverse forme.  La più semplice è il confronto diretto del valore di una variabile `Boolean` con un valore letterale `Boolean`, come illustrato nell'esempio riportato di seguito.  
  
 [!code-vb[VbVbalrOperators#87](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_1.vb)]  
  
## Due significati dell'operatore \=  
 Si noti che l'istruzione di assegnazione `newCustomer = True` sembra uguale all'espressione dell'esempio precedente, ma esegue una funzione diversa e viene usata in modo diverso.  Nell'esempio precedente, l'espressione `newCustomer = True` rappresenta un valore booleano e il segno `=` viene interpretato come un operatore di confronto.  In un'istruzione autonoma, il segno `=` viene interpretato come un operatore di assegnazione e assegna il valore di destra alla variabile di sinistra.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#88](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_2.vb)]  
  
 Per ulteriori informazioni, vedere [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md) e [Statements](../../../../visual-basic/language-reference/statements/index.md).  
  
## Operatori di confronto  
 Gli operatori di confronto come `=`, `<`, `>`, `<>`, `<=` e `>=` producono espressioni booleane tramite il confronto dell'espressione a sinistra dell'operatore con l'espressione a destra dell'operatore e valutando il risultato come `True` o `False`.  Questa condizione è illustrata nell'esempio che segue.  
  
 `42 < 81`  
  
 Poiché 42 è inferiore a 81, l'espressione booleana nell'esempio riportato in precedenza restituisce `True`.  Per ulteriori informazioni su questo tipo di espressione, vedere [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md).  
  
### Operatori di confronto combinati con operatori logici  
 Le espressioni di confronto possono essere combinate utilizzando gli operatori logici per produrre espressioni booleane più complesse.  Nell'esempio seguente viene dimostrato l'uso degli operatori di confronto in combinazione con un operatore logico.  
  
 `x > y And x < 1000`  
  
 Nell'esempio illustrato in precedenza, il valore dell'espressione generale dipende dai valori delle espressioni su ogni lato dell'operatore `And`.  Se entrambe le espressioni sono `True`, l'espressione totale restituisce `True`.  Se una delle due espressioni è `False`, l'intera espressione restituirà `False`.  
  
## Operatori short circuit  
 Gli operatori logici `AndAlso` e `OrElse` esibiscono un comportamento noto come *short\-circuit*.  Un operatore di short\-circuit restituisce prima l'operando di sinistra.  Se l'operatore di sinistra determina il valore dell'intera espressione, l'esecuzione del programma procederà senza valutare l'espressione corretta.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#89](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_3.vb)]  
  
 Nell'esempio riportato in precedenza, l'operatore restituisce l'espressione di sinistra, `45 < 12`.  Poiché l'espressione di sinistra restituisce `False`, l'intera espressione logica deve restituire `False`.  L'esecuzione del programma salta quindi l'esecuzione del codice all'interno del blocco `If` senza valutare l'espressione di destra, `testFunction(3)`.  Questo esempio non consente di chiamare `testFunction()` in quando l'espressione di sinistra falsifica l'intera espressione.  
  
 In modo simile, se l'espressione di sinistra in un'espressione logica che utilizza `OrElse` restituisce `True`, l'esecuzione procederà alla riga di codice successiva senza valutare l'espressione di destra, in quanto l'espressione di sinistra ha già convalidato l'intera espressione.  
  
### Confronto con gli operatori di non short\-circuit  
 Entrambi i lati dell'operatore logico invece sono valutati quando vengono utilizzati gli operatori logici `And` e `Or`.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#90](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/boolean-expressions_4.vb)]  
  
 Nell'esempio elencato in precedenza viene chiamato `testFunction()` anche se l'espressione di sinistra restituisce `False`.  
  
## Espressioni tra parentesi  
 È possibile utilizzare le parentesi per controllare l'ordine di valutazione delle espressioni booleane.  Le espressioni racchiuse tra parentesi vengono valutate per prime.  Nel caso di più livelli di annidamento, la precedenza è accordata alle espressioni annidate più interne.  All'interno delle parentesi, la valutazione viene eseguita in base alle regole di precedenza tra gli operatori.  Per ulteriori informazioni, vedere [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md).  
  
## Vedere anche  
 [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Statements](../../../../visual-basic/programming-guide/language-features/statements.md)   
 [Comparison Operators](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Efficient Combination of Operators](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)   
 [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Boolean Data Type](../../../../visual-basic/language-reference/data-types/boolean-data-type.md)