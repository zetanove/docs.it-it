---
title: "How to: Put a Value in a Property (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "property values"
  - "Visual Basic code, procedures"
  - "values, properties"
  - "Visual Basic code, properties"
  - "properties [Visual Basic], values"
ms.assetid: c39401e5-b5fc-4439-8f31-ed640f7ce6ed
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Put a Value in a Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per memorizzare un valore in una proprietà, è necessario inserirne il nome a sinistra di un'istruzione di assegnazione.  
  
 La routine `Set` della proprietà memorizza un valore ma questo non viene chiamato esplicitamente in base al nome.  È possibile utilizzare la proprietà esattamente come si utilizzerebbe una variabile.  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] effettua le chiamate alle routine della proprietà.  
  
### Per memorizzare un valore in una proprietà  
  
1.  Utilizzare il nome della proprietà a sinistra di un'istruzione di assegnazione.  
  
     Nell'esempio riportato di seguito viene impostato il valore della proprietà `TimeOfDay` di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] su mezzogiorno mediante la chiamata implicita alla rispettiva routine `Set`.  
  
     [!code-vb[VbVbcnProcedures#11](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-put-a-value-in-a-property_1.vb)]  
  
2.  Se la proprietà accetta argomenti, far seguire il nome della proprietà da parentesi tra cui racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  Verificare di inserire gli argomenti nello stesso ordine con cui la proprietà definisce i parametri corrispondenti.  
  
4.  Il valore generato a destra dell'istruzione di assegnazione viene memorizzato nella proprietà.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A>   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)