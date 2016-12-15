---
title: "How to: Refer to the Current Instance of an Object (Visual Basic) | Microsoft Docs"
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
  - "variables [Visual Basic], object"
  - "objects [Visual Basic], referring to current instance"
  - "instances, referring to current"
  - "current instance"
  - "object variables"
ms.assetid: 7f9b2c77-03cd-428f-adc2-b18070226e7c
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Refer to the Current Instance of an Object (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'*istanza corrente* di un oggetto è l'istanza nella quale il codice è attualmente in esecuzione.  
  
 Per fare riferimento all'istanza corrente, utilizzare la parola chiave`Me` .  
  
### Per fare riferimento all'istanza corrente  
  
-   Utilizzare la parola chiave `Me` laddove normalmente si utilizzerebbe il nome di una variabile oggetto.  
  
    ```  
    Me.ForeColor = System.Drawing.Color.Crimson  
    Me.Close()  
    ```  
  
     Sebbene `Me` agisca come una variabile oggetto, non è possibile dichiararla o assegnarvi alcun valore.  `Me` fa sempre riferimento all'istanza corrente.  
  
## Vedere anche  
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Assignment](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)