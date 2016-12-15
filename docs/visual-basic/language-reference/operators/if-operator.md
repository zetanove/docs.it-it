---
title: "If Operator (Visual Basic) | Microsoft Docs"
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
  - "vb.IfOperator"
  - "IfOperator"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ternary operators"
  - "conditional execution"
  - "If expressions [Visual Basic]"
  - "conditional operator [Visual Basic]"
  - "If Operator [Visual Basic]"
ms.assetid: dd56c9df-7cd4-442c-9ba6-20c70ee44c8f
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# If Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Viene utilizzata la valutazione short\-circuit per restituire in modo condizionale uno tra due valori.  L'operatore `If` può venire chiamato con due o tre argomenti.  
  
## Sintassi  
  
```  
If( [argument1,] argument2, argument3 )  
```  
  
## Chiamare l'operatore If con tre argomenti  
 Quando `If` viene chiamato utilizzando tre argomenti, il primo argomento deve restituire un valore di cui può essere eseguito il cast come un `Boolean`.  Tale valore `Boolean` determinerà quale degli altri due argomenti viene valutato e restituisce.  L'elenco seguente è valido solo quando l'operatore `If` viene chiamato utilizzando tre argomenti.  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`argument1`|Obbligatorio.  `Boolean`.  Determina quale degli altri argomenti deve venire valutato e restituito.|  
|`argument2`|Obbligatorio.  `Object`.  Valutato e restituito se `argument1` restituisce `True`.|  
|`argument3`|Obbligatorio.  `Object`.  Valutato e restituito se `argument1` dà come risultato `False` o se `argument1` è una variabile di [nullable](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)`Boolean` che restituisce [Nothing](../../../visual-basic/language-reference/nothing.md).|  
  
 Un operatore `If` chiamato con tre argomenti opera come una funzione `IIf` con la differenza che utilizza la valutazione short\-circuit.  Una funzione `IIf` valuta sempre tutti i tre argomenti, mentre un operatore `If` che ha tre argomenti ne valuta solo due.  Viene valutato il primo argomento `If` e viene eseguito il cast del risultato come un valore `Boolean`, `True` o `False`.  Se il valore è `True`, viene valutato `argument2` e il relativo valore viene restituito, ma `argument3` non viene valutato.  Se il valore dell'espressione `Boolean` è `False`, viene valutato `argument3` e il relativo valore viene restituito, ma `argument2` non viene valutato.  Negli esempi seguenti viene illustrato l'utilizzo di `If` quando vengono utilizzati tre argomenti:  
  
 [!code-vb[VbVbalrOperators#100](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_1.vb)]  
  
 Nell'esempio seguente viene illustrato il valore della valutazione short\-circuit.  Nell'esempio vengono descritti due tentativi di dividere una variabile `number` per una variabile `divisor` tranne quando `divisor` è zero.  In tal caso, deve essere restituito uno 0 e non si deve tentare di eseguire la divisione perché verrebbe generato un errore di runtime.  Poiché l'espressione `If` utilizza la valutazione short\-circuit, valuta il secondo o il terzo argomento, in funzione del valore del primo argomento.  Se il primo argomento è true, il divisore non è zero e se è sicuro valutare il secondo argomento ed eseguire la divisione.  Se il primo argomento è false, viene valutato solo il terzo argomento è viene restituito uno 0.  Pertanto, quando il divisore è 0, non viene eseguita la divisione e non si verifica alcun errore.  Tuttavia, poiché `IIf` non utilizza la valutazione short\-circuit, il secondo argomento viene valutato anche quando il primo argomento è false.  Questo provoca un errore di runtime divisione per zero.  
  
 [!code-vb[VbVbalrOperators#101](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_2.vb)]  
  
## Chiamare l'operatore If con due argomenti  
 Il primo argomento da fornire a `If` può essere omesso.  Questo consente di chiamare l'operatore utilizzando solo due argomenti.  L'elenco seguente è valido solo quando l'operatore `If` viene chiamato utilizzando due argomenti.  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`argument2`|Obbligatorio.  `Object`.  Deve essere un tipo di riferimento o nullable.  Valutato e restituito quando restituisce un valore qualsiasi diverso da `Nothing`.|  
|`argument3`|Obbligatorio.  `Object`.  Valutato e restituito se `argument2` restituisce `Nothing`.|  
  
 Quando l'argomento `Boolean` viene omesso, il primo argomento deve essere un tipo di riferimento o nullable.  Se il primo argomento restituisce `Nothing`, viene restituito il valore del secondo argomento.  In tutti gli altri casi viene restituito il valore del primo argomento.  Nell'esempio riportato di seguito viene illustrato come funziona questa valutazione.  
  
 [!code-vb[VbVbalrOperators#102](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_3.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.IIf%2A>   
 [Nullable Value Types](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Nothing](../../../visual-basic/language-reference/nothing.md)