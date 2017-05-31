---
title: int (Riferimenti per C#) | Microsoft Docs
ms.date: 2017-03-14
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- int_CSharpKeyword
- int
dev_langs:
- CSharp
helpviewer_keywords:
- int keyword [C#]
ms.assetid: 212447b4-5d2a-41aa-88ab-84fe710bdb52
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: 48283ce80bbbff4182362ea9ae6258d31e175e0d
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="int-c-reference"></a>int (Riferimenti per C#)

`int` denota un tipo integrale che archivia valori in base alla dimensione e all'intervallo visualizzato nella tabella seguente.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|Valore predefinito|  
|----------|-----------|----------|-------------------------|-------------------|  
|`int`|da -2.147.483.648 a 2.147.483.647|Valore intero a 32 bit con segno|<xref:System.Int32?displayProperty=fullName>|0|  
  
## <a name="literals"></a>Valori letterali  
 
È possibile dichiarare e inizializzare una variabile `int` assegnandole un valore letterale decimale, un valore letterale esadecimale o (a partire da C# 7) un valore letterale binario.  Se il valore letterale intero non è incluso nell'intervallo `int` (ovvero, se è minore di <xref:System.Int32.MinValue?displayProperty=fullName> o maggiore di <xref:System.Int32.MaxValue?displayProperty=fullName>) si verifica un errore di compilazione. 

Nell'esempio seguente, i valori interi uguali a 16.342 rappresentati come valori letterali decimali, esadecimali o binari vengono assegnati a valori `int`.  
  
[!code-cs[int](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#Int)]  

> [!NOTE] 
> Viene usato il prefisso `0x` o `0X` per identificare un valore letterale esadecimale e il prefisso `0b` o `0B` per identificare un valore letterale binario. I valori letterali decimali non hanno prefissi. 

A partire da C# 7, è anche possibile usare il carattere di sottolineatura, `_`, come separatore di cifre per migliorare la leggibilità, come illustrato nell'esempio seguente.

[!code-cs[int](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#IntS)]  
 
 I valori letterali integer possono includere anche un suffisso che denoti il tipo, anche se non è disponibile alcun suffisso che denoti il tipo `int`. Se un valore letterale integer non ha alcun suffisso, il suo tipo corrisponderà al primo dei tipi seguenti in cui il suo valore può essere rappresentato: 

1. `int`
2. [uint](../../../csharp/language-reference/keywords/uint.md)
3. [long](../../../csharp/language-reference/keywords/long.md)
4. [ulong](../../../csharp/language-reference/keywords/ulong.md) 
 
In questi esempi il valore letterale 90946 è di tipo `int`.
  
## <a name="conversions"></a>Conversioni  
 Si verifica una conversione implicita predefinita da `int` a [long](../../../csharp/language-reference/keywords/long.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md). Ad esempio:  
  
```csharp  
// '123' is an int, so an implicit conversion takes place here:  
float f = 123;  
```  
  
 Si verifica una conversione implicita predefinita da [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md) o [char](../../../csharp/language-reference/keywords/char.md) a `int`. L'istruzione di assegnazione seguente, ad esempio, genera un errore di compilazione se non viene usato un cast:  
  
```csharp  
long aLong = 22;  
int i1 = aLong;       // Error: no implicit conversion from long.  
int i2 = (int)aLong;  // OK: explicit conversion.  
```  
  
 Si noti inoltre che non avviene alcuna conversione implicita dai tipi a virgola mobile in `int`. L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga usato un cast esplicito:  
  
```csharp  
int x = 3.0;         // Error: no implicit conversion from double.  
int y = (int)3.0;    // OK: explicit conversion.  
```  
  
 Per altre informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Int32>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
