---
title: "UShort Data Type (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ushort"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "numbers, whole"
  - "literal type characters, US"
  - "whole numbers"
  - "integral data types"
  - "integer numbers"
  - "numbers, integer"
  - "integers, data types"
  - "integers, types"
  - "data types [Visual Basic], integral"
  - "UShort data type"
  - "US literal type characters"
ms.assetid: 138db892-665d-4ba8-9cae-d8d91c4a8f39
caps.latest.revision: 16
caps.handback.revision: 16
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# UShort Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene valori integer a 16 bit \(2 byte\) senza segno in un intervallo compreso tra 0 e 65.535.  
  
## Note  
 Utilizzare il tipo di dati `UShort` per contenere dati binari di dimensioni eccessive per `Byte`.  
  
 Il valore predefinito di `UShort` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** Poiché `UShort` è un tipo senza segno, non può rappresentare un numero negativo.  Se si utilizza l'operatore unario meno \(`-`\) su un'espressione che restituisce un valore di tipo `UShort`, tale espressione verrà innanzitutto convertita nel tipo `Integer`.  
  
-   **Compatibilità con CLS.** Il tipo di dati `UShort` non fa parte delle specifiche [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), pertanto un codice compatibile con le specifiche CLS non può utilizzare un componente che utilizza tale tipo di dati.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `UShort` viene convertito verso i tipi più grandi `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single` e `Double`.  È pertanto possibile convertire `UShort` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo i caratteri di tipo letterale `US` a un valore letterale, se ne determina la conversione nel tipo di dati `UShort`.  Il tipo `UShort` non dispone di caratteri di tipo identificatore.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.UInt16?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.UInt16>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)