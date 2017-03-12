---
title: "Long Data Type (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Long"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "identifier type characters, &"
  - "numbers, whole"
  - "whole numbers"
  - "integral data types"
  - "& identifier type character"
  - "integer numbers"
  - "literal type characters, L"
  - "numbers, integer"
  - "integers, data types"
  - "L literal type character"
  - "integers, types"
  - "Long keyword"
  - "data types [Visual Basic], integral"
  - "data types [Visual Basic], assigning"
  - "Long data type"
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Long Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene valori integer a 64 bit \(8 byte\) con segno compresi nell'intervallo tra \-9.223.372.036.854.775.808 e 9.223.372.036.854.775.807 \(9,2...E\+18\).  
  
## Note  
 Utilizzare il tipo di dati `Long` per contenere numeri interi troppo grandi per essere compresi nel tipo di dati `Integer`.  
  
 Il valore predefinito di `Long` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti i tipi `Long` hanno un'ampiezza dei dati diversa \(32 bit\).  Se si passa un argomento a 32 bit a un componente di questo tipo, nel nuovo codice Visual Basic è necessario eseguirne la dichiarazione come `Integer` anziché come `Long`.  
  
     Inoltre, l'automazione non supporta i numeri interi a 64 bit in Windows 95, Windows 98 Windows o Windows 2000.  Non è possibile passare un argomento Visual Basic `Long` a un componente di automazione su questi sistemi operativi.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `Long` viene convertito verso il tipo più `Decimal`, `Single` o `Double`.  È pertanto possibile convertire `Long` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `L` a un valore letterale, se ne determina la conversione nel tipo di dati `Long`.  Aggiungendo il carattere identificatore di tipo `&` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Long`.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Int64?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Int64>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Integer Data Type](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Short Data Type](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)