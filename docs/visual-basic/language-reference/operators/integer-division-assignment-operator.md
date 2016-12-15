---
title: "-= Operator (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.-="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "-= operator [Visual Basic]"
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "operator -="
  - "compound assignment statements"
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# -= Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Sottrae il valore di un'espressione dal valore di una variabile o di una proprietà e assegna il risultato alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty -= expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi variabile o proprietà numerica.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Note  
 L'elemento a sinistra dell'operatore `-=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 L'operatore di `-=` innanzitutto astrae il valore dell' espressione \(sul lato destro dell' operatore\) dal valore della variabile o della proprietà \(a sinistra dell' operatore\).  L'operatore quindi assegnare il risultato dell' operazione alla variabile o alla proprietà.  
  
## Overload  
 L'[\- Operator](../../../visual-basic/language-reference/operators/subtraction-operator.md) può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `-` ha effetto sul comportamento dell'operatore `-=`.  Se il codice utilizza `-=` su una classe o una struttura che esegue l'overload di `-`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `-=` viene utilizzato per sottrarre una variabile `Integer` da un'altra variabile e assegnare il risultato a quest'ultima.  
  
 [!code-vb[VbVbalrOperators#11](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/integer-division-assignment-operator_1.vb)]  
  
## Vedere anche  
 [\- Operator](../../../visual-basic/language-reference/operators/subtraction-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)