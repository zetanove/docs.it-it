---
title: "How to: Create a Procedure that Returns a Value (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "procedures, returning a value"
ms.assetid: 8ee19f95-a9ef-4033-963b-d224dca207c4
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Create a Procedure that Returns a Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per restituire un valore al codice chiamante, utilizzare una routine `Function`.  
  
### Per creare una routine che restituisce un valore  
  
1.  Al di fuori di qualsiasi altra routine, utilizzare un'istruzione `Function` seguita da un'istruzione `End Function`.  
  
2.  Nell'istruzione `Function` aggiungere il nome della routine dopo la parola chiave `Function`, quindi l'elenco di parametri tra parentesi.  
  
3.  Aggiungere una clausola `As` dopo le parentesi per specificare il tipo di dati del valore restituito.  
  
4.  Inserire le istruzioni del codice della routine tra le istruzioni `Function` e `End Function`.  
  
5.  Utilizzare un'istruzione `Return` per restituire il valore al codice chiamante.  
  
     La routine `Function` che segue consente di calcolare il lato più lungo, o ipotenusa, di un triangolo retto, dati i valori degli altri due lati.  
  
     [!code-vb[VbVbcnProcedures#1](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-create-a-procedure-that-returns-a-value_1.vb)]  
  
     Nell'esempio che segue è illustrata una tipica chiamata a  `hypotenuse`.  
  
     [!code-vb[VbVbcnProcedures#6](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-create-a-procedure-that-returns-a-value_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [How to: Return a Value from a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [How to: Call a Procedure That Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)