---
title: "Optional (Visual Basic) | Microsoft Docs"
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
  - "vb.Optional"
  - "vb.optional"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Optional keyword, contexts"
  - "Optional keyword"
ms.assetid: 4571ce88-a539-4115-b230-54eb277c6aa7
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Optional (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica che è possibile omettere un argomento di routine quando si chiama la routine.  
  
## Note  
 Per ogni parametro facoltativo, è necessario specificare un'espressione costante come valore predefinito del parametro.  Se l'espressione restituisce [Nothing](../../../visual-basic/language-reference/nothing.md), il valore predefinito del tipo di dati valore viene utilizzato come valore predefinito del parametro.  
  
 Se l'elenco di parametri contiene un parametro facoltativo, ciascun parametro dall'deve essere facoltativo.  
  
 Il modificatore `Optional` può essere utilizzato nei seguenti contesti:  
  
-   [Istruzione Declare](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
-   [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Istruzione Property](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
> [!NOTE]
>  Nel chiamare una routine con o senza parametri facoltativi, è possibile passare gli argomenti tramite posizione o per nome.  Per ulteriori informazioni, vedere [Passing Arguments by Position and by Name](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md).  
  
> [!NOTE]
>  È inoltre possibile definire una routine con parametri facoltativi utilizzando l'overload.  Se si dispone di un parametro facoltativo, è possibile definire due versioni di overload della routine, di che accetta il parametro e che non fa.  Per ulteriori informazioni, vedere [Procedure Overloading](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).  
  
## Esempio  
 Nell'esempio seguente viene definita una routine con un parametro facoltativo.  
  
```  
Public Function FindMatches(ByRef values As List(Of String),  
                            ByVal searchString As String,  
                            Optional ByVal matchCase As Boolean = False) As List(Of String)  
  
    Dim results As IEnumerable(Of String)  
  
    If matchCase Then  
        results = From v In values  
                  Where v.Contains(searchString)  
    Else  
        results = From v In values  
                  Where UCase(v).Contains(UCase(searchString))  
    End If  
  
    Return results.ToList()  
End Function  
```  
  
## Esempio  
 Nell'esempio seguente viene illustrato come chiamare una routine con gli argomenti passati dalla posizione e gli argomenti passati per nome.  La routine presenta due parametri facoltativi.  
  
 [!code-vb[VbVbalrKeywords#21](../../../visual-basic/language-reference/codesnippet/VisualBasic/optional_1.vb)]  
  
## Vedere anche  
 [Parameter List](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Optional Parameters](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)