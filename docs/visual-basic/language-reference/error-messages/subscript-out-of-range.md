---
title: "Subscript out of range (Visual Basic) | Microsoft Docs"
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
  - "vbrID9"
dev_langs: 
  - "VB"
ms.assetid: d0344a65-ec02-4caf-8d3c-9977392ca353
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Subscript out of range (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'indice di matrice non è valido perché non rientra nell'intervallo consentito.  Il valore di indice più basso per una dimensione è sempre 0 e il valore di indice massimo viene restituito dal metodo `GetUpperBound` per tale dimensione.  
  
### Per correggere l'errore  
  
-   Cambiare l'indice in modo che rientri nell'intervallo valido.  
  
## Vedere anche  
 <xref:System.Array.GetUpperBound%2A?displayProperty=fullName>   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)