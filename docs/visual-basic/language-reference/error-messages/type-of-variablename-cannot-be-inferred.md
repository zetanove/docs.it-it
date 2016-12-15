---
title: "Type of &#39;&lt;variablename&gt;&#39; cannot be inferred because the loop bounds and the step variable do not widen to the same type | Microsoft Docs"
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
  - "bc30982"
  - "vbc30982"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30982"
ms.assetid: 741e85d9-a747-42ad-a1e1-a3f1928aaff5
caps.latest.revision: 30
caps.handback.revision: 30
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type of &#39;&lt;variablename&gt;&#39; cannot be inferred because the loop bounds and the step variable do not widen to the same type
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È stato scritto un ciclo `For...Next` nel quale il compilatore non è in grado di dedurre un tipo di dati per la variabile di controllo del ciclo poiché si verificano le seguenti condizioni:  
  
-   Il tipo di dati della variabile di controllo del ciclo non è specificato con una clausola `As`.  
  
-   I limiti del ciclo e la clausola dell'istruzione contengono almeno due tipi di dati.  
  
-   Non esiste alcuna conversione standard tra i tipi di dati.  
  
 Pertanto, il compilatore non è in grado di dedurre il tipo di dati della variabile di controllo di un ciclo.  
  
 Nell'esempio seguente, la clausola dell'istruzione è un carattere e i limiti del ciclo sono entrambi numeri interi.  Poiché non vi è conversione standard tra caratteri e numeri interi, viene segnalato questo errore.  
  
```vb#  
Dim stepVar = "1"c  
Dim m = 0  
Dim n = 20  
  
' Not valid.  
' For i = 1 To 10 Step stepVar  
    ' Loop processing  
' Next  
```  
  
 **ID errore:** BC30982  
  
### Per correggere l'errore  
  
-   Modificare i tipi dei limiti del ciclo e della clausola dell'istruzione secondo necessità, così che almeno uno di essi sia un tipo al quale gli altri possano essere convertiti.  Nell'esempio precedente modificare il tipo di `stepVar` con `Integer`.  
  
    ```  
    Dim stepVar = 1  
    ```  
  
     \-oppure\-  
  
    ```  
    Dim stepVar As Integer = 1  
    ```  
  
-   Utilizzare le funzioni di conversione esplicite per convertire i limiti del ciclo e la clausola dell'istruzione nei tipi appropriati.  Nell'esempio precedente, applicare la funzione `Val` a `stepVar`.  
  
    ```  
    For i = 1 To 10 Step Val(stepVar)  
        ' Loop processing  
    Next  
    ```  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Conversion.Val%2A>   
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer Statement](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)