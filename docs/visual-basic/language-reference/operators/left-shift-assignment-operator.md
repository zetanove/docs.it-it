---
title: "&lt;&lt;= Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.<<="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operator <<="
  - "assignment statements, compound"
  - "<<= operator [Visual Basic]"
  - "statements [Visual Basic], compound assignment"
  - "operator<<="
  - "compound assignment statements"
ms.assetid: 8ad26613-faff-4e2f-89ee-63feee33bfda
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# &lt;&lt;= Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue uno spostamento aritmetico a sinistra sul valore di una variabile o di una proprietà e riassegna il risultato alla variabile o alla proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty <<= amount  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Variabile o proprietà di un tipo integrale \(`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long` o `ULong`\).  
  
 `amount`  
 Obbligatorio.  Espressione numerica di un tipo di dati che viene convertito verso il tipo più grande `Integer`.  
  
## Note  
 L'elemento a sinistra dell'operatore `<<=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 L'operatore di `<<=` innanzitutto esegue uno spostamento aritmetico a sinistra sul valore della variabile o della proprietà.  L'operatore quindi assegnare il risultato dell' operazione di nuovo a tale variabile o proprietà.  
  
 Gli spostamenti aritmetici non sono circolari. In altre parole, i bit spostati oltre una delle estremità del risultato non vengono reintrodotti all'altra estremità.  In uno spostamento aritmetico a sinistra, i bit spostati oltre l'intervallo del tipo di dati del risultato vengono ignorati e le posizioni dei bit liberate a destra sono impostate su zero.  
  
## Overload  
 L'[\<\< Operator](../../../visual-basic/language-reference/operators/left-shift-operator.md) può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `<<` ha effetto sul comportamento dell'operatore `<<=`.  Se il codice utilizza `<<=` su una classe o una struttura che esegue l'overload di `<<`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `<<=` viene utilizzato per spostare a sinistra lo schema di bit di una variabile `Integer` in base al numero specificato e per assegnare il risultato alla variabile.  
  
 [!code-vb[VbVbalrOperators#13](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/left-shift-assignment-op_1_1.vb)]  
  
## Vedere anche  
 [\<\< Operator](../../../visual-basic/language-reference/operators/left-shift-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Bit Shift Operators](../../../visual-basic/language-reference/operators/bit-shift-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)