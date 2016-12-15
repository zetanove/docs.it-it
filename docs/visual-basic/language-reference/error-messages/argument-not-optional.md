---
title: "Argument not optional (Visual Basic) | Microsoft Docs"
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
  - "vbrID449"
dev_langs: 
  - "VB"
ms.assetid: 76e7bcf3-24ed-4cd5-945b-b98f1c76944b
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Argument not optional (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È necessario che gli argomenti corrispondano per numero e tipo a quelli previsti.  È stato specificato un numero di argomenti non corretto o uno degli argomenti omessi non è facoltativo.  È possibile omettere un argomento da una chiamata a una routine definita dall'utente solo se tale argomento è stato dichiarato `Optional` nella definizione della routine.  
  
### Per correggere l'errore  
  
1.  Fornire tutti gli argomenti necessari.  
  
2.  Assicurarsi che gli argomenti omessi siano facoltativi.  In caso contrario, fornire l'argomento nella chiamata o dichiarare il parametro `Optional` nella definizione.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)