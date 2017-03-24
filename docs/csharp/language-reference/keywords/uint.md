---
title: "uint (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "uint"
  - "uint_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "uint (parola chiave) [C#]"
ms.assetid: e93e42c6-ec72-4b0b-89df-2fd8d36f7a7b
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# uint (Riferimenti per C#)
La parola chiave `uint` rappresenta un tipo di dati integrale che archivia valori in base alla dimensione e all'intervallo indicati nella tabella seguente.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`uint`|Da 0 a 4.294.967.295|Numero intero senza segno a 32 bit|<xref:System.UInt32?displayProperty=fullName>|  
  
 **Nota** Il tipo `uint` non è conforme a CLS.  Utilizzare `int` quando possibile.  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile di tipo `uint` come nell'esempio seguente:  
  
```  
  
uint myUint = 4294967290;  
```  
  
 Quando un valore letterale integer non ha alcun suffisso, il tipo è il primo dei seguenti tipi in cui è possibile rappresentarne il valore: [int](../../../csharp/language-reference/keywords/int.md), `uint`, [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md).  In questo esempio è `uint`:  
  
```  
  
uint uInt1 = 123;  
```  
  
 È inoltre possibile utilizzare il suffisso u o U, come illustrato di seguito:  
  
```  
  
uint uInt2 = 123U;  
```  
  
 Quando si utilizza il suffisso `U` o `u`, il tipo del valore letterale viene specificato come `uint` o `ulong`, a seconda del valore numerico del valore letterale.  Di seguito è riportato un esempio:  
  
```  
Console.WriteLine(44U.GetType());  
Console.WriteLine(323442434344U.GetType());  
```  
  
 In questo codice viene visualizzato `System.UInt32`, seguito da `System.UInt64`, rispettivamente i tipi sottostanti di `uint` e `ulong`, perché il secondo valore letterale è troppo grande per essere archiviato dal tipo `uint`.  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `uint` in [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  Di seguito è riportato un esempio:  
  
```  
float myFloat = 4294967290;   // OK: implicit conversion to float  
```  
  
 Si verifica una conversione implicita predefinita da [byte](../../../csharp/language-reference/keywords/byte.md), [ushort](../../../csharp/language-reference/keywords/ushort.md) o [char](../../../csharp/language-reference/keywords/char.md) in `uint`.  In tutti gli altri casi è necessario ricorrere a un cast.  Nella seguente istruzione di assegnazione verrà ad esempio generato un errore di compilazione senza un cast:  
  
```  
long aLong = 22;  
// Error -- no implicit conversion from long:  
uint uInt1 = aLong;   
// OK -- explicit conversion:  
uint uInt2 = (uint)aLong;  
```  
  
 Si noti inoltre che non esiste alcuna conversione implicita dai tipi a virgola mobile a `uint`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
// Error -- no implicit conversion from double:  
uint x = 3.0;  
// OK -- explicit conversion:  
uint y = (uint)3.0;   
```  
  
 Per ulteriori informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per ulteriori informazioni sulle regole di conversione numerica implicita, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.UInt32>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)