---
title: "Nullable type inference is not supported in this context | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36629"
  - "bc36629"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36629"
ms.assetid: 0a1e2dbc-d9a4-433d-9306-c5540782b81d
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Nullable type inference is not supported in this context
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I tipi di valore e le strutture possono essere dichiarati nullable.  
  
```vb#  
Dim a? As Integer  
Dim b As Integer?  
```  
  
 Tuttavia, non è possibile utilizzare la dichiarazione nullable in combinazione con l'inferenza dei tipi.  Negli esempi seguenti viene generato questo errore.  
  
```vb#  
' Not valid.  
' Dim c? = 10  
' Dim d? = a  
```  
  
 **ID errore:** BC36629  
  
### Per correggere l'errore  
  
-   Utilizzare una clausola `As` per dichiarare la variabile come nullable.  
  
## Vedere anche  
 [Nullable Value Types](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)