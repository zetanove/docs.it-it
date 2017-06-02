---
title: long (Riferimenti per C#) | Microsoft Docs
ms.date: 2017-03-14
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- long_CSharpKeyword
- long
dev_langs:
- CSharp
helpviewer_keywords:
- long keyword [C#]
ms.assetid: f9b24319-1f39-48be-a42b-d528ee28a7fd
caps.latest.revision: 17
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
ms.openlocfilehash: 0ea7f109ab934660418aab1a88bff7206ef23a37
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="long-c-reference"></a>long (Riferimenti per C#)

`long` denota un tipo integrale che archivia valori in base alla dimensione e all'intervallo visualizzato nella tabella seguente.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|  
|----------|-----------|----------|-------------------------|  
|`long`|Da –9,223,372,036,854,775,808 a 9,223,372,036,854,775,807|Numero intero con segno a 64 bit|<xref:System.Int64?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali 

È possibile dichiarare e inizializzare una variabile `long` assegnandole un valore letterale decimale, un valore letterale esadecimale o (a partire da C# 7) un valore letterale binario. 

Nell'esempio seguente, i valori interi uguali a 4.294.967.296 rappresentati come valori letterali decimali, esadecimali o binari vengono assegnati a valori `long`.  
  
[!code-cs[long](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#Long)]  

> [!NOTE] 
> Viene usato il prefisso `0x` o `0X` per identificare un valore letterale esadecimale e il prefisso `0b` o `0B` per identificare un valore letterale binario. I valori letterali decimali non hanno prefissi. 

A partire da C# 7, è anche possibile usare il carattere di sottolineatura, `_`, come separatore di cifre per migliorare la leggibilità, come illustrato nell'esempio seguente.

[!code-cs[long](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#LongS)]  
 
 Valori letterali integer possono anche includere un suffisso che denota il tipo. Il suffisso `L` denota un `long`. L'esempio seguente usa il suffisso `L` per indicare un valore long integer:
 
```csharp
long value = 4294967296L;  
```  

> [!NOTE]
>  È anche possibile usare la lettera minuscola "l" come suffisso. In questo caso, viene tuttavia generato un avviso del compilatore perché la lettera "l" viene facilmente confusa con la cifra "1". Per maggiore chiarezza, usare la lettera "L".  
  
 Quando si usa il suffisso `L`, il tipo del valore letterale integer viene impostato su `long` o [ulong](../../../csharp/language-reference/keywords/ulong.md) a seconda delle dimensioni. In questo caso è di tipo `long` perché è minore dell'intervallo di [ulong](../../../csharp/language-reference/keywords/ulong.md).  
  
 Un uso comune del suffisso è la chiamata di metodi di overload. I metodi di overload seguenti, ad esempio, hanno parametri di tipo `long` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```csharp
public static void SampleMethod(int i) {}  
public static void SampleMethod(long l) {}  
```  
  
 Il suffisso `L` garantisce che venga chiamato l'overload corretto:  
  
```csharp  
SampleMethod(5);    // Calls the method with the int parameter  
SampleMethod(5L);   // Calls the method with the long parameter  
```  
Se un valore letterale integer non ha alcun suffisso, il suo tipo corrisponderà al primo dei tipi seguenti in cui il suo valore può essere rappresentato: 

1. [int](int.md)
2. [uint](../../../csharp/language-reference/keywords/uint.md)
3. `long`
4. [ulong](../../../csharp/language-reference/keywords/ulong.md) 

Il valore letterale 4294967296 nell'esempio precedente è di tipo `long` perché è esterno all'intervallo di [uint](../../../csharp/language-reference/keywords/uint.md). Per informazioni sullo spazio necessario per l'archiviazione dei tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md).  
  
 Se si usa il tipo `long` con altri tipi integrali nella stessa espressione, l'espressione darà un risultato di tipo `long` (o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane). Ad esempio, l'espressione riportata di seguito restituisce `long`:  
  
```csharp  
898L + 88  
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
## <a name="conversions"></a>Conversioni  
 Si verifica una conversione implicita predefinita da `long` a [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md). In tutti gli altri casi è necessario usare un cast. L'istruzione seguente, ad esempio, genera un errore di compilazione se non viene usato un cast esplicito:  
  
```csharp  
int x = 8L;        // Error: no implicit conversion from long to int  
int x = (int)8L;   // OK: explicit conversion to int  
```  
  
 Si verifica una conversione implicita predefinita da [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md) o [char](../../../csharp/language-reference/keywords/char.md) in `long`.  
  
 Si noti anche che non esiste alcuna conversione implicita dai tipi a virgola mobile a `long`. L'istruzione seguente, ad esempio, genera un errore di compilazione a meno che non venga usato un cast esplicito:  
  
```csharp  
long x = 3.0;         // Error: no implicit conversion from double  
long y = (long)3.0;   // OK: explicit conversion  
```  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Int64>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
