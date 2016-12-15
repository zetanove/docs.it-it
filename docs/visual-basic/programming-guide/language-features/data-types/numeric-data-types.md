---
title: "Numeric Data Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "integral types, Visual Basic"
  - "Short data type, numeric data types"
  - "Double data type, numeric data types"
  - "Long data type, Visual Basic numeric data types"
  - "numbers, whole"
  - "fractions"
  - "numbers"
  - "whole numbers"
  - "integer numbers"
  - "numbers, integer"
  - "fractional data types"
  - "mantissas, of fractional numbers"
  - "mantissas"
  - "data types [Visual Basic], numeric"
  - "Integer data type, numeric data types"
  - "exponent, of fractional numbers"
  - "integers"
  - "numeric data types, Visual Basic"
  - "Single data type, numeric types"
  - "Decimal data type, numeric data types"
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
caps.latest.revision: 25
caps.handback.revision: 25
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Numeric Data Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sono disponibili numerosi *tipi di dati numerici* che consentono di gestire i numeri in diverse rappresentazioni.  I tipi *integrali* rappresentano soltanto numeri interi \(positivi, negativi e zero\), mentre i tipi *non integrali* rappresentano numeri con una parte intera e una parte frazionaria.  
  
 Per un confronto dettagliato dei tipi di dati di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], vedere [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## Tipi numerici integrali  
 I *tipi di dati integrali* sono quelli che rappresentano soltanto numeri senza parti frazionarie.  
  
 I tipi di dati integrali *con segno* sono [SByte Data Type](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md) \(8 bit\), [Short Data Type](../../../../visual-basic/language-reference/data-types/short-data-type.md) \(16 bit\), [Integer Data Type](../../../../visual-basic/language-reference/data-types/integer-data-type.md) \(32 bit\) e [Long Data Type](../../../../visual-basic/language-reference/data-types/long-data-type.md) \(64 bit\).  Se una variabile contiene sempre Integer anziché numeri frazionari, dichiararla utilizzando uno di questi tipi.  
  
 I tipi integrali *senza segno* sono [Byte Data Type](../../../../visual-basic/language-reference/data-types/byte-data-type.md) \(8 bit\), [UShort Data Type](../../../../visual-basic/language-reference/data-types/ushort-data-type.md) \(16 bit\), [UInteger Data Type](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md) \(32 bit\) e [ULong Data Type](../../../../visual-basic/language-reference/data-types/ulong-data-type.md) \(64 bit\).  Se una variabile contiene dati binari o dati di natura sconosciuta, dichiararla utilizzando uno di questi tipi.  
  
### Prestazioni  
 Le operazioni aritmetiche risultano più veloci con i tipi integrali che con altri tipi di dati.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] le prestazioni migliori si ottengono con i tipi `Integer` e `UInteger`.  
  
### Valori integer grandi  
 Se è necessario contenere un intero più grande del tipo di dati `Integer` che è possibile contenere, in alternativa si può utilizzare il tipo di dati `Long`.  Le variabili `Long` possono includere numeri compresi tra \-9,223,372,036,854,775,808 e 9,223,372,036,854,775,807.  Le operazioni con `Long` sono leggermente più lente rispetto a quelle con `Integer`.  
  
 Se sono necessari valori ancora più grandi, è possibile utilizzare il [Decimal Data Type](../../../../visual-basic/language-reference/data-types/decimal-data-type.md).  Se non si utilizzano posizioni decimali, in una variabile `Decimal` è possibile archiviare numeri compresi tra \-79.228.162.514.264.337.593.543.950.335 e 79.228.162.514.264.337.593.543.950.335.  Le operazioni con i numeri `Decimal` risultano tuttavia molto più lente rispetto a quelle che utilizzano un qualsiasi altro tipo di dati numerici.  
  
### Valori integer piccoli  
 Se non è necessario l'intervallo completo di tipi di dati `Integer`, è possibile utilizzare il tipo di dati `Short` che può contenere Integer compresi tra \-32,768 e 32,767.  Nell'intervallo più piccolo di interi il tipo di dati `SByte` contiene numeri interi compresi tra \-128 e 127.  In alcuni casi, se si utilizzano numerose variabili che contengono interi piccoli, Common Language Runtime è in grado di archiviare le variabili `Short` e `SByte` in modo più efficace riducendo il consumo di memoria.  Le operazioni con `Short` e `SByte`, tuttavia, sono più lente rispetto a quelle con `Integer`.  
  
