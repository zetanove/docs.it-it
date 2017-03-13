---
title: "^ Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.^"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "raising numbers to powers"
  - "^ operator [Visual Basic], exponention"
  - "square operator"
  - "^ operator [Visual Basic]"
  - "exponentiation operator [Visual Basic]"
  - "exponent"
  - "numbers, rasing"
  - "powers"
  - "arithmetic operators, exponentiation"
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# ^ Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Eleva a potenza un numero.  
  
## Sintassi  
  
```  
  
number ^ exponent  
```  
  
## Parti  
 `number`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
 `exponent`  
 Obbligatorio.  Qualsiasi espressione numerica.  
  
## Risultato  
 Il risultato corrisponde a `number` elevato alla potenza di `exponent`, sempre come valore `Double`.  
  
## Tipi supportati  
 `Double`.  Gli operandi di qualsiasi tipo diverso vengono convertiti in `Double`.  
  
## Note  
 In Visual Basic l'elevamento a potenza viene sempre eseguito nel [Double Data Type](../../../visual-basic/language-reference/data-types/double-data-type.md).  
  
 Il valore di `exponent` può essere frazionario, negativo o entrambi.  
  
 Quando in un'unica espressione vengono eseguite più operazioni di elevamento a potenza, l'operatore `^` viene valutato da sinistra a destra nell'ordine di inserimento nell'espressione.  
  
> [!NOTE]
>  L'operatore `^` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `^` viene utilizzato per elevare a potenza un numero.  Il risultato è dato dall'elevamento del primo operando alla potenza indicata dal secondo.  
  
 [!code-vb[VbVbalrOperators#20](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/exponentiation-operator_1.vb)]  
  
 Di seguito sono riportati i risultati prodotti dall'esempio precedente:  
  
 `exp1` viene impostato su 4 \(2 al quadrato\).  
  
 `exp2` viene impostato su 19683 \(3 al cubo, quindi il risultato al cubo\).  
  
 `exp3` viene impostato su \-125 \(\-5 al cubo\).  
  
 `exp4` viene impostato su 625 \(\-5 alla quarta potenza\).  
  
 `exp5` viene impostato su 2 \(radice cubica di 8\).  
  
 `exp6` viene impostato su 0,5 \(1 diviso per la radice cubica di 8\).  
  
 Si noti l'importanza delle parentesi nelle espressioni dell'esempio precedente.  In base alle regole di *precedenza tra gli operatori*, l'operatore `^` viene in genere eseguito prima degli altri, perfino prima dell'operatore unario `–`.  Se il calcolo di `exp4` e `exp6` fosse stato eseguito senza parentesi, i risultati prodotti sarebbero stati i seguenti:  
  
 `exp4 = -5 ^ 4` viene calcolato come – \(5 nella quarta potenza\), che restituirà \-625.  
  
 `exp6 = 8 ^ -1.0 / 3.0` sarebbe stato calcolato come \(8 alla potenza di –1 o 0,125\) diviso per 3 con risultato uguale a 0,041666666666666666666666666666667.  
  
## Vedere anche  
 [^\= Operator](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [Arithmetic Operators](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Arithmetic Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)