---
title: "Variable &#39;&lt;variablename&gt;&#39; hides a variable in an enclosing block | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30616"
  - "bc30616"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30616"
ms.assetid: e7658ebc-da45-451b-a409-a0f8915f0beb
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Variable &#39;&lt;variablename&gt;&#39; hides a variable in an enclosing block
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una variabile in un blocco ha lo stesso nome di un'altra variabile locale.  
  
 **ID errore:** BC30616  
  
### Per correggere l'errore  
  
-   Rinominare la variabile nel blocco che la contiene in modo che non corrisponda a nessuna variabile locale.  Di seguito è riportato un esempio:  
  
    ```  
    Dim a, b, x As Integer  
    If a = b Then  
       Dim y As Integer = 20 ' Uniquely named block variable.  
    End If  
    ```  
  
-   Una delle cause più comuni di questo errore è l'utilizzo di `Catch e As Exception` all'interno di un gestore eventi.  In tal caso assegnare alla variabile del blocco `Catch` il nome `ex` anziché `e`.  
  
-   Un'altra causa comune di questo errore è un tentativo di accedere a una variabile locale dichiarata all'interno di un blocco `Try` in un blocco `Catch` distinto.  Per risolvere il problema, dichiarare la variabile al di fuori della struttura `Try...Catch...Finally`.  
  
## Vedere anche  
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Dichiarazione di variabili](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)