---
title: "Operators and Expressions in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "operators [Visual Basic], operands"
  - "operators [Visual Basic]"
  - "operands, definition"
  - "Visual Basic code, operators"
  - "Visual Basic code, expressions"
  - "operands"
  - "expressions [Visual Basic]"
ms.assetid: b86f3131-94ee-448f-96cd-79611e028b26
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operators and Expressions in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Un *operatore* è un elemento di codice che esegue un'operazione su uno o più elementi di codice che contengono i valori.  Gli elementi di valore includono variabili, costanti, letterali, proprietà, restituzioni dalle procedure `Function` e `Operator` ed espressioni.  
  
 Un'*espressione* è una serie di elementi di valore combinati con gli operatori e che restituisce un nuovo valore.  Gli operatori agiscono sugli elementi di valore eseguendo calcoli, confronti o altre operazioni.  
  
## Tipi di operatori  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono forniti i seguenti tipi di operatori:  
  
-   [Operatori aritmetici](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md) che eseguono calcoli familiari sui valori numerici, compreso lo spostamento degli schemi di bit.  
  
-   [Operatori di confronto](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md) che consentono di confrontare due espressioni e restituiscono un valore `Boolean` che rappresenta il risultato del confronto.  
  
-   [Operatori di concatenazione](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md) che consentono di unire più stringhe in una stringa singola.  
  
-   [Operatori logici e bit per bit in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md) che combinano valori `Boolean` o numerici e restituiscono un risultato dello stesso tipo di dati dei valori.  
  
 Gli elementi di valore combinati con un operatore vengono denominati *operandi* di quell'operatore.  Gli operatori combinati con gli elementi di valore formano espressioni, ad eccezione dell'operatore di assegnazione, che forma un'*istruzione*.  Per ulteriori informazioni, vedere [Statements](../../../../visual-basic/programming-guide/language-features/statements.md).  
  
## Valutazione delle espressioni  
 Il risultato finale di un'espressione rappresenta un valore, che è generalmente di un tipo di dati familiare come `Boolean`, `String` o un tipo numerico.  
  
 Di seguito sono elencati esempi di espressioni.  
  
 `5 + 4`  
  
 `' The preceding expression evaluates to 9.`  
  
 `15 * System.Math.Sqrt(9) + x`  
  
 `' The preceding expression evaluates to 45 plus the value of x.`  
  
 `"Concat" & "ena" & "tion"`  
  
 `' The preceding expression evaluates to "Concatenation".`  
  
 `763 < 23`  
  
 `' The preceding expression evaluates to False.`  
  
 Numerosi operatori sono in grado di eseguire azioni in un'espressione o istruzione singola, come illustrato nell'esempio seguente.  
  
 [!code-vb[VbVbalrOperators#56](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/index_1.vb)]  
  
 Nell'esempio precedente, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono effettuate le operazioni dell'espressione a destra dell'operatore di assegnazione \(`=`\), quindi viene assegnato il valore risultante alla variabile `x` sulla sinistra.  Non esiste un limite pratico al numero di operatori che possono essere combinati in un'espressione, ma è necessario capire [Operator Precedence in Visual Basic](../../../../visual-basic/language-reference/operators/operator-precedence.md) per assicurarsi di ottenere i risultati previsti.  
  
 Per ulteriori informazioni ed esempi, vedere [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Operators](../../../../visual-basic/language-reference/operators/index.md)   
 [Efficient Combination of Operators](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)   
 [Statements](../../../../visual-basic/language-reference/statements/index.md)