---
title: "&#39;Class&#39; statement must end with a matching &#39;End Class&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30481"
  - "bc30481"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30481"
ms.assetid: 583f3029-bc3a-4e06-866f-92dbecc46f19
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &#39;Class&#39; statement must end with a matching &#39;End Class&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'istruzione `Class` è utilizzata per iniziare un blocco `Class`, pertanto può trovarsi solo all'inizio del blocco e quest'ultimo deve terminare con un'istruzione `End Class` corrispondente.  L'istruzione `Class` è ridondante oppure il blocco `Class` non è stato terminato con un'istruzione `End Class`.  
  
 **ID errore:** BC30481  
  
### Per correggere l'errore  
  
-   Individuare e rimuovere l'istruzione `Class` superflua.  
  
-   Concludere il blocco `Class` con un'istruzione `End Class` corrispondente.  
  
## Vedere anche  
 [End \<keyword\> Statement](../../../visual-basic/language-reference/statements/end-keyword-statement.md)   
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)