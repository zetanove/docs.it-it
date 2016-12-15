---
title: "AndAlso Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.AndAlso"
  - "AndAlso"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "short-circuiting"
  - "AndAlso operator"
  - "operators [Visual Basic], short-circuiting"
  - "operators [Visual Basic], conjunction"
  - "short-circuit evaluation"
ms.assetid: bbc15191-b374-495b-9b8f-7b8c2f4388eb
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# AndAlso Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Esegue una congiunzione logica di corto circuito tra due espressioni.  
  
## Sintassi  
  
```  
  
result = expression1 AndAlso expression2  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`result`|Obbligatorio.  Qualsiasi espressione `Boolean`.  Il risultato è il valore `Boolean` ottenuto dal confronto tra le due espressioni.|  
|`expression1`|Obbligatorio.  Qualsiasi espressione `Boolean`.|  
|`expression2`|Obbligatorio.  Qualsiasi espressione `Boolean`.|  
  
## Note  
 Un'operazione logica viene definita *di corto circuito* se il codice compilato può evitare la valutazione di un'espressione sulla base del risultato di un'altra espressione.  Se il risultato della prima espressione valutata determina il risultato finale dell'operazione, non sarà necessario valutare la seconda espressione, in quanto non potrà modificare il risultato finale.  Il meccanismo di corto circuito può migliorare le prestazioni se l'espressione ignorata è complessa o se prevede anche chiamate di routine.  
  
 Se entrambe le espressioni restituiscono `True`, anche `result` sarà `True`.  Nella tabella riportata di seguito viene illustrato come si determina il valore di `result`.  
  
||||  
|-|-|-|  
|Se `expression1` è|Ed `expression2` è|Il valore di `result` sarà|  
|`True`|`True`|`True`|  
|`True`|`False`|`False`|  
|`False`|\(non valutato\)|`False`|  
  
## Tipi di dati  
 L'operatore `AndAlso` è definito solo per il [Boolean Data Type](../../../visual-basic/language-reference/data-types/boolean-data-type.md).  Ciascun operando viene convertito, se necessario, in `Boolean` e l'operazione viene eseguita interamente in `Boolean`.  Se si assegna il risultato a un tipo numerico, tale risultato viene convertito da `Boolean` nel tipo specificato.  Questa operazione può determinare un comportamento imprevisto.  Ad esempio, il risultato di `5 AndAlso 12` è `–1` se viene eseguita la conversione in `Integer`.  
  
## Overload  
 L'[And Operator](../../../visual-basic/language-reference/operators/and-operator.md) e l'[IsFalse Operator](../../../visual-basic/language-reference/operators/isfalse-operator.md) possono essere sottoposti a *overload*. In altri termini, una classe o una struttura può ridefinirne il comportamento quando un operando specifica il tipo di tale classe o struttura.  L'esecuzione dell'overload degli operatori `And` e `IsFalse` ha effetto sul comportamento dell'operatore `AndAlso`.  Se il codice utilizza `AndAlso` su una classe o una struttura che esegue l'overload di `And` e `IsFalse`, è importante comprendere il comportamento ridefinito da tali operatori.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Esempio  
 Nell'esempio riportato di seguito l'operatore `AndAlso` viene utilizzato per eseguire una congiunzione logica tra due espressioni.  Il risultato è un valore `Boolean` che indica se l'intera espressione di congiunzione è True.  Se la prima espressione è `False`, la seconda non verrà valutata.  
  
 [!code-vb[VbVbalrOperators#24](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/andalso-operator_1.vb)]  
  
 I risultati ottenuti dall'esempio precedente sono rispettivamente `True`, `False` e `False`.  Nel calcolo di `secondCheck` la seconda espressione non viene valutata perché la prima è già `False`.  La seconda espressione, tuttavia, viene valutata nel calcolo di `thirdCheck`.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una routine `Function` che esegue la ricerca di un determinato valore tra gli elementi di una matrice.  Se la matrice è vuota o se ne è stata superata la lunghezza, l'istruzione `While` non testa l'elemento della matrice rispetto al valore di ricerca.  
  
 [!code-vb[VbVbalrOperators#25](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/andalso-operator_2.vb)]  
  
## Vedere anche  
 [Logical\/Bitwise Operators](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [Operator Precedence in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Operators Listed by Functionality](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [And Operator](../../../visual-basic/language-reference/operators/and-operator.md)   
 [IsFalse Operator](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [Logical and Bitwise Operators in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)