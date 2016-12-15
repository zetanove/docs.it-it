---
title: "Not Operator (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Not"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Boolean expressions, negating"
  - "operators [Visual Basic], bitwise"
  - "negation operator"
  - "inverse bit values in variables"
  - "bitwise operators, NOT operator"
  - "bitwise comparison"
  - "Not operator [Visual Basic]"
  - "logical negation"
  - "operators [Visual Basic], negation"
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Not Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Esegue una negazione logica con un'espressione `Boolean` oppure una negazione bit per bit con un'espressione numerica.  
  
## Sintassi  
  
```  
  
result = Not expression  
```  
  
## Parti  
 `result`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
 `expression`  
 Obbligatorio.  Qualsiasi espressione `Boolean` o numerica.  
  
## Note  
 Nella tabella riportata di seguito viene illustrato come si determina il valore di `result` con espressioni `Boolean`.  
  
|Se `expression` è|Il valore di `result` sarà|  
|-----------------------|--------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 In presenza di espressioni numeriche, l'operatore `Not` inverte i valori dei bit di qualsiasi espressione numerica e imposta il bit corrispondente nell'argomento `result` come indicato nella seguente tabella:  
  
|Se il bit in `expression` è|Il bit in `result` sarà|  
|---------------------------------|-----------------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
>  Poiché il livello di precedenza degli operatori logici e bit per bit è inferiore rispetto a quello degli operatori aritmetici e relazionali, è necessario racchiudere le operazioni bit per bit tra parentesi per garantire un'esecuzione accurata.  
  
## Tipi di dati  
 Nel caso di una negazione di valori booleani il tipo di dati del risultato sarà `Boolean`.  Per una negazione bit per bit il tipo di dati del risultato sarà uguale a quello di `expression`.  Se tuttavia l'espressione è `Decimal`, il risultato sarà `Long`.  
  
## Overload  
 L'operatore `Not` può essere sottoposto a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando presenta il tipo di tale classe o struttura.  Se il codice utilizza l'operatore su una classe o una struttura di questo tipo, è importante comprendere il comportamento ridefinito di tale operatore.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Not` viene utilizzato per eseguire la negazione logica in un'espressione `Boolean`.  Il risultato è un valore `Boolean` che rappresenta il contrario del valore dell'espressione.  
  
 [!code-vb[VbVbalrOperators#33](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/not-operator_1.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente `False` e `True`.  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `Not` viene utilizzato per eseguire la negazione logica dei singoli bit di un'espressione numerica.  Il bit nello schema del risultato sarà l'opposto del corrispondente bit nel modello dell'operando, compreso il bit di segno.  
  
 [!code-vb[VbVbalrOperators#34](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/not-operator_2.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente –11, –9 e –7.  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)