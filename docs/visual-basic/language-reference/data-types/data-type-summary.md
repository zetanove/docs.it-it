---
title: "Data Type Summary (Visual Basic) | Microsoft Docs"
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
  - "Boolean data type, supported types in Visual Basic"
  - "storage, order of storage"
  - "data types [Visual Basic], Visual Basic"
  - "Single data type, supported types in Visual Basic"
  - "notation, scientific"
  - "memory requirements, data types"
  - "user-defined data types, Visual Basic"
  - "Date data type, Visual Basic"
  - "Visual Basic, data types"
  - "storage, allocation"
  - "Integer data type, Visual Basic data types"
  - "storage, space"
  - "Variant data types, supported types in Visual Basic"
  - "Char data type, Visual Basic data types"
  - "intrinsic data types"
  - "memory consumption, data types"
  - "single-precision numbers"
  - "data types [Visual Basic], order of storage"
  - "Long data type, supported types in Visual Basic"
  - "String data type, Visual Basic data types"
  - "storage order, data types"
  - "StructLayoutAttribute class, Visual Basic data type storage"
  - "scientific notation"
  - "Double data type, Visual Basic data types"
  - "Byte data type, Visual Basic data types"
  - "Object data type, supported types in Visual Basic"
  - "data types [Visual Basic], storage allocation"
  - "double-precision numbers"
  - "data types [Visual Basic], summary"
  - "dates [Visual Basic], data types"
  - "strings [Visual Basic], data types"
  - "memory consumption"
  - "storage order, controlling in Visual Basic"
  - "data types [Visual Basic], memory requirements"
