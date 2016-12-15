---
title: "Bad DLL calling convention | Microsoft Docs"
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
  - "vbrID49"
dev_langs: 
  - "VB"
ms.assetid: 7c7def45-b0ab-450f-ad3f-4383dfd9aed7
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Bad DLL calling convention
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli argomenti passati a una libreria a collegamento dinamico \(DLL\) devono corrispondere esattamente a quelli previsti dalla routine.  Le convenzioni di chiamata riguardano il numero, il tipo e l'ordine degli argomenti.  Forse il programma chiama una routine in una DLL a cui viene passato un tipo o un numero di argomenti errato.  
  
### Per correggere l'errore  
  
1.  Controllare che tutti i tipi di argomento corrispondano a quelli specificati nella dichiarazione della routine che si sta chiamando.  
  
2.  Controllare che il numero di argomenti che si stanno passando corrisponda a quanto indicato nella dichiarazione della routine che si sta chiamando.  
  
3.  Se la routine della DLL si aspetta argomenti in base al valore, accertarsi che nella dichiarazione della routine sia specificato per essi `ByVal`.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Call Statement](../../../visual-basic/language-reference/statements/call-statement.md)   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)