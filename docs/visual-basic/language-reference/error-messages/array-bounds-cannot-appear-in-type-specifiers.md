---
title: "Array bounds cannot appear in type specifiers | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30638"
  - "bc30638"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30638"
ms.assetid: 93b654f4-70fa-4a48-baed-ffae42075550
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Array bounds cannot appear in type specifiers
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Non è possibile dichiarare le dimensioni di matrice come parte di un identificatore del tipo di dati.  
  
 **ID errore:** BC30638  
  
### Per correggere l'errore  
  
-   Specificare la dimensione della matrice subito dopo il nome della variabile, invece di inserire la dimensione di matrice dopo il tipo, come illustrato nel seguente esempio.  
  
    ```  
    Dim Array(8) As Integer   
    ```  
  
-   Definire una matrice e inizializzarla con il numero desiderato di elementi, come illustrato nel seguente esempio.  
  
    ```  
    Dim Array2() As Integer = New Integer(8) {}  
    ```  
  
## Vedere anche  
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)