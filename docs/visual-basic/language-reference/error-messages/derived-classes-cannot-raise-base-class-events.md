---
title: "Derived classes cannot raise base class events | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30029"
  - "bc30029"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30029"
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Derived classes cannot raise base class events
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un evento può essere generato solo dallo spazio di dichiarazione in cui è dichiarato.  Una classe non può pertanto generare eventi da un'altra classe, nemmeno da quella da cui deriva.  
  
 **ID errore:** BC30029  
  
### Per correggere l'errore  
  
-   Spostare l'istruzione `Event` o l'istruzione `RaiseEvent` in modo che si trovino entrambe nella stessa classe.  
  
## Vedere anche  
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [RaiseEvent Statement](../../../visual-basic/language-reference/statements/raiseevent-statement.md)