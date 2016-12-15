---
title: "Statement is not valid inside a method/multiline lambda | Microsoft Docs"
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
  - "vbc30024"
  - "bc30024"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30024"
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Statement is not valid inside a method/multiline lambda
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'istruzione non è valida all'interno di una routine `Sub` o `Function` oppure all'interno di una routine della proprietà `Get` o `Set`.  Alcune istruzioni possono essere inserite a livello di modulo o di classe.  Altre, ad esempio `Option Strict`, devono essere inserite a livello di spazio dei nomi e precedere qualsiasi altra dichiarazione.  
  
 **ID errore:** BC30024  
  
### Per correggere l'errore  
  
-   Rimuovere l'istruzione dalla routine.  
  
## Vedere anche  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set Statement](../../../visual-basic/language-reference/statements/set-statement.md)