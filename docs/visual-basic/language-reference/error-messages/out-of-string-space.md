---
title: "Out of string space (Visual Basic) | Microsoft Docs"
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
  - "vbrID14"
dev_langs: 
  - "VB"
ms.assetid: 16681c75-a400-422d-9351-c691d3c7614e
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Out of string space (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In Visual Basic è possibile utilizzare stringhe di dimensioni considerevoli.  Questo errore può essere tuttavia generato dalle richieste di altri programmi e dal modo in cui le stringhe vengono utilizzate.  
  
### Per correggere l'errore  
  
1.  Controllare che un'espressione che richiede la creazione di stringhe temporanee durante la valutazione non sia la causa dell'errore.  
  
2.  Rimuovere dalla memoria le applicazioni non necessarie per liberare spazio.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [String Manipulation Summary](../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)