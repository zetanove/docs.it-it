---
title: "Function Expression (Visual Basic) | Microsoft Docs"
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
  - "Function expression [Visual Basic]"
  - "functions [Visual Basic], function expressions"
  - "lambda expressions [Visual Basic], function expression"
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Function Expression (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Dichiara i parametri e il codice che consentono di definire un'espressione lambda Function.  
  
## Sintassi  
  
```  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`parameterlist`|Parametro facoltativo.  Elenco dei nomi di variabili locali che rappresentano i parametri di questa routine.  Le parentesi devono anche essere presenti quando l'elenco è vuoto.  Vedere [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md).|  
|`expression`|Obbligatorio.  Espressione singola.  Il tipo dell'espressione è il tipo restituito della funzione.|  
|`statements`|Obbligatorio.  Elenco di istruzioni che consente di restituire un valore tramite l'istruzione `Return`.  Per ulteriori informazioni, vedere [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md). Il tipo del valore restituito è il tipo restituito della funzione.|  
  
## Note  
 Un'*espressione lambda* è una funzione senza nome tramite cui viene calcolato e restituito un valore.  Un'espressione lambda può essere utilizzata ovunque sia previsto un tipo delegato, tranne come un argomento dell'oggetto `RemoveHandler`.  Per ulteriori informazioni sui delegati e sull'utilizzo delle espressioni lambda con i delegati, vedere [Delegate Statement](../../../visual-basic/language-reference/statements/delegate-statement.md) e [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## Sintassi delle espressioni lambda  
 La sintassi di un'espressione lambda è simile a quella di una funzione standard.  Le differenze sono le seguenti.  
  
-   Un'espressione lambda non possiede un nome.  
  
-   Le espressioni lambda non possono avere modificatori, ad esempio `Overloads` o `Overrides`.  
  
-   Le espressioni lambda non utilizzano una clausola `As` per definire il tipo restituito della funzione.  Il tipo viene invece dedotto dal valore restituito dal corpo di un'espressione lambda a riga singola o dal valore restituito di un'espressione lambda su più righe.  Ad esempio, se il corpo di un'espressione lambda a riga singola è `Where cust.City = "London"`, il relativo tipo restituito è `Boolean`.  
  
-   Il corpo di un'espressione lambda a riga singola deve essere un'espressione, non un'istruzione.  Il corpo può essere costituito da una chiamata a una routine di funzione, ma non da una chiamata a una subroutine.  
  
-   Tutti i parametri devono avere tipi di dati specificati oppure tutti devono essere dedotti.  
  
-   Non sono permessi parametri Optional e Paramarray .  
  
-   Non sono permessi parametri generici.  
  
## Esempio  
 Negli esempi seguenti vengono illustrati due modi per creare espressioni lambda semplici.  Nel primo caso viene utilizzato un oggetto `Dim` per fornire un nome alla funzione.  Per chiamare la funzione, inviare un valore per il parametro.  
  
 [!code-vb[VbVbalrLambdas#1](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_1.vb)]  
  
 [!code-vb[VbVbalrLambdas#2](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_2.vb)]  
  
## Esempio  
 In alternativa, è possibile dichiarare ed eseguire contemporaneamente la funzione.  
  
 [!code-vb[VbVbalrLambdas#3](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_3.vb)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'espressione lambda tramite la quale viene incrementato l'argomento e restituito il valore.  Nell'esempio viene illustrata la sintassi delle espressioni lambda sia a riga singola che con più righe per una funzione.  Per ulteriori esempi, vedere [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 [!code-vb[VbVbalrLambdas#14](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_4.vb)]  
  
## Esempio  
 Molti degli operatori di query standard hanno espressioni lambda sottostanti in [!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext_md.md)] che possono essere utilizzate in modo esplicito nelle query basate su metodo.  Nell'esempio seguente viene mostrata una query [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] tipica, seguita dalla conversione della query nel formato del metodo.  
  
```vb#  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 Per ulteriori informazioni sui metodi di query, vedere [Queries](../../../visual-basic/language-reference/queries/queries.md).  Per ulteriori informazioni sugli operatori di query standard, vedere [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
## Vedere anche  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Operators and Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Value Comparisons](../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Boolean Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [If Operator](../../../visual-basic/language-reference/operators/if-operator.md)   
 [Relaxed Delegate Conversion](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)