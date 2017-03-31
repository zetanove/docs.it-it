---
title: uint (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- uint
- uint_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- uint keyword [C#]
ms.assetid: e93e42c6-ec72-4b0b-89df-2fd8d36f7a7b
caps.latest.revision: 18
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
ms.openlocfilehash: fe4f7fcbbadee600e0ba6de70508312173d098ff
ms.lasthandoff: 03/13/2017

---
# <a name="uint-c-reference"></a>uint (Riferimenti per C#)
La parola chiave `uint` rappresenta un tipo integrale che archivia valori in base alla dimensione e all'intervallo mostrato nella tabella seguente.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|  
|----------|-----------|----------|-------------------------|  
|`uint`|Da 0 a 4.294.967.295|Intero senza segno a 32 bit|<xref:System.UInt32?displayProperty=fullName>|  
  
 **Nota** Il tipo `uint` non è conforme a CLS. Usare `int`, laddove possibile.  
  
## <a name="literals"></a>Valori letterali  
 È possibile dichiarare e inizializzare una variabile di tipo `uint`, come illustrato nell'esempio seguente:  
  
```  
  
uint myUint = 4294967290;  
```  
  
 Quando un valore letterale intero non ha suffisso, il tipo è il primo dei seguenti tipi in cui è possibile rappresentarne il valore: [int](../../../csharp/language-reference/keywords/int.md), `uint`, [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md). In questo esempio è `uint`:  
  
```  
  
uint uInt1 = 123;  
```  
  
 È possibile anche usare il suffisso u o U, come illustrato di seguito:  
  
```  
  
uint uInt2 = 123U;  
```  
  
 Quando si usa il suffisso `U` o `u`, il tipo del valore letterale viene specificato come `uint` o `ulong`, a seconda del valore numerico del valore letterale. Ad esempio:  
  
```  
Console.WriteLine(44U.GetType());  
Console.WriteLine(323442434344U.GetType());  
```  
  
 In questo codice viene visualizzato `System.UInt32`, seguito da `System.UInt64` rispettivamente i tipi sottostanti di `uint` e `ulong`, rispettivamente, perché il secondo valore letterale è troppo grande per essere archiviato dal tipo `uint`.  
  
## <a name="conversions"></a>Conversioni  
 Si verifica una conversione implicita predefinita da `uint` a [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md). Ad esempio:  
  
```  
float myFloat = 4294967290;   // OK: implicit conversion to float  
```  
  
 Viene eseguita una conversione implicita predefinita da [byte](../../../csharp/language-reference/keywords/byte.md), [ushort](../../../csharp/language-reference/keywords/ushort.md) o [char](../../../csharp/language-reference/keywords/char.md) a `uint`. In tutti gli altri casi è necessario ricorrere a un cast. Nella seguente istruzione di assegnazione, ad esempio, verrà generato un errore di compilazione senza un cast:  
  
```  
long aLong = 22;  
// Error -- no implicit conversion from long:  
uint uInt1 = aLong;   
// OK -- explicit conversion:  
uint uInt2 = (uint)aLong;  
```  
  
 Si noti inoltre che non avviene alcuna conversione implicita dai tipi a virgola mobile in `uint`. Ad esempio, l'istruzione seguente genera un errore del compilatore, a meno che non venga usato un cast esplicito:  
  
```  
// Error -- no implicit conversion from double:  
uint x = 3.0;  
// OK -- explicit conversion:  
uint y = (uint)3.0;   
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per altre informazioni sulle regole di conversione numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.UInt32>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
