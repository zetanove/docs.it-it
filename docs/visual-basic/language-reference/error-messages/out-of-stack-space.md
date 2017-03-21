---
title: (Visual Basic) di spazio dello stack | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID28
dev_langs:
- VB
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
caps.latest.revision: 8
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6343767da28ea4e02f9443006b222640755f7882
ms.lasthandoff: 03/13/2017

---
# <a name="out-of-stack-space-visual-basic"></a>Spazio dello stack insufficiente (Visual Basic)
Lo stack è un'area di lavoro di memoria aumenta e si riduce in modo dinamico alle richieste del programma in esecuzione. I limiti sono stati superati.  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Verificare che le procedure non sono eccessivamente annidate.  
  
2.  Assicurarsi che le routine ricorsive terminino correttamente.  
  
3.  Se le variabili locali richiedono uno spazio più a quello disponibile, provare a dichiarare alcune variabili a livello di modulo. È inoltre possibile dichiarare tutte le variabili nella procedura static facendo precedere il `Property`, `Sub`, o `Function` parola chiave with `Static`. Oppure è possibile utilizzare il `Static` istruzione per dichiarare variabili static individuali all'interno delle procedure.  
  
4.  Ridefinire alcune delle stringhe a lunghezza fissa come stringhe a lunghezza variabile, come stringhe a lunghezza fissa utilizzino più spazio di stack di stringhe a lunghezza variabile. È inoltre possibile definire la stringa a livello di modulo in cui richiede nessuno spazio dello stack.  
  
5.  Verificare il numero di nidificata `DoEvents` chiamate di funzioni, utilizzando il `Calls` la finestra di dialogo per visualizzare le routine attive nello stack.  
  
6.  Assicurarsi che non si ha provocato una cascata di"eventi" generando un evento che chiama una routine evento già nello stack. Una cascata di eventi è simile a una chiamata di routine ricorsiva non terminata, ma è meno ovvio, poiché la chiamata viene effettuata da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] invece di una chiamata esplicita nel codice. Utilizzare il `Calls`la finestra di dialogo per visualizzare le routine attive nello stack.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra Memoria](https://docs.microsoft.com/visualstudio/debugger/memory-windows)
