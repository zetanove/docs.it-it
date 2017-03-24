---
title: "Statement is not valid inside a method/multiline lambda | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30024"
  - "bc30024"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30024"
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Statement is not valid inside a method/multiline lambda
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'istruzione non è valida all'interno di una routine `Sub` o `Function` oppure all'interno di una routine della proprietà `Get` o `Set`.  Alcune istruzioni possono essere inserite a livello di modulo o di classe.  Altre, ad esempio `Option Strict`, devono essere inserite a livello di spazio dei nomi e precedere qualsiasi altra dichiarazione.  
  
 **ID errore:** BC30024  
  
### Per correggere l'errore  
  
-   Rimuovere l'istruzione dalla routine.  
  
## Vedere anche  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set Statement](../../../visual-basic/language-reference/statements/set-statement.md)