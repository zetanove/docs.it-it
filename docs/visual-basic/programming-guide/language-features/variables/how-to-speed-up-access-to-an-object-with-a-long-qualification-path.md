---
title: "How to: Speed Up Access to an Object with a Long Qualification Path (Visual Basic) | Microsoft Docs"
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
  - "variables [Visual Basic], accessing"
  - "variables [Visual Basic], object"
  - "With statement"
  - "With block"
  - "object variables, accessing"
ms.assetid: 3eb7657f-c9fe-4e05-8bc3-4bb14d5ae585
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# How to: Speed Up Access to an Object with a Long Qualification Path (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Se si esegue spesso l'accesso a un oggetto per il quale è necessario un percorso di qualificazione con numerosi metodi e proprietà, è possibile migliorare l'efficienza del codice evitando di ripetere tale percorso.  
  
 Esistono due metodi per evitare di ripetere il percorso di qualificazione.  È possibile assegnare l'oggetto a una variabile oppure utilizzarlo in un blocco `With`...`End With`.  
  
### Per velocizzare l'accesso a un oggetto con un percorso di qualificazione lungo mediante l'assegnazione dell'oggetto a una variabile  
  
1.  Dichiarare una variabile dello stesso tipo dell'oggetto a cui si esegue spesso l'accesso.  Specificare il percorso di qualificazione nella parte di inizializzazione della dichiarazione.  
  
    ```  
    Dim ctrlActv As Control = someForm.ActiveForm.ActiveControl  
    ```  
  
2.  Utilizzare la variabile per accedere ai membri dell'oggetto.  
  
    ```  
    ctrlActv.Text = "Test"  
    ctrlActv.Location = New Point(100, 100)  
    ctrlActv.Show()  
    ```  
  
### Per velocizzare l'accesso a un oggetto con un percorso di qualificazione lungo mediante l'utilizzo di un blocco With...End With  
  
1.  Inserire il percorso di qualificazione in un'istruzione `With`.  
  
    ```  
    With someForm.ActiveForm.ActiveControl  
    ```  
  
2.  Accedere ai membri dell'oggetto all'interno del blocco `With` prima dell'istruzione `End With`.  
  
    ```  
        .Text = "Test"  
        .Location = New Point(100, 100)  
        .Show()  
    End With  
    ```  
  
## Vedere anche  
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [With...End With Statement](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)