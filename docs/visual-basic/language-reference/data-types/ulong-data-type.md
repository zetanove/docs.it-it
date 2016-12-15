---
title: "ULong Data Type (Visual Basic) | Microsoft Docs"
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
  - "vb.ulong"
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
  - "literal type characters, UL"
  - "ULong data type"
  - "UL literal type characters"
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# ULong Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene interi senza segno a 64 bit \(8 byte\) il cui valore è compreso tra 0 e 18.446.744.073.709.551.615 \(oltre 1,84 volte 10 ^ 19\).  
  
## Note  
 Utilizzare il tipo di dati `ULong` per includere dati binari eccessivamente grandi per il tipo `UInteger` oppure Unsigned Integer più grandi possibile.  
  
 Il valore predefinito di `ULong` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** Poiché `ULong` è un tipo senza segno, non può rappresentare un numero negativo.  Se si utilizza l'operatore unario meno \(`-`\) su un'espressione che restituisce un valore di tipo `ULong`, tale espressione verrà innanzitutto convertita nel tipo `Decimal`.  
  
-   **Compatibilità con CLS.** Il tipo di dati `ULong` non fa parte delle specifiche [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), pertanto un codice compatibile con le specifiche CLS non può utilizzare un componente che utilizza tale tipo di dati.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti tipi come `ulong` possono avere un'ampiezza dei dati diversa \(32 bit\).  Se si passa un argomento a 32 bit a un componente di questo tipo, nel codice gestito Visual Basic è necessario eseguirne la dichiarazione come `UInteger` anziché come `ULong`.  
  
     Inoltre, l'automazione non supporta i numeri interi a 64 bit in Windows 95, Windows 98 Windows o Windows 2000.  Non è possibile passare un argomento Visual Basic `ULong` a un componente di automazione su queste piattaforme.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `ULong` viene convertito verso i tipi più ampi `Decimal`, `Single` e `Double`.  È pertanto possibile convertire `ULong` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo i caratteri di tipo letterale `UL` a un valore letterale, se ne determina la conversione nel tipo di dati `ULong`.  Il tipo `ULong` non dispone di caratteri di tipo identificatore.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.UInt64?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.UInt64>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)