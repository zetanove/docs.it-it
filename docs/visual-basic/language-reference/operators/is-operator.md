---
title: "Is Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.is"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "comparison operators"
  - "equivalent objects"
  - "TypeOf...Is expression"
  - "Is operator [Visual Basic]"
ms.assetid: 8045a6c8-2a83-45b6-ad47-d09a704c656d
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Is Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Confronta due variabili di riferimento a un oggetto.  
  
## Sintassi  
  
```  
  
result = object1 Is object2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi valore `Boolean`.  
  
 `object1`  
 Obbligatorio.  Qualsiasi nome `Object`.  
  
 `object2`  
 Obbligatorio.  Qualsiasi nome `Object`.  
  
## Note  
 L'operatore `Is` determina se due riferimenti a oggetti si riferiscono allo stesso oggetto,  senza tuttavia eseguire alcun confronto di valori.  Se `object1` e `object2` fanno entrambi riferimento alla stessa istanza di oggetto, `result` sarà `True`. In caso contrario, `result` sarà `False`.  
  
 `Is` può essere utilizzato anche con la parola chiave `TypeOf` per creare un'espressione `TypeOf`...`Is`, che consente di testare se una variabile oggetto è compatibile con un tipo di dati.  
  
> [!NOTE]
>  La parola chiave `Is` viene anche utilizzata nell'[Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Is` viene utilizzato per confrontare coppie di riferimenti a oggetti.  I risultati vengono assegnati a un valore `Boolean` che indica se i due oggetti sono identici.  
  
 [!code-vb[VbVbalrOperators#27](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/is-operator_1.vb)]  
  
 Come illustrato nell'esempio precedente, è possibile utilizzare l'operatore `Is` per testare sia gli oggetti ad associazione anticipata che quelli ad associazione tardiva.  
  
## Vedere anche  
 [TypeOf Operator](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [IsNot Operator](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Comparison Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)