---
title: "Logical and Bitwise Operators in Visual Basic | Microsoft Docs"
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
  - "short-circuiting"
  - "Boolean expressions"
  - "logical operators, Boolean expressions"
  - "operators [Visual Basic], logical"
  - "AndAlso operator"
  - "Not operator [Visual Basic], Boolean expressions"
  - "Xor operator [Visual Basic], Boolean expressions"
  - "And operator [Visual Basic], logical operators"
  - "logical operators"
  - "expressions [Visual Basic], Boolean"
  - "Or operator, logical operators"
  - "Visual Basic code, operators"
  - "short-circuiting, logical operators"
  - "logical operators, short-circuiting"
  - "Visual Basic code, expressions"
  - "logical operators, binary"
  - "OrElse operator [Visual Basic]"
  - "logical operators, unary"
ms.assetid: ca474e13-567d-4b1d-a18b-301433705e57
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Logical and Bitwise Operators in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Gli operatori logici confrontano le espressioni `Boolean` e restituiscono il risultato `Boolean`.  Gli operatori `And`, `Or`, `AndAlso`, `OrElse` e `Xor` sono *binari* in quanto prendono due operandi, mentre l'operatore `Not` è *unario* in quanto prende un unico operando.  Alcuni di questi operatori possono inoltre eseguire operazioni logiche bit per bit sui valori integrali.  
  
