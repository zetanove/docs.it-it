---
title: "Byte Data Type (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Byte"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Byte data type"
  - "data types [Visual Basic], assigning"
ms.assetid: eed44dff-eaee-4937-a89f-444e418e74f6
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Byte Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene valori integer con segno a 8 bit \(1 byte\) in un intervallo compreso tra 0 e 255.  
  
## Note  
 Utilizzare il tipo di dati `Byte` per contenere dati binari.  
  
 Il valore predefinito di `Byte` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** Poiché `Byte` è un tipo senza segno, non può rappresentare un numero negativo.  Se si utilizza l'operatore unario meno \(`-`\) su un'espressione che restituisce un valore di tipo `Byte`, tale espressione verrà innanzitutto convertita nel tipo `Short`.  
  
-   **Conversioni dei formati.** In Visual Basic è consentita la conversione automatica tra i formati di dati durante le operazioni di lettura e scrittura dei file o le chiamate di DLL, metodi e proprietà.  I dati binari memorizzati in variabili e matrici `Byte` vengono preservati nel corso di tali conversioni.  Si consiglia di non utilizzare una variabile `String` per i dati binari, in quanto è possibile che il contenuto venga danneggiato durante la conversione tra i formati ANSI e Unicode.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `Byte` può ampliarsi nel tipo `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single` o `Double`.  È pertanto possibile convertire `Byte` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** `Byte` non ha alcun carattere di tipo letterale o carattere identificatore di tipo.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Byte?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio seguente `b` è una variabile `Byte`.  Le istruzioni indicano l'intervallo della variabile e l'applicazione di operatori di scorrimento bit.  
  
 [!code-vb[VbVbalrDataTypes#16](../../../visual-basic/language-reference/data-types/codesnippet/visualbasic/byte-data-type_1.vb)]  
  
## Vedere anche  
 <xref:System.Byte?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)