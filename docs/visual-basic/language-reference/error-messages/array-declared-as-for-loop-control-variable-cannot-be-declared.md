---
title: "Array declared as for loop control variable cannot be declared with an initial size | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32039"
  - "bc32039"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32039"
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Array declared as for loop control variable cannot be declared with an initial size
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In un ciclo `For Each` che esegue l'inizializzazione di una matrice viene utilizzata la stessa matrice come variabile *element* di iterazione.  
  
 Le istruzioni seguenti mostrano come viene generato questo errore:  
  
```  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 La prima istruzione `For Each` è il modo corretto per accedere agli elementi di `arrayList`.  La seconda istruzione `For Each` genera l'errore.  
  
 **ID errore:** BC32039  
  
### Per correggere l'errore  
  
-   Rimuovere l'inizializzazione dalla dichiarazione della variabile *element* di iterazione.  
  
## Vedere anche  
 [Istruzione For...Next](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)