---
title: "&#39;&lt;methodname&gt;&#39; has multiple definitions with identical signatures | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30269"
  - "bc30269"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30269"
ms.assetid: 39489621-6617-4e5c-9b24-c2faf8273891
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &#39;&lt;methodname&gt;&#39; has multiple definitions with identical signatures
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una dichiarazione di routine `Function` o `Sub` utilizza lo stesso nome di routine e lo stesso elenco di argomenti di una dichiarazione precedente.  Una causa possibile è un tentativo di overload della routine originale.  Le routine sottoposte a overload devono avere elenchi di argomenti differenti.  
  
 **ID errore:** BC30269  
  
### Per correggere l'errore  
  
-   Cambiare il nome della routine o l'elenco degli argomenti, oppure rimuovere la dichiarazione duplicata.  
  
## Vedere anche  
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Considerations in Overloading Procedures](../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)