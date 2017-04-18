---
title: Funzione routine (Visual Basic) | Documenti di Microsoft
ms.custom: 
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
- Function procedures
- return values, function procedures
- Visual Basic code, procedures
- procedures, calling
- procedures, Function procedures
- syntax, function procedures
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 11baaa6985f0681aa9c67c4f2470fb9917db5b78
ms.lasthandoff: 03/13/2017

---
# <a name="function-procedures-visual-basic"></a>Routine Function (Visual Basic)
Oggetto `Function` routine è una serie di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] racchiuso tra istruzioni il `Function` e `End Function` istruzioni. Il `Function` routine esegue un'attività e quindi restituisce il controllo al codice chiamante. Quando restituisce il controllo, restituisce anche un valore al codice chiamante.  
  
 Ogni volta che viene chiamata la routine, le relative istruzioni di esecuzione, a partire dalla prima istruzione eseguibile dopo il `Function` istruzione e terminando con il primo `End Function`, `Exit Function`, o `Return` istruzione rilevata.  
  
 È possibile definire un `Function` procedura in un modulo, classe o struttura. È `Public` per impostazione predefinita, il che significa è possibile chiamare da qualsiasi punto dell'applicazione che ha accesso al modulo, classe o struttura in cui è stata definita.  
  
 Oggetto `Function` procedure può accettare argomenti, ad esempio costanti, variabili o espressioni, che vengono passate al metodo dal codice chiamante.  
  
## <a name="declaration-syntax"></a>Sintassi di dichiarazione  
 La sintassi per dichiarare un `Function` è la seguente procedura:  
  
```vb  
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType  
    [Statements]  
End Function  
```  
  
 Il *modificatori* possibile specificare il livello di accesso e le informazioni su overload, override, condivisione e shadowing. Per ulteriori informazioni, vedere [istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
 Ciascun parametro viene dichiarato esattamente come avviene per [Sub (routine)](./sub-procedures.md).  
  
### <a name="data-type"></a>Tipo di dati  
 Ogni `Function` routine ha un tipo di dati, solo ogni variabile. Questo tipo di dati è specificato mediante il `As` clausola il `Function` istruzione che determina il tipo di dati del valore restituito dalla funzione al codice chiamante. Le seguenti dichiarazioni di esempio illustrare questo concetto.  
  
```vb  
Function yesterday() As Date  
End Function  
  
Function findSqrt(ByVal radicand As Single) As Single  
End Function  
```  
  
 Per ulteriori informazioni, vedere "Parti" in [istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
## <a name="returning-values"></a>Restituzione di valori  
 Il valore di un `Function` procedure invia back al codice chiamante viene chiamato il relativo valore restituito. La procedura restituisce questo valore in uno dei due modi:  
  
-   Usa il `Return` controllare l'istruzione per specificare il valore restituito e restituisce immediatamente al programma chiamante. Questa condizione è illustrata nell'esempio seguente.  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement immediately transfers control back  
    ' to the calling code and returns the value of Expression.  
    Return Expression  
End Function  
```  
  
-   Assegna un valore per il proprio nome di funzione in una o più istruzioni della procedura. Il controllo viene restituito al programma chiamante fino a un `Exit Function` o `End Function` viene eseguita un'istruzione. Questa condizione è illustrata nell'esempio seguente.  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement does not transfer control back to the calling code.  
    FunctionName = Expression  
    ' When control returns to the calling code, Expression is the return value.  
End Function  
```  
  
 Il vantaggio dell'assegnazione del valore restituito per il nome della funzione è che il controllo viene restituito dalla routine finché non viene rilevata un' `Exit Function` o `End Function` istruzione. In questo modo è possibile assegnare un valore preliminare e modificarlo in un secondo momento se necessario.  
  
 Per ulteriori informazioni sulla restituzione di valori, vedere [istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md). Per informazioni sulla restituzione di matrici, vedere [matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="calling-syntax"></a>Sintassi di chiamata  
 Richiamare un `Function` procedura includendo il nome e gli argomenti sul lato destro di un'istruzione di assegnazione o in un'espressione. È necessario fornire valori per tutti gli argomenti che non sono facoltativi e racchiudere l'elenco di argomenti racchiuso tra parentesi. Se viene fornito alcun argomento, è possibile omettere le parentesi.  
  
 La sintassi per una chiamata a un `Function` è la seguente procedura:  
  
 *lvalue*`=`*functionname* `[(` *argumentlist*    `)]`  
  
 `If ((`*functionname* `[(` *argumentlist* `)] / 3) <=` *espressione*  `) Then`  
  
 Quando si chiama un `Function` procedura, non è necessario utilizzare il valore restituito. In caso contrario, vengono eseguite tutte le azioni della funzione, ma il valore restituito viene ignorato. <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>viene spesso definito in questo modo.</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
### <a name="illustration-of-declaration-and-call"></a>Illustrazione di dichiarazione e chiamata  
 Nell'esempio `Function` procedure calcola il lato più lungo, ovvero l'ipotenusa, di un triangolo rettangolo, in base ai valori degli altri due lati.  
  
 [!code-vb[VbVbcnProcedures n.&1;](./codesnippet/VisualBasic/function-procedures_1.vb)]  
  
 Nell'esempio seguente viene illustrata una tipica chiamata a `hypotenuse`.  
  
 [!code-vb[6 VbVbcnProcedures](./codesnippet/VisualBasic/function-procedures_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Procedura: creare una routine che restituisce un valore](./how-to-create-a-procedure-that-returns-a-value.md)   
 [Procedura: restituire un valore da una routine](./how-to-return-a-value-from-a-procedure.md)   
 [Procedura: Chiamare una routine che restituisce un valore](./how-to-call-a-procedure-that-returns-a-value.md)
