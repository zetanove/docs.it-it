---
title: "+= Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.+="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "+= operator [Visual Basic]"
  - "assignment statements, compound"
  - "statements [Visual Basic], compound assignment"
  - "+= operator [Visual Basic], appending strings"
  - "compound assignment statements"
ms.assetid: d3e959f4-85d4-4e47-87c4-77b62335a5b3
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# += Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Aggiunge il valore di un'espressione numerica a quello di una proprietà o di una variabile numerica e assegna il risultato alla proprietà o alla variabile.  Consente inoltre di concatenare un'espressione `String` a una proprietà o a una variabile `String` e di assegnare il risultato alla proprietà o alla variabile.  
  
## Sintassi  
  
```  
  
variableorproperty += expression  
```  
  
## Parti  
 `variableorproperty`  
 Obbligatorio.  Qualsiasi proprietà o variabile numerica o `String`.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione numerica o `String`.  
  
## Note  
 L'elemento a sinistra dell'operatore `+=` può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 `+=` l'operatore aggiunge il valore della relativa destra alla variabile o proprietà sulla sinistra e assegna il risultato alla variabile o proprietà sulla sinistra.  `+=` l'operatore può essere utilizzato per concatenare  `String` espressione della relativa a destra  `String` la variabile o proprietà sulla sinistra e assegna il risultato alla variabile o proprietà sulla sinistra.  
  
> [!NOTE]
>  Quando si utilizza l'operatore `+=`, non sempre è possibile stabilire se verrà eseguita una somma o una concatenazione di stringhe.  Per eliminare qualsiasi ambiguità e fornire codice autodocumentato, si consiglia di utilizzare l'operatore `&=` per la concatenazione.  
  
 Questo operatore di assegnazione consente di eseguire in modo implicito conversioni verso tipi di dati più grandi ma non verso tipi di dati più piccoli se nell'ambiente di compilazione viene applicata una semantica rigida.  Per ulteriori informazioni su questo tipo di conversioni, vedere [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  Per informazioni sulla semantica rigida e permissiva, vedere [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
 Se è consentita la semantica permissiva, l'operatore `+=` eseguirà in modo implicito una serie di conversioni di stringhe e numeriche identiche a quelle eseguite dall'operatore `+`.  Per informazioni dettagliate su questo tipo di conversioni, vedere [\+ Operator](../../../visual-basic/language-reference/operators/addition-operator.md).  
  
## Overload  
 L'operatore `+` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload dell'operatore `+` ha effetto sul comportamento dell'operatore `+=`.  Se il codice utilizza `+=` su una classe o una struttura che esegue l'overload di `+`, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `+=` viene utilizzato per combinare i valori di due variabili.  Nella prima parte l'operatore `+=` viene utilizzato con le variabili numeriche per aggiungere un valore a un altro.  Nella seconda parte l'operatore `+=` viene utilizzato con le variabili `String` per concatenare due valori.  In entrambi i casi, il risultato viene assegnato alla prima variabile.  
  
 [!code-vb[VbVbalrOperators#7](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_1.vb)]  
  
 [!code-vb[VbVbalrOperators#8](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/addition-assignment-operator_2.vb)]  
  
 A questo punto i valori di `num1` e `str1` sono rispettivamente 13 e "103".  
  
## Vedere anche  
 [\+ Operator](../../../visual-basic/language-reference/operators/addition-operator.md)   
 [Assignment Operators](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Concatenation Operators](../../../visual-basic/language-reference/operators/concatenation-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)