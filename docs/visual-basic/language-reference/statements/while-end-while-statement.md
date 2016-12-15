---
title: "While...End While Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.While"
  - "vb.While...EndWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "While statement, While...End While"
  - "While statement"
  - "While...End While statements"
ms.assetid: b931d1ce-e8ed-44d8-a13d-92a4f5458a1e
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# While...End While Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di eseguire una serie di istruzioni purché la condizione sia `True`.  
  
## Sintassi  
  
```  
While condition  
    [ statements ]  
    [ Continue While ]  
    [ statements ]  
    [ Exit While ]  
    [ statements ]  
End While  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`condition`|Necessario.  Espressione `Boolean`.  Se la `condition` è `Nothing`, Visual Basic la considera `False`.|  
|`statements`|Opzionale.  Una o più istruzioni basate su `While`, eseguite ogni volta che `condition` è `True`.|  
|`Continue While`|Opzionale.  Trasferisce il controllo all'iterazione successiva del blocco `While`.|  
|`Exit While`|Opzionale.  Trasferisce il controllo all'esterno del blocco `While`.|  
|`End While`|Necessario.  Termina la definizione del blocco `While`.|  
  
## Note  
 Utilizzare una struttura `While...End While` quando si desidera ripetere un gruppo di iistruzioni un numero infinito di volte, fino a quando la condizione rimane `True`.  Se si desidera una maggiore flessibilità su dove verificare la condizione o per quale risultato si esegue il test, è possibile scegliere l'[Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md).  Per ripetere le istruzioni un numero di volte definito, l' [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md) costituisce generalmente una scelta migliore.  
  
> [!NOTE]
>  La parola chiave `While` viene utilizzata anche nell'[Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md), nella [Skip While Clause](../../../visual-basic/language-reference/queries/skip-while-clause.md) e nella [Take While Clause](../../../visual-basic/language-reference/queries/take-while-clause.md).  
  
 Se `condition` è `True`, tutte le `statements` vengono eseguite fino a quando non viene rilevata l'istruzione `End While`.  Il controllo torna quindi all'istruzione `While` e `condition` viene controllato di nuovo.  Se `condition` è ancora `True`, il processo verrà ripetuto.  Se è `False`, il controllo passa all'istruzione che segue l'istruzione `End While`.  
  
 L'istruzione `While` verifica sempre la condizione prima di avviare il ciclo.  Il looping continua mentre la condizione rimane `True`.  Se `condition` è `False` quando è attivato il ciclo, non funziona anche una volta.  
  
 `condition` in genere il risultato di un confronto tra due valori, ma può essere qualsiasi espressione che restituisca a [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md) un valore \(`True` o `False`\).  L'espressione può includere un valore di un altro tipo di dati, come un tipo numerico, che è stato convertito in `Boolean`.  
  
 È possibile annidare cicli `While` inserendo un ciclo all'interno di un altro.  È inoltre possibile annidare strutture di controllo di tipo diverso inserendone una all'interno di un altra.  Per ulteriori informazioni, vedere [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
## Mentre uscita  
 L'istruzione [Mentre uscita](../../../visual-basic/language-reference/statements/exit-statement.md) può fornire un altro modo per uscire da un ciclo `While`.  Di`Exit While` trasferisce il controllo immediatamente all'istruzione che segue l'istruzione `End While`.  
  
 In genere si utilizza `Exit While` dopo che una condizione verrà valutata, ad esempio in una struttura `If...Then...Else` \).  È possibile uscire da un ciclo se si rileva una condizione che rende inutile o impossibile continuare a scorrere, quale un valore erroneo o una richiesta di interruzione.  È possibile utilizzare `Exit While` quando si testano per una condizione che potrebbe causare *un ciclo infinito*, un ciclo che potrebbe richiedere un numero di volte estremamente grande o addirittura infinito.  È quindi possibile utilizzare `Exit While` per utilizzare caratteri di escape il ciclo.  
  
 È possibile inserire un numero illimitato di istruzioni `Exit While` in qualsiasi punto del ciclo `While`.  
  
 Se utilizzata all'interno di cicli `While` annidati, l'istruzione `Exit While` consente il trasferimento del controllo dal ciclo più interno al livello di annidamento successivo superiore.  
  
 Di `Continue While` di istruzione del controllo trasferisce immediatamente all'iterazione successiva del ciclo.  Per ulteriori informazioni, vedere [Continue Statement](../../../visual-basic/language-reference/statements/continue-statement.md).  
  
## Esempio  
 Nell'esempio seguente l'esecuzione delle istruzioni nel ciclo continua finché la variabile `index` non risulta maggiore di 10.  
  
 [!code-vb[VbVbalrStatements#171](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_1.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo delle istruzioni `Continue While` e `Exit While`.  
  
 [!code-vb[VbVbalrStatements#172](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_2.vb)]  
  
## Esempio  
 Nell'esempio seguente vengono lette tutte le righe di un file di testo.  Il file viene aperto tramite il metodo <xref:System.IO.File.OpenText%2A>, mediante il quale viene restituito un oggetto <xref:System.IO.StreamReader> che consente la lettura dei caratteri.  Lo stato `While`, il metodo <xref:System.IO.StreamReader.Peek%2A>`StreamReader` determina se il file contiene caratteri aggiuntivi.  
  
 [!code-vb[VbVbalrStatements#173](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_3.vb)]  
  
## Vedere anche  
 [Loop Structures](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Continue Statement](../../../visual-basic/language-reference/statements/continue-statement.md)