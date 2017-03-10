---
title: "Efficient Combination of Operators (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "expressions [Visual Basic], parentheses"
  - "operators [Visual Basic], associativity"
  - "expressions [Visual Basic], operators"
  - "operators [Visual Basic], precedence"
  - "Visual Basic code, operators"
  - "Visual Basic code, expressions"
  - "operators [Visual Basic], complex expressions"
  - "expressions [Visual Basic], complex"
  - "parentheses, complex expressions"
  - "numeric expressions"
ms.assetid: bd22340e-b5be-458b-8772-3916c02309a4
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Efficient Combination of Operators (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le espressioni complesse possono contenere molti operatori diversi.  Questa condizione è illustrata nell'esempio che segue.  
  
 `x = (45 * (y + z)) ^ (2 / 85) * 5 + z`  
  
 Per creare espressioni complesse come quelle dell'esempio precedente è necessaria una comprensione completa delle regole della precedenza degli operatori.  Per ulteriori informazioni, vedere [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md).  
  
## Espressioni tra parentesi  
 Capita spesso che si desideri che le operazioni procedano in un ordine diverso da quello determinato dalla precedenza degli operatori.  Prendere in considerazione l'esempio riportato di seguito.  
  
 `x = z * y + 4`  
  
 Nell'esempio riportato in precedenza `z` è moltiplicato per `y`, quindi il risultato viene aggiunto a `4`.  Se invece si desidera aggiungere `y` e `4` prima di moltiplicare il risultato per `z`, è possibile eseguire l'override della precedenza normale degli operatori utilizzando le parentesi.  Racchiudendo tra parentesi un'espressione, si impone a quella espressione di essere valutata per prima a prescindere dalla precedenza degli operatori.  Per imporre all'esempio riportato in precedenza di eseguire prima l'addizione, è necessario riscriverla come nell'esempio riportato di seguito.  
  
 `x = z * (y + 4)`  
  
 Nell'esempio riportato in precedenza `y` viene aggiunto a `4`, quindi la somma viene moltiplicata per `z`.  
  
### Espressioni annidate tra parentesi  
 È possibile annidare le espressioni nei livelli multipli delle parentesi per eseguire ulteriormente l'override della precedenza.  Le espressioni annidate più in profondità tra parentesi vengono valutate per prime, seguite da quelle annidate subito dopo e così via fino a quella annidata meno in profondità e infine alle espressioni al di fuori delle parentesi  Questa condizione è illustrata nell'esempio che segue.  
  
 `x = (z * 4) ^ (y * (z + 2))`  
  
 Nell'esempio riportato in precedenza, `z + 2` viene valutato per primo, quindi vengono valutate le altre espressioni tra parentesi.  L'elevamento a potenza, che normalmente ha una precedenza più alta rispetto ad addizione e moltiplicazione, in questo esempio viene valutato per ultimo perché le altre espressioni sono racchiuse tra parentesi.  
  
## Vedere anche  
 [Arithmetic Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [Logical\/Bitwise Operators](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Boolean Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [Value Comparisons](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [How to: Calculate Numeric Values](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-calculate-numeric-values.md)   
 [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md)