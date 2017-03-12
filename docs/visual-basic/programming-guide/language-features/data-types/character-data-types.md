---
title: "Character Data Types (Visual Basic) | Microsoft Docs"
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
  - "data types [Visual Basic], character"
  - "String data type, character data types"
  - "character data types [Visual Basic]"
  - "Char data type, character data types"
  - "data types [Visual Basic], choosing"
ms.assetid: 902479ef-1679-47fc-9911-0c1c5008226c
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# Character Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili *tipi di dati carattere* per la gestione dei caratteri stampabili e visualizzabili.  Sebbene gestiscano entrambi caratteri Unicode, `Char` contiene un singolo carattere, mentre `String` ne contiene un numero indefinito.  
  
 Per un confronto side\-by\-side dei tipi di dati di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)], vedere [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## Tipo Char  
 Il tipo di dati `Char` è un unico carattere Unicode a due byte \(16 bit\).  Se una variabile memorizza sempre esattamente un carattere, dichiararla come `Char`.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbVbalrCharTypes#1](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/visualbasic/character-data-types_1.vb)]  
  
 Ogni valore possibile in una variabile `Char` o `String` è un *punto di codice*, o codice carattere, del set di caratteri Unicode.  I caratteri Unicode comprendono il set di caratteri ASCII di base, altre lettere di diversi alfabeti, accenti, simboli di valuta, frazioni, segni diacritici, oltre a simboli matematici e tecnici.  
  
> [!NOTE]
>  Il set di caratteri Unicode riserva i punti di codice da D800 a DFFF \(da 55296 a 55551 in formato decimale\) alle *coppie di surrogati*, per cui sono necessari due valori a 16 bit per rappresentare un singolo punto di codice.  Una variabile `Char` non può contenere una coppia di surrogati, mentre una variabile `String` può contenere coppie di questo tipo utilizzando due posizioni.  
  
 Per ulteriori informazioni, vedere [Char Data Type](../../../../visual-basic/language-reference/data-types/char-data-type.md).  
  
## Tipo String  
 Il tipo di dati `String` è una sequenza di zero o più caratteri Unicode a due byte \(16 bit\).  Se una variabile può contenere un numero indefinito di caratteri, dichiararla come `String`.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbVbalrCharTypes#2](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/visualbasic/character-data-types_2.vb)]  
  
 Per ulteriori informazioni, vedere [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md).  
  
## Vedere anche  
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)