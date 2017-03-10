---
title: "How to: Create a Variable that Does Not Change in Value (Visual Basic) | Microsoft Docs"
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
  - "variables [Visual Basic], read-only"
  - "variables [Visual Basic], constant value"
ms.assetid: 86b59266-25df-4635-ae15-9b59c411d036
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Create a Variable that Does Not Change in Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La nozione di variabile il cui valore rimane invariato può apparire contraddittoria.  Esistono tuttavia situazioni in cui l'utilizzo di una costante non è praticabile, mentre può essere utile disporre di una variabile con un valore fisso.  In casi di questo tipo è possibile definire una variabile membro con la parola chiave [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md).  
  
 Non è possibile utilizzare l'[Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md) per dichiarare e assegnare un valore costante nelle seguenti situazioni:  
  
-   L'istruzione `Const` non accetta il tipo di dati che si desidera utilizzare.  
  
-   In fase di compilazione non si conosce il valore.  
  
-   In fase di compilazione non è possibile calcolare il valore costante.  
  
### Per creare una variabile che non cambia di valore  
  
1.  A livello di modulo dichiarare una variabile membro con l'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md) e includere la parola chiave [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md).  
  
    ```  
  
    Dim ReadOnly timeStarted  
    ```  
  
     È possibile specificare `ReadOnly` solo per una variabile membro.  Questo significa che è necessario definire la variabile a livello di modulo, all'esterno di qualsiasi routine.  
  
2.  Se in fase di compilazione è possibile calcolare il valore in una singola istruzione, utilizzare una clausola di inizializzazione nell'istruzione `Dim`.  Dopo la clausola [As](../../../../visual-basic/language-reference/statements/as-clause.md) inserire un segno di uguale \(`=`\) seguito da un'espressione.  Accertarsi che il compilatore sia in grado di valutare questa espressione come valore costante.  
  
    ```  
    Dim ReadOnly timeStarted As Date = Now  
    ```  
  
     È possibile assegnare un valore a una variabile `ReadOnly` una sola volta.  Dopo questa operazione, il valore non potrà essere modificato da alcun codice.  
  
     Se in fase di compilazione non si conosce il valore né è possibile calcolarlo in una singola istruzione, è comunque possibile assegnarlo in fase di esecuzione in un costruttore.  Per eseguire questa operazione, è necessario dichiarare la variabile `ReadOnly` a livello di classe o di struttura.  Nel costruttore relativo alla classe o alla struttura calcolare il valore fisso e assegnarlo alla variabile prima di uscire dal costruttore.  
  
## Vedere anche  
 [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md)