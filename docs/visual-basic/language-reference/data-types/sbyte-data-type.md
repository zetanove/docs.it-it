---
title: "SByte Data Type (Visual Basic) | Microsoft Docs"
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
  - "vb.sbyte"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "numbers, whole"
  - "whole numbers"
  - "integral data types"
  - "integer numbers"
  - "numbers, integer"
  - "integers, data types"
  - "integers, types"
  - "data types [Visual Basic], integral"
  - "SByte data type"
ms.assetid: 5c38374a-18a1-4cc2-b493-299e3dcaa60f
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# SByte Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene valori integer con segno a 8 bit \(1 byte\) compresi tra \-128 e 127.  
  
## Note  
 Utilizzare il tipo di dati `SByte` per contenere valori integer che non richiedono l'intera ampiezza dei dati di `Integer` o la metà dell'ampiezza dei dati di `Short`.  In alcuni casi è possibile che Common Language Runtime sia in grado di unire le variabili `SByte` e ridurre il consumo di memoria.  
  
 Il valore predefinito di `SByte` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Compatibilità con CLS.** Il tipo di dati `SByte` non fa parte delle specifiche [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), pertanto un codice compatibile con le specifiche CLS non può utilizzare un componente che utilizza tale tipo di dati.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `SByte` viene convertito verso i tipi più ampi `Short`, `Integer`, `Long`, `Decimal`, `Single` e `Double`.  È pertanto possibile convertire `SByte` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** `SByte` non ha alcun carattere di tipo letterale o carattere identificatore di tipo.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.SByte?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.SByte?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Short Data Type](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [Integer Data Type](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Long Data Type](../../../visual-basic/language-reference/data-types/long-data-type.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)