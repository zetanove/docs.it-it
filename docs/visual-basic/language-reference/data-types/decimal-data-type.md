---
title: "Decimal Data Type (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Decimal"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "literal type characters, D"
  - "trailing zeros"
  - "real numbers"
  - "trailing 0 characters"
  - "Decimal data type"
  - "D literal type character"
  - "decimals, Decimal data type"
  - "0 characters, trailing"
  - "data types [Visual Basic], assigning"
  - "decimal keyword"
  - "numbers, real"
  - "variable-precision numbers"
  - "zeros, trailing"
  - "@ identifier type character"
  - "identifier type characters, @"
ms.assetid: 1d855b45-afe2-45b0-a623-96b6f63a43d5
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Decimal Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Contiene valori a 128 bit \(16 byte\) con segno che rappresentano valore integer di 96 bit \(12 byte\) scalati in base a una potenza variabile di 10.  Il fattore di scala specifica il numero di cifre a destra del separatore decimale, da 0 a 28.  Con una scala pari a 0 \(nessuna posizione decimale\), il più alto valore possibile è \+\/\-79.228.162.514.264.337.593.543.950.335 \(\+\/\-7.9228162514264337593543950335E\+28\).  Con 28 posizioni decimali, il più alto valore possibile è \+\/\-7,9228162514264337593543950335, mentre il valore più piccolo diverso da zero è \+\/\-0,0000000000000000000000000001 \(\+\/\-1E\-28\).  
  
## Note  
 Il tipo di dati `Decimal` fornisce il numero più elevato di cifre possibili per un numero.  Supporta fino a 29 cifre significative e può rappresentare valori superiori a 7.9228 x 10^28.  È particolarmente adatto per i calcoli, ad esempio finanziari, che richiedono un numero elevato di cifre ma non sono in grado di tollerare errori di arrotondamento.  
  
 Il valore predefinito di `Decimal` è 0.  
  
## Suggerimenti per la programmazione  
  
-   **Precisione.** `Decimal` non è un tipo di dati a virgola mobile.  La struttura `Decimal` contiene un valore integer binario nonché un bit di segno e un fattore di scala integer che specifica quale parte del valore è una frazione decimale.  Per questa ragione, i numeri `Decimal` hanno una rappresentazione in memoria più precisa rispetto ai tipi a virgola mobile \(`Single` e `Double`\).  
  
-   **Prestazioni.** Il tipo di dati `Decimal` è il più lento di tutti i tipi numerici.  Prima di scegliere un tipo di dati è opportuno valutare l'importanza della precisione rispetto alle prestazioni.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `Decimal` viene convertito verso il tipo più grande `Single` o `Double`.  È pertanto possibile convertire `Decimal` in uno di questi tipi senza generare un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Zeri finali.** In Visual Basic gli zeri finali non vengono archiviati in un valore letterale `Decimal`.  Una variabile `Decimal`, tuttavia, conserva gli zeri finali acquisiti a seguito di un calcolo.  Questa condizione è illustrata nell'esempio che segue.  
  
    ```  
    Dim d1, d2, d3, d4 As Decimal  
    d1 = 2.375D  
    d2 = 1.625D  
    d3 = d1 + d2  
    d4 = 4.000D  
    MsgBox("d1 = " & CStr(d1) & ", d2 = " & CStr(d2) &  
          ", d3 = " & CStr(d3) & ", d4 = " & CStr(d4))  
    ```  
  
     Il risultato di `MsgBox` dell'esempio precedente è riportato di seguito:  
  
     d1 \= 2.375, d2 \= 1.625, d3 \= 4.000, d4 \= 4  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `D` a un valore letterale, se ne determina la conversione nel tipo di dati `Decimal`.  Aggiungendo il carattere identificatore di tipo `@` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `Decimal`.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Decimal?displayProperty=fullName>.  
  
## Intervallo  
 Per assegnare un valore alto a una costante o variabile `Decimal`, può essere necessario utilizzare il tipo di carattere `D`.  Questo requisito perché il compilatore interpreta un valore letterale come `Long` a meno che un carattere di tipo letterale segua il valore letterale, come illustrato di seguito.  
  
```  
Dim bigDec1 As Decimal = 9223372036854775807   ' No overflow.  
Dim bigDec2 As Decimal = 9223372036854775808   ' Overflow.  
Dim bigDec3 As Decimal = 9223372036854775808D  ' No overflow.  
```  
  
 La dichiarazione per `bigDec1` non produce un overflow perché il valore assegnato fa parte dell'intervallo per `Long`.  Il valore `Long` può essere assegnato alla variabile `Decimal`.  
  
 La dichiarazione per `bigDec2` generato un errore di overflow perché il valore assegnato è troppo grande per `Long`.  Poiché il valore letterale numerico non può essere dapprima interpretato come `Long`, non può essere assegnato alla variabile `Decimal`.  
  
 Per `bigDec3`, il carattere di tipo letterale `D` risolve il problema forzando il compilatore per interpretare il valore letterale come `Decimal` anziché come `Long`.  
  
## Vedere anche  
 <xref:System.Decimal?displayProperty=fullName>   
 <xref:System.Decimal.%23ctor%2A?displayProperty=fullName>   
 <xref:System.Math.Round%2A?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Single Data Type](../../../visual-basic/language-reference/data-types/single-data-type.md)   
 [Double Data Type](../../../visual-basic/language-reference/data-types/double-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)