ms.assetid: e975cdb6-64d8-4a4a-ae27-f3b3ed198ae0
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Data Type Summary (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella tabella riportata di seguito vengono illustrati i tipi di dati Visual Basic, i relativi tipi di supporto in Common Language Runtime, la relativa allocazione di memoria nominale e gli intervalli di valori corrispondenti.  
  
|Tipo Visual Basic|Struttura dei tipi in Common Language Runtime|Allocazione di memoria nominale|Intervallo di valori|  
|-----------------------|---------------------------------------------------|-------------------------------------|--------------------------|  
|[Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md)|<xref:System.Boolean>|Dipende dalla piattaforma di implementazione|`True` o `False`|  
|[Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md)|<xref:System.Byte>|1 byte|Da 0 a 255 \(senza segno\)|  
|[Char](../../../visual-basic/language-reference/data-types/char-data-type.md) \(carattere singolo\)|<xref:System.Char>|2 byte|Da 0 a 65535 \(senza segno\)|  
|[Data](../../../visual-basic/language-reference/data-types/date-data-type.md)|<xref:System.DateTime>|8 byte|Dalle 0.00.00 \(mezzanotte\) dell'1 gennaio 0001 alle 23.59.59 del 31 dicembre 9999|  
|[Decimal](../../../visual-basic/language-reference/data-types/decimal-data-type.md)|<xref:System.Decimal>|16 byte|Da 0 a \+\/\-79.228.162.514.264.337.593.543.950.335 \(\+\/\-7,9...E\+28\) <sup>†</sup> senza decimali; da 0 a \+\/\-7,9228162514264337593543950335 con 28 posizioni decimali;<br /><br /> il numero più piccolo diverso da zero è \+\/\-0,0000000000000000000000000001 \(\+\/\-1E\-28\) <sup>†</sup>|  
|[Double](../../../visual-basic/language-reference/data-types/double-data-type.md) \(virgola mobile a precisione doppia\)|<xref:System.Double>|8 byte|Da \-1,79769313486231570E\+308 a \-4,94065645841246544E\-324 <sup>†</sup> per i valori negativi;<br /><br /> Da 4,94065645841246544E\-324 a 1,79769313486231570E\+308 <sup>†</sup> per i valori positivi|  
|[Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)|<xref:System.Int32>|4 byte|Da \-2.147.483.648 a 2.147.483.647 \(con segno\)|  
|[Long](../../../visual-basic/language-reference/data-types/long-data-type.md) \(valore long integer\)|<xref:System.Int64>|8 byte|Da \-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 \(9,2...E\+18 <sup>†</sup>\) \(con segno\)|  
|[Object](../../../visual-basic/language-reference/data-types/object-data-type.md)|<xref:System.Object> \(classe\)|4 byte su piattaforma a 32 bit<br /><br /> 8 byte su piattaforma a 64 bit|In una variabile di tipo `Object` è possibile memorizzare qualsiasi tipo|  
|[SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|<xref:System.SByte>|1 byte|Da \-128 a 127 \(con segno\)|  
|[Short](../../../visual-basic/language-reference/data-types/short-data-type.md) \(valore short integer\)|<xref:System.Int16>|2 byte|Da \-32.768 a 32.767 \(con segno\)|  
|[Single](../../../visual-basic/language-reference/data-types/single-data-type.md) \(virgola mobile a precisione singola\)|<xref:System.Single>|4 byte|Da \-3,4028235E\+38 a \-1,401298E\-45 <sup>†</sup> per i valori negativi;<br /><br /> Da 1,401298E\-45 a 3,4028235E\+38 <sup>†</sup> per i valori positivi|  
|[String](../../../visual-basic/language-reference/data-types/string-data-type.md) \(lunghezza variabile\)|<xref:System.String> \(classe\)|Dipende dalla piattaforma di implementazione|Da 0 a circa 2 miliardi di caratteri Unicode|  
|[UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|<xref:System.UInt32>|4 byte|Da 0 a 4.294.967.295 \(senza segno\)|  
|[ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md)|<xref:System.UInt64>|8 byte|Da 0 a 18.446.744.073.709.551.615 \(1,8...E\+19 <sup>†</sup>\) \(senza segno\)|  
|[Tipo di dati definito dall'utente](../../../visual-basic/language-reference/data-types/user-defined-data-type.md) \(struttura\)|\(eredita da <xref:System.ValueType>\)|Dipende dalla piattaforma di implementazione|Ciascun membro della struttura presenta un intervallo determinato dal relativo tipo di dati e indipendente dagli intervalli degli altri membri|  
|[UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md)|<xref:System.UInt16>|2 byte|Da 0 a 65.535 \(senza segno\)|  
  
 <sup>†</sup> In *notazione scientifica*, la lettera "E" si riferisce a un potenza di 10.  3,56E\+2 corrisponde pertanto a 3.56 x 10<sup>2</sup> o 356 e 3,56E\-2 corrisponde a 3.56 \/ 10<sup>2</sup> o 0,0356.  
  
> [!NOTE]
>  Per le stringhe contenenti testo utilizzare la funzione <xref:Microsoft.VisualBasic.Strings.StrConv%2A> per eseguire la conversione da un formato di testo a un altro.  
  
 Oltre a specificare un tipo di dati in un'istruzione di dichiarazione, è possibile definire il tipo di dati degli elementi di programmazione utilizzando un carattere tipo.  Vedere [Type Characters](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md).  
  
## Consumo di memoria  
 Quando si dichiara un tipo di dati elementare, supporre che il relativo consumo di memoria corrisponda all'allocazione di memoria nominale presenta alcuni rischi.  È opportuno considerare i seguenti aspetti:  
  
-   **Assegnazione di memoria.** Utilizzando Common Language Runtime è possibile assegnare memoria in base alle caratteristiche correnti della piattaforma su cui viene eseguita l'applicazione.  Se la memoria è quasi piena, è possibile comprimere il più possibile gli elementi dichiarati.  In altri casi, è possibile allineare i relativi indirizzi di memoria ai limiti dell'hardware al fine di ottimizzare le prestazioni.  
  
-   **Ampiezza della piattaforma.** L'assegnazione di memoria varia a seconda che venga eseguita su una piattaforma a 64 o a 32 bit.  
  
### Tipi di dati compositi  
 Le stesse considerazioni si applicano a ciascun membro di un tipo di dati composito, ad esempio una struttura o una matrice.  Non è sufficiente sommare le allocazioni di memoria nominali dei membri del tipo.  È necessario inoltre considerare altri aspetti, come quelli illustrati di seguito:  
  
-   **Overhead.** Alcuni tipi compositi sono caratterizzati da requisiti di memoria aggiuntivi.  Per una matrice, ad esempio, viene utilizzata memoria aggiuntiva sia per la matrice stessa che per ciascuna dimensione.  Su una piattaforma a 32 bit tale overhead corrisponde attualmente a 12 byte più 8 byte per ciascuna dimensione.  Su una piattaforma a 64 bit tale requisito risulta raddoppiato.  
  
-   **Layout di memoria.** Non è possibile presupporre con certezza che l'ordine di archiviazione in memoria corrisponda all'ordine di dichiarazione,  né tantomeno ipotizzare l'allineamento dei byte, ad esempio in base a un limite di 2 o 4 byte.  Quando si definisce una classe o una struttura ed è necessario controllare il layout di memoria dei relativi membri, è possibile applicare l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute> alla classe o alla struttura.  
  
### Overhead di Object  
 Un tipo di dati `Object` che fa riferimento a un tipo elementare o composito utilizza 4 byte in aggiunta ai dati contenuti nel tipo di dati.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.StrConv%2A>   
 <xref:System.Runtime.InteropServices.StructLayoutAttribute>   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Type Characters](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)