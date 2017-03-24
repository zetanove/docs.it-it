---
title: "Lambda expressions are not valid in the first expression of a &#39;Select Case&#39; statement | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36635"
  - "vbc36635"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36635"
ms.assetid: 74609979-9c03-4864-bbce-f588aa2e0917
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Lambda expressions are not valid in the first expression of a &#39;Select Case&#39; statement
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Non è possibile utilizzare un'espressione lambda per l'espressione di test in un'istruzione `Select Case`.  Le definizioni delle espressioni lambda restituiscono funzioni e l'espressione di test di un'istruzione `Select Case` deve essere un tipo di dati elementare.  
  
 Il codice seguente causa questo errore:  
  
```vb#  
' Select Case (Function(arg) arg Is Nothing)  
    ' List of the cases.  
' End Select  
```  
  
 **ID errore:** BC36635  
  
### Per correggere l'errore  
  
-   Esaminare il codice per determinare se una costruzione condizionale diversa, ad esempio un'istruzione `If...Then...Else`, sia altrettanto adatta.  
  
-   È possibile che si intendesse chiamare la funzione, come mostrato nel codice seguente:  
  
    ```vb#  
    Dim num? As Integer  
    Select Case ((Function(arg? As Integer) arg Is Nothing)(num))  
        ' List of the cases  
    End Select  
    ```  
  
## Vedere anche  
 [Lambda Expressions](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Select...Case Statement](../../../visual-basic/language-reference/statements/select-case-statement.md)