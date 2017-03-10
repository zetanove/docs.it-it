---
title: "#If...Then...#Else Directives | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.#EndIf"
  - "#End If"
  - "#Then"
  - "#ElseIf"
  - "vb.#ElseIf"
  - "vb.#Else"
  - "vb.#If"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, compiling"
  - "#If directive [Visual Basic]"
  - "conditional compilation, directives"
  - "#End if directive [Visual Basic]"
  - "selective compiling"
  - "else directive (#else)"
  - "#Else directive [Visual Basic]"
ms.assetid: 10bba104-e3fd-451b-b672-faa472530502
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# #If...Then...#Else Directives
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Compilano in modo condizionale blocchi selezionati di codice Visual Basic.  
  
## Sintassi  
  
```  
#If expression Then  
   statements  
[ #ElseIf expression Then  
   [ statements ]  
...  
#ElseIf expression Then  
   [ statements ] ]  
[ #Else  
   [ statements ] ]  
#End If  
```  
  
## Parti  
 `expression`  
 Obbligatoria per le istruzioni `#If` e `#ElseIf`, facoltativa negli altri casi.  Qualsiasi espressione, costituita esclusivamente da una o più costanti di compilazione condizionale, valori letterali e operatori, che restituisca `True` o `False`.  
  
 `statements`  
 Obbligatoria per il blocco di istruzioni `#If`, facoltativa negli altri casi.  Righe di programma o direttive di compilazione che vengono compilate se l'espressione associata restituisce `True`.  
  
 `#End If`  
 Termina il blocco di istruzioni `#If`.  
  
## Note  
 Apparentemente, il comportamento delle direttive `#If...Then...#Else` è lo stesso delle istruzioni `If...Then...Else`.  Tuttavia, mentre le istruzioni `#If...Then...#Else` valutano i risultati della compilazione effettuata dal compilatore, le istruzioni `If...Then...Else` valutano le condizioni in fase di esecuzione.  
  
 La compilazione condizionale viene utilizzata in genere per la compilazione di uno stesso programma per piattaforme diverse.  Viene anche utilizzata per evitare che il codice di debug venga visualizzato in un file eseguibile.  Il codice escluso durante la compilazione condizionale viene completamente omesso dal file eseguibile finale e non ha effetto su dimensioni e prestazioni.  
  
 Indipendentemente dal risultato di eventuali valutazioni, tutte le espressioni vengono valutate utilizzando `Option Compare Binary`.  L'istruzione `Option Compare` non ha effetto sulle espressioni nelle istruzioni `#If` e `#ElseIf`.  
  
> [!NOTE]
>  Non esiste alcun form a riga singola delle istruzioni `#If`, `#Else`, `#ElseIf` e `#End If`.  Nessun altro codice può essere visualizzato sulla stessa riga delle istruzioni.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato il costrutto `#If...Then...#Else` per stabilire se devono essere compilate determinate istruzioni.  
  
 [!code-vb[VbVbalrConditionalComp#1](../../../visual-basic/language-reference/directives/codesnippet/visualbasic/if-then-else-directives_1.vb)]  
  
## Vedere anche  
 [\#Const Directive](../../../visual-basic/language-reference/directives/const-directive.md)   
 [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)