---
title: "Single Data Type (Visual Basic) | Microsoft Docs"
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
  - "vb.Single"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Single data type"
  - "F literal type character"
  - "trailing zeros"
  - "real numbers"
  - "literal type characters, F"
  - "trailing 0 characters"
  - "identifier type characters, !"
  - "single-precision numbers"
  - "! identifier type character"
  - "0 characters, trailing"
  - "data types [Visual Basic], assigning"
  - "floating-point numbers, Single data type"
  - "numbers, real"
  - "zeros, trailing"
  - "numbers, floating point"
ms.assetid: 224a2795-4cd5-496c-8f7a-a4f05a06d45d
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Single Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene numeri con segno di 32 bit \(4 byte\) con virgola mobile a precisione singola conformi alle specifiche IEEE compresi nell'intervallo tra \-3,4028235E\+38 e \-1,401298E\-45 per i valori negativi e tra 1,401298E\-45 e 3,4028235E\+38 per i valori positivi.  Con i numeri a precisione singola viene memorizzata un'approssimazione a un numero reale.  
  
## Note  
 Utilizzare il tipo di dati `Single` per contenere valori a virgola mobile per i quali non è richiesta l'ampiezza completa dei dati `Double`.  In alcuni casi è possibile che Common Language Runtime sia in grado di unire le variabili `Single` e ridurre il consumo di memoria.  
  
 Il valore predefinito di `Single` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Precisione.** Quando si utilizzano numeri a virgola mobile, tenere presente che non vengono sempre memorizzati con una rappresentazione precisa.  Per questo motivo, è possibile che determinate operazioni restituiscano risultati imprevisti, come il confronto dei valori e l'operatore `Mod`.  Per ulteriori informazioni, vedere [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `Single` viene convertito verso il tipo più grande `Double`.  In altri termini, è possibile convertire `Single` in `Double` senza che si verifichi un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Zeri finali.** I tipi di dati a virgola mobile non contengono alcuna rappresentazione interna degli zeri finali.  Ad esempio, non viene fatta distinzione tra 4,2000 e 4,2.  Di conseguenza, gli zeri finali non sono presenti quando vengono visualizzati o stampati valori a virgola mobile.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `F` a un valore letterale, se ne determina la conversione nel tipo di dati `Single`.  Aggiungendo il carattere identificatore di tipo `!` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Single`.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Single?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Single?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Decimal Data Type](../../../visual-basic/language-reference/data-types/decimal-data-type.md)   
 [Double Data Type](../../../visual-basic/language-reference/data-types/double-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)