---
title: "Event &#39;&lt;eventname1&gt;&#39; cannot implement event &#39;&lt;eventname2&gt;&#39; on interface &#39;&lt;interface&gt;&#39; because their delegate types &#39;&lt;delegate1&gt;&#39; and &#39;&lt;delegate2&gt;&#39; do not match | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc31423"
  - "bc31423"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31423"
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Event &#39;&lt;eventname1&gt;&#39; cannot implement event &#39;&lt;eventname2&gt;&#39; on interface &#39;&lt;interface&gt;&#39; because their delegate types &#39;&lt;delegate1&gt;&#39; and &#39;&lt;delegate2&gt;&#39; do not match
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non è possibile implementare un evento perché il tipo delegato dell'evento non corrisponde al tipo delegato dell'evento nell'interfaccia.  Questo errore può insorgere quando si definiscono più eventi in un'interfaccia e si tenta di implementarli assieme con lo stesso evento.  Un evento può implementare due o più eventi solo se tutti gli eventi implementati vengono dichiarati utilizzando la sintassi `As` e se tutti specificano lo stesso tipo delegato.  
  
 **ID errore:** BC31423  
  
### Per correggere l'errore  
  
-   Implementare gli eventi separatamente.  
  
     \-oppure\-  
  
-   Definire gli eventi nell'interfaccia utilizzando la sintassi `As` e specificare lo stesso tipo delegato.  
  
## Vedere anche  
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [Events](../../../visual-basic/programming-guide/language-features/events/events.md)