---
title: "Leading &#39;.&#39; or &#39;!&#39; can only appear inside a &#39;With&#39; statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30157"
  - "bc30157"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30157"
ms.assetid: 70daaee1-14f9-45b7-9f30-53794310b95e
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Leading &#39;.&#39; or &#39;!&#39; can only appear inside a &#39;With&#39; statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È presente un punto \(.\) o un punto esclamativo \(\!\) al di fuori di un blocco `With` senza un'espressione a sinistra.  L'accesso ai membri \(`.`\) e l'accesso ai membri dizionario \(`!`\) richiedono un'espressione che specifichi l'elemento che contiene il membro.  L'espressione deve trovarsi subito a sinistra della funzione di accesso oppure deve essere la destinazione di un blocco `With` contenente l'accesso al membro.  
  
 **ID errore:** BC30157  
  
### Per correggere l'errore  
  
1.  Assicurarsi che la formattazione del blocco `With` sia corretta.  
  
2.  Se non esiste alcun blocco `With`, aggiungere un'espressione a sinistra della funzione di accesso che restituisce un elemento definito contenente il membro.  
  
## Vedere anche  
 [Special Characters in Code](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)   
 [With...End With Statement](../../../visual-basic/language-reference/statements/with-end-with-statement.md)