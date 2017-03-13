---
title: "Utilizzo di foreach con matrici (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#], foreach"
  - "foreach (istruzione) [C#], utilizzo con matrici"
ms.assetid: 5f2da2a9-1f56-4de5-94cc-e07f4f7a0244
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Utilizzo di foreach con matrici (Guida per programmatori C#)
In C\# è disponibile anche l'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  Questa istruzione offre un metodo semplice e diretto per scorrere gli elementi di una matrice o qualsiasi raccolta enumerabile.  L'istruzione `foreach` elabora gli elementi nell'ordine restituito dalla matrice o dall'enumeratore del tipo di raccolta, in genere dall'elemento zero all'ultimo.  Il codice che segue, ad esempio, consente la creazione di una matrice denominata `numbers` e di scorrere tale matrice con l'istruzione `foreach`:  
  
 [!code-cs[csProgGuideArrays#28](../../../csharp/programming-guide/arrays/codesnippet/CSharp/using-foreach-with-arrays_1.cs)]  
  
 Con le matrici multidimensionali è possibile utilizzare lo stesso metodo per scorrere gli elementi, ad esempio:  
  
 [!code-cs[csProgGuideArrays#29](../../../csharp/programming-guide/arrays/codesnippet/CSharp/using-foreach-with-arrays_2.cs)]  
  
 Con le matrici multidimensionali, tuttavia, l'utilizzo di un ciclo [for](../../../csharp/language-reference/keywords/for.md) annidato fornisce maggiore controllo sugli elementi della matrice.  
  
## Vedere anche  
 <xref:System.Array>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Matrici](../../../csharp/programming-guide/arrays/index.md)   
 [Matrici unidimensionali](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)   
 [Matrici multidimensionali](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)   
 [Matrici irregolari](../../../csharp/programming-guide/arrays/jagged-arrays.md)