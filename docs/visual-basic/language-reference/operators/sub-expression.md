---
title: "Sub Expression (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "lambda expressions [Visual Basic], sub expression"
  - "Sub Expression [Visual Basic]"
  - "subroutines [Visual Basic], sub expressions"
ms.assetid: 36b6bfd1-6539-4d8f-a5eb-6541a745ffde
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Sub Expression (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara i parametri e il codice che consentono di definire un'espressione lambda Subroutine.  
  
## Sintassi  
  
```  
Sub ( [ parameterlist ] ) statement  
- or -  
Sub ( [ parameterlist ] )  
  [ statements ]  
End Sub  
  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`parameterlist`|Parametro facoltativo.  Elenco dei nomi di variabili locali che rappresentano i parametri della routine.  Le parentesi devono anche essere presenti quando l'elenco è vuoto.  Per ulteriori informazioni, vedere [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md).|  
|`statement`|Obbligatorio.  Singola istruzione.|  
|`statements`|Obbligatorio.  Elenco di istruzioni.|  
  
## Note  
 Un'*espressione lambda* è una subroutine che non ha un nome e tramite la quale vengono eseguite una o più istruzioni.  Un'espressione lambda può essere utilizzata ovunque sia possibile utilizzare un tipo delegato, tranne come un argomento dell'oggetto `RemoveHandler`.  Per ulteriori informazioni sui delegati e sull'utilizzo delle espressioni lambda con i delegati, vedere [Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md) e [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## Sintassi delle espressioni lambda  
 La sintassi di un'espressione lambda è simile a quella di una subroutine standard.  Le differenze sono le seguenti.  
  
-   Un'espressione lambda non possiede un nome.  
  
-   Le espressioni lambda non possono avere modificatori, ad esempio `Overloads` o `Overrides`.  
  
-   Il corpo di un'espressione lambda a riga singola deve essere un'istruzione, non un'espressione.  Il corpo può essere costituito da una chiamata a una routine Sub, ma non da una chiamata a una routine Function.  
  
-   In un'espressione lambda, tutti i parametri devono disporre di tipi di dati specificati o devono essere dedotti.  
  
-   I parametri facoltativi e `ParamArray` non sono consentiti nelle espressioni lambda.  
  
-   Nelle espressioni lambda non sono consentiti parametri generici.  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'espressione lambda tramite la quale viene scritto un valore nella console.  Nell'esempio viene illustrata la sintassi delle espressioni lambda sia a riga singola che con più righe per una subroutine.  Per ulteriori esempi, vedere [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 [!code-vb[VbVbalrLambdas#15](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/sub-expression_1.vb)]  
  
## Vedere anche  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)