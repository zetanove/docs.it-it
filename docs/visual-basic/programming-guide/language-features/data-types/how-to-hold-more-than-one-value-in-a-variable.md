---
title: "How to: Hold More Than One Value in a Variable (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "classes [Visual Basic], composite data types"
  - "composite types"
  - "composite data types"
  - "data types [Visual Basic], composite"
  - "arrays [Visual Basic], composite data types"
  - "structures, composite data types"
  - "arrays [Visual Basic], compilation errors"
  - "types [Visual Basic], composite"
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Hold More Than One Value in a Variable (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Per poter contenere più valori, una variabile deve essere dichiarata come *tipo di dati composito*.  
  
 I [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md) comprendono strutture, matrici e classi.  Una variabile di tipo composito può contenere una combinazione di tipi di dati elementari e altri tipi compositi.  Le strutture e le classi possono contenere sia codice che dati.  
  
### Per inserire più valori in una variabile  
  
1.  Determinare il tipo di dati composito che si desidera utilizzare per la variabile.  
  
2.  Definire il tipo di dati composito, se non è già stato definito, affinché possa essere utilizzato dalla variabile.  
  
    -   Definire una struttura con un'[Structure Statement](../../../../visual-basic/language-reference/statements/structure-statement.md).  
  
    -   Definire una matrice con un'[Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md).  
  
    -   Definire una classe con un'[Class Statement](../../../../visual-basic/language-reference/statements/class-statement.md).  
  
3.  Dichiarare la variabile con un'istruzione `Dim`.  
  
4.  Dopo il nome della variabile inserire una clausola `As`.  
  
5.  Dopo la parola chiave `As` inserire il nome del tipo di dati composito appropriato.  
  
## Vedere anche  
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)