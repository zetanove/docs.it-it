---
title: "Too many files | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID67"
dev_langs: 
  - "VB"
ms.assetid: 2ff203e2-bba6-43ae-b72f-8e92a881c98f
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Too many files
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il numero di file creati nella directory radice è superiore a quello permesso dal sistema operativo, oppure sono stati aperti più file di quanto specificato per **files\=** nel file CONFIG.SYS.  
  
### Per correggere l'errore  
  
1.  Se il programma sta aprendo, chiudendo o salvando file nella directory radice, cambiarlo in modo che utilizzi una sottodirectory.  
  
2.  Aumentare il numero di file specificato per l'impostazione **files\=** nel file CONFIG.SYS e riavviare il computer.  
  
## Vedere anche  
 [Error Types](../../../visual-basic/programming-guide/language-features/error-types.md)