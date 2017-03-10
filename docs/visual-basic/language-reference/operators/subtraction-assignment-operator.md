---
title: "\= Operator | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "\="
  - "vb.\="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "\= operator [Visual Basic]"
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "operator \= [Visual Basic]"
  - "compound assignment statements"
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# \= Operator
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Divide il valore di una variabile o di una proprietà per il valore di un'espressione e assegna il valore integer risultante alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty \= expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi variabile o proprietà numerica.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Note  
 L'elemento a sinistra dell'operatore `\=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 L'operatore di `\=` divide il valore di una variabile o di una proprietà a sinistra del valore di sulla destra e assegna il risultato intero alla variabile o proprietà sulla sinistra  
  
 Per ulteriori informazioni sulla divisione di valori integer, vedere [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md).  
  
## Overload  
 L'operatore `\` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `\` ha effetto sul comportamento dell'operatore `\=`.  Se il codice utilizza `\=` su una classe o una struttura che esegue l'overload di `\`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `\=` viene utilizzato per dividere una variabile `Integer` per una seconda variabile e assegnare il risultato integer alla prima variabile.  
  
 [!code-vb[VbVbalrOperators#19](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/subtraction-assignment-o_2_1.vb)]  
  
## Vedere anche  
 [\\ Operator](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [\/\= Operator](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)