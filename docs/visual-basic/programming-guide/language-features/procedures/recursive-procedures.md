---
title: Routine ricorsive (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, procedures
- procedures, that call themselves
- procedures, recursive
- procedures, calling
- recursive procedures
- functions [Visual Basic], calling recursively
- recursion
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
caps.latest.revision: 13
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 9fc95cd5f7cfd5637f6282c6ef571eb81bac1816
ms.lasthandoff: 03/13/2017

---
# <a name="recursive-procedures-visual-basic"></a>Routine ricorsive (Visual Basic)
Oggetto *ricorsiva* procedura è quella che chiama se stesso. In generale, questo non è il modo più efficace per scrivere [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] codice.  
  
 La procedura seguente utilizza la ricorsione per calcolare il fattoriale del relativo argomento originale.  
  
 [!code-vb[51 VbVbcnProcedures](./codesnippet/VisualBasic/recursive-procedures_1.vb)]  
  
## <a name="considerations-with-recursive-procedures"></a>Considerazioni sulle routine ricorsive  
 **Le condizioni di limitazione**. È necessario progettare una routine ricorsiva per verificare se almeno una condizione in grado di terminare la ricorsione ed è necessario gestire anche nel caso in cui tale condizione non viene soddisfatta entro un numero ragionevole di chiamate ricorsive. Senza almeno una condizione che può essere soddisfatta senza errori, la routine esegue un elevato rischio di esecuzione in un ciclo infinito.  
  
 **Utilizzo della memoria**. L'applicazione dispone di una quantità limitata di spazio per le variabili locali. Ogni volta che una routine chiama se stessa, utilizza una quantità di spazio per le copie aggiuntive delle variabili locali. Se questo processo continua in modo indefinito, provoca un <xref:System.StackOverflowException>errore.</xref:System.StackOverflowException>  
  
 **Efficienza**. È quasi sempre possibile sostituire un ciclo per la ricorsione. Un ciclo non hanno il sovraccarico del passaggio di argomenti, l'inizializzazione di ulteriore spazio di archiviazione e la restituzione di valori. Le prestazioni migliorano in modo significativo senza chiamate ricorsive.  
  
 **Ricorsione reciproca**. È possibile osservare molto scarse prestazioni, o anche un ciclo infinito, se due procedure comunicano tra loro. Tale progettazione presenta gli stessi problemi come una singola routine ricorsiva, ma può essere difficile rilevare ed eseguire il debug.  
  
 **La chiamata con parentesi**. Quando un `Function` routine chiama se stessa in modo ricorsivo, è necessario seguire il nome della routine tra parentesi, anche se non esiste alcun elenco di argomenti. In caso contrario, il nome della funzione viene eseguito come che rappresenta il valore restituito della funzione.  
  
 **Test**. Se si scrive una routine ricorsiva, è necessario eseguirne il test con molta attenzione per assicurarsi che soddisfi sempre alcune condizioni di limitazione. È inoltre necessario assicurarsi che non è possibile eseguire esaurito la memoria a causa di un numero eccessivo di chiamate ricorsive.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.StackOverflowException></xref:System.StackOverflowException>   
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Routine di funzione](./function-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Overload di routine](./procedure-overloading.md)   
 [Le procedure di risoluzione](./troubleshooting-procedures.md)   
 [Cicli (strutture)](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Risoluzione dei problemi relativi ad eccezioni: System.StackOverflowException](http://msdn.microsoft.com/library/51b71217-c507-4f5b-bc35-0236180d7968)
