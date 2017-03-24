---
title: "^= Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.^="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "^= operator [Visual Basic]"
  - "compound assignment statements"
ms.assetid: 397da132-2d96-4a85-a7bc-f7c730a608c9
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# ^= Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Eleva il valore di una variabile o di una proprietà alla potenza indicata da un'espressione e riassegna il risultato alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty ^= expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi variabile o proprietà numerica.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Note  
 L'elemento a sinistra dell'operatore `^=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 L'operatore di `^=` innanzitutto genera il valore della variabile o della proprietà \(a sinistra dell' operatore\) alla potenza del valore dell' espressione \(sul lato destro dell' operatore\).  L'operatore quindi assegnare il risultato dell' operazione di nuovo alla variabile o alla proprietà.  
  
 In Visual Basic l'elevamento a potenza viene sempre eseguito nel [Double Data Type](../../../visual-basic/language-reference/data-types/double-data-type.md).  Gli operandi di tipo diverso vengono convertiti in `Double` e il risultato è sempre `Double`.  
  
 Il valore di `expression` può essere frazionario, negativo o entrambi.  
  
## Overload  
 L'[^ Operator](../../../visual-basic/language-reference/operators/exponentiation-operator.md) può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `^` ha effetto sul comportamento dell'operatore `^=`.  Se il codice utilizza `^=` su una classe o una struttura che esegue l'overload di `^`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `^=` viene utilizzato per elevare il valore di una variabile `Integer` alla potenza di una seconda variabile e assegnare il risultato alla prima variabile.  
  
 [!code-vb[VbVbalrOperators#21](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/exponentiation-assignment-operator_1.vb)]  
  
## Vedere anche  
 [^ Operator](../../../visual-basic/language-reference/operators/exponentiation-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)