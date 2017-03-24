---
title: "How to: Sort An Array in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Array.Sort"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "arrays [Visual Basic], sorting"
  - "examples [Visual Basic], arrays"
ms.assetid: 9289aeaa-9626-4698-94a7-1d1fd3702b87
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# How to: Sort An Array in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Nell'esempio riportato di seguito una matrice di oggetti `String` denominata `zooAnimals` viene dichiarata, compilata e ordinata alfabeticamente.  
  
## Esempio  
  
```  
Private Sub sortAnimals()  
    Dim zooAnimals(2) As String  
    zooAnimals(0) = "lion"  
    zooAnimals(1) = "turtle"  
    zooAnimals(2) = "ostrich"  
    Array.Sort(zooAnimals)  
End Sub  
```  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Accedere a Mscorlib.dll e allo spazio dei nomi <xref:System>.  
  
## Programmazione efficiente  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   La matrice è vuota \(classe <xref:System.ArgumentNullException>\)  
  
-   La matrice è multidimensionale \(classe <xref:System.RankException>\)  
  
-   In uno o più elementi della matrice non è implementata l'interfaccia <xref:System.IComparable> \(classe <xref:System.InvalidOperationException>\)  
  
## Vedere anche  
 <xref:System.Array.Sort%2A?displayProperty=fullName>   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Troubleshooting Arrays](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)   
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)