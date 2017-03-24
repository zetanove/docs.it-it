---
title: "Object Variables in Visual Basic | Microsoft Docs"
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
  - "object variables, about object variables"
  - "variables [Visual Basic], object"
  - "objects [Visual Basic], accessing"
  - "object variables"
ms.assetid: 6169a196-2b13-4ba5-a205-154bc1b87844
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Object Variables in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Oltre a memorizzare dei valori direttamente, una variabile può anche fare riferimento a un oggetto.  Si assegna un oggetto a una variabile per gli stessi motivi per i quali si assegna un valore a una variabile:  
  
-   Un nome di variabile è spesso più breve e facile da ricordare rispetto al percorso completo dei metodi e delle proprietà necessario per accedere all'oggetto.  
  
-   L'utilizzo di una variabile che fa riferimento a un oggetto è più efficiente dell'accesso ripetuto all'oggetto, tramite i metodi o le proprietà necessarie.  
  
-   È possibile modificare gli oggetti cui fa riferimento una variabile mentre il codice è in esecuzione.  
  
## Abbreviazione del codice  
 Le variabili oggetto possono essere utilizzate per abbreviare il codice da digitare.  Nell'esempio che segue viene utilizzato il percorso completo dei metodi e delle proprietà per accedere a un oggetto <xref:System.Windows.Forms.Control>.  
  
```  
' Assume Me is a valid Form, or replace Me with a valid Form.  
Me.ActiveForm.ActiveControl.Text = "Test"  
Me.ActiveForm.ActiveControl.Location = New Point(100, 100)  
Me.ActiveForm.ActiveControl.Show()  
```  
  
 È possibile abbreviarlo e velocizzare l'esecuzione utilizzando una variabile oggetto per il controllo.  È necessario dichiarare la variabile oggetto con la classe specifica che si intende assegnarle \(`Control` in questo caso\).  Una volta assegnato un oggetto alla variabile, è possibile considerarla come l'oggetto cui fa riferimento.  È possibile impostare o recuperare le proprietà dell'oggetto oppure utilizzare uno qualsiasi dei relativi metodi.  Nell'esempio che segue viene utilizzata una variabile oggetto per semplificare il codice riportato nell'esempio precedente.  
  
```  
Dim ctrlActv As System.Windows.Forms.Control = Me.ActiveForm.ActiveControl  
ctrlActv.Text = "Test"  
ctrlActv.Location = New Point(100, 100)  
ctrlActv.Show()  
```  
  
## Vedere anche  
 [Dichiarazione di variabili](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [How to: Speed Up Access to an Object with a Long Qualification Path](../../../../visual-basic/programming-guide/language-features/variables/how-to-speed-up-access-to-an-object-with-a-long-qualification-path.md)   
 [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object Variable Assignment](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)