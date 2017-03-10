---
title: "Events of shared WithEvents variables cannot be handled by non-shared methods | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30594"
  - "vbc30594"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30594"
ms.assetid: 5b9fceb4-ab11-41bb-ad3b-6f1a9da8ae7e
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Events of shared WithEvents variables cannot be handled by non-shared methods
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una variabile condivisa è una variabile dichiarata con il modificatore `Shared` che identifica in modo preciso una posizione di archiviazione.  Una variabile dichiarata con il modificatore `WithEvents` asserisce che il tipo a cui appartiene gestisce gli eventi da essa generati.  Quando alla variabile viene assegnato un valore, la proprietà creata dalla dichiarazione `WithEvents` disconnette qualsiasi gestore eventi esistente e connette il nuovo gestore tramite il metodo `Add`.  
  
 **ID errore:** BC30594  
  
### Per correggere l'errore  
  
-   Dichiarare il gestore eventi `Shared`.  
  
## Vedere anche  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)