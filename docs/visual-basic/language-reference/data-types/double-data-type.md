---
title: "Double Data Type (Visual Basic) | Microsoft Docs"
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
  - "vb.Double"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "identifier type characters, #"
  - "trailing zeros"
  - "real numbers"
  - "trailing 0 characters"
  - "0 characters, trailing"
  - "literal type characters, R"
  - "data types [Visual Basic], assigning"
  - "Double data type [Visual Basic]"
  - "# identifier type character"
  - "double-precision numbers"
  - "floating-point numbers, Double data type"
  - "R literal type character"
  - "zeros, trailing"
  - "Double data type"
ms.assetid: 0c5670f7-fcb1-453a-bef1-374730cd38fd
caps.latest.revision: 25
caps.handback.revision: 25
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Double Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene numeri con segno IEEE a 64 bit \(8 byte\) a virgola mobile e precisione doppia compresi tra \-1,79769313486231570E\+308 e \-4,94065645841246544E\-324 per i valori negativi e tra 4,94065645841246544E\-324 e 1,79769313486231570E\+308 per i valori positivi.  Con i numeri a precisione doppia viene memorizzata un'approssimazione a un numero reale.  
  
## Note  
 Il tipo di dati `Double` fornisce l'ordine di grandezza più alto e più basso per un numero.  
  
 Il valore predefinito di `Double` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Precisione.** Quando si utilizzano numeri a virgola mobile, tenere presente che non sempre contengono una rappresentazione precisa in memoria.  Per questo motivo, è possibile che determinate operazioni restituiscano risultati imprevisti, come il confronto dei valori e l'operatore `Mod`.  Per ulteriori informazioni, vedere [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md).  
  
-   **Zeri finali.** I tipi di dati a virgola mobile non contengono alcuna rappresentazione interna degli zeri finali.  Ad esempio, non viene fatta distinzione tra 4,2000 e 4,2.  Di conseguenza, gli zeri finali non sono presenti quando vengono visualizzati o stampati valori a virgola mobile.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `R` a un valore letterale, se ne determina la conversione nel tipo di dati `Double`.  Ad esempio, se un valore intero è seguito da `R`, il valore viene impostato su `Double`.  
  
    ```  
    ' Visual Basic expands the 4 in the statement Dim dub As Double = 4R to 4.0:  
    Dim dub As Double = 4.0R  
    ```  
  
     Aggiungendo il carattere identificatore di tipo `#` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Double`.  Nell'esempio riportato di seguito, la variabile `num` viene tipizzata come un oggetto `Double`:  
  
    ```  
    Dim num# = 3  
    ```  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Double?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Double?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Decimal Data Type](../../../visual-basic/language-reference/data-types/decimal-data-type.md)   
 [Single Data Type](../../../visual-basic/language-reference/data-types/single-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Troubleshooting Data Types](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Type Characters](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)