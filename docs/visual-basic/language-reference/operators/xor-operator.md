---
title: "Xor Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Xor"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "exclusive OR operator"
  - "logical exclusion"
  - "operators [Visual Basic], exclusive or"
  - "exclusion operator"
  - "operators [Visual Basic], bitwise"
  - "bitwise operators, XOR operator"
  - "Xor operator [Visual Basic]"
  - "Xor keyword"
  - "bitwise comparison"
ms.assetid: 036000a9-3934-4e7f-a9d0-a816de3d84a6
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Xor Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue un'esclusione logica tra due espressioni `Boolean` oppure un'esclusione bit per bit tra due espressioni numeriche.  
  
## Sintassi  
  
```  
  
result = expression1 Xor expression2  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi variabile `Boolean` o numerica.  Nel caso di un confronto tra valori booleani, `result` rappresenta l'esclusione logica \(disgiunzione logica esclusiva\) di due valori `Boolean`.  Nel caso di operazioni bit per bit, `result` è un valore numerico che rappresenta l'esclusione bit per bit \(disgiunzione bit per bit esclusiva\) di due schemi di bit numerici.  
  
 `expression1`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
 `expression2`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
## Note  
 Per un confronto tra valori booleani, `result` è `True` soltanto se esattamente una tra `expression1` e `expression2` restituisce `True`,  ovvero se `expression1` e `expression2` restituiscono valori `Boolean` opposti.  Nella tabella riportata di seguito viene illustrato come si determina il valore di `result`.  
  
|Se `expression1` è|Ed `expression2` è|Il valore di `result` sarà|  
|------------------------|------------------------|--------------------------------|  
|`True`|`True`|`False`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  In un confronto tra valori booleani, l'operatore `Xor` valuta sempre entrambe le espressioni, inclusa l'eventuale esecuzione di chiamate di routine.  Non esiste un operatore equivalente di corto circuito per `Xor`, dal momento che il risultato dipende sempre da entrambi gli operandi.  Per informazioni sugli operatori logici di *corto circuito*, vedere [AndAlso Operator](../../../visual-basic/language-reference/operators/andalso-operator.md) e [OrElse Operator](../../../visual-basic/language-reference/operators/orelse-operator.md).  
  
 Nelle operazioni bit per bit, l'operatore `Xor` esegue un confronto bit per bit tra bit che occupano la stessa posizione in due espressioni numeriche e imposta il bit corrispondente nel parametro `result` in base alla tabella seguente.  
  
|Se il bit nel parametro `expression1` è|E il bit in `expression2` è|Il bit in `result` sarà|  
|---------------------------------------------|---------------------------------|-----------------------------|  
|1|1|0|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
>  Poiché il livello di precedenza degli operatori logici e bit per bit è inferiore rispetto a quello degli operatori aritmetici e relazionali, è necessario racchiudere le operazioni bit per bit tra parentesi per garantire un'esecuzione accurata.  
  
 Ad esempio, 5 `Xor` 3 è uguale a 6.  Per visualizzarne il motivo, convertire 5 e 3 nelle rispettive rappresentazioni binarie 101 e 011.  Utilizzare quindi la tabella precedente per stabilire che 101 Xor 011 è uguale a 110, ovvero la rappresentazione binaria del numero decimale 6.  
  
## Tipi di dati  
 Se gli operandi sono costituiti da un'espressione `Boolean` e un'espressione numerica, l'espressione `Boolean` verrà convertita in un valore numerico \(–1 per `True` e 0 per `False`\) e verrà eseguita un'operazione bit per bit.  
  
 Nel caso di un confronto tra valori `Boolean` il tipo di dati del risultato sarà `Boolean`,  mentre per un confronto bit per bit il tipo di dati del risultato sarà un tipo numerico appropriato ai tipi di dati di `expression1` e `expression2`.  Per informazioni, vedere la tabella "Confronti relazionali e bit per bit" in [Data Types of Operator Results](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## Overload  
 L'operatore `Xor` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Xor` viene utilizzato per eseguire l'esclusione logica \(disgiunzione logica esclusiva\) tra due espressioni.  Il risultato è un valore `Boolean` che indica se una sola delle espressioni è `True`.  
  
 [!code-vb[VbVbalrOperators#40](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xor-operator_1.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente `False`, `True` e `False`.  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Xor` viene utilizzato per eseguire l'esclusione logica \(disgiunzione logica esclusiva\) tra i singoli bit di due espressioni numeriche.  Il bit nello schema dei risultati viene impostato se uno solo dei bit corrispondenti negli operandi è impostato su 1.  
  
 [!code-vb[VbVbalrOperators#41](../../../visual-basic/language-reference/operators/codesnippet/visualbasic/xor-operator_2.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente 2, 12 e 14.  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)