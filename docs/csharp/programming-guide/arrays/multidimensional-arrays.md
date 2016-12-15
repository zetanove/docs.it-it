---
title: "Matrici multidimensionali (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], multidimensionali"
  - "Matrici multidimensionali (C#)"
ms.assetid: 020ce02e-7dff-4273-8e53-bf0b33747232
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Matrici multidimensionali (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le matrici possono avere più di una dimensione.  La dichiarazione che segue, ad esempio, crea una matrice bidimensionale di quattro righe e due colonne.  
  
 [!code-cs[csProgGuideArrays#11](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_1.cs)]  
  
 La dichiarazione che segue crea una matrice a tre dimensioni, 4, 2 e 3.  
  
 [!code-cs[csProgGuideArrays#12](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_2.cs)]  
  
## Inizializzazione di una matrice  
 È possibile inizializzare la matrice al momento della dichiarazione come illustrato nel seguente esempio.  
  
 [!code-cs[csProgGuideArrays#13](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_3.cs)]  
  
 È inoltre possibile inizializzare la matrice senza specificarne il numero di dimensioni.  
  
 [!code-cs[csProgGuideArrays#14](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_4.cs)]  
  
 Se si sceglie di dichiarare una variabile di matrice senza inizializzazione, sarà necessario utilizzare l'operatore `new` per assegnare una matrice alla variabile.  L'utilizzo di `new` è illustrato nell'esempio seguente.  
  
 [!code-cs[csProgGuideArrays#15](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_5.cs)]  
  
 Nell'esempio seguente viene assegnato un valore a un elemento specifico della matrice.  
  
 [!code-cs[csProgGuideArrays#16](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_6.cs)]  
  
 Analogamente, nell'esempio riportato di seguito viene ottenuto il valore di un elemento specifico di una matrice e viene assegnato alla variabile `elementValue`.  
  
 [!code-cs[csProgGuideArrays#42](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_7.cs)]  
  
 Nell'esempio di codice riportato di seguito gli elementi della matrice vengono inizializzati in base ai valori predefiniti, ad eccezione delle matrici irregolari.  
  
 [!code-cs[csProgGuideArrays#17](../../../csharp/programming-guide/arrays/codesnippet/CSharp/multidimensional-arrays_8.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici unidimensionali](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Matrici irregolari](../../../csharp/programming-guide/arrays/jagged-arrays.md)