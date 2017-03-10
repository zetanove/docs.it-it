---
title: "&#39;#ElseIf&#39; must be preceded by a matching &#39;#If&#39; or &#39;#ElseIf&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30014"
  - "bc30014"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30014"
ms.assetid: 5215585e-2efa-485a-9efe-9833a1cc83a0
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &#39;#ElseIf&#39; must be preceded by a matching &#39;#If&#39; or &#39;#ElseIf&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

`#ElseIf` è una direttiva di compilazione condizionale.  Una clausola `#ElseIf` deve essere preceduta da una clausola `#If` o `#ElseIf` corrispondente.  
  
 **ID errore:** BC30014  
  
### Per correggere l'errore  
  
1.  Verificare che una clausola `#If`  o `#ElseIf` precedente non sia stata separata da questa clausola `#ElseIf` dalla frapposizione di un blocco di compilazione condizionale o da una clausola `#End If` inserita in una posizione errata.  
  
2.  Se `#ElseIf` è preceduta da una direttiva `#Else`, rimuovere `#Else` o sostituirla con una clausola `#ElseIf`.  
  
3.  Se non sono presenti altri errori, aggiungere una direttiva `#If` all'inizio del blocco di compilazione condizionale.  
  
## Vedere anche  
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)