---
title: Tipi di dati numerici (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- integral types, Visual Basic
- Short data type, numeric data types
- Double data type, numeric data types
- Long data type, Visual Basic numeric data types
- numbers, whole
- fractions
- numbers
- whole numbers
- integer numbers
- numbers, integer
- fractional data types
- mantissas, of fractional numbers
- mantissas
- data types [Visual Basic], numeric
- Integer data type, numeric data types
- exponent, of fractional numbers
- integers
- numeric data types, Visual Basic
- Single data type, numeric types
- Decimal data type, numeric data types
ms.assetid: a27bd4d0-7e14-43eb-9cc4-b42eaab323c9
caps.latest.revision: 25
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3c3098370b8d9dcb6aafcb06dcfb8f4e144b899a
ms.lasthandoff: 03/13/2017

---
# <a name="numeric-data-types-visual-basic"></a>Tipi di dati numerici (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce diversi *tipi di dati numerici* per gestire i numeri in varie rappresentazioni. *Integrale* tipi rappresentano solo numeri interi (positivi, negativi e zero), e *non integrali* tipi rappresentano numeri integer sia parti frazionarie.  
  
 Per una tabella che mostra un confronto side-by-side di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tipi di dati, vedere [tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## <a name="integral-numeric-types"></a>Tipi numerici integrali  
 *Tipi di dati integrali* sono quelli che rappresentano solo numeri senza parti frazionarie.  
  
 Il *firmato* sono tipi di dati integrali [tipo di dati SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md) (8 bit), [tipo di dati Short](../../../../visual-basic/language-reference/data-types/short-data-type.md) (16 bit), [tipo di dati Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md) (32-bit) e [tipo di dati Long](../../../../visual-basic/language-reference/data-types/long-data-type.md) (64 bit). Se una variabile memorizza sempre numeri interi anziché numeri frazionari, dichiararla come uno di questi tipi.  
  
 Il *unsigned* tipi integrali sono [tipo di dati Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md) (8 bit), [tipo di dati UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md) (16 bit), [tipo di dati UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md) (32-bit) e [tipo di dati ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md) (64 bit). Se una variabile contiene dati binari o dati di natura sconosciuta, dichiararla come uno di questi tipi.  
  
### <a name="performance"></a>Prestazioni  
 Operazioni aritmetiche sono più veloci con tipi integrali che con altri tipi di dati. Sono più veloci con il `Integer` e `UInteger` tipi [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### <a name="large-integers"></a>Numeri interi grandi  
 Se è necessario includere un numero intero maggiore di `Integer` può contenere il tipo di dati, è possibile utilizzare il `Long` invece del tipo di dati. `Long`le variabili possono contenere numeri compresi tra -9.223.372.036.854.775.808 e 9.223.372.036.854.775.807. Operazioni con `Long` sono leggermente più lento con `Integer`.  
  
 Se sono necessari più valori, è possibile utilizzare il [tipo di dati Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md). È possibile archiviare numeri compresi tra -79.228.162.514.264.337.593.543.950.335 e 79.228.162.514.264.337.593.543.950.335 in un `Decimal` variabile se non si utilizza tutte le posizioni decimali. Tuttavia, le operazioni con `Decimal` numeri sono considerevolmente più lenti con qualsiasi altro tipo di dati numerici.  
  
### <a name="small-integers"></a>Small integer  
 Se non è necessaria l'intera gamma di `Integer` tipo di dati, è possibile utilizzare il `Short` tipo di dati, che può contenere numeri interi compresi tra -32.768 e 32.767. Per l'intervallo di valori integer più piccolo, il `SByte` tipo di dati contiene numeri interi compresi tra -128 e 127. Se si dispone di un numero molto elevato di variabili che contengono small integer, common language runtime a volte è possibile archiviare il `Short` e `SByte` variabili in modo più efficiente e ridurre il consumo di memoria. Tuttavia, le operazioni con `Short` e `SByte` sono leggermente più lente con `Integer`.  
  
### <a name="unsigned-integers"></a>Numeri interi senza segno  
 Se si sa che la variabile non dovrà mai contenere un numero negativo, è possibile utilizzare il *tipi senza segno*`Byte`, `UShort`, `UInteger`, e `ULong`. Ognuno di questi tipi di dati può contenere un numero intero positivo due volte più grande come corrispondente tipo con segno (`SByte`, `Short`, `Integer`, e `Long`). In termini di prestazioni, un tipo senza segno è esattamente efficiente come il corrispondente tipo con segno. In particolare, `UInteger` condivide con `Integer` sono le più efficienti di tutti i tipi di dati numerici elementari.  
  
## <a name="nonintegral-numeric-types"></a>Tipi numerici non integrali  
 *Tipi di dati non integrali* sono quelli che rappresentano numeri integer sia parti frazionarie.  
  
 I tipi di dati numerici non integrali sono `Decimal` (a virgola fissa a&128; bit), [singolo tipo di dati](../../../../visual-basic/language-reference/data-types/single-data-type.md) (a virgola mobile a&32; bit) e [tipo di dati Double](../../../../visual-basic/language-reference/data-types/double-data-type.md) (a virgola mobile a&64; bit). Sono tutti tipi con segno. Se una variabile può contenere una frazione, dichiararla come uno di questi tipi.  
  
 `Decimal`non è un tipo di dati a virgola mobile. `Decimal`numeri contengono un valore integer binario e un fattore di scala integer che specifica quale parte del valore è una frazione decimale.  
  
 È possibile utilizzare `Decimal` variabili per valori di valuta. Il vantaggio è la precisione dei valori. Il `Double` tipo di dati è più veloce e richiede meno memoria, ma è soggetto a errori di arrotondamento. Il `Decimal` tipo di dati mantiene un'accuratezza completa a 28 cifre decimali.  
  
 A virgola mobile (`Single` e `Double`) i numeri hanno intervalli più ampi rispetto `Decimal` numeri ma possono essere soggette a errori di arrotondamento. Tipi a virgola mobile supportano un numero di cifre significative rispetto a `Decimal` , ma possono rappresentare i valori dell'ordine di grandezza maggiore.  
  
 Valori numerici non integrali possono essere espresse come mmmEeee, in cui mmm è la *mantissa* (le cifre significative) ed eee è il *esponente* (una potenza di 10). Il valore più grande positivo dei tipi non integrali, 7.9228162514264337593543950335 + 28 per `Decimal`, 3, 4028235E + 38 per `Single`e 1.79769313486231570 e + 308 per `Double`.  
  
### <a name="performance"></a>Prestazioni  
 `Double`è la più efficiente dei tipi di dati frazionari, perché i processori disponibili sulle attuali piattaforme eseguono operazioni a virgola mobile a precisione doppia. Tuttavia, le operazioni con `Double` non sono più veloci con i tipi integrali, ad esempio `Integer`.  
  
### <a name="small-magnitudes"></a>Ordini di grandezza piccole  
 Per i numeri con il più piccolo ordine di grandezza possibile (il più vicino a 0), `Double` le variabili possono contenere numeri - 4.94065645841246544-324 per valori negativi e 4, 94065645841246544E-324 per i valori positivi.  
  
### <a name="small-fractional-numbers"></a>Numeri frazionari piccoli  
 Se non è necessaria l'intera gamma di `Double` tipo di dati, è possibile utilizzare il `Single` tipo di dati, che può contenere numeri a virgola mobile da - 3, 4028235E + 38 e 3, 4028235E + 38. I più piccolo ordini di grandezza per `Single` le variabili sono - 1, 401298E-45 per i valori negativi e 1, 401298E-45 per i valori positivi. Se si dispone di numerose variabili che contengono numeri a virgola mobile piccoli, common language runtime a volte è possibile archiviare le `Single` le variabili in modo più efficiente e ridurre il consumo di memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi di dati carattere](../../../../visual-basic/programming-guide/language-features/data-types/character-data-types.md)   
 [Tipi di dati vari](../../../../visual-basic/programming-guide/language-features/data-types/miscellaneous-data-types.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Procedura: Chiamare una funzione Windows che accetta tipi senza segno](../../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
