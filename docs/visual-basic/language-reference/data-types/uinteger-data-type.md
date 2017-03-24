---
title: "UInteger Data Type | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.uinteger"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "numbers, whole"
  - "UInteger data type"
  - "literal type characters, UI"
  - "whole numbers"
  - "integral data types"
  - "integer numbers"
  - "numbers, integer"
  - "integers, data types"
  - "integers, types"
  - "UI literal type characters"
  - "data types [Visual Basic], integral"
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# UInteger Data Type
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene valori integer a 32 bit \(4 byte\) senza segno in un intervallo compreso tra 0 e 4.294.967.295.  
  
## Note  
 Il tipo di dati `UInteger` fornisce il valore massimo senza segno nell'ampiezza di dati più efficace.  
  
 Il valore predefinito di `UInteger` è 0.  
  
## Suggerimenti per la programmazione  
 I tipi di dati `UInteger` e `Integer` forniscono prestazioni ottimali su un processore a 32 bit poiché i tipi integer più piccoli \(`UShort`, `Short`, `Byte` e `SByte`\), pur utilizzando un numero inferiore di bit, richiedono un intervallo di tempo maggiore per il caricamento, l'archiviazione e il recupero.  
  
-   **Numeri negativi.** Poiché `UInteger` è un tipo senza segno, non può rappresentare un numero negativo.  Se si utilizza l'operatore unario meno \(`-`\) su un'espressione che restituisce un valore di tipo `UInteger`, tale espressione verrà innanzitutto convertita nel tipo `Long`.  
  
-   **Compatibilità con CLS.** Il tipo di dati `UInteger` non fa parte delle specifiche [Indipendenza del linguaggio e componenti indipendenti dal linguaggio](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), pertanto un codice compatibile con le specifiche CLS non può utilizzare un componente che utilizza tale tipo di dati.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti tipi come `uint` possono avere un'ampiezza dei dati diversa \(16 bit\).  Se si passa un argomento a 16 bit a un componente di questo tipo, nel codice gestito Visual Basic è necessario eseguirne la dichiarazione come `UShort` anziché come `UInteger`.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `UInteger` viene convertito nei tipi `Long`, `ULong`, `Decimal`, `Single` e `Double` più ampi.  È pertanto possibile convertire `UInteger` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo i caratteri di tipo letterale `UI` a un valore letterale, se ne determina la conversione nel tipo di dati `UInteger`.  Il tipo `UInteger` non dispone di caratteri di tipo identificatore.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.UInt32?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.UInt32>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)