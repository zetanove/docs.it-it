---
title: "Tipi di dati in Visual Basic | Microsoft Docs"
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
  - "tipi di dati [Visual Basic], dichiarazione"
  - "tipizzazione"
  - "tipi di dati [Visual Basic]"
  - "Visual Basic (codice), tipi di dati"
  - "tipi di dati [Visual Basic], incremento della velocità"
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Tipi di dati in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Il *tipo di dati* di un elemento di programmazione fa riferimento al genere di dati che esso è in grado di contenere e alle modalità di memorizzazione di tali dati.  I tipi di dati sono applicabili a tutti i valori che è possibile memorizzare in un computer o che intervengono nella valutazione di un'espressione.  Qualsiasi variabile, valore letterale, costante, enumerazione, proprietà, parametro di routine, argomento di routine e valore restituito da routine presenta un determinato tipo di dati.  
  
## Tipi di dati dichiarati  
 Un elemento di programmazione viene definito con istruzioni di dichiarazione e il relativo tipo di dati viene specificato mediante la clausola `As`.  Nella tabella seguente sono riportate le istruzioni utilizzate per dichiarare i vari elementi.  
  
|Elemento di programmazione|Dichiarazione del tipo di dati|  
|--------------------------------|------------------------------------|  
|Variabile|In un'istruzione [Dim Statement](../../../../visual-basic/language-reference/statements/dim-statement.md)<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|Literal|Con un carattere di tipo letterale. Vedere "Valori letterali di carattere tipo" in [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|Costante|In un'[Const Statement](../../../../visual-basic/language-reference/statements/const-statement.md)<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|Enumerazione|In un'[Enum Statement](../../../../visual-basic/language-reference/statements/enum-statement.md)<br /><br /> `Public`   `Enum`   `colors`|  
|Proprietà|In un'istruzione [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)<br /><br /> `Property`   `region() As String`|  
|Parametro di routine|In un'[Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md), un'[Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md) o un'[Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|Argomento di routine|Nel codice chiamante, ogni argomento è un elemento di programmazione che è già stato dichiarato o un'espressione che contiene elementi dichiarati<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|Valore restituito da routine|In un'[Function Statement](../../../../visual-basic/language-reference/statements/function-statement.md) o un'[Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 Per un elenco di tipi di dati di Visual Basic, vedere [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## Vedere anche  
 [Type Characters](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Composite Data Types](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Structures](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Efficient Use of Data Types](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)