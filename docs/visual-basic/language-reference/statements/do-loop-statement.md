---
title: "Do...Loop Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Do"
  - "vb.Loop"
  - "vb.Until"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "conditional statements, Do…Loop"
  - "while statement, Do...Loop"
  - "execution, conditional"
  - "Do loops"
  - "Until keyword, Do...Loop statement"
  - "Do...Loop statement"
  - "instructions, repeating"
  - "Do statement"
  - "Exit statement, in Do...Loop statements"
  - "loop structures, Do…Loop statements"
  - "do-while statements"
  - "loops, exiting"
  - "Loop keyword, Do...Loop statement"
ms.assetid: 892f9096-b3e2-4aee-834d-83bc4e2c379d
caps.latest.revision: 37
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 37
---
# Do...Loop Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di ripetere un blocco di istruzioni fino a quando una condizione `Boolean` resta `True` o non diventa `True`.  
  
## Sintassi  
  
```  
Do { While | Until } condition  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop  
-or-  
Do  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop { While | Until } condition  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`Do`|Necessario.  Consente di avviare la definizione del ciclo `Do`.|  
|`While`|Obbligatoria a meno che non venga utilizzato `Until`.  Ripetere il ciclo finché `condition` è `False`.|  
|`Until`|Obbligatoria a meno che non venga utilizzato `While`.  Ripetere il ciclo finché `condition` è `True`.|  
|`condition`|Opzionale.  Espressione `Boolean`.  Se la `condition` è `Nothing`, Visual Basic la considera `False`.|  
|`statements`|Opzionale.  Una o più istruzioni ripetute finché la valutazione di `condition` resta o non diventa `True`.|  
|`Continue Do`|Opzionale.  Trasferisce il controllo all'iterazione successiva del ciclo `Do`.|  
|`Exit Do`|Opzionale.  Trasferisce il controllo al di fuori del ciclo `Do`.|  
|`Loop`|Necessario.  Consente di terminare la definizione del ciclo `Do`.|  
  
## Note  
 Utilizzare una struttura `Do...Loop` per ripetere un insieme di istruzioni un numero indefinito di volte, finché non viene soddisfatta una condizione.  Se si desidera ripetere le istruzioni un numero determinato di volte, in genere è più indicata l'[istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md).  
  
 È possibile utilizzare `While` o `Until` per specificare il parametro `condition`, ma non entrambi.  
  
 È possibile testare l'espressione `condition` soltanto una volta, all'inizio o alla fine del ciclo.  Se si esegue il test di `condition` all'inizio del ciclo \(nell'istruzione `Do`\), è possibile che il ciclo non venga eseguito nemmeno una volta.  Se si esegue il test alla fine del ciclo \(nell'istruzione `Loop`\), il ciclo viene sempre eseguito almeno una volta.  
  
 La condizione è in genere il risultato di un confronto tra due valori, ma può anche essere una qualsiasi espressione che restituisca un valore [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md) \(`True` o `False`\).  Sono compresi i valori di altri tipi di dati, come i tipi numerici, convertiti in `Boolean`.  
  
 È possibile annidare cicli `Do` inserendo un ciclo all'interno dell'altro.  È inoltre possibile annidare strutture di controllo di tipo diverso inserendole una all'interno dell'altra.  Per ulteriori informazioni, vedere [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
> [!NOTE]
>  La struttura `Do...Loop` offre maggiore flessibilità rispetto alla struttura [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md) in quanto consente di decidere se terminare il ciclo nel momento in cui il valore di `condition` non è più `True` oppure quando diventa `True` per la prima volta.  La struttura consente inoltre di verificare la `condition` all'inizio o alla fine del ciclo.  
  
## Exit Do  
 L'istruzione [Exit Do](../../../visual-basic/language-reference/statements/exit-statement.md) consente di fornire un modo alternativo per uscire da un ciclo `Do…Loop`.  Tramite l'istruzione `Exit Do` il controllo viene trasferito immediatamente all'istruzione che segue l'istruzione `Loop`.  
  
 L'istruzione `Exit Do` spesso viene utilizzata dopo la valutazione di una determinata condizione, ad esempio in una struttura `If...Then...Else`.  È possibile uscire da un ciclo se si rileva una condizione che rende inutile o impossibile continuare a scorrere, quale un valore erroneo o una richiesta di interruzione.  L'istruzione `Exit Do` può essere utilizzata per eseguire un controllo su una condizione tramite la quale potrebbe essere generato un *ciclo infinito*, vale a dire un ciclo che potrebbe essere eseguito per un numero di volte elevato o persino infinito.  È possibile utilizzare il controllo `Exit Do` per uscire dal ciclo.  
  
 È possibile inserire un numero illimitato di istruzioni `Exit Do` in qualsiasi punto di un ciclo `Do…Loop`.  
  
 Se utilizzata all'interno di cicli `Do` annidati, l'istruzione `Exit Do` consente il trasferimento del controllo dal ciclo più interno al livello di annidamento successivo superiore.  
  
## Esempio  
 Nell'esempio seguente l'esecuzione delle istruzioni nel ciclo continua finché la variabile `index` non risulta maggiore di 10.  La clausola `Until` si trova alla fine del ciclo.  
  
 [!code-vb[VbVbalrStatements#131](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/do-loop-statement_1.vb)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzata una clausola `While` invece di una clausola `Until` e viene eseguito il test `condition` all'inizio del ciclo invece che alla fine.  
  
 [!code-vb[VbVbalrStatements#132](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/do-loop-statement_2.vb)]  
  
## Esempio  
 Nell'esempio seguente, il ciclo viene interrotto da `condition` quando la variabile `index` è maggiore di 100.  Tramite l'istruzione `If` nel ciclo, tuttavia, viene causata l'interruzione del ciclo mediante l'istruzione `Exit Do` quando la variabile di indice è maggiore di 10.  
  
 [!code-vb[VbVbalrStatements#133](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/do-loop-statement_3.vb)]  
  
## Esempio  
 Nell'esempio seguente vengono lette tutte le righe di un file di testo.  Il file viene aperto tramite il metodo <xref:System.IO.File.OpenText%2A>, mediante il quale viene restituito un oggetto <xref:System.IO.StreamReader> che consente la lettura dei caratteri.  Nella condizione `Do...Loop`, tramite il metodo <xref:System.IO.StreamReader.Peek%2A> dell'oggetto `StreamReader` viene determinato se sono presenti eventuali caratteri aggiuntivi.  
  
 [!code-vb[VbVbalrStatements#134](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/do-loop-statement_4.vb)]  
  
## Vedere anche  
 [Loop Structures](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md)