---
title: "How to: Determine Whether Two Objects Are Identical (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "testing, objects"
  - "objects [Visual Basic], comparing"
  - "object variables, determining identity"
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# How to: Determine Whether Two Objects Are Identical (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] due riferimenti variabili vengono considerati identici se i relativi puntatori sono uguali, ovvero se entrambe le variabili puntano alla stessa istanza di classe nella memoria.  In un'applicazione Windows Form è ad esempio possibile eseguire un confronto per determinare se l'istanza corrente \(`Me`\) corrisponde a un'istanza specifica, ad esempio `Form2`.  
  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili due operatori che consentono di confrontare i puntatori.  L'[Is Operator](../../../../visual-basic/language-reference/operators/is-operator.md) restituisce `True` se gli oggetti sono identici, mentre l'[IsNot Operator](../../../../visual-basic/language-reference/operators/isnot-operator.md) restituisce `True` se non lo sono.  
  
## Determinazione dell'identicità di due oggetti  
  
#### Per determinare se due oggetti sono identici  
  
1.  Impostare un'espressione `Boolean` per eseguire la verifica dei due oggetti.  
  
2.  Nell'espressione di verifica utilizzare l'operatore `Is` con i due oggetti come operandi.  
  
     `Is` restituisce `True` se gli oggetti puntano alla stessa istanza di classe.  
  
## Determinazione della non identicità di due oggetti  
 A volte si desidera eseguire un'azione se i due oggetti non sono identici, ma può essere difficile combinare `Not` e `Is`, ad esempio `If Not obj1 Is obj2`.  In casi di questo tipo è possibile utilizzare l'operatore `IsNot`.  
  
#### Per determinare se due oggetti non sono identici  
  
1.  Impostare un'espressione `Boolean` per eseguire la verifica dei due oggetti.  
  
2.  Nell'espressione di verifica utilizzare l'operatore `IsNot` con i due oggetti come operandi.  
  
     `IsNot` restituisce `True` se gli oggetti non puntano alla stessa istanza di classe.  
  
## Esempio  
 Nell'esempio riportato di seguito viene eseguita la verifica di coppie di variabili `Object` per stabilire se puntano alla stessa istanza di classe.  
  
 [!code-vb[VbVbalrKeywords#14](../../../../visual-basic/language-reference/codesnippet/visualbasic/how-to-determine-whether_1_1.vb)]  
  
 Di seguito è riportato l'output dell'esempio precedente.  
  
 `objA different from objB?  True`  
  
 `objA identical to objC?  True`  
  
## Vedere anche  
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [Is Operator](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot Operator](../../../../visual-basic/language-reference/operators/isnot-operator.md)   
 [How to: Determine Whether Two Objects Are Related](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)