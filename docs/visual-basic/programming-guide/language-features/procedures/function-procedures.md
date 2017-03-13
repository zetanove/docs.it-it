---
title: "Routine Function (Visual Basic) | Microsoft Docs"
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
  - "routine di Function"
  - "valori restituiti, routine di Function"
  - "Visual Basic (codice), routine"
  - "routine, chiamata"
  - "routine, Function"
  - "sintassi, routine di Function"
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Routine Function (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine `Function` è costituita da una serie di istruzioni [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] racchiuse tra le istruzioni `Function` ed `End Function`.  La routine `Function` esegue un'attività e quindi restituisce il controllo al codice chiamante.  Contemporaneamente, restituisce al codice chiamante anche un valore.  
  
 Ogni volta che la routine viene chiamata, le relative istruzioni vengono eseguite a partire dalla prima istruzione eseguibile dopo l'istruzione `Function` e fino alla prima istruzione `End Function`, `Exit Function` o `Return` rilevata.  
  
 È possibile definire una routine `Function` in un modulo, una classe o una struttura.  Per impostazione predefinita, tale routine è `Public` e pertanto è possibile chiamarla da qualsiasi punto dell'applicazione che disponga di accesso al modulo, alla classe o alla struttura nella quale è stata definita.  
  
 Una routine `Function` può accettare argomenti, come costanti, variabili o espressioni, passati a essa dal codice chiamante.  
  
## Sintassi di dichiarazione  
 La sintassi per dichiarare una routine `Function` è la seguente:  
  
```vb  
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType  
    [Statements]  
End Function  
```  
  
 Nei *modificatori* è possibile specificare il livello di accesso e le informazioni sull'overload, l'override, la condivisione e lo shadowing.  Per ulteriori informazioni, vedere [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Per la dichiarazione di ciascun parametro, si segue una procedura analoga a quella usata per [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md).  
  
### Tipo di dati  
 Ogni routine `Function` dispone di un tipo di dati, così come ogni variabile.  Il tipo di dati è specificato dalla clausola `As` nell'istruzione `Function` e determina il tipo di dati del valore restituito dalla funzione al codice chiamante.  Le dichiarazioni che seguono forniscono un esempio in proposito.  
  
```vb  
Function yesterday() As Date  
End Function  
  
Function findSqrt(ByVal radicand As Single) As Single  
End Function  
```  
  
 Per ulteriori informazioni, vedere "Parti" in [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
## Restituzione di valori  
 Il valore di una routine di `Function` invia di nuovo il codice chiamante viene chiamato il valore restituito.  La routine restituisce il valore in uno dei seguenti modi:  
  
-   Viene utilizzata l'istruzione `Return` per specificare il valore restituito, mentre il controllo viene restituito immediatamente al  programma chiamante.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```vb  
    Function FunctionName [(ParameterList)] As ReturnType  
        ' The following statement immediately transfers control back  
        ' to the calling code and returns the value of Expression.  
        Return Expression  
    End Function  
    ```  
  
-   Assegna un valore al proprio nome di funzione in una o più istruzioni della routine.  Il controllo non viene restituito al programma chiamante fino a quando non viene eseguita un'istruzione `Exit Function` o `End Function`.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```vb  
    Function FunctionName [(ParameterList)] As ReturnType  
        ‘ The following statement does not transfer control back to the calling code.  
        FunctionName = Expression  
        ' When control returns to the calling code, Expression is the return value.  
    End Function  
    ```  
  
 Il vantaggio dell'assegnazione del valore restituito al nome di funzione è rappresentato dal fatto che il controllo non viene restituito dalla routine finché non viene rilevata un'istruzione `Exit Function` o `End Function`.  È quindi possibile assegnare un valore preliminare e, se necessario, modificarlo successivamente.  
  
 Per ulteriori informazioni sulla restituzione di valori, vedere [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md).  Per informazioni sulla restituzione delle matrici, vedere [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## Sintassi di chiamata  
 Una routine `Function` viene chiamata includendone il nome e gli argomenti nella parte destra di un'istruzione di assegnazione o in un'espressione.  È necessario specificare valori per tutti gli argomenti non facoltativi e racchiudere l'elenco degli argomenti tra parentesi.  Se non viene specificato alcun argomento, è anche possibile omettere le parentesi.  
  
 La sintassi per una chiamata a una routine `Function` è la seguente:  
  
 *lvalue* `=` *functionname* `[(` *argumentlist* `)]`  
  
 `If ((`\(\(*functionname*`[(`*argumentlist*`)] / 3) <=`*espressione*`) Then`  
  
 Quando si chiama una routine `Function`, non è necessario utilizzare il relativo valore restituito.  In caso contrario, tutte le operazioni della funzione vengono eseguite ma il valore restituito viene ignorato.  <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> viene spesso chiamato in questo modo.  
  
### Illustrazione della dichiarazione e della chiamata  
 La routine `Function` che segue consente di calcolare il lato più lungo, o ipotenusa, di un triangolo retto, dati i valori degli altri due lati.  
  
 [!code-vb[VbVbcnProcedures#1](./codesnippet/VisualBasic/function-procedures_1.vb)]  
  
 Nell'esempio che segue è illustrata una tipica chiamata a `hypotenuse`.  
  
 [!code-vb[VbVbcnProcedures#6](./codesnippet/VisualBasic/function-procedures_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [How to: Create a Procedure that Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure-that-returns-a-value.md)   
 [How to: Return a Value from a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-return-a-value-from-a-procedure.md)   
 [How to: Call a Procedure That Returns a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-returns-a-value.md)