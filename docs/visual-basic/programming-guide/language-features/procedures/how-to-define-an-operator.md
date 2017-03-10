---
title: "How to: Define an Operator (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "operators [Visual Basic], defining"
  - "procedures, operator"
  - "Visual Basic code, operators"
  - "syntax, Operator procedures"
  - "operators [Visual Basic], overloading"
  - "operator procedures, about operator procedures"
  - "return values, Operator procedures"
  - "operator overloading"
ms.assetid: d4b0e253-092a-4e6e-9fe2-01f562140a29
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Define an Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se è stata definita una classe o una struttura, è possibile definire il comportamento di un operatore, quale `*`, `<>` o `And`, quando uno o entrambi gli operandi sono del tipo della classe o della struttura in questione.  
  
 È possibile definire l'operatore standard come routine con operatore all'interno della classe o della struttura.  Tutte le routine con operatore devono essere `Public` `Shared`.  
  
 La definizione di un operatore su una classe o una struttura viene anche detta *overload* dell'operatore.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definito l'operatore `+` per una struttura denominata `height`.  La struttura utilizza altezze misurate in piedi e pollici.  Un *pollice* e un *piede* corrispondono rispettivamente a 2,54 cm e a 12 pollici.  Per garantire valori normalizzati \(pollici \< 12\), il costruttore esegue il *modulo* aritmetico 12.  L'operatore `+` utilizza il costruttore per generare valori normalizzati.  
  
 [!code-vb[VbVbcnProcedures#25](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-define-an-operator_1.vb)]  
  
 È possibile testare la struttura `height` con il codice riportato di seguito.  
  
 [!code-vb[VbVbcnProcedures#26](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-define-an-operator_2.vb)]  
  
 Per ulteriori informazioni ed esempi, vedere [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [How to: Call an Operator Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [How to: Use a Class that Defines Operators](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)   
 [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [How to: Declare a Structure](../../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Operatore Mod](../../../../visual-basic/language-reference/operators/mod-operator.md)