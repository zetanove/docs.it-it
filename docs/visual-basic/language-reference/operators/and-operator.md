---
title: "And Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.And"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "operators [Visual Basic], bitwise"
  - "logical conjunction"
  - "bitwise AND operator [Visual Basic]"
  - "conjunction operator"
  - "And operator [Visual Basic]"
  - "bitwise operators, AND operator"
  - "operators [Visual Basic], conjunction"
  - "bitwise comparison"
ms.assetid: 2ea711f3-439a-4c7c-9e3a-1ffe3b0d6046
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# And Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue una congiunzione logica tra due espressioni `Boolean` oppure una congiunzione bit per bit tra due espressioni numeriche.  
  
## Sintassi  
  
```  
  
result = expression1 And expression2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  Nel caso di un confronto tra valori booleani, `result` rappresenta la congiunzione logica di due valori `Boolean`.  Nel caso di operazioni bit per bit, `result` è invece un valore numerico che rappresenta la congiunzione bit per bit di due schemi di bit numerici.  
  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
## Note  
 Per un confronto tra valori booleani, `result` è `True` soltanto se `expression1` ed `expression2` restituiscono entrambi `True`.  Nella tabella riportata di seguito viene illustrato come si determina il valore di `result`.  
  
|Se `expression1` è|Ed `expression2` è|Il valore di `result` sarà|  
|------------------------|------------------------|--------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`False`|  
|`False`|`True`|`False`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  In un confronto tra valori booleani l'operatore `And` valuta sempre entrambe le espressioni, inclusa l'eventuale esecuzione di chiamate di routine.  L'[AndAlso Operator](../../../visual-basic/language-reference/operators/andalso-operator.md) esegue un'operazione di *corto circuito*. In altri termini, se `expression1` è `False`, `expression2` non verrà valutata.  
  
 Se applicato a valori numerici, l'operatore `And` esegue un confronto bit per bit tra bit che occupano la stessa posizione in due espressioni numeriche e imposta il bit corrispondente in `result` in base ai valori riportati nella seguente tabella.  
  
|Se il bit nel parametro `expression1` è|E il bit in `expression2` è|Il bit in `result` sarà|  
|---------------------------------------------|---------------------------------|-----------------------------|  
|1|1|1|  
|1|0|0|  
|0|1|0|  
|0|0|0|  
  
> [!NOTE]
>  Poiché il livello di precedenza degli operatori logici e bit per bit è inferiore rispetto a quello degli operatori aritmetici e relazionali, è necessario racchiudere tra parentesi le operazioni bit per bit per garantire un risultato accurato.  
  
## Tipi di dati  
 Se gli operandi sono costituiti da un'espressione `Boolean` e un'espressione numerica, l'espressione `Boolean` verrà convertita in un valore numerico \(–1 per `True` e 0 per `False`\) e verrà eseguita un'operazione bit per bit.  
  
 Nel caso di un confronto tra valori booleani il tipo di dati del risultato sarà `Boolean`,  mentre per un confronto bit per bit il tipo di dati del risultato sarà un tipo numerico appropriato ai tipi di dati di `expression1` e `expression2`.  Per informazioni, vedere la tabella "Confronti relazionali e bit per bit" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
> [!NOTE]
>  L'operatore `And` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `And` viene utilizzato per eseguire una congiunzione logica tra due espressioni.  Il risultato è un valore `Boolean` che indica se entrambe le espressioni sono `True`.  
  
 [!code-vb[VbVbalrOperators#22](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/and-operator_1.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente `True` e `False`.  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `And` viene utilizzato per eseguire la congiunzione logica tra i singoli bit di due espressioni numeriche.  Il bit nello schema dei risultati viene impostato se i bit corrispondenti negli operandi sono entrambi impostati su 1.  
  
 [!code-vb[VbVbalrOperators#23](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/and-operator_2.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente 8, 2 e 0.  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [AndAlso Operator](../../../visual-basic/language-reference/operators/andalso-operator.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)