---
title: "ulong (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ulong_CSharpKeyword"
  - "ulong"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ulong (parola chiave) [C#]"
ms.assetid: f2ece624-837a-40cf-92c5-343e7f33397c
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ulong (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `ulong` denota un tipo integrale che memorizza valori in base alla dimensione e all'intervallo indicati nella seguente tabella.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`ulong`|Da 0 a 18,446,744,073,709,551,615|Numero intero senza segno a 64 bit|<xref:System.UInt64?displayProperty=fullName>|  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile `ulong` come nell'esempio riportato di seguito:  
  
```  
  
ulong uLong = 9223372036854775808;  
```  
  
 Quando un valore letterale integer non ha alcun suffisso, il tipo è il primo dei seguenti tipi in cui è possibile rappresentarne il valore: [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), `ulong`.  Nell'esempio precedente il tipo è `ulong`.  
  
 È inoltre possibile utilizzare un suffisso per specificare il tipo del valore letterale in base ai criteri descritti di seguito.  
  
-   Se si utilizza L o l, il tipo del valore letterale integer sarà [long](../../../csharp/language-reference/keywords/long.md) o `ulong`, a seconda delle dimensioni.  
  
    > [!NOTE]
    >  È possibile utilizzare la lettera minuscola "l" come suffisso.  In questo caso, viene tuttavia generato un avviso del compilatore perché la lettera "l" viene facilmente confusa con la cifra "1". Per maggiore chiarezza, utilizzare la lettera "L".  
  
-   Se si utilizza`U` o `u`, il tipo del valore letterale integer sarà [uint](../../../csharp/language-reference/keywords/uint.md) o `ulong`, a seconda delle dimensioni.  
  
-   Se si utilizza UL, ul, Ul, uL, LU, lu, Lu o lU, il tipo del valore letterale integer sarà `ulong`.  
  
     L'output delle tre istruzioni riportate di seguito, ad esempio, sarà il tipo di sistema `UInt64` che corrisponde all'alias `ulong`:  
  
    ```  
    Console.WriteLine(9223372036854775808L.GetType());  
    Console.WriteLine(123UL.GetType());  
    Console.WriteLine((123UL + 456).GetType());  
    ```  
  
 Il suffisso viene comunemente utilizzato per la chiamata di metodi di overload.  Si considerino, ad esempio, i seguenti metodi di overload che utilizzano parametri `ulong` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(ulong l) {}  
```  
  
 L'utilizzo di un suffisso con il parametro `ulong` garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
SampleMethod(5);    // Calling the method with the int parameter  
SampleMethod(5UL);  // Calling the method with the ulong parameter  
```  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `ulong` in [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non esiste alcuna conversione implicita da `ulong` ai tipi integrali.  L'istruzione seguente, ad esempio, genera un errore di compilazione, se non viene utilizzato un cast esplicito:  
  
```  
long long1 = 8UL;   // Error: no implicit conversion from ulong  
```  
  
 Si verifica una conversione implicita predefinita da [byte](../../../csharp/language-reference/keywords/byte.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [uint](../../../csharp/language-reference/keywords/uint.md) o [char](../../../csharp/language-reference/keywords/char.md) in `ulong`.  
  
 Non esiste inoltre alcuna conversione implicita dai tipi a virgola mobile a `ulong`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
// Error -- no implicit conversion from double:  
ulong x = 3.0;  
// OK -- explicit conversion:  
ulong y = (ulong)3.0;    
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per ulteriori informazioni sulle regole di conversione numerica implicita, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.UInt64>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)