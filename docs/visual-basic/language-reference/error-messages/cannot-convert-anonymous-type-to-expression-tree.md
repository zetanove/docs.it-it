---
title: "Cannot convert anonymous type to expression tree because it contains a field that is used in the initialization of another field | Microsoft Docs"
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
  - "bc36548"
  - "vbc36548"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36548"
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Cannot convert anonymous type to expression tree because it contains a field that is used in the initialization of another field
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il compilatore non accetta la conversione di un tipo anonimo in una struttura ad albero dell'espressione quando una proprietà del tipo anonimo è utilizzata per inizializzare un'altra proprietà del tipo anonimo.  Nel codice riportato di seguito, ad esempio, `Prop1` viene dichiarato nell'elenco di inizializzazione e quindi utilizzato come valore iniziale per `Prop2`.  
  
```vb#  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **ID errore:** BC36548  
  
### Per correggere l'errore  
  
-   Assegnare il valore iniziale per `Prop1` a una variabile locale.  Assegnare la variabile a `Prop1` e `Prop2`, come mostrato nel codice seguente.  
  
    ```  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## Vedere anche  
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Strutture ad albero dell'espressione](../Topic/Expression%20Trees%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: Usare strutture ad albero dell'espressione per la compilazione di query dinamiche](../Topic/How%20to:%20Use%20Expression%20Trees%20to%20Build%20Dynamic%20Queries%20\(C%23%20and%20Visual%20Basic\).md)