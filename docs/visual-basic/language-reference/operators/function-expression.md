---
title: Espressione (Visual Basic) della funzione | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Function expression [Visual Basic]
- functions [Visual Basic], function expressions
- lambda expressions [Visual Basic], function expression
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9b181b18a28a8b92a392fffdc10e08690d54f545
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="function-expression-visual-basic"></a>Espressione di funzione (Visual Basic)
Dichiara i parametri e il codice che definiscono un'espressione lambda function.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`parameterlist`|Facoltativo. Un elenco di nomi di variabili locali che rappresentano i parametri di questa procedura. Le parentesi devono essere presenti anche quando l'elenco è vuoto. Vedere [elenco parametri](../../../visual-basic/language-reference/statements/parameter-list.md).|  
|`expression`|Obbligatorio. Una singola espressione. Il tipo dell'espressione è il tipo restituito della funzione.|  
|`statements`|Obbligatorio. Un elenco di istruzioni che restituisce un valore utilizzando il `Return` istruzione. (Vedere [istruzione Return](../../../visual-basic/language-reference/statements/return-statement.md).) Il tipo del valore restituito è il tipo restituito della funzione.|  
  
## <a name="remarks"></a>Note  
 Oggetto *espressione lambda* è una funzione senza un nome che calcola e restituisce un valore. È possibile utilizzare un'espressione lambda in qualsiasi punto è possibile utilizzare un tipo delegato, tranne come argomento di `RemoveHandler`. Per ulteriori informazioni sui delegati e l'utilizzo delle espressioni lambda con i delegati, vedere [istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md) e [conversione di tipo Relaxed del delegato](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## <a name="lambda-expression-syntax"></a>Sintassi delle espressioni lambda  
 La sintassi di un'espressione lambda è simile a quello di una funzione standard. Le differenze sono come segue:  
  
-   Un'espressione lambda non ha un nome.  
  
-   Espressioni lambda non possono avere modificatori, ad esempio `Overloads` o `Overrides`.  
  
-   Le espressioni lambda non utilizzano un `As` clausola per definire il tipo restituito della funzione. Al contrario, il tipo viene dedotto dal valore che restituisce il corpo di un'espressione lambda a riga singola, o il valore restituito di un'espressione lambda su più righe. Ad esempio, se il corpo di un'espressione lambda a riga singola è `Where cust.City = "London"`, il tipo restituito `Boolean`.  
  
-   Il corpo di un'espressione lambda a riga singola deve essere un'espressione, non un'istruzione. Il corpo può essere costituito da una chiamata a una routine di funzione, ma non da una chiamata a una routine sub.  
  
-   Tutti i parametri devono avere specificato deve essere dedotto, tipi di dati o tutti.  
  
-   Parametri Optional e Paramarray non consentiti.  
  
-   Parametri generici non sono consentiti.  
  
## <a name="example"></a>Esempio  
 Gli esempi seguenti illustrano due modi per creare espressioni lambda semplici. Il primo caso viene utilizzato un `Dim` per fornire un nome per la funzione. Per chiamare la funzione, si invia un valore per il parametro.  
  
 [!code-vb[VbVbalrLambdas n.&1;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_1.vb)]  
  
 [!code-vb[VbVbalrLambdas n.&2;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_2.vb)]  
  
## <a name="example"></a>Esempio  
 In alternativa, è possibile dichiarare ed eseguire la funzione nello stesso momento.  
  
 [!code-vb[VbVbalrLambdas n.&3;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_3.vb)]  
  
## <a name="example"></a>Esempio  
 Seguito è riportato un esempio di un'espressione lambda che incrementa il proprio argomento e restituisce il valore. L'esempio mostra sia la sintassi delle espressioni lambda a riga singola e su più righe per una funzione. Per ulteriori esempi, vedere [le espressioni Lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
 [!code-vb[VbVbalrLambdas&#14;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_4.vb)]  
  
## <a name="example"></a>Esempio  
 Le espressioni lambda sottostanti molti degli operatori di query in [!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext_md.md)]e può essere utilizzato in modo esplicito nelle query basate su metodo. Nell'esempio seguente viene illustrato un tipico [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)] query, seguita dalla conversione della query nel formato del metodo.  
  
```vb  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 Per ulteriori informazioni sui metodi di query, vedere [query](../../../visual-basic/language-reference/queries/queries.md). Per ulteriori informazioni sugli operatori di query standard, vedere [Cenni preliminari sugli operatori di Query Standard](http://msdn.microsoft.com/library/24cda21e-8af8-4632-b519-c404a839b9b2).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Espressioni lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [Operatori ed espressioni](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Istruzioni](../../../visual-basic/programming-guide/language-features/statements.md)   
 [Confronto di valori](../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [Espressioni booleane](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [Se (operatore)](../../../visual-basic/language-reference/operators/if-operator.md)   
 [Conversione di tipo relaxed del delegato](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)

