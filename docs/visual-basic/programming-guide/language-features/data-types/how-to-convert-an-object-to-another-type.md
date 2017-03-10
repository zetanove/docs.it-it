---
title: "How to: Convert an Object to Another Type in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "objects [Visual Basic], converting"
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# How to: Convert an Object to Another Type in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per convertire una variabile `Object` in un altro tipo di dati è possibile utilizzare una parola chiave di conversione quale [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md).  
  
## Esempio  
 Nell'esempio riportato di seguito una variabile `Object` viene convertita in `Integer` e in `String`.  
  
```  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 Se si è certi che il contenuto di una variabile `Object` sia di un determinato tipo di dati, è preferibile convertire la variabile in tale tipo di dati.  Se si continua a utilizzare la variabile `Object`, verrà eseguita una conversione *boxing* e *unboxing* \(per un tipo di valore\) o un'*associazione tardiva* \(per un tipo di riferimento\).  Queste operazioni richiedono un tempo di esecuzione aggiuntivo con conseguente riduzione delle prestazioni.  
  
## Compilazione del codice  
 L'esempio presenta i seguenti requisiti:  
  
-   Un riferimento allo spazio dei nomi <xref:System?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Object>   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversions Between Strings and Other Types](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [Array Conversions](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)