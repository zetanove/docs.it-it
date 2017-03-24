---
title: "Can&#39;t create necessary temporary file | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID322"
dev_langs: 
  - "VB"
ms.assetid: 53617b5b-eb06-4188-b4c2-8607cb9fbc79
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Can&#39;t create necessary temporary file
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'unità contenente la directory specificata dalla variabile di ambiente TEMP è piena, oppure questa variabile specifica un'unità o una directory non valida o in sola lettura.  
  
### Per correggere l'errore  
  
1.  Se l'unità è piena, eliminare dei file.  
  
2.  Specificare un'unità diversa nella variabile di ambiente TEMP.  
  
3.  Specificare un'unità valida per la variabile di ambiente TEMP.  
  
4.  Rimuovere la restrizione di sola lettura dall'unità o dalla directory specificata correntemente.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)