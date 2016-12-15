---
title: "How to: Declare a Property with Mixed Access Levels (Visual Basic) | Microsoft Docs"
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
  - "access levels, properties"
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "mixed access levels"
  - "Visual Basic code, properties"
  - "properties [Visual Basic], access levels"
  - "Property statement, declaring mixed access levels"
ms.assetid: fdbb2d97-279a-4956-b26c-cbdfbc34915a
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Declare a Property with Mixed Access Levels (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per far sì che le routine `Get` e `Set` di una proprietà presentino livelli di accesso differenti, è possibile utilizzare il livello meno restrittivo e più restrittivo rispettivamente nell'istruzione `Property` e nell'istruzione `Get` o `Set`.  I livelli di accesso misto vengono utilizzati in una proprietà quando si desidera che determinate parti di codice siano in grado di ottenere il valore della proprietà mentre altre parti siano in grado di modificarlo.  
  
 Per ulteriori informazioni sui livelli di accesso, vedere [Access Levels in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
### Per dichiarare una proprietà con livelli di accesso misto  
  
1.  Dichiarare la proprietà nel modo consueto e specificare il livello di accesso meno restrittivo, quale `Public`, nell'istruzione `Property`.  
  
2.  Dichiarare la routine `Get` o `Set` specificando il livello di accesso più restrittivo, come `Friend`.  
  
3.  Non specificare un livello di accesso sull'altra routine di proprietà  in quanto assume il livello di accesso dichiarato nella proprietà `Property`.  L'accesso può essere limitato solo su una delle routine di proprietà.  
  
     [!code-vb[VbVbcnProcedures#10](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-declare-a-property-with-mixed-access-levels_1.vb)]  
  
     Nell'esempio precedente la routine `Get` presenta lo stesso livello di accesso `Protected` della proprietà stessa, mentre la routine `Set` dispone del livello di accesso `Private`.  Una classe derivata da `employee` può leggere il valore `salary`, ma tale valore può essere impostato solo dalla classe `employee`.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)