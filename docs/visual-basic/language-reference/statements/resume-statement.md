---
title: "Resume Statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Resume"
  - "vb.ResumeNext"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Next statement, Resume"
  - "Resume Next statement"
  - "execution, resuming"
  - "run-time errors, resuming after"
  - "Resume statement, syntax"
  - "errors [Visual Basic], resuming after"
  - "Error statement, and Resume statement"
  - "execution"
  - "Resume statement"
ms.assetid: e24d058b-1a5c-4274-acb9-7d295d3ea537
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Resume Statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di riprendere l'esecuzione al termine di una routine di gestione degli errori.  
  
 Si consiglia di utilizzare la gestione delle eccezioni strutturata nel codice laddove possibile, anziché utilizzare la gestione delle eccezioni non strutturata e `On Error` e  `Resume` istruzioni.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## Sintassi  
  
```  
Resume [ Next | line ]  
```  
  
## Parti  
 `Resume`  
 Obbligatorio.  Se l'errore si è verificato nella stessa routine del gestore errori, l'esecuzione riprenderà dall'istruzione che ha causato l'errore.  Se l'errore si è verificato in una routine chiamata, l'esecuzione riprenderà dall'ultima istruzione che ha richiamato la routine di gestione degli errori.  
  
 `Next`  
 Parametro facoltativo.  Se l'errore si è verificato nella stessa routine del gestore errori, l'esecuzione riprenderà dall'istruzione immediatamente successiva a quella che ha causato l'errore.  Se l'errore si è verificato in una routine chiamata, l'esecuzione riprenderà dall'istruzione immediatamente successiva all'ultima istruzione che ha richiamato la routine di gestione degli errori \(o istruzione `On Error Resume Next`\).  
  
 `line`  
 Parametro facoltativo.  L'esecuzione riprende dalla riga specificata nell'argomento obbligatorio `line`.  L'argomento `line` corrisponde a un'etichetta o un numero di riga e deve trovarsi nella stessa routine del gestore errori.  
  
## Note  
  
> [!NOTE]
>  Si consiglia di utilizzare la gestione delle eccezioni strutturata nel codice laddove possibile, anziché utilizzare la gestione delle eccezioni non strutturata e `On Error` e  `Resume` istruzioni.  Per ulteriori informazioni, vedere [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
 Se si utilizza un'istruzione `Resume` in un contesto diverso da una routine di gestione degli errori, verrà generato un errore.  
  
 Non è possibile utilizzare l'istruzione `Resume` in alcuna routine contenente l'istruzione `Try...Catch...Finally`.  
  
## Esempio  
 In questo esempio viene utilizzata l'istruzione `Resume` per terminare la gestione degli errori in una routine e quindi riprendere l'esecuzione dall'istruzione che ha determinato l'errore.  Per illustrare l'utilizzo dell'istruzione `Resume` viene generato il numero di errore 55.  
  
 [!code-vb[VbVbalrErrorHandling#16](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/resume-statement_1.vb)]  
  
## Requisiti  
 **Spazio dei nomi:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Assembly:** Visual Basic Runtime Library \(in Microsoft.VisualBasic.dll\)  
  
## Vedere anche  
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Error Statement](../../../visual-basic/language-reference/statements/error-statement.md)   
 [On Error Statement](../../../visual-basic/language-reference/statements/on-error-statement.md)