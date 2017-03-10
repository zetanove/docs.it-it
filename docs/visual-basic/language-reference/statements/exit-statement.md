---
title: "Exit Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Exit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "execution, ending"
  - "files, closing"
  - "programs, quitting"
  - "code, exiting"
  - "Exit statement"
  - "program termination"
  - "execution, stopping"
ms.assetid: 760bfb32-5c3f-4bdb-a432-9a6001c92db7
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Exit Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di uscire da una routine o da un blocco e di trasferire immediatamente il controllo all'istruzione successiva alla chiamata della routine o alla definizione del blocco.  
  
## Sintassi  
  
```  
Exit { Do | For | Function | Property | Select | Sub | Try | While }  
```  
  
## Istruzioni  
 `Exit Do`  
 Esce immediatamente dal ciclo `Do` nel quale è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione `Loop`.  L'istruzione `Exit Do` può essere utilizzata solo all'interno di un ciclo `Do`.  Se utilizzata all'interno di cicli `Do` annidati, `Exit Do` esce dal ciclo più interno e trasferisce il controllo al livello superiore più prossimo di annidamento.  
  
 `Exit For`  
 Esce immediatamente dal ciclo `For` nel quale è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione `Next`.  L'istruzione `Exit For` può essere utilizzata solo all'interno di un ciclo `For`...`Next` o `For Each`...`Next`.  Se utilizzata all'interno di cicli `For` annidati, `Exit For` esce dal ciclo più interno e trasferisce il controllo al livello superiore più prossimo di annidamento.  
  
 `Exit Function`  
 Consente di uscire immediatamente dalla routine `Function` in cui è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione che ha chiamato la routine `Function`.  L'istruzione `Exit Function` può essere utilizzata solo all'interno di una routine `Function`.  
  
 Per specificare un valore restituito, è possibile assegnare il valore al nome della funzione su una riga prima dell'istruzione `Exit Function`.  Per assegnare il valore restituito e uscire dalla funzione in un'istruzione, è possibile utilizzare [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md).  
  
 `Exit Property`  
 Consente di uscire immediatamente dalla routine `Property` in cui è inserita.  L'esecuzione continua con l'istruzione che ha chiamato la routine `Property`, ovvero con l'istruzione che richiede o imposta il valore della proprietà.  L'istruzione `Exit Property` può essere utilizzata solo all'interno di una routine `Get` o `Set` di una proprietà.  
  
 Per specificare un valore restituito in una routine `Get`, è possibile assegnare il valore al nome della funzione su una riga prima dell'istruzione `Exit Property`.  Per assegnare il valore restituito e uscire dalla routine `Get` in un'istruzione, è possibile utilizzare l'istruzione `Return`.  
  
 In una routine `Set`, l'istruzione `Exit Property` riportata di seguito equivale all'istruzione `Return`.  
  
 `Exit Select`  
 Consente di uscire immediatamente dal blocco `Select Case` nel quale è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione `End Select`.  L'istruzione `Exit Select` può essere utilizzata solo all'interno di un'istruzione `Select Case`.  
  
 `Exit Sub`  
 Consente di uscire immediatamente dalla routine `Sub` in cui è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione che ha chiamato la routine `Sub`.  L'istruzione `Exit Sub` può essere utilizzata solo all'interno di una routine `Sub`.  
  
 In una routine `Sub`, l'istruzione `Exit Sub` riportata di seguito equivale all'istruzione `Return`.  
  
 `Exit Try`  
 Consente di uscire immediatamente dal blocco `Try` o `Catch` nel quale è inserita.  L'esecuzione continua con il blocco `Finally`, se disponibile, o in caso contrario con l'istruzione che segue l'istruzione `End Try`.  L'istruzione `Exit Try` può essere utilizzata all'interno di un blocco `Try` o `Catch` e non all'interno di un blocco `Finally`.  
  
 `Exit While`  
 Consente di uscire immediatamente dal ciclo `While` nel quale è inserita.  L'esecuzione continua con l'istruzione successiva all'istruzione `End While`.  L'istruzione `Exit While` può essere utilizzata solo all'interno di un ciclo `While`.  Se utilizzata all'interno di cicli `While` annidati, l'istruzione `Exit While` consente di trasferire il controllo al ciclo annidato al livello immediatamente superiore a quello nel quale è inserita.  
  
## Note  
 Non confondere le istruzioni `Exit` con le istruzioni `End`.  `Exit` non definisce la fine di un'istruzione.  
  
## Esempio  
 Nell'esempio seguente, il ciclo viene interrotto dalla condizione del ciclo quando la variabile `index` è maggiore di 100.  Tramite l'istruzione `If` nel ciclo, tuttavia, viene causata l'interruzione del ciclo mediante l'istruzione `Exit Do` quando la variabile di indice è maggiore di 10.  
  
 [!code-vb[VbVbalrStatements#133](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/exit-statement_1.vb)]  
  
## Esempio  
 Nell'esempio seguente il valore restituito viene assegnato al nome di funzione `myFunction` e viene quindi utilizzata l'istruzione `Exit Function` per la restituzione dalla funzione.  
  
 [!code-vb[VbVbalrStatements#23](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/exit-statement_2.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md) per assegnare il valore restituito e uscire dalla funzione.  
  
 [!code-vb[VbVbalrStatements#24](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/exit-statement_3.vb)]  
  
## Vedere anche  
 [Continue Statement](../../../visual-basic/language-reference/statements/continue-statement.md)   
 [Do...Loop Statement](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [End Statement](../../../visual-basic/language-reference/statements/end-statement.md)   
 [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md)   
 [Stop Statement](../../../visual-basic/language-reference/statements/stop-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)