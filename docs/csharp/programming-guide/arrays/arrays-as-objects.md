---
title: "Matrici come oggetti (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], come oggetti"
ms.assetid: f76d4403-bd0a-42a0-9bc8-694c55b2c926
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Matrici come oggetti (Guida per programmatori C#)
In C\# le matrici sono in realtà oggetti e non solo aree indirizzabili di memoria contigua come in C e C\+\+.  <xref:System.Array> rappresenta il tipo di base astratto di tutti i tipi di matrice.  È quindi possibile utilizzare le proprietà e gli altri membri di classe previsti da <xref:System.Array>.  È ad esempio possibile utilizzare la proprietà <xref:System.Array.Length%2A> per ottenere la lunghezza di una matrice.  Nel codice riportato di seguito viene assegnata la lunghezza della matrice `numbers`, `5`, a una variabile denominata `lengthOfNumbers`:  
  
 [!code-cs[csProgGuideArrays#3](../../../csharp/programming-guide/arrays/codesnippet/csharp/arrays-as-objects_1.cs)]  
  
 La classe <xref:System.Array> offre numerosi altri utili metodi e proprietà, quali metodi per ordinare, copiare le matrici ed effettuare ricerche all'interno di esse.  
  
## Esempio  
 In questo esempio viene utilizzata la proprietà <xref:System.Array.Rank%2A> per visualizzare il numero di dimensioni di una matrice.  
  
 [!code-cs[csProgGuideArrays#2](../../../csharp/programming-guide/arrays/codesnippet/csharp/arrays-as-objects_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici unidimensionali](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)   
 [Matrici irregolari](../../../csharp/programming-guide/arrays/jagged-arrays.md)