---
title: "&#39;Set&#39; accessor of property &#39;&lt;propertyname&gt;&#39; is not accessible | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc31102"
  - "bc31102"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31102"
ms.assetid: 6f7b31b7-3656-4ae1-8851-90f5f4c6950a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Set&#39; accessor of property &#39;&lt;propertyname&gt;&#39; is not accessible
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'istruzione sta tentando di archiviare il valore di una proprietà pur non avendo accesso alla routine `Set` della proprietà.  
  
 Se l'[Set Statement](../../../visual-basic/language-reference/statements/set-statement.md) è contrassegnata con un livello di accesso più restrittivo dell'[Property Statement](../../../visual-basic/language-reference/statements/property-statement.md), il tentativo di impostare il valore della proprietà potrebbe avere esito negativo nei casi seguenti:  
  
-   L'istruzione `Set` è contrassegnata come [Private](../../../visual-basic/language-reference/modifiers/private.md) e il codice chiamante è esterno alla classe o alla struttura in cui la proprietà è definita.  
  
-   L'istruzione `Set` è contrassegnata come [Protected](../../../visual-basic/language-reference/modifiers/protected.md) e il codice chiamante non è incluso nella classe o nella struttura in cui la proprietà è definita, né in una classe derivata.  
  
-   L'istruzione `Set` è contrassegnata come [Friend](../../../visual-basic/language-reference/modifiers/friend.md) e il codice chiamante non è incluso nello stesso assembly in cui la proprietà è definita.  
  
 **ID errore:** BC31102  
  
### Per correggere l'errore  
  
-   Se si ha la possibilità di intervenire sul codice sorgente che definisce la proprietà, valutare l'ipotesi di dichiarare la routine `Set` con lo stesso livello di accesso della proprietà.  
  
-   Se non si ha la possibilità di intervenire sul codice sorgente che definisce la proprietà, o se è necessario limitare il livello di accesso della routine `Set` più di quello della proprietà stessa, provare a spostare l'istruzione che permette di impostare il valore della proprietà in un'area del codice che offre un accesso migliore alla proprietà.  
  
## Vedere anche  
 [Routine Property](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)