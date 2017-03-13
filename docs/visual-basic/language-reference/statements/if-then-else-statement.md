---
title: "If...Then...Else Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ElseIf"
  - "vb.Then"
  - "vb.If"
  - "vb.EndIf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ElseIf statement, If...Then...Else"
  - "Then statement, If...Then...Else"
  - "control flow, branching"
  - "execution, conditional"
  - "TypeOf...Is expression, and If...Then...Else statements"
  - "If...Then...Else statements"
  - "If statement, If...Then...Else"
  - "If statement"
  - "Is operator [Visual Basic], in If...Then...Else statements"
  - "If Operator [Visual Basic]"
  - "branching, conditional"
  - "IIf function, and If...Then...Else statements"
  - "Else statement [Visual Basic]"
ms.assetid: 790068a2-1307-4e28-8a72-be5ebda099e9
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# If...Then...Else Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue un gruppo di istruzioni in base a determinate condizioni, a seconda del valore di un espressione.  
  
## Sintassi  
  
```  
' Multiple-line syntax:  
If condition [ Then ]  
    [ statements ]  
[ ElseIf elseifcondition [ Then ]  
    [ elseifstatements ] ]  
[ Else  
    [ elsestatements ] ]  
End If  
  
' Single-line syntax:  
If condition Then [ statements ] [ Else [ elsestatements ] ]  
```  
  
## Parti  
 `condition`  
 Necessario.  Espressione.  Deve restituire `True` o `False` oppure un tipo di dati convertibile in modo implicito in `Boolean`.  
  
 Se l'espressione è una variabile [Nullable](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)`Boolean` che restituisce [Niente](../../../visual-basic/language-reference/nothing.md), la condizione viene considerata come se l'espressione non sia `True`e il blocco `Else` viene eseguito.  
  
 `Then`  
 Obbligatoria nella sintassi a riga singola, facoltativa in quella a più righe.  
  
 `statements`  
 Opzionale.  Una o più istruzioni successive a `If`...`Then` che vengono eseguite se `condition` restituisce `True`.  
  
 `elseifcondition`  
 Obbligatoria se è presente `ElseIf`.  Espressione.  Deve restituire `True` o `False` oppure un tipo di dati convertibile in modo implicito in `Boolean`.  
  
 `elseifstatements`  
 Opzionale.  Una o più istruzioni successive a `ElseIf`...`Then` che vengono eseguite se `elseifcondition` restituisce `True`.  
  
 `elsestatements`  
 Opzionale.  Una o più istruzioni eseguite se nessuna delle espressioni `condition` o `elseifcondition` precedenti restituisce `True`.  
  
 `End If`  
 Termina il blocco `If`...`Then`...`Else`.  
  
## Note  
  
## Sintassi a più righe  
 Quando viene rilevata un'istruzione `If`...`Then`...`Else`, l'espressione `condition` viene testata.  Se `condition` è `True`, verranno eseguite le istruzioni successive a `Then`,  Se `condition` è `False`, ogni istruzione `ElseIf` \(se presenti\) viene valutata seguendo un ordine.  Quando viene rilevata una parte `elseifcondition` che restituisce `True`, verranno eseguite le istruzioni immediatamente successive all'istruzione `ElseIf` associata.  Se nessuna parte `elseifcondition` restituisce `True`, o se non vi sono istruzioni `ElseIf`, verranno eseguite le istruzioni successive a `Else`.  Dopo l'esecuzione delle istruzioni successive a `Then`, `ElseIf` o `Else`, l'esecuzione procede con l'istruzione successiva all'istruzione `End If`.  
  
 Le clausole `ElseIf` e `Else` sono entrambe facoltative.  Il numero di clausole `ElseIf` consentito in un'istruzione `If`...`Then`...`Else` è illimitato, a condizione che nessuna clausola `ElseIf` venga visualizzata dopo la clausola `Else`.  Le istruzioni `If`...`Then`...`Else` possono essere annidate una all'interno dell'altra.  
  
 Nella sintassi a più righe, l'istruzione `If` deve essere l'unica istruzione sulla prima riga.  Le istruzioni `ElseIf`, `Else` e `End If` possono essere precedute solo da un'etichetta di riga.  È necessario che il blocco `If`...`Then`...`Else` termini con un'istruzione `End If`.  
  
> [!TIP]
>  L'istruzione [Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md) potrebbe essere più utile quando viene valutata una sola espressione con diversi valori possibili.  
  
## Sintassi a riga singola  
 È possibile utilizzare la sintassi a riga singola per testi brevi e semplici.  Tuttavia, la struttura fornita tramite la sintassi a più righe risulta migliore, più flessibile e garantisce maggiore facilità nelle operazioni di lettura, gestione e debug.  
  
 Il testo che segue la parola chiave `Then` viene esaminato per determinare se l'istruzione è un'istruzione `If` a riga singola.  Se dopo `Then`, sulla stessa riga viene visualizzato un elemento diverso da un commento, l'istruzione viene considerata come un'istruzione `If` a riga singola.  Se la parola chiave `Then` non è presente, si tratta dell'inizio di un'istruzione `If`...`Then`...`Else` a più righe.  
  
 In una sintassi a riga singola è possibile fare in modo che vengano eseguite più istruzioni come risultato di una decisione `If`...`Then`.  Tutte le istruzioni devono trovarsi sulla stessa riga ed essere separate da due punti.  
  
## Esempio  
 Nell'esempio seguente viene illustrato l'utilizzo della sintassi a più righe dell'istruzione `If`...`Then`...`Else`.  
  
 [!code-vb[VbVbalrStatements#101](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_1.vb)]  
  
## Esempio  
 Nell'esempio seguente sono presenti istruzioni `If`...`Then`...`Else` annidate.  
  
 [!code-vb[VbVbalrStatements#102](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_2.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato l'utilizzo della sintassi a riga singola.  
  
 [!code-vb[VbVbalrStatements#103](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_3.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.Choose%2A>   
 <xref:Microsoft.VisualBasic.Interaction.Switch%2A>   
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md)   
 [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Decision Structures](../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [If Operator](../../../visual-basic/language-reference/operators/if-operator.md)