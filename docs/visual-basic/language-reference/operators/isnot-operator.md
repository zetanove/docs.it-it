---
title: "IsNot Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.isnot"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "IsNot operator"
ms.assetid: 8dd2bcdb-0166-48a2-9094-60dfb448f36c
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# IsNot Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Confronta due variabili di riferimento a un oggetto.  
  
## Sintassi  
  
```  
  
result = object1 IsNot object2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Valore di `Boolean`.  
  
 `object1`  
 Obbligatorio.  Qualsiasi variabile o espressione `Object`.  
  
 `object2`  
 Obbligatorio.  Qualsiasi variabile o espressione `Object`.  
  
## Note  
 L'operatore `IsNot` determina se due riferimenti a oggetti si riferiscono a oggetti diversi,  senza tuttavia eseguire alcun confronto di valori.  Se `object1` e `object2` fanno entrambi riferimento alla stessa istanza di oggetto, `result` sarà `False`. In caso contrario, `result` sarà `True`.  
  
 `IsNot` è l'opposto dell'operatore `Is`.  Il vantaggio offerto dall'operatore `IsNot` è quello di semplificare la lettura di una sintassi complessa evitando l'utilizzo di `Not` e `Is`.  
  
 È possibile utilizzare gli operatori `Is` e `IsNot` per testare sia gli oggetti ad associazione anticipata che quelli ad associazione tardiva.  
  
> [!NOTE]
>  L'operatore `IsNot` non può essere utilizzato per confrontare espressioni restituite dall'operatore `TypeOf`.  È invece necessario utilizzare gli operatori `Not` e `Is`.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito gli operatori `Is` e `IsNot` vengono utilizzati per eseguire lo stesso confronto.  
  
 [!code-vb[VbVbalrOperators#29](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/isnot-operator_1.vb)]  
  
## Vedere anche  
 [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md)   
 [TypeOf Operator](../../../visual-basic/language-reference/operators/typeof-operator.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [How to: Test Whether Two Objects Are the Same](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-test-whether-two-objects-are-the-same.md)