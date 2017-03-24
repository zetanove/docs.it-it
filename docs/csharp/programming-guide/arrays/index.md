---
title: "Matrici (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "matrici [C#]"
  - "linguaggio C#, matrici"
ms.assetid: bb79bdde-e570-4c30-adb0-1dd5759ae041
caps.latest.revision: 33
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 33
---
# Matrici (Guida per programmatori C#)
È possibile archiviare più variabili dello stesso tipo in una struttura di dati di matrice.  Dichiarare una matrice specificando il tipo degli elementi.  
  
 `type[] arrayName;`  
  
 Negli esempi riportati di seguito vengono create matrici unidimensionali, multidimensionali e irregolari:  
  
 [!code-cs[csProgGuideArrays#1](../../../csharp/programming-guide/arrays/codesnippet/CSharp/index_1.cs)]  
  
## Cenni preliminari sulle matrici  
 Di seguito sono riportate le caratteristiche delle matrici:  
  
-   Una matrice può essere [unidimensionale](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md), [multidimensionale](../../../csharp/programming-guide/arrays/multidimensional-arrays.md) o [irregolare](../../../csharp/programming-guide/arrays/jagged-arrays.md).  
  
-   Il numero di dimensioni e la lunghezza di ogni dimensione sono definiti durante la creazione dell'istanza della matrice.  Questi valori non possono essere modificati per la durata dell'istanza.  
  
-   I valori predefiniti degli elementi numerici della matrice sono impostati su zero, mentre gli elementi di riferimento sono impostati su null.  
  
-   Gli elementi di una matrice irregolare sono tipi di riferimento inizializzati su `null`.  
  
-   Le matrici sono a indice zero. Una matrice con `n` elementi viene indicizzata da `0` a `n-1`.  
  
-   Gli elementi di una matrice possono essere di qualsiasi tipo, anche di tipo matrice.  
  
-   I tipi matrice sono [tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md) derivati dal tipo di base astratto <xref:System.Array>.  Poiché questo tipo implementa <xref:System.Collections.IEnumerable> e <xref:System.Collections.Generic.IEnumerable%601>, è possibile utilizzare l'iterazione [foreach](../../../csharp/language-reference/keywords/foreach-in.md) su tutte le matrici in C\#.  
  
## Sezioni correlate  
  
-   [Matrici come oggetti](../../../csharp/programming-guide/arrays/arrays-as-objects.md)  
  
-   [Utilizzo di foreach con matrici](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
-   [Passaggio di matrici come argomenti](../../../csharp/programming-guide/arrays/passing-arrays-as-arguments.md)  
  
-   [Passaggio di matrici mediante ref e out](../../../csharp/programming-guide/arrays/passing-arrays-using-ref-and-out.md)  
  
-   [Informazioni sulle variabili](http://go.microsoft.com/fwlink/?LinkId=221230) in [Introduzione a Visual C\# 2010](http://go.microsoft.com/fwlink/?LinkId=221214)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [Array Collection Type](http://msdn.microsoft.com/it-it/8a9964de-8941-47b1-a3cf-a01bc88db9e8)