## Operatore logico unario  
 L'[Not Operator](../../../../visual-basic/language-reference/operators/not-operator.md) esegue una *negazione* logica su un'espressione `Boolean`.  Viene generato il risultato contrario logico del suo operando.  Se l'espressione restituisce `True`, `Not` restituirà `False`; se l'espressione restituisce `False`, `Not` restituirà `True`.  Questa condizione è illustrata nell'esempio che segue.  
  
 [!code-vb[VbVbalrOperators#77](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_1.vb)]  
  
## Operatori logici binari  
 L'[And Operator](../../../../visual-basic/language-reference/operators/and-operator.md) esegue una *congiunzione* logica su due espressioni `Boolean`.  Se entrambe le espressioni restituiscono `True`, `And` restituirà `True`.  Se almeno una delle espressioni restituisce `False`, `And` restituirà `False`.  
  
 L'[Or Operator](../../../../visual-basic/language-reference/operators/or-operator.md) esegue una *disgiunzione* logica o un'*inclusione* su due espressioni `Boolean`.  Se una delle espressioni restituisce `True` o se entrambe restituiscono `True`, `Or` restituirà `True`.  Se una delle espressioni restituisce `True`, `Or` restituisce `False`.  
  
 L'[Xor Operator](../../../../visual-basic/language-reference/operators/xor-operator.md) esegue un' *esclusione* logica su due espressioni `Boolean`.  Se esattamente un'espressione restituisce `True`, ma non entrambe, `Xor` restituirà `True`.  Se entrambe le espressioni restituiscono `True` o entrambe restituiscono `False`, `Xor` restituirà `False`.  
  
 Nell'esempio illustrato vengono illustrati gli operatori `And`, `Or` e `Xor`.  
  
 [!code-vb[VbVbalrOperators#78](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_2.vb)]  
  
## Operatori logici di corto circuito  
 L'[AndAlso Operator](../../../../visual-basic/language-reference/operators/andalso-operator.md) è molto simile all'operatore `And`, in quanto anch'esso esegue una congiunzione logica tra due espressioni `Boolean`.  La differenza fondamentale tra le due consiste nel fatto che `AndAlso` mostra un comportamento di tipo *short circuit*.  Se la prima espressione in un'espressione `AndAlso` restituisce `False`, la seconda espressione non verrà valutata in quanto non può alterare il risultato finale e `AndAlso` restituisce `False`.  
  
 Analogamente, l'[OrElse Operator](../../../../visual-basic/language-reference/operators/orelse-operator.md) esegue una disgiunzione logica short circuit tra due espressioni `Boolean`.  Se la prima espressione in un'espressione `OrElse` restituisce `True`, la seconda espressione non verrà valutata in quanto non può alterare il risultato finale e `OrElse` restituisce `True`.  
  
### Vantaggi e svantaggi dello short\-circuit  
 Lo short\-circuit può migliorare le prestazioni non valutando un'espressione che non può alterare il risultato dell'operazione logica.  Tuttavia se tale espressione esegue operazioni aggiuntive, lo short\-circuit ignorerà quelle azioni.  Se l'espressione include una chiamata a una procedura `Function` ad esempio, quella procedura non verrà chiamata se si esegue un corto circuito dell'espressione e se qualsiasi codice aggiuntivo contenuto nella `Function` non viene eseguito.  Pertanto, la funzione potrebbe venire eseguita solo occasionalmente e potrebbe non venire testata correttamente.  In alternativa la logica di programma potrebbe dipendere dal codice nella `Function`.  
  
 Nell'esempio seguente viene illustrata la differenza tra `And`, `Or` e le loro controparti di corto circuito.  
  
 [!code-vb[VbVbalrOperators#81](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_3.vb)]  
  
 [!code-vb[VbVbalrOperators#80](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_4.vb)]  
  
 [!code-vb[VbVbalrOperators#79](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/logical-and-bitwise-operators_5.vb)]  
  
 Nell'esempio illustrato in precedenza, si noti che una parte del codice importante in `checkIfValid()` non viene eseguita quando viene eseguito un "corto circuito" della chiamata.  La prima istruzione `If` chiama `checkIfValid()` anche se `12 > 45` restituisce `False`, in quanto non viene eseguito il corto circuito di `And`.  La seconda istruzione `If` non chiama `checkIfValid()`, in quanto quando `12 > 45` restituisce `False`, `AndAlso` provoca un corto circuito della seconda espressione.  La terza istruzione `If` chiama `checkIfValid()` anche se `12 < 45` restituisce `True`, in quando non viene eseguito il corto circuito di `Or`.  La quarta istruzione `If` non chiama `checkIfValid()`, in quanto quando `12 < 45` restituisce `True`, `OrElse` provoca un corto circuito della seconda espressione.  
  
## Operazioni bit per bit  
 Le operazioni bit per bit valutano due valori integrali nella forma binaria \(base 2\).  Esse confrontano i bit in posizioni corrispondenti quindi assegnare i valori in base al confronto.  Nell'esempio riportato di seguito viene illustrato l'operatore `And`.  
  
 [!code-vb[VbVbalrConcepts#2](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/logical-and-bitwise-operators_6.vb)]  
  
 Nell'esempio precedente il valore `x` viene impostato su 1.  Questa situazione si verifica per i seguenti motivi:  
  
-   I valori vengono considerati come binari:  
  
     3 in forma binaria \= 011  
  
     5 in forma binaria \= 101  
  
-   L'operatore `And` confronta le rappresentazioni binarie, una posizione binaria \(bit\) alla volta.  Se entrambi i bit in una determinata posizione sono 1, nel risultato viene inserito 1 in quella posizione.  Se uno dei bit è 0, nel risultato viene inserito 0 in quella posizione.  Nell'esempio illustrato in precedenza si ottiene il seguente risultato:  
  
     011 \(3 in forma binaria\)  
  
     101 \(5 in forma binaria\)  
  
     001 \(il risultato, in forma binaria\)  
  
-   Il risultato viene considerato come decimale.  Il valore 001 è la rappresentazione binaria di 1, quindi `x` \= 1.  
  
 L'operazione `Or` bit per bit è simile, tranne per il fatto che viene assegnato un 1 al bit risultante se uno o entrambi i bit paragonati corrisponde a 1.  `Xor` assegna un 1 al bit risultante se esattamente uno dei bit paragonati \(non entrambi\) corrisponde a 1.  `Not` accetta un operando singolo e inverte tutti i bit, incluso il bit del segno e assegna il valore al risultato.  Ciò significa che per i numeri positivi firmati, `Not` restituisce sempre un valore negativo e per i numeri negativi `Not` restituisce sempre un valore positivo o pari a zero.  
  
 Gli operatori `AndAlso` e `OrElse` non supportano le operazioni bit per bit.  
  
> [!NOTE]
>  Le operazioni bit per bit possono essere eseguite solo sui tipi integrali.  I valori a virgola mobile devono essere convertiti in tipi integrali prima che possa proseguire l'operazione bit per bit.  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Boolean Expressions](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [Arithmetic Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Comparison Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Concatenation Operators in Visual Basic](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/concatenation-operators.md)   
 [Efficient Combination of Operators](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/efficient-combination-of-operators.md)