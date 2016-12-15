---
title: "How to: Call a Property Procedure (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "Visual Basic code, properties"
  - "procedures, calling"
  - "properties [Visual Basic], property procedures"
  - "procedure calls, property procedures"
ms.assetid: 96bc4d74-d9c3-4b7a-954d-58ac8553cd94
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Call a Property Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per chiamare una routine di proprietà, è necessario memorizzare un valore nella proprietà o recuperare il valore di quest'ultima.  L'accesso a una proprietà avviene con le stesse modalità utilizzate per accedere a una variabile.  
  
 Nella routine `Set` della proprietà viene memorizzato un valore recuperato dalla relativa routine `Get`.  Tali routine, tuttavia, non vengono chiamate in modo esplicito per nome.  La proprietà viene utilizzata in un'istruzione di assegnazione o in un'espressione, con le stesse modalità con cui viene archiviato o recuperato il valore di una variabile.  [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] effettua le chiamate alle routine della proprietà.  
  
### Per chiamare la routine Get di una proprietà  
  
1.  Utilizzare il nome della proprietà in un'espressione in modo analogo al nome di una variabile.  È possibile utilizzare una proprietà in tutti i contesti in cui è consentito l'utilizzo di una variabile o di una costante.  
  
     In alternativa  
  
     Utilizzare il nome della proprietà che segue il segno di uguale \(`=`\) in un'istruzione di assegnazione.  
  
     Nell'esempio seguente viene letto il valore della proprietà <xref:Microsoft.VisualBasic.DateAndTime.Now%2A> chiamando in modo implicito la relativa routine `Get`.  
  
     [!code-vb[VbVbalrDateProperties#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-call-a-property-procedure_1.vb)]  
  
2.  Se la proprietà accetta argomenti, far seguire il nome della proprietà da parentesi tra cui racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  Verificare di inserire gli argomenti nello stesso ordine con cui la proprietà definisce i parametri corrispondenti.  
  
 Il valore della proprietà viene utilizzato nell'espressione con le stesse modalità di una variabile o costante e viene quindi memorizzato nella variabile o proprietà a sinistra dell'istruzione di assegnazione.  
  
### Per chiamare la routine Set di una proprietà  
  
1.  Utilizzare il nome della proprietà a sinistra di un'istruzione di assegnazione.  
  
     Nell'esempio seguente viene impostato il valore della proprietà <xref:Microsoft.VisualBasic.DateAndTime.TimeOfDay%2A> chiamando in modo implicito la routine `Set`.  
  
     [!code-vb[VbVbcnProcedures#11](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-call-a-property-procedure_2.vb)]  
  
2.  Se la proprietà accetta argomenti, far seguire il nome della proprietà da parentesi tra cui racchiudere l'elenco di argomenti.  Se non sono presenti argomenti, è possibile omettere le parentesi.  
  
3.  Racchiudere gli argomenti dell'elenco tra parentesi, separati da virgole.  Verificare di inserire gli argomenti nello stesso ordine con cui la proprietà definisce i parametri corrispondenti.  
  
 Il valore generato a destra dell'istruzione di assegnazione viene memorizzato nella proprietà.  
  
## Vedere anche  
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)   
 [Get Statement](../../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set Statement](../../../../visual-basic/language-reference/statements/set-statement.md)