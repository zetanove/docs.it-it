---
title: "ByVal (Visual Basic) | Microsoft Docs"
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
  - "vb.ByVal"
  - "ByVal"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ByVal keyword, contexts"
  - "ByVal keyword"
ms.assetid: 1eaf4e58-b305-4785-9e3d-e416b9c75598
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# ByVal (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che un argomento viene passato in modo tale che la routine o la proprietà chiamata non sia in grado di modificare il valore della variabile sottostante nel codice chiamante.  
  
## Note  
 Il modificatore `ByVal` può essere utilizzato nei seguenti contesti:  
  
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Esempio  
 Nell'esempio seguente viene illustrato l'utilizzo del meccanismo di passaggio del parametro `ByVal` con un argomento del tipo di riferimento.  Nell'esempio l'argomento è `c1`, un'istanza della classe `Class1`.  `ByVal` impedisce al codice nelle routine di modificare il valore sottostante dell'argomento di riferimento, `c1`, ma non protegge i campi e le proprietà accessibili di `c1`.  
  
 [!code-vb[VbVbalrKeywords#10](../../../visual-basic/language-reference/codesnippet/VisualBasic/byval_1.vb)]  
  
## Vedere anche  
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Passing Arguments by Value and by Reference](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)