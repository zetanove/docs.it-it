---
title: Tabelle di conversione dei tipi
description: Tabelle di conversione dei tipi
keywords: .NET, .NET Core
author: stevehoag
manager: wpickett
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: d602f260-e7cf-49c8-a37f-731f40e4a538
translationtype: Human Translation
ms.sourcegitcommit: fb00da6505c9edb6a49d2003ae9bcb8e74c11d6c
ms.openlocfilehash: 16f38150f26b477de5685d2d3b0ef18afb94c236

---

# <a name="type-conversion-tables"></a>Tabelle di conversione dei tipi

Si parla di conversione verso un tipo di dati più grande quando un valore di un certo tipo viene convertito in un altro tipo di dimensioni identiche o maggiori. Si parla di conversione verso un tipo di dati più piccolo quando un valore di un certo tipo viene convertito in un valore di un altro tipo di dimensioni inferiori. Le tabelle in questo argomento illustrano i comportamenti di entrambi i tipi di conversioni.

## <a name="widening-conversions"></a>Conversioni verso un tipo di dati più grande

Tipo | Conversione senza perdita di dati in
---- | -------------------------------------
[Byte](xref:System.Byte) | [UInt16](xref:System.UInt16), [Int16](xref:System.Int16), [UInt32](xref:System.UInt32), [Int32](xref:System.Int32), [UInt64](xref:System.UInt64), [Int64](xref:System.Int64), [Single](xref:System.Single), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[SByte](xref:System.SByte) | [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [Single](xref:System.Single), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[Int16](xref:System.Int16) | [Int32](xref:System.Int32), [Int64](xref:System.Int64), [Single](xref:System.Single), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[UInt16](xref:System.UInt16) | [UInt32](xref:System.UInt32), [Int32](xref:System.Int32), [UInt64](xref:System.UInt64), [Int64](xref:System.Int64), [Single](xref:System.Single), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[Char](xref:System.Char) | [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [Int32](xref:System.Int32), [UInt64](xref:System.UInt64), [Int64](xref:System.Int64), [Single](xref:System.Single), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[Int32](xref:System.Int32) | [Int64](xref:System.Int64), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[UInt32](xref:System.UInt32) | [Int64](xref:System.Int64), [UInt64](xref:System.UInt64), [Double](xref:System.Double), [Decimal](xref:System.Decimal)
[Int64](xref:System.Int64) | [Decimal](xref:System.Decimal)
[UInt64](xref:System.UInt64) | [Decimal](xref:System.Decimal)
[Single](xref:System.Single) | [Double](xref:System.Double)

Alcune conversioni verso il tipo di dati più grande [Single](xref:System.Single) o [Double](xref:System.Double) possono causare una perdita di precisione. Nella tabella seguente sono elencate le conversioni verso un tipo di dati più grande che possono generare una perdita di informazioni.

Tipo | Conversione in
---- | -------------------
[Int32](xref:System.Int32) | [Single](xref:System.Single)
[UInt32](xref:System.UInt32) | [Single](xref:System.Single)
[Int64](xref:System.Int64) | [Single](xref:System.Single), [Double](xref:System.Double)
[UInt64](xref:System.UInt64) | [Single](xref:System.Single), [Double](xref:System.Double)
[Decimal](xref:System.Decimal) | [Single](xref:System.Single), [Double](xref:System.Double)

## <a name="narrowing-conversions"></a>Conversioni verso un tipo di dati più piccolo

Alcune conversioni verso il tipo di dati più piccolo [Single](xref:System.Single) o [Double](xref:System.Double) possono causare una perdita di informazioni. Se il tipo di destinazione non è in grado di rappresentare in modo appropriato l'ordine di grandezza dell'origine, il tipo risultante viene impostato sulla costante `PositiveInfinity` o `NegativeInfinity`. `PositiveInfinity` è il risultato della divisione di un numero positivo per zero e viene restituito anche quando il valore di un tipo [Single](xref:System.Single) o [Double](xref:System.Double) supera il valore del campo `MaxValue`. `NegativeInfinity` è il risultato della divisione di un numero negativo per zero e viene restituito anche quando il valore di un tipo [Single](xref:System.Single) o [Double](xref:System.Double) è minore del valore del campo `MinValue`. Una conversione da un tipo [Double](xref:System.Double) a un tipo [Single](xref:System.Single) potrebbe avere come risultato un valore `PositiveInfinity` o `NegativeInfinity`.

Una conversione verso un tipo di dati più piccolo può generare una perdita di informazioni anche per altri tipi di dati. Viene tuttavia generato un evento [OverflowException](xref:System.OverflowException)se il valore di un tipo da convertire non rientra nell'intervallo specificato dai campi `MaxValue` e `MinValue` del tipo di destinazione e il processo di conversione viene controllato dal runtime in modo da assicurare che il valore del tipo di destinazione non superi `MaxValue` o `MinValue`. Le conversioni eseguite tramite la classe [System.Convert](xref:System.Convert) vengono sempre controllate in questo modo.

Nella tabella seguente sono elencate le conversioni che generano un evento [OverflowException](xref:System.OverflowException) tramite la classe [System.Convert](xref:System.Convert) o qualsiasi conversione controllata se il valore del tipo convertito non rientra nell'intervallo specificato per il tipo risultante.

Tipo | Conversione in
---- | -------------------
[Byte](xref:System.Byte) | [SByte](xref:System.SByte)
[SByte](xref:System.SByte) | [Byte](xref:System.Byte), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64)
[Int16](xref:System.Int16) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [UInt16](xref:System.UInt16)
[UInt16](xref:System.UInt16) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16)
[Int32](xref:System.Int32) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32)
[UInt32](xref:System.UInt32) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32)
[Int64](xref:System.Int64) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32), [UInt32](xref:System.UInt32), [UInt64](xref:System.UInt64)
[UInt64](xref:System.UInt64) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32), [UInt32](xref:System.UInt32), [Int64](xref:System.Int64)
[Decimal](xref:System.Decimal) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32), [UInt32](xref:System.UInt32), [Int64](xref:System.Int64), [UInt64](xref:System.UInt64)
[Single](xref:System.Single) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32), [UInt32](xref:System.UInt32), [Int64](xref:System.Int64), [UInt64](xref:System.UInt64)
[Double](xref:System.Double) | [Byte](xref:System.Byte), [SByte](xref:System.SByte), [Int16](xref:System.Int16), [UInt16](xref:System.UInt16), [Int32](xref:System.Int32), [UInt32](xref:System.UInt32), [Int64](xref:System.Int64), [UInt64](xref:System.UInt64)

## <a name="see-also"></a>Vedere anche

[System.Convert](xref:System.Convert)

[Conversione di tipi](type-conversion.md)




<!--HONumber=Nov16_HO3-->


