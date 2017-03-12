---
title: "Out of stack space (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID28"
dev_langs: 
  - "VB"
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Out of stack space (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Lo stack è un'area di lavoro della memoria le cui dimensioni aumentano e si riducono dinamicamente in base alle richieste del programma in esecuzione.  I suoi limiti sono stati superati.  
  
### Per correggere l'errore  
  
1.  Assicurarsi che le routine non siano eccessivamente annidate.  
  
2.  e che le routine ricorsive terminino in modo appropriato.  
  
3.  Se le variabili locali richiedono uno spazio superiore a quello disponibile, provare a dichiarare alcune variabili a livello di modulo.  È anche possibile dichiarare come statiche tutte le variabili della routine inserendo `Static` come prefisso davanti alla parola chiave `Property`, `Sub` o `Function`,  oppure utilizzare l'istruzione `Static` per dichiarare variabili Static individuali all'interno delle routine.  
  
4.  Ridefinire alcune delle stringhe a lunghezza fissa come stringhe a lunghezza variabile, poiché le stringhe a lunghezza fissa richiedono più spazio nello stack rispetto a quelle a lunghezza variabile.  È anche possibile definire la stringa a livello di modulo, dove non richiede spazio dello stack.  
  
5.  Verificare il numero di chiamate annidate alla funzione `DoEvents` utilizzando la finestra di dialogo `Calls` per visualizzare le routine attive nello stack.  
  
6.  Assicurarsi di non aver generato una cascata di eventi generando un evento che chiama una routine evento già presente nello stack.  Una cascata di eventi è simile a una chiamata a una routine ricorsiva non terminata, ma risulta meno ovvia, poiché la chiamata viene effettuata da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], non da una chiamata esplicita nel codice.  Utilizzare la finestra di dialogo `Calls`per visualizzare le routine attive nello stack.  
  
## Vedere anche  
 [Finestra Memoria](/visual-studio/debugger/memory-windows)