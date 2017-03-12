---
title: "Array subscript expression missing | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30306"
  - "vbc30306"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30306"
ms.assetid: 3c0d9732-ee37-436f-a1df-29d65712f48a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Array subscript expression missing
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'inizializzazione di una matrice omette uno o più indici che ne definiscono i limiti.  L'istruzione, ad esempio, potrebbe contenere l'espressione `myArray (5,5,,10)`, che omette il terzo indice.  
  
 **ID errore:** BC30306  
  
### Per correggere l'errore  
  
-   Fornire l'indice mancante.  
  
## Vedere anche  
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)