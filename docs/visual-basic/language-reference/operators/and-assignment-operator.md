---
title: "&amp;= Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.&="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operator &="
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "&= operator [Visual Basic]"
  - "compound assignment statements"
ms.assetid: 0cf262fc-1a05-419a-a503-60013f111c8a
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &amp;= Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Concatena un'espressione `String` a una variabile o a una proprietà `String` e assegna il risultato alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty &= expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi variabile o proprietà `String`.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione `String`.  
  
## Note  
 L'elemento a sinistra dell'operatore `&=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  `&=` l'operatore concatena  `String` espressione della relativa a destra  `String` la variabile o proprietà sulla sinistra e assegna il risultato alla variabile o proprietà sulla sinistra.  
  
## Overload  
 L'[& Operator](../../../visual-basic/language-reference/operators/concatenation-operator.md) può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `&` ha effetto sul comportamento dell'operatore `&=`.  Se il codice utilizza `&=` su una classe o una struttura che esegue l'overload di `&`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `&=` viene utilizzato per concatenare due variabili `String` e assegnare il risultato alla prima variabile.  
  
 [!code-vb[VbVbalrOperators#3](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/and-assignment-operator_1.vb)]  
  
## Vedere anche  
 [& Operator](../../../visual-basic/language-reference/operators/concatenation-operator.md)   
 [\+\= Operator](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Concatenation Operators](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)