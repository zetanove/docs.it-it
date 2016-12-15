---
title: "&#39;Get&#39; accessor of property &#39;&lt;propertyname&gt;&#39; is not accessible | Microsoft Docs"
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
  - "vbc31103"
  - "bc31103"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31103"
ms.assetid: 3c346c32-7669-4b04-841d-7a9df9cb703e
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Get&#39; accessor of property &#39;&lt;propertyname&gt;&#39; is not accessible
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'istruzione tenta di recuperare il valore di una proprietà quando non ha accesso alla routine `Get` della proprietà stessa.  
  
 Se [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md) è contrassegnata con un livello di accesso più restrittivo della relativa [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md), il tentativo di leggere il valore della proprietà potrebbe non riuscire nei seguenti casi:  
  
-   l'istanza `Get` è contrassegnata come [Private](../../../visual-basic/language-reference/modifiers/private.md) e il codice chiamante è esterno alla classe o alla struttura nella quale viene definita la proprietà;  
  
-   l'istanza `Get` è contrassegnata come [Protected](../../../visual-basic/language-reference/modifiers/protected.md) e il codice chiamante non si trova nella classe o nella struttura nella quale viene definita la proprietà né in una classe derivata;  
  
-   l'istanza `Get` è contrassegnata come [Friend](../../../visual-basic/language-reference/modifiers/friend.md) e il codice chiamante non si trova nello stesso assembly nel quale viene definita la proprietà.  
  
 **ID errore:** BC31103  
  
### Per correggere l'errore  
  
-   Se è possibile accedere al codice sorgente che definisce la proprietà, dichiarare la routine `Get` con lo stesso livello di accesso della proprietà stessa.  
  
-   Se non è possibile accedere al codice sorgente che definisce la proprietà o se è necessario limitare il livello di accesso della routine `Get` più della proprietà stessa, spostare l'istruzione che legge il valore della proprietà in un'area del codice da cui si possa accedere alla proprietà.  
  
## Vedere anche  
 [Routine Property](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)