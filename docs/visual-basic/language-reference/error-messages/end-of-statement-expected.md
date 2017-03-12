---
title: "Prevista fine dell&#39;istruzione | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30205"
  - "vbc30205"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30205"
ms.assetid: 53c7f825-a737-4b76-a1fa-f67745b8bd40
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# Prevista fine dell&#39;istruzione
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'istruzione è completa, da punto di vista sintattico, ma l'elemento che la compila è seguito da un elemento di programmazione supplementare.  Al termine di ogni istruzione è richiesto un terminatore di riga.  
  
 Un terminatore di riga divide i caratteri di un file di origine Visual Basic righe.  Esempi di terminatori di riga rappresentano il carattere di ritorno a capo Unicode \(&HD\), il carattere di avanzamento riga Unicode \(&HA\) e un carattere di ritorno a capo Unicode seguito dal carattere di avanzamento riga Unicode.  Per ulteriori informazioni sui terminatori di riga, vedere [Visual Basic Language Specification](../../../visual-basic/reference/language-specification.md)\).  
  
 **ID errore:** BC30205  
  
### Per correggere l'errore  
  
1.  Controllare se, per errore, sono state inserite due istruzioni diverse nella stessa riga.  
  
2.  Inserire un terminatore di riga dopo l'elemento che completa l'istruzione.  
  
## Vedere anche  
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)