### Interi senza segno  
 Se si ha la certezza che la variabile non dovrà mai contenere un numero negativo, è possibile utilizzare i *tipi senza segno* `Byte`, `UShort`, `UInteger` e `ULong`.  Ciascuno di questi tipi è in grado di contenere un valore integer di grandezza doppia rispetto a quella del corrispondente tipo con segno \(`SByte`, `Short`, `Integer` e `Long`\).  Le prestazioni di un tipo senza segno sono equivalenti a quelle del corrispondente tipo con segno.  In particolare, `UInteger` e `Integer` sono i più efficaci tra i tipi di dati numerici elementari.  
  
## Tipi numerici non integrali  
 I *tipi di dati non integrali* sono quelli che rappresentano numeri con parti sia intere che frazionarie.  
  
 I tipi di dati numerici non integrali sono `Decimal` \(a virgola fissa a 128 bit\), [Single Data Type](../../../../visual-basic/language-reference/data-types/single-data-type.md) \(a virgola mobile a 32 bit\) e [Double Data Type](../../../../visual-basic/language-reference/data-types/double-data-type.md) \(a virgola mobile a 64 bit\).  Sono tutti tipi con segno.  Se una variabile può contenere una frazione, dichiararla utilizzando uno di questi tipi.  
  
 `Decimal` non è un tipo di dati a virgola mobile.  I numeri `Decimal` contengono un valore intero binario e un fattore di scala intero che specifica quale parte del valore è una frazione decimale.  
  
 È possibile utilizzare le variabili di `Decimal` per i valori di valuta.  Il vantaggio è la precisione.  Il tipo di dati `Double` assicura una maggiore velocità e richiede una minore quantità di memoria, ma è soggetto a errori di arrotondamento.  Il tipo di dati di `Decimal` mantiene un'accuratezza completa a 28 posizioni decimali.  
  
 I numeri a virgola mobile \(`Single` e `Double`\) sono caratterizzati da un intervallo maggiore rispetto a quello dei numeri `Decimal`, ma possono essere soggetti a errori di arrotondamento.  I tipi a virgola mobile supportano un numero di cifre significative minore rispetto a `Decimal`, ma sono in grado di rappresentare valori con un ordine di grandezza maggiore.  
  
 I valori numerici non integrali possono essere espressi come mmmEeee, in cui mmm è la *mantissa* \(le cifre significative\) e eee è l'*esponente* \(una potenza di 10\).  Il valore più grande positivo dei tipi non integrali è 7,9228162514264337593543950335E\+28 per `Decimal`, 3,4028235E\+38 per `Single` e 1,79769313486231570E\+308 per `Double`.  
  
### Prestazioni  
 `Double` è il più efficace tra i tipi di dati frazionari, poiché i processori disponibili sulle attuali piattaforme eseguono operazioni a virgola mobile in precisione doppia.  Tuttavia, l'esecuzione delle operazioni con tipo di dati `Double` richiede più tempo rispetto a quella delle operazioni con i tipi integrali, ad esempio `Integer`.  
  
### Numeri con il più piccolo ordine di grandezza  
 Per i numeri con il più piccolo ordine di grandezza possibile \(il più vicino a 0\), le variabili `Double` possono contenere numeri fino a \-4.94065645841246544E\-324 per i valori negativi e fino a 4.94065645841246544E\-324 per i valori positivi.  
  
### Numeri frazionari piccoli  
 Se non è necessario disporre dell'intervallo completo del tipo di dati `Double`, è possibile utilizzare il tipo di dati `Single`, che può contenere numeri a virgola mobile compresi tra \-3.4028235E\+38 e 3.4028235E\+38.  Gli ordini di grandezza più piccoli per le variabili `Single` sono \-1,401298E\-45 per i valori negativi e 1,401298E\-45 per i valori positivi.  In alcuni casi, se si utilizzano numerose variabili che contengono numeri a virgola mobile piccoli, Common Language Runtime è in grado di archiviare le variabili `Single` in modo più efficace riducendo il consumo di memoria.  
  
## Vedere anche  
 [Elementary Data Types](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Character Data Types](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [Miscellaneous Data Types](../../../../visual-basic/programming-guide/language-features/data-types/miscellaneous-data-types.md)   
 [Troubleshooting Data Types](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)