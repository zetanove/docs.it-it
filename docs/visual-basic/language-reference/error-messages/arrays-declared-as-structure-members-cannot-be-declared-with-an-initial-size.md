---
title: "Arrays declared as structure members cannot be declared with an initial size | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31043"
  - "bc31043"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31043"
ms.assetid: 5bd90c71-1b78-444b-91e1-4789451ef085
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# Arrays declared as structure members cannot be declared with an initial size
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una matrice di una struttura è stata dichiarata con una dimensione iniziale.  Non è possibile inizializzare alcun elemento di una struttura e la dichiarazione della dimensione di una matrice rappresenta una forma di inizializzazione.  
  
 **ID errore:** BC31043  
  
### Per correggere l'errore  
  
1.  Definire la matrice della struttura come dinamica \(senza dimensione iniziale\).  
  
2.  Se è necessaria una matrice di una determinata dimensione, è possibile ridimensionare una matrice dinamica con un'[ReDim Statement](../../../visual-basic/language-reference/statements/redim-statement.md) quando il codice è in esecuzione.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```  
    Structure demoStruct  
        Public demoArray() As Integer  
    End Structure  
    Sub useStruct()  
        Dim struct As demoStruct  
        ReDim struct.demoArray(9)  
        Struct.demoArray(2) = 777  
    End Sub  
    ```  
  
## Vedere anche  
 [Matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [How to: Declare a Structure](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)