---
title: "Anonymous type member name can be inferred only from a simple or qualified name with no arguments | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36556"
  - "bc36556"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36556"
ms.assetid: e3ba1f33-3a71-4f03-9b04-ed5ec17de17c
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Anonymous type member name can be inferred only from a simple or qualified name with no arguments
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Non è possibile dedurre un nome del membro di tipo anonimo da un'espressione complessa.  
  
```vb#  
Dim numbers() As Integer = {1, 2, 3, 4, 5}  
' Not valid.  
' Dim instanceName1 = New With {numbers(3)}  
```  
  
 Per ulteriori informazioni sulle origini da cui i tipi anonimi possono dedurre o meno i nomi e i tipi dei membri, vedere [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md).  
  
 **ID errore:** BC36556  
  
### Per correggere l'errore  
  
-   Assegnare l'espressione al nome di un membro, come mostrato nel codice seguente:  
  
    ```  
    Dim instanceName2 = New With {.number = numbers(3)}  
    ```  
  
## Vedere anche  
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Procedura: dedurre tipi e nomi di proprietà nelle dichiarazioni di tipo anonimo](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)