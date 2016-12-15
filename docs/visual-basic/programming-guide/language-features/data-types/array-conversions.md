---
title: "Array Conversions (Visual Basic) | Microsoft Docs"
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
  - "arrays [Visual Basic], converting type"
  - "type conversion, arrays"
  - "conversions, type"
  - "arrays [Visual Basic], data types"
  - "conversions, data type"
  - "object arrays, converting type"
  - "data type conversion, array conversions"
  - "conversions, array types"
  - "object arrays"
ms.assetid: fceff7d2-a1b7-44c7-b9aa-8bd831d8a444
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Array Conversions (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile convertire un tipo di matrice in un altro tipo di matrice, ma solo in presenza di determinate condizioni:  
  
-   **Numero di dimensioni uguale.** È necessario che le matrici presentino lo stesso numero di dimensioni.  Non è tuttavia necessario che corrispondano anche le lunghezze delle rispettive dimensioni.  
  
-   **Tipo di dati degli elementi.** È necessario che i tipi di dati degli elementi di entrambe le matrici siano tipi di riferimento.  Non è possibile convertire una matrice `Integer` in una matrice `Long` né in una matrice `Object`, perché è interessato almeno un tipo valore.  Per ulteriori informazioni, vedere [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
-   **Possibilità di conversione.** È necessario che sia possibile una conversione, sia essa verso un tipo di dati più grande o più piccolo, tra i tipi di elementi delle due matrici.  Un esempio di mancato adempimento di questo requisito è un tentativo di conversione fra una matrice `String` e una matrice di una classe derivata da <xref:System.Attribute?displayProperty=fullName>.  I due tipi non hanno alcun elemento in comune e la conversione tra loro non è possibile.  
  
 La conversione di un tipo di matrice in un altro è di ampliamento o di restrizione a seconda che la conversione dei rispettivi elementi sia di ampliamento o restrizione.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).  
  
## Conversione in una matrice Object  
 Quando si dichiara una matrice `Object` senza inizializzarla, il tipo di elemento della matrice è `Object` e rimarrà tale finché non verrà inizializzata.  Quando viene impostata su una matrice di una classe specifica, assume il tipo di quella classe.  Tuttavia il tipo sottostante è ancora `Object` ed è possibile quindi impostarla successivamente su un'altra matrice di una classe non correlata.  Poiché tutte le classi derivano da `Object`, è possibile trasformare il tipo di elemento della matrice da qualsiasi classe in qualsiasi altra classe.  
  
 Nell'esempio che segue non è possibile alcuna conversione tra i tipi `student` e `String`, ma entrambi derivano da `Object`, pertanto tutte le assegnazioni sono valide.  
  
```  
' Assume student has already been defined as a class.  
Dim testArray() As Object  
' testArray is still an Object array at this point.  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
testArray = New student(3) {}  
' testArray is now of type student().  
testArray = names  
' testArray is now a String array.  
```  
  
### Tipo sottostante di una matrice  
 Se originariamente si dichiara una matrice con una classe specifica, il tipo di elemento sottostante sarà rappresentato da quella classe.  Se successivamente viene impostata su una matrice di un'altra classe, è necessario che esista una conversione tra le due classi.  
  
 Nell'esempio che segue `students` è una matrice `student`.  Dal momento che non è possibile alcuna conversione tra `String` e `student`, l'ultima istruzione avrà esito negativo.  
  
```  
Dim students() As student  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
students = New Student(3) {}  
' The following statement fails at compile time.  
students = names  
```  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversions Between Strings and Other Types](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [How to: Convert an Object to Another Type in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)