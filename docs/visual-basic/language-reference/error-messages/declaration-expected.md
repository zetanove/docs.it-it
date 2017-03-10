---
title: "Declaration expected | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30188"
  - "bc30188"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30188"
ms.assetid: da6b1df3-fe6b-4415-88e6-0977e5189e0b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Declaration expected
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'istruzione non dichiarativa, ad esempio un'istruzione di assegnazione o ciclo, si trova al di fuori di una routine.  Solo le dichiarazioni possono trovarsi al di fuori delle routine.  
  
 In alternativa, un elemento di programmazione è dichiarato senza una parola chiave di dichiarazione quale ad esempio `Dim` o `Const`.  
  
 **ID errore:** BC30188  
  
### Per correggere l'errore  
  
-   Spostare l'istruzione non dichiarativa nel corpo di una routine.  
  
-   Iniziare la dichiarazione con una parola chiave di dichiarazione appropriata.  
  
-   Controllare che la parola chiave di dichiarazione sia scritta correttamente.  
  
## Vedere anche  
 [Procedures](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)