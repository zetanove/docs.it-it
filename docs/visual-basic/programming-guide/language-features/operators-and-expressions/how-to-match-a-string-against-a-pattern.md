---
title: "How to: Match a String against a Pattern (Visual Basic) | Microsoft Docs"
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
  - "comparison operators, comparing strings"
  - "pattern matching"
  - "strings [Visual Basic], comparing"
  - "string comparison [Visual Basic], operators"
  - "Visual Basic code, operators"
  - "pattern matching, string comparison"
  - "string comparison [Visual Basic]"
  - "Like operator [Visual Basic], pattern matching"
  - "pattern matching, empty strings"
  - "operators [Visual Basic], comparison"
ms.assetid: 19a83804-b5af-4739-928b-ac93e64e457f
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Match a String against a Pattern (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per verificare se un'espressione dell'oggetto [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md) soddisfa un modello, è possibile utilizzare l'operatore [Like Operator](../../../../visual-basic/language-reference/operators/like-operator.md).  
  
 L'operatore `Like` accetta due operandi.  L'operando di sinistra è un'espressione stringa, mentre l'operando di destra è una stringa contenente il modello da utilizzare per il confronto.  `Like` restituisce un valore `Boolean` che indica se l'espressione stringa soddisfa il modello.  
  
 È possibile confrontare ciascun carattere incluso nell'espressione stringa con un carattere specifico, un carattere jolly, un elenco o un intervallo di caratteri.  Le posizioni delle specifiche nella stringa modello corrispondono alle posizioni dei caratteri da confrontare nell'espressione stringa.  
  
### Per confrontare un carattere incluso nell'espressione stringa con un carattere specifico  
  
-   Inserire il carattere specifico direttamente nella stringa modello.  Alcuni caratteri speciali devono essere racchiusi da parentesi \(`[ ]`\).  Per ulteriori informazioni, vedere [Like Operator](../../../../visual-basic/language-reference/operators/like-operator.md).  
  
     Il seguente esempio consente di verificare se l'oggetto `myString` è costituito esattamente dal singolo carattere `H`.  
  
     [!code-vb[VbVbalrOperators#70](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_1.vb)]  
  
### Per confrontare un carattere incluso nell'espressione stringa con un carattere jolly  
  
-   Inserire un punto interrogativo \(`?`\) nella stringa modello.  Qualsiasi carattere valido in questa posizione determina una corrispondenza corretta.  
  
     Il seguente esempio consente di verificare se l'oggetto `myString` è costituito dal singolo carattere `W` seguito da due caratteri qualsiasi.  
  
     [!code-vb[VbVbalrOperators#71](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_2.vb)]  
  
### Per confrontare un carattere incluso nell'espressione stringa con un elenco di caratteri  
  
-   Inserire le parentesi nella stringa modello \(`[ ]`\) e racchiudere tra le parentesi l'elenco di caratteri.  Non separare i caratteri con virgole o altri separatori.  Qualsiasi carattere incluso nell'elenco determina una corrispondenza corretta.  
  
     Il seguente esempio consente di verificare se l'oggetto `myString` è costituito da un qualsiasi carattere valido seguito da un solo carattere `A`, `C`, o `E`.  
  
     [!code-vb[VbVbalrOperators#72](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_3.vb)]  
  
     In questo tipo di confronto viene fatta distinzione tra maiuscole e minuscole.  
  
### Per confrontare un carattere incluso nell'espressione stringa con un intervallo di caratteri  
  
-   Inserire le parentesi nella stringa modello \(`[ ]`\) e racchiudere tra le parentesi il carattere minore e quello maggiore dell'intervallo, separati da un trattino \(`–`\).  Qualsiasi carattere incluso nell'intervallo determina una corrispondenza corretta.  
  
     Il seguente esempio consente di verificare se l'oggetto `myString` è costituito dai caratteri `num` seguiti da un solo carattere `i`, `j`, `k`, `l`, `m`, o `n`.  
  
     [!code-vb[VbVbalrOperators#73](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_4.vb)]  
  
     In questo tipo di confronto viene fatta distinzione tra maiuscole e minuscole.  
  
## Confronto di stringhe vuote  
 L'operatore `Like` considera la sequenza `[]` come una stringa di lunghezza zero \(`""`\).  È possibile utilizzare la sequenza `[]` per verificare se l'espressione stringa è completamente vuota, ma non per verificare se è vuota una particolare posizione all'interno dell'espressione stringa.  Se si desidera verificare una posizione vuota, è possibile utilizzare l'operatore `Like` più volte.  
  
#### Per confrontare un carattere incluso nell'espressione stringa con un elenco di caratteri o con nessun carattere  
  
1.  Chiamare due volte l'operatore `Like` sulla stessa espressione stringa e connettere le due chiamate con l'operatore [Or Operator](../../../../visual-basic/language-reference/operators/or-operator.md) o [OrElse Operator](../../../../visual-basic/language-reference/operators/orelse-operator.md).  
  
2.  Nella stringa modello per la prima clausola `Like`, è necessario inserire l'elenco di caratteri racchiuso tra parentesi \(`[ ]`\).  
  
3.  Nella stringa modello per la seconda clausola `Like` non inserire alcun carattere nella posizione in questione.  
  
     Il seguente esempio consente di verificare il numero telefonico di sette cifre `phoneNum` che deve essere composto da tre cifre seguite da uno spazio, da un trattino \(`–`\), da un punto \(`.`\) o da nessun carattere, e quindi da altre quattro cifre.  
  
     [!code-vb[VbVbalrOperators#74](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_5.vb)]  
  
## Vedere anche  
 [Comparison Operators](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Operators and Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Like Operator](../../../../visual-basic/language-reference/operators/like-operator.md)   
 [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md)