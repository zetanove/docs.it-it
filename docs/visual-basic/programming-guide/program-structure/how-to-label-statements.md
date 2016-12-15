---
title: "How to: Label Statements (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "colons (:)"
  - "statements [Visual Basic], labels"
  - ": separator character"
  - "Visual Basic code, labeling statements"
ms.assetid: 38f1ff43-2054-42cb-963b-1998e60c6ed4
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Label Statements (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

I blocchi di istruzioni sono costituiti da righe di codice delimitate dai due punti.  Le righe di codice precedute da una stringa o da un integer di identificazione sono denominate *con etichetta*.  Le etichette delle istruzioni vengono utilizzate per contrassegnare una riga di codice da identificare per l'utilizzo con istruzioni, ad esempio `On Error Goto`.  
  
 Le etichette possono essere qualsiasi Visual Basic valido validi per identificare gli elementi di programmazione elemento\-o i valori letterali Integer.  L'etichetta deve essere inserita all'inizio di una riga del codice sorgente e deve essere seguita da i due punti, indipendentemente dall'eventuale presenza di un'istruzione dopo l'etichetta sulla stessa riga.  
  
 Il compilatore identifica le etichette verificando se l'inizio di una riga corrisponde a un identificatore già definito.  In caso contrario, il compilatore presuppone che sia un'etichetta.  
  
 Le etichette dispongono di un proprio spazio di dichiarazione e non interferiscono con altri identificatori.  L'ambito di un'etichetta è il corpo del metodo.  In caso di ambiguità, la dichiarazione di etichetta è sempre prioritaria.  
  
> [!NOTE]
>  È possibile utilizzare le etichette solo su istruzioni eseguibili all'interno di metodi.  
  
### Per assegnare un'etichetta a una riga di codice  
  
-   Inserire un identificatore, seguito dai due punti, all'inizio della riga del codice sorgente.  
  
     Le due righe di codice riportate di seguito, ad esempio, sono contrassegnate rispettivamente dalle etichette `Jump` e `120`.  
  
     [!code-vb[VbVbalrStatements#708](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/how-to-label-statements_1.vb)]  
  
## Vedere anche  
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)