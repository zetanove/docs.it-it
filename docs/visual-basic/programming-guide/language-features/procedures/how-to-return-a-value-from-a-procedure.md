---
title: "How to: Return a Value from a Procedure (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "procedures, returning from"
  - "procedures, returning a value"
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Return a Value from a Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Function` restituisce un valore al codice chiamante mediante l'esecuzione di un'istruzione `Return` o l'individuazione di un'istruzione `Exit Function` o `End Function`.  
  
### Per restituire un valore utilizzando l'istruzione Return  
  
1.  Inserire un'istruzione `Return` in corrispondenza del punto in cui viene completata l'attività della routine.  
  
2.  Far seguire la parola chiave `Return` da un'espressione che produce il valore che si desidera venga restituito al codice chiamante.  
  
3.  Nella stessa routine possono essere presenti più istruzioni `Return`.  
  
     La routine `Function` riportata di seguito calcola il lato più lungo di un triangolo rettangolo, ovvero l'ipotenusa, e restituisce il valore ottenuto al codice chiamante.  
  
     [!code-vb[VbVbcnProcedures#1](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-return-a-value-fr_1.vb)]  
  
     Nell'esempio riportato di seguito viene illustrata una chiamata tipica a `hypotenuse`, che memorizza il valore restituito.  
  
     [!code-vb[VbVbcnProcedures#6](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-return-a-value-fr_2.vb)]  
  
### Per restituire un valore utilizzando l'istruzione Exit Function o End Function  
  
1.  In almeno un punto della routine `Function` assegnare un valore al nome della routine.  
  
2.  Quando si esegue un'istruzione `Exit Function` o `End Function`, viene restituito l'ultimo valore assegnato al nome della routine.  
  
3.  Nella stessa routine possono essere presenti più istruzioni `Exit Function` ed è possibile combinare le istruzioni `Return` e `Exit Function`.  
  
4.  In una routine `Function`, invece, può essere presente una sola istruzione `End Function`.  
  
     Per ulteriori informazioni e un esempio, vedere "Valore restituito" in [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return Statement](../../../../visual-basic/language-reference/statements/return-statement.md)   
 [How to: Create a Procedure that Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [How to: Call a Procedure That Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)