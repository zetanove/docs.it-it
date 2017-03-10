---
title: "How to: Make an Object Variable Not Refer to Any Instance (Visual Basic) | Microsoft Docs"
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
  - "Nothing keyword, variable assignment"
  - "object variables, null reference"
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# How to: Make an Object Variable Not Refer to Any Instance (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile eliminare l'associazione di una variabile oggetto a qualsiasi istanza di oggetto impostando la variabile a [Nothing](../../../../visual-basic/language-reference/nothing.md).  
  
### Per eliminare l'associazione di una variabile oggetto a qualsiasi istanza di oggetto  
  
-   In un'istruzione di assegnazione impostare la variabile su `Nothing`.  
  
    ```  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## Programmazione efficiente  
 Se il codice tenta di accedere a un membro di una variabile oggetto impostata su `Nothing`, viene generato un oggetto <xref:System.NullReferenceException>.  Se si imposta spesso una variabile oggetto su `Nothing` o se è possibile che la variabile non sia inizializzata, è opportuno includere gli accessi ai membri in un blocco `Try...Catch...Finally`.  
  
## Sicurezza di .NET Framework  
 Se si utilizza una variabile oggetto per oggetti contenenti dati riservati o sensibili, è possibile impostarla su `Nothing` quando non si utilizza attivamente uno di questi oggetti.  In questo modo si riduce il rischio di accesso ai dati da parte di malware.  
  
## Vedere anche  
 <xref:System.NullReferenceException>   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Assignment](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)   
 [Try...Catch...Finally Statement](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Risoluzione dei problemi relativi alle eccezioni: System.NullReferenceException](../Topic/Troubleshooting%20Exceptions:%20System.NullReferenceException.md)