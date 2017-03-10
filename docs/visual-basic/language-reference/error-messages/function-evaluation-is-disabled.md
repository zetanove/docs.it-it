---
title: "Function evaluation is disabled because a previous function evaluation timed out | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30957"
  - "vbc30957"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30957"
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# Function evaluation is disabled because a previous function evaluation timed out
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Valutazione della funzione disabilitata a causa del timeout di una valutazione di funzione precedente.Per riattivare la valutazione della funzione, eseguire nuovamente la funzione o riavviare il debug.  
  
 Nel debugger di Visual Studio, un'espressione specifica una chiamata di routine, ma di è verificato il timeout di un'altra valutazione.  
  
 Fra le possibili cause del timeout di una chiamata di routine sono compresi un ciclo infinito o *ciclo senza termine*.  Per ulteriori informazioni, vedere [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md).  
  
 Un caso particolare di ciclo infinito è la *ricorsione*.  Per ulteriori informazioni, vedere [Recursive Procedures](../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md).  
  
 **ID errore:** BC30957  
  
### Per correggere l'errore  
  
1.  Se possibile, determinare qual era la valutazione di funzione precedente e che cosa ne ha causato il timeout;  in caso contrario, è possibile che l'errore si verifichi nuovamente.  
  
2.  Ripetere l'operazione tentata dal debugger oppure arrestare e riavviare il debug.  
  
## Vedere anche  
 [Debug in Visual Studio](/visual-studio/debugger/debugging-in-visual-studio)   
 [Spostarsi nel codice con il Debugger](/visual-studio/debugger/navigating-through-code-with-the-debugger)   
 [Espressioni in linguaggio Visual Basic](../Topic/Expressions%20in%20Visual%20Basic.md)