---
title: byte (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- byte
- byte_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- byte keyword [C#]
ms.assetid: 111f1db9-ca32-4f0e-b497-4783517eda47
caps.latest.revision: 19
author: BillWagner
ms.author: wiwagn
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7c522506b4541edb2a81036e93e8872711f849b9
ms.lasthandoff: 03/13/2017

---
# <a name="byte-c-reference"></a>byte (Riferimenti per C#)
La parola chiave `byte` denota un tipo integrale che archivia valori come indicato nella tabella seguente.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|  
|----------|-----------|----------|-------------------------|  
|`byte`|Da 0 a 255|Intero senza segno a 8 bit|<xref:System.Byte?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali  
 È possibile dichiarare e inizializzare una variabile `byte` come illustrato nell'esempio seguente:  
  
```  
byte myByte = 255;  
```  
  
 Nella dichiarazione precedente, il valore letterale intero `255` viene convertito implicitamente da [int](../../../csharp/language-reference/keywords/int.md) a `byte`. Se il valore letterale intero supera l'intervallo di `byte`, si verifica un errore di compilazione.  
  
## <a name="conversions"></a>Conversioni  
 È disponibile una conversione implicita predefinita da `byte` a [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non è possibile convertire in modo implicito i tipi numerici non letterali di dimensioni di archiviazione maggiori di `byte`. Per altre informazioni sulle dimensioni di archiviazione dei tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md). Considerare, ad esempio, le due variabili `byte` seguenti, `x` e `y`:  
  
```  
  
byte x = 10, y = 20;  
```  
  
 L'istruzione di assegnazione seguente genererà un errore di compilazione, poiché l'espressione aritmetica a destra dell'operatore di assegnazione restituisce `int` per impostazione predefinita.  
  
```  
// Error: conversion from int to byte:  
byte z = x + y;  
```  
  
 Per risolvere il problema, usare un cast:  
  
```  
// OK: explicit conversion:  
byte z = (byte)(x + y);  
```  
  
 È possibile tuttavia usare le istruzioni seguenti dove la variabile di destinazione ha dimensioni uguali o superiori di archiviazione:  
  
```  
int x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 Non è disponibile nessuna conversione implicita dai tipi a virgola mobile a `byte`. Ad esempio, l'istruzione seguente genera un errore di compilazione, a meno che non venga usato un cast esplicito:  
  
```  
// Error: no implicit conversion from double:  
byte x = 3.0;   
// OK: explicit conversion:  
byte y = (byte)3.0;  
```  
  
 Quando si chiamano metodi di overload, è necessario usare un cast. Considerare, ad esempio, i metodi seguenti di overload che usano i parametri `byte` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(byte b) {}  
```  
  
 L'uso del cast `byte` garantisce che verrà chiamato il tipo corretto, ad esempio:  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the byte parameter:  
SampleMethod((byte)5);  
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per altre informazioni sulle regole di conversione numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Byte>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
