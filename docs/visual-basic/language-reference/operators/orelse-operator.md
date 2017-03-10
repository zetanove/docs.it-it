---
title: "OrElse Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "OrElse"
  - "vb.OrElse"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "short-circuiting"
  - "operators [Visual Basic], short-circuiting"
  - "operators [Visual Basic], disjunction"
  - "short-circuit evaluation"
  - "OrElse operator [Visual Basic]"
ms.assetid: 253803d8-05b0-47d7-b213-abd222847779
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# OrElse Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue una disgiunzione logica inclusiva di corto circuito tra due espressioni.  
  
## Sintassi  
  
```  
  
result = expression1 OrElse expression2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi espressione `Boolean`.  
  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione `Boolean`.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione `Boolean`.  
  
## Note  
 Un'operazione logica viene definita *di corto circuito* se il codice compilato può evitare la valutazione di un'espressione sulla base del risultato di un'altra espressione.  Se il risultato della prima espressione valutata determina il risultato finale dell'operazione, non sarà necessario valutare la seconda espressione, in quanto non potrà modificare il risultato finale.  Il meccanismo di corto circuito può migliorare le prestazioni se l'espressione ignorata è complessa o se prevede anche chiamate di routine.  
  
 Se una o entrambe le espressioni restituiscono `True`, anche `result` sarà `True`.  Nella tabella riportata di seguito viene illustrato come si determina il valore di `result`.  
  
|Se `expression1` è|Ed `expression2` è|Il valore di `result` sarà|  
|------------------------|------------------------|--------------------------------|  
|`True`|\(non valutato\)|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
## Tipi di dati  
 L'operatore `OrElse` è definito solo per il [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md).  Ciascun operando viene convertito, se necessario, in `Boolean` e l'operazione viene eseguita interamente in `Boolean`.  Se si assegna il risultato a un tipo numerico, tale risultato viene convertito da `Boolean` nel tipo specificato.  Questa operazione può determinare un comportamento imprevisto.  Ad esempio, il risultato di `5 OrElse 12` è `–1` se viene eseguita la conversione in `Integer`.  
  
## Overload  
 L'[Or Operator](../../../visual-basic/language-reference/operators/or-operator.md) e l'[IsTrue Operator](../../../visual-basic/language-reference/operators/istrue-operator.md) possono essere sottoposti a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload degli operatori `Or` e `IsTrue` ha effetto sul comportamento dell'operatore `OrElse`.  Se il codice utilizza `OrElse` su una classe o una struttura che esegue l'overload di `Or` e `IsTrue`, è importante comprendere il comportamento ridefinito da tali operatori.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `OrElse` viene utilizzato per eseguire la disgiunzione logica tra due espressioni.  Il risultato è un valore `Boolean` che indica se una delle due espressioni è True.  Se la prima espressione è `True`, la seconda non verrà valutata.  
  
 [!code-vb[VbVbalrOperators#37](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/orelse-operator_1.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente `True`, `True` e `False`.  Nel calcolo di `firstCheck` la seconda espressione non viene valutata perché la prima è già `True`.  La seconda espressione, tuttavia, viene valutata nel calcolo di `secondCheck`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene visualizzata un'istruzione `If`...`Then` contenente due chiamate di routine.  Se la prima chiamata restituisce `True`, la seconda routine non verrà chiamata.  Questa operazione può generare risultati imprevisti se la seconda routine esegue attività importanti che dovrebbero essere sempre eseguite durante l'esecuzione di questa sezione di codice.  
  
 [!code-vb[VbVbalrOperators#38](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/orelse-operator_2.vb)]  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Or Operator](../../../visual-basic/language-reference/operators/or-operator.md)   
 [IsTrue Operator](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)