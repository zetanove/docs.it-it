---
title: "Statement cannot end a block outside of a line &#39;If&#39; statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32005"
  - "bc32005"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32005"
ms.assetid: 4039f51b-e0ee-4789-a89b-45d06de06b5d
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Statement cannot end a block outside of a line &#39;If&#39; statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione `If` a riga singola contiene più istruzioni separate da due punti \(:\), una delle quali è un'istruzione `End` per un blocco di controllo all'esterno dell'istruzione `If` a riga singola.  Le istruzioni `If` a riga singola non utilizzano l'istruzione `End If`.  
  
 **ID errore:** BC32005  
  
### Per correggere l'errore  
  
-   Spostare l'istruzione `If` a riga singola all'esterno del blocco di controllo che contiene l'istruzione `End If`.  
  
## Vedere anche  
 [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md)