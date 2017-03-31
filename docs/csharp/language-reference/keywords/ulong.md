---
title: ulong (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ulong_CSharpKeyword
- ulong
dev_langs:
- CSharp
helpviewer_keywords:
- ulong keyword [C#]
ms.assetid: f2ece624-837a-40cf-92c5-343e7f33397c
caps.latest.revision: 16
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
ms.openlocfilehash: 36de0add1d7fdf58745c65d231f3789c532ab69f
ms.lasthandoff: 03/13/2017

---
# <a name="ulong-c-reference"></a>ulong (Riferimenti per C#)
La parola chiave `ulong` denota un tipo integrale che archivia valori in base alla dimensione e all'intervallo mostrato nella tabella seguente.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|  
|----------|-----------|----------|-------------------------|  
|`ulong`|Da 0 a 18.446.744.073.709.551.615|Intero senza segno a 64 bit|<xref:System.UInt64?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali  
 È possibile dichiarare e inizializzare una variabile `ulong` come illustrato nell'esempio seguente:  
  
```  
  
ulong uLong = 9223372036854775808;  
```  
  
 Quando un valore letterale integer non ha alcun suffisso, il tipo è il primo di questi tipi in cui può essere rappresentato il relativo valore: [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), `ulong`. Nell'esempio precedente, è di tipo `ulong`.  
  
 È anche possibile usare un suffisso per specificare il tipo del valore letterale in base alle regole seguenti:  
  
-   Se si usa L o l, il tipo di valore letterale intero sarà [long](../../../csharp/language-reference/keywords/long.md) o `ulong` in base alle dimensioni.  
  
    > [!NOTE]
    >  È possibile usare la lettera minuscola "l" come suffisso. In questo caso, viene tuttavia generato un avviso del compilatore perché la lettera "l" viene facilmente confusa con la cifra "1". Per maggiore chiarezza, usare la lettera "L".  
  
-   Se si usa `U` o `u`, il tipo di valore letterale intero sarà [uint](../../../csharp/language-reference/keywords/uint.md) o `ulong` in base alle dimensioni.  
  
-   Se si usa UL, ul, Ul, uL, LU, lu, Lu o lU, il tipo di valore letterale sarà `ulong`.  
  
     Ad esempio, l'output delle tre istruzioni seguenti tre sarà il tipo di sistema `UInt64`, che corrisponde all'alias `ulong`:  
  
    ```  
    Console.WriteLine(9223372036854775808L.GetType());  
    Console.WriteLine(123UL.GetType());  
    Console.WriteLine((123UL + 456).GetType());  
    ```  
  
 Il suffisso viene comunemente usato per la chiamata di metodi di overload. Considerare, ad esempio, i metodi seguenti di overload che usano i parametri `ulong` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(ulong l) {}  
```  
  
 L'uso del suffisso con il parametro `ulong` garantisce che verrà chiamato il tipo corretto, ad esempio:  
  
```  
SampleMethod(5);    // Calling the method with the int parameter  
SampleMethod(5UL);  // Calling the method with the ulong parameter  
```  
  
## <a name="conversions"></a>Conversioni  
 Si verifica una conversione implicita predefinita da `ulong` a [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non viene eseguita alcuna conversione implicita da `ulong` a qualsiasi tipo integrale. L'istruzione seguente, ad esempio, genera un errore di compilazione se non viene usato un cast esplicito:  
  
```  
long long1 = 8UL;   // Error: no implicit conversion from ulong  
```  
  
 Viene eseguita una conversione implicita predefinita da [byte](../../../csharp/language-reference/keywords/byte.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [uint](../../../csharp/language-reference/keywords/uint.md) o [char](../../../csharp/language-reference/keywords/char.md) a `ulong`.  
  
 Non viene eseguita alcuna conversione implicita dai tipi a virgola mobile a `ulong`. Ad esempio, l'istruzione seguente genera un errore del compilatore, a meno che non venga usato un cast esplicito:  
  
```  
// Error -- no implicit conversion from double:  
ulong x = 3.0;  
// OK -- explicit conversion:  
ulong y = (ulong)3.0;    
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per altre informazioni sulle regole di conversione numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.UInt64>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
