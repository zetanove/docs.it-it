---
title: "Continue Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.continue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Continue statement [Visual Basic]"
  - "loops, transferring to next iteration"
ms.assetid: 3ad00103-358b-4af3-a3a8-1b9ea0e995d3
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Continue Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Trasferisce immediatamente il controllo all'iterazione successiva del ciclo.  
  
## Sintassi  
  
```  
Continue { Do | For | While }  
```  
  
## Note  
 È possibile trasferire il controllo dall'interno di un ciclo `Do`, `For` o `While` all'iterazione successiva del ciclo.  Il controllo passa immediatamente alla verifica della condizione del ciclo, ossia viene trasferito all'istruzione `For` o `While` oppure all'istruzione `Do` o `Loop` che contiene la clausola `Until` o `While`.  
  
 È possibile utilizzare `Continue` in qualsiasi punto del ciclo in cui è consentito il trasferimento del controllo.  Le regole che consentono il trasferimento del controllo corrispondono a quelle di [GoTo Statement](../../../visual-basic/language-reference/statements/goto-statement.md).  
  
 Se, ad esempio, un ciclo è contenuto completamente all'interno di un blocco `Try`, di un blocco `Catch` o di un blocco `Finally`, è possibile utilizzare `Continue` per uscire dal ciclo.  Se, invece, la struttura `Try`...`End Try` è contenuta all'interno del ciclo, non è possibile utilizzare `Continue` per trasferire il controllo all'esterno del blocco `Finally` ed è possibile utilizzarlo per uscire da un blocco `Try` o `Catch` solo se si esce completamente dalla struttura `Try`...`End Try`.  
  
 Se sono presenti cicli annidati dello stesso tipo, ad esempio un ciclo `Do` all'interno di un altro ciclo `Do`, un'istruzione `Continue Do` passa all'iterazione successiva del ciclo `Do` più interno che la contiene.  Non è possibile utilizzare `Continue` per passare all'iterazione successiva di un ciclo dello stesso tipo diverso da quello più interno che contiene l'istruzione.  
  
 Se sono presenti cicli annidati di tipo diverso, ad esempio un ciclo `Do` all'interno di un ciclo `For`, è possibile passare all'iterazione successiva di uno dei due cicli utilizzando `Continue Do` o `Continue For`.  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene utilizzata l'istruzione `Continue While` per passare alla colonna successiva di una matrice se uno dei divisori è zero.  L'istruzione `Continue While` si trova in un ciclo `For`.  Passa all'istruzione `While col < lastcol`, ossia all'iterazione successiva del ciclo `While` più interno che contiene il ciclo `For`.  
  
 [!code-vb[VbVbalrStatements#14](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/continue-statement_1.vb)]  
  
## Vedere anche  
 [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [While...End While Statement](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)