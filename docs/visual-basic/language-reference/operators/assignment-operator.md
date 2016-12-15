---
title: "= Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.Assign"
  - "vb.="
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "= operator [Visual Basic]"
  - "= assignment statements [Visual Basic]"
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# = Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Assegna un valore a una variabile o a una proprietà.  
  
## Sintassi  
  
```  
  
variableorproperty = value  
```  
  
## Parti  
 `variableorproperty`  
 Qualsiasi variabile modificabile o qualsiasi proprietà.  
  
 `value`  
 Qualsiasi valore letterale, costante o espressione.  
  
## Note  
 L'elemento a sinistra del segno di uguale \(`=`\) può essere una semplice variabile scalare, una proprietà oppure un elemento di una matrice.  La variabile o la proprietà non può essere [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md).  L'operatore `=` assegna il valore specificato a destra alla variabile o alla proprietà indicata a sinistra.  
  
> [!NOTE]
>  L'operatore `=` viene utilizzato anche come operatore di confronto.  Per informazioni dettagliate, vedere [Comparison Operators](../../../visual-basic/language-reference/operators/comparison-operators.md).  
  
## Overload  
 L'operatore `=` può essere sottoposto a overload solo come operatore di confronto relazionale, non come operatore di assegnazione.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'operatore di assegnazione.  Il valore a destra viene assegnato alla variabile a sinistra.  
  
 [!code-vb[VbVbalrOperators#9](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/assignment-operator_1.vb)]  
  
## Vedere anche  
 [&\= Operator](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [\*\= Operator](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [\+\= Operator](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [\-\= Operator](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [\/\= Operator](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\\= Operator](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [^\= Operator](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Comparison Operators](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)