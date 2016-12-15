---
title: "TypeOf Operator (Visual Basic) | Microsoft Docs"
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
  - "TypeOf"
  - "vb.TypeOf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "types [Visual Basic], compatible"
  - "comparison operators"
  - "TypeOf...Is expression"
  - "data types [Visual Basic], compatible"
  - "TypeOf operator [Visual Basic]"
  - "compatible data types"
ms.assetid: 33f65296-659a-4b9a-9a29-c2a91cff68b2
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# TypeOf Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Confronta una variabile di riferimento a un oggetto con un tipo di dati.  
  
## Sintassi  
  
```  
  
result = TypeOf objectexpression Is typename  
```  
  
```  
  
result = TypeOf objectexpression IsNot typename  
```  
  
## Parti  
 `result`  
 Restituita.  Valore `Boolean`.  
  
 `objectexpression`  
 Necessario.  Qualsiasi espressione che restituisce un tipo riferimento.  
  
 `typename`  
 Necessario.  Qualsiasi nome di un tipo di dati.  
  
## Note  
 L'operatore `TypeOf` determina se il tipo di `objectexpression` in fase di esecuzione è compatibile con `typename`.  La compatibilità dipende dalla categoria del tipo di `typename`.  La tabella seguente illustra come viene determinata la compatibilità.  
  
|Categoria del tipo di `typename`|Criterio di compatibilità|  
|--------------------------------------|-------------------------------|  
|Classe|`objectexpression` è del tipo `typename` o eredita da `typename`|  
|Struttura|`objectexpression` è del tipo `typename`|  
|Interfaccia|`objectexpression` implementa `typename` o eredita da una classe che implementa `typename`|  
  
 Se il tipo di `objectexpression` in fase di esecuzione soddisfa il criterio di compatibilità, `result` sarà `True`.  In caso contrario, `result` sarà `False`.  Se `objectexpression` è null, `TypeOf`...`Is` restituisce `False` e ...`IsNot` restituisce `True`.  
  
 `TypeOf` viene sempre usato con la parola chiave `Is` per costruire un'espressione `TypeOf`...`Is` oppure con la parola chiave `IsNot` per costruire un'espressione `TypeOf`...`IsNot`.  
  
## Esempio  
 Nell'esempio seguente le espressioni `TypeOf`...`Is` vengono usate per verificare la compatibilità dei tipi di due variabili di riferimento a un oggetto con diversi tipi di dati..  
  
 [!code-vb[VbVbalrOperators#39](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/typeof-operator_1.vb)]  
  
 La variabile `refInteger` presenta un tipo in fase di esecuzione `Integer`.  È compatibile con `Integer`, ma non con `Double`.  La variabile `refForm` presenta un tipo in fase di esecuzione <xref:System.Windows.Forms.Form>.  È compatibile con <xref:System.Windows.Forms.Form> perché si tratta del relativo tipo, con <xref:System.Windows.Forms.Control> perché <xref:System.Windows.Forms.Form> eredita da <xref:System.Windows.Forms.Control> e con <xref:System.ComponentModel.IComponent> perché <xref:System.Windows.Forms.Form> eredita da <xref:System.ComponentModel.Component>, che implementa <xref:System.ComponentModel.IComponent>.  `refForm` non è invece compatibile con <xref:System.Windows.Forms.Label>.  
  
## Vedere anche  
 [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [Comparison Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)