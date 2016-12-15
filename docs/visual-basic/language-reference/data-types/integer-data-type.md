---
title: "Integer Data Type (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Integer"
  - "Integer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "numbers, whole"
  - "enumerated values"
  - "whole numbers"
  - "integral data types"
  - "integer numbers"
  - "numbers, integer"
  - "integers, data types"
  - "literal type characters, I"
  - "integers, types"
  - "data types [Visual Basic], integral"
  - "% identifier type character"
  - "data types [Visual Basic], assigning"
  - "identifier type characters, %"
  - "I literal type character"
  - "Integer data type"
ms.assetid: a8f233b4-4be3-455c-861b-05af2fbb6c60
caps.latest.revision: 22
caps.handback.revision: 22
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Integer Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene valori integer con segno a 32 bit \(4 byte\) in un intervallo compreso tra \-2.147.483.648 e 2.147.483.647.  
  
## Note  
 Il tipo di dati `Integer` consente di ottenere prestazioni ottimali su processori a 32 bit.  Gli altri tipi integrali vengono caricati e memorizzati più lentamente.  
  
 Il valore predefinito di `Integer` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti i tipi `Integer` hanno un'ampiezza dei dati diversa \(16 bit\).  Se si passa un argomento a 16 bit a un componente di questo tipo, nel nuovo codice Visual Basic è necessario eseguirne la dichiarazione come `Short` anziché come `Integer`.  
  
-   **Widening.** Il tipo di dati `Integer` può ampliarsi nel tipo `Long`, `Decimal`, `Single` o `Double`.  È pertanto possibile convertire `Integer` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `I` a un valore letterale, se ne determina la conversione nel tipo di dati `Integer`.  Aggiungendo il carattere identificatore di tipo `%` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Integer`.  
  
-   **Tipo di framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Int32?displayProperty=fullName>.  
  
## Intervallo  
 Se si tenta di impostare una variabile di un tipo integrale su un numero esterno all'intervallo valido per tale tipo, verrà generato un errore.  Se si tenta di impostarlo in una frazione, il numero viene arrotondato all'intero pari più vicino.  Se il numero è egualmente vicino a due valori interi, il valore viene arrotondato all'intero pari più vicino.  Questo comportamento riduce al minimo gli errori di arrotondamento risultanti dall'arrotondamento coerente di un valore del punto centrale in una singola direzione.  Nel codice riportato di seguito vengono illustrati esempi di arrotondamento.  
  
```  
' The valid range of an Integer variable is -2147483648 through +2147483647.  
Dim k As Integer  
' The following statement causes an error because the value is too large.  
k = 2147483648  
' The following statement sets k to 6.  
k = 5.9  
' The following statement sets k to 4  
k = 4.5  
' The following statement sets k to 6  
' Note, Visual Basic uses banker’s rounding (toward nearest even number)  
k = 5.5  
```  
  
## Vedere anche  
 <xref:System.Int32?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Long Data Type](../../../visual-basic/language-reference/data-types/long-data-type.md)   
 [Short Data Type](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)