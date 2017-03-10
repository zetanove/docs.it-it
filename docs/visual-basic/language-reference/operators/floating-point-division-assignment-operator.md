---
title: "/= Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb./="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "/= operator [Visual Basic]"
  - "operator /="
  - "compound assignment statements"
ms.assetid: a1e22d0e-8380-4761-9da1-84fb51c34821
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# /= Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Divide il valore di una variabile o di una proprietà per il valore di un'espressione e assegna il risultato a virgola mobile alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty /= expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi variabile o proprietà numerica.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Note  
 L'elemento a sinistra dell'operatore `/=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 L'operatore di `/=` innanzitutto divide il valore della variabile o della proprietà \(a sinistra dell' operatore\) dal valore dell' espressione \(sul lato destro dell' operatore\).  L'operatore quindi assegnare il risultato a virgola mobile dell' operazione alla variabile o alla proprietà.  
  
 Questa istruzione assegna un valore di `Double` alla variabile o la proprietà a sinistra.  Se `Option Strict` è `On`, `variableorproperty` deve essere di tipo `Double`.  Se `Option Strict` è `Off`, verrà eseguita una conversione implicita e il valore ottenuto verrà assegnato a `variableorproperty`, con la possibilità che si verifichi un errore in fase di esecuzione.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) e [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
## Overload  
 L'[\/ Operator](../../../visual-basic/language-reference/operators/floating-point-division-operator.md) può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `/` ha effetto sul comportamento dell'operatore `/=`.  Se il codice utilizza `/=` su una classe o una struttura che esegue l'overload di `/`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `/=` viene utilizzato per dividere una variabile `Integer` per una seconda variabile e assegnare il quoziente alla prima variabile.  
  
 [!code-vb[VbVbalrOperators#17](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/floating-point-division-_0_1.vb)]  
  
## Vedere anche  
 [\/ Operator](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)   
 [\\\= Operator](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)