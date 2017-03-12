---
title: "Handles clause requires a WithEvents variable defined in the containing type or one of its base types | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30506"
  - "bc30506"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30506"
ms.assetid: 5b66f6a8-f050-4e03-a57f-a64e85f80cb5
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Handles clause requires a WithEvents variable defined in the containing type or one of its base types
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nella clausola `Handles` non è stata specificata una variabile `WithEvents`.  La parola chiave `Handles` alla fine di una dichiarazione di routine consente a tale routine di gestire gli eventi generati da una variabile oggetto dichiarata con la parola chiave `WithEvents`.  
  
 **ID errore:** BC30506  
  
### Per correggere l'errore  
  
-   Fornire la variabile `WithEvents` necessaria.  
  
## Vedere anche  
 [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)