---
title: "Optional Parameters (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "parameters, optional"
  - "Visual Basic code, procedures"
  - "procedures, optional arguments"
  - "optional arguments"
  - "named arguments, and optional arguments"
  - "optional parameters"
  - "Optional keyword, optional arguments"
  - "arguments [Visual Basic], optional"
  - "optional arguments, and named arguments"
ms.assetid: 398d2845-1069-4e94-b934-a73b545c8b87
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Optional Parameters (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile specificare che un parametro di routine è facoltativo e non è necessario fornire alcun argomento quando la routine viene chiamata.  I *parametri facoltativi* sono indicati dalla parola chiave `Optional` nella definizione della routine.  È necessario attenersi alle regole che seguono:  
  
-   È necessario che ciascun parametro facoltativo nella definizione della routine specifichi un valore predefinito.  
  
-   È necessario che tale valore predefinito per un parametro facoltativo sia un'espressione costante.  
  
-   Ciascun parametro che segue un parametro facoltativo nella definizione della routine deve essere anch'esso facoltativo.  
  
 Nella sintassi seguente viene illustrata una dichiarazione di routine con un parametro facoltativo:  
  
```  
Sub sub name(ByVal parameter1 As datatype1, Optional ByVal parameter2 As datatype2 = defaultvalue)  
```  
  
## Chiamata di routine con parametri facoltativi  
 Quando si chiama una routine con un parametro facoltativo, è possibile scegliere se fornire l'argomento o meno.  Se non lo si fornisce, la routine utilizza il valore predefinito dichiarato per quel parametro.  
  
 Quando si omettono uno o più argomenti facoltativi nell'elenco degli argomenti, utilizzare virgole in sequenza per contrassegnarne la posizione.  La chiamata di esempio che segue fornisce il primo e il quarto argomento, ma non il secondo o il terzo:  
  
```  
  
sub name(argument 1, , , argument 4)  
```  
  
 Nell'esempio riportato di seguito vengono effettuate diverse chiamate alla funzione `MsgBox` che include un parametro obbligatorio e due parametri facoltativi.  
  
 Nella prima chiamata a `MsgBox` vengono forniti tutti e tre gli argomenti nell'ordine in cui sono definiti da `MsgBox`.  Nella seconda chiamata viene fornito solo l'argomento obbligatorio.  Nella terza e quarta chiamata vengono forniti il primo e il terzo argomento.  Nella terza chiamata gli argomenti vengono forniti in base alla posizione, nella quarta in base al nome.  
  
 [!code-vb[VbVbcnProcedures#47](./codesnippet/VisualBasic/optional-parameters_1.vb)]  
  
## Determinazione dell'eventuale presenza di un argomento facoltativo  
 Una routine non può rilevare, in fase di esecuzione, se un determinato argomento è stato omesso o se il codice di chiamata ha fornito in modo esplicito il valore predefinito.  Se è necessario fare questa distinzione, è possibile impostare come predefinito un valore improbabile.  La routine riportata di seguito definisce il parametro facoltativo `office` e ne verifica il valore predefinito,  `QJZ`, per controllare se è stato omesso nella chiamata:  
  
 [!code-vb[VbVbcnProcedures#46](./codesnippet/VisualBasic/optional-parameters_2.vb)]  
  
 Se il parametro facoltativo è un tipo di riferimento come `String`, è possibile utilizzare `Nothing` come valore predefinito, a meno che esso non sia un valore previsto per l'argomento.  
  
## Parametri facoltativi e overload  
 Un altro modo per definire una routine con parametri facoltativi consiste nell'utilizzare l'overload.  Nel caso di un parametro facoltativo, è possibile definire due versioni di overload della routine, una con il parametro e l'altra senza.  Questo metodo diventa più complesso con l'aumentare del numero dei parametri facoltativi,  tuttavia ha il vantaggio di assicurare che il programma di chiamata fornisca tutti gli argomenti facoltativi.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Passing Arguments by Position and by Name](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)   
 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)