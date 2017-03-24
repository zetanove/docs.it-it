---
title: "Select...Case Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Select"
  - "vb.Case"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Select statement"
  - "Case statement"
  - "Select...Case statements"
  - "conditional statements, Select Case"
  - "control flow, branching"
  - "Else keyword [Visual Basic], in Select...Case statements"
  - "execution, conditional"
  - "To keyword, in Select...Case statements"
  - "Select Case statement, Select...Case"
  - "Select statement, Select...Case"
  - "Is operator [Visual Basic], in Select...Case statements"
  - "branching, conditional"
  - "Case Else statement, Select...Case"
  - "End keyword, Select Case statements"
  - "Case statement, Select...Case"
ms.assetid: 68877b65-5419-4bf0-a465-20cd0e4c7d44
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Select...Case Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di eseguire uno dei vari gruppi di istruzioni disponibili in base al valore di un'espressione.  
  
## Sintassi  
  
```  
Select [ Case ] testexpression  
    [ Case expressionlist  
        [ statements ] ]  
    [ Case Else  
        [ elsestatements ] ]  
End Select  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`testexpression`|Obbligatorio.  Espressione.  È necessario che restituisca un tipo di dati elementare, ovvero `Boolean`, `Byte`, `Char`, `Date`, `Double`, `Decimal`, `Integer`, `Long`, `Object`, `SByte`, `Short`, `Single`, `String`, `UInteger`, `ULong` e `UShort`.|  
|`expressionlist`|Obbligatoria in un'istruzione `Case`.  Elenco di clausole di espressione che rappresentano i valori delle corrispondenze di `testexpression`.  Le clausole sono separate da una virgola.  Ogni clausola può accettare una delle seguenti forme:<br /><br /> -   *expression1* `To` *expression2*<br />-   \[ `Is` \] *comparisonoperator* *expression*<br />-   *espressione*<br /><br /> La parola chiave `To` può essere utilizzata per specificare i limiti di un intervallo di valori delle corrispondenze di `testexpression`.  Il valore di `expression1` deve essere minore di o uguale al valore di `expression2`.<br /><br /> Utilizzare la parola chiave `Is` con un operatore di confronto \(`=`, `<>`, `<`, `<=`, `>` o `>=`\) per specificare una limitazione in relazione ai valori delle corrispondenze di `testexpression`.  Se non viene fornita la parola chiave `Is` verrà inserita automaticamente prima di *comparisonoperator*.<br /><br /> Se un form specifica solo `expression`, viene considerato un caso speciale del form `Is` in cui *comparisonoperator* è il segno uguale \(`=`\)  Questo form verrà valutato come `testexpression` \= `expression`.<br /><br /> Per le espressioni di `expressionlist` può essere utilizzato qualsiasi tipo di dati, a condizione che sia convertibile in modo implicito nel tipo di `testexpression` e che l'opportuno `comparisonoperator` sia valido per i due tipi con i quali viene utilizzato.|  
|`statements`|Parametro facoltativo.  Una o due istruzioni successive a `Case` che vengono eseguite se `testexpression` corrisponde a qualsiasi clausola `expressionlist`.|  
|`elsestatements`|Parametro facoltativo.  Una o più istruzioni successive a `Case Else` che vengono eseguite se `testexpression` non corrisponde ad alcuna clausola nell'`expressionlist` di una qualsiasi istruzione `Case`.|  
|`End Select`|Consente di terminare la definizione della costruzione `Select`...`Case`.|  
  
## Note  
 Se `testexpression` corrisponde a qualsiasi clausola `expressionlist` di `Case`, le istruzioni che seguono l'istruzione `Case` arrivano fino alla successiva istruzione `Case`, `Case Else` o `End Select`.  Il controllo passa quindi all'istruzione che segue `End Select`.  Se il parametro `testexpression` corrisponde a una clausola `expressionlist` in più clausole `Case`, vengono eseguite solo le istruzioni che seguono la prima corrispodenza.  
  
 L'istruzione `Case Else` viene utilizzata per introdurre il parametro `elsestatements` da eseguire qualora non venga rilevata alcuna corrispondenza fra `testexpression` e la clausola `expressionlist` in nessuna delle altre istruzioni `Case`.  Anche se non richiesto, è consigliabile inserire un'istruzione `Case Else` nella costruzione `Select Case` per la gestione di valori `testexpression` non previsti.  Se nessuna clausola `expressionlist` di `Case` corrisponde a `testexpression` e non esiste un'istruzione `Case Else`, il controllo passa all'istruzione che segue `End Select`.  
  
 In ciascuna clausola `Case` è possibile utilizzare più espressioni o intervalli.  La riga seguente, ad esempio, è valida:  
  
 `Case 1 To 4, 7 To 9, 11, 13, Is > maxNumber`  
  
> [!NOTE]
>  La parola chiave `Is` utilizzata nelle istruzioni `Case` e `Case Else` non è uguale a [Is Operator](../../../visual-basic/language-reference/operators/is-operator.md), che viene utilizzata per il confronto per riferimenti a oggetti.  
  
 È possibile specificare intervalli ed espressioni multiple per le stringhe di caratteri.  Nell'esempio riportato di seguito, `Case` è corrispondente a qualsiasi stringa che è identica a "apples", ha un valore compreso fra "nuts" e "soup" in ordine alfabetico oppure contiene un valore identico al valore corrente di `testItem`.  
  
 `Case "apples", "nuts" To "soup", testItem`  
  
 L'impostazione di `Option Compare` può influire sul confronto tra stringhe.  Per `Option Compare Text`, le stringhe "Apples" e "apples" appaiono identiche al confronto, ma non se si utilizza  `Option Compare Binary`.  
  
> [!NOTE]
>  Un'istruzione `Case` con molteplici clausole può presentare un tipo di comportamento noto come *short circuit*.  In Visual Basic le clausole vengono valutate da sinistra a destra e se una di esse genera una corrispondenza con `testexpression`, le restanti clausole non vengono valutate.  Lo short\-circuit può migliorare le prestazioni, ma può generare risultati imprevisti se ci si aspetta che venga valutata ogni espressione inclusa in `expressionlist`.  Per ulteriori informazioni sul short\-cirtuit, vedere [Boolean Expressions](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md).  
  
 Se il codice in un blocco di istruzioni `Case` o `Case Else` non deve più eseguire alcuna istruzione del blocco, può abbandonare il blocco utilizzando l'istruzione `Exit Select`.  Il controllo viene trasferito immediatamente all'istruzione che segue `End Select`.  
  
 Le costruzioni `Select Case` possono essere annidate.  Ogni costruzione `Select Case` annidata deve avere un'istruzione `End Select` corrispondente e deve essere completamente contenuta in un singolo blocco di istruzioni `Case` o `Case Else` della costruzione esterna `Select Case` in cui è annidata.  
  
## Esempio  
 In questo esempio la costruzione `Select Case` viene utilizzata per scrivere una riga che corrisponde al valore della variabile `number`.  La seconda istruzione `Case` contiene il valore che corrisponde al valore corrente di `number`, in modo che venga eseguita l'istruzione che scrive "Between 6 and 8, inclusive".  
  
 [!code-vb[VbVbalrStatements#54](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/select-case-statement_1.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.Choose%2A>   
 [End Statement](../../../visual-basic/language-reference/statements/end-statement.md)   
 [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Option Compare Statement](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)