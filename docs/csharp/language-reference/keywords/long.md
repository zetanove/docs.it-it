---
title: "long (Riferimenti per C#) | Microsoft Docs"
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
  - "long_CSharpKeyword"
  - "long"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "long (parola chiave) [C#]"
ms.assetid: f9b24319-1f39-48be-a42b-d528ee28a7fd
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# long (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `long` denota un tipo integrale che memorizza valori in base alla dimensione e all'intervallo indicati nella seguente tabella.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`long`|Da –9.223.372.036.854.775.808 a 9.223.372.036.854.775.807|Numero intero con segno a 64 bit|<xref:System.Int64?displayProperty=fullName>|  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile `long` come nell'esempio riportato di seguito:  
  
```  
  
long long1 = 4294967296;  
```  
  
 Quando un valore letterale integer non ha alcun suffisso, il tipo è il primo dei seguenti tipi in cui è possibile rappresentarne il valore: [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), `long`, [ulong](../../../csharp/language-reference/keywords/ulong.md).  Nell'esempio precedente il valore è di tipo `long` poiché è esterno all'intervallo di [uint](../../../csharp/language-reference/keywords/uint.md). Per informazioni sullo spazio necessario per l'archiviazione dei tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md).  
  
 È inoltre possibile utilizzare il suffisso L con il tipo `long`, come illustrato di seguito:  
  
```  
  
long long2 = 4294967296L;  
```  
  
 Quando si utilizza il suffisso L, il tipo del valore letterale integer viene impostato automaticamente su `long` o [ulong](../../../csharp/language-reference/keywords/ulong.md) a seconda delle dimensioni.  In questo caso è di tipo `long` perché è minore dell'intervallo di [ulong](../../../csharp/language-reference/keywords/ulong.md).  
  
 Il suffisso viene comunemente utilizzato per la chiamata di metodi di overload.  Si considerino, ad esempio, i seguenti metodi di overload che utilizzano parametri `long` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(long l) {}  
```  
  
 L'utilizzo del suffisso L garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
SampleMethod(5);    // Calling the method with the int parameter  
SampleMethod(5L);   // Calling the method with the long parameter  
```  
  
 È possibile utilizzare il tipo `long` con altri tipi integrali numerici nella stessa espressione. In questo caso l'espressione darà un risultato di tipo `long` \(o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane\).  Ad esempio, l'espressione riportata di seguito restituisce `long`:  
  
```  
898L + 88  
```  
  
> [!NOTE]
>  È anche possibile utilizzare la lettera minuscola "l" come suffisso.  In questo caso, viene tuttavia generato un avviso del compilatore perché la lettera "l" viene facilmente confusa con la cifra "1". Per maggiore chiarezza, utilizzare la lettera "L".  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `long` in [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  In tutti gli altri casi è necessario utilizzare un cast.  L'istruzione seguente, ad esempio, genera un errore di compilazione, se non viene utilizzato un cast esplicito:  
  
```  
int x = 8L;        // Error: no implicit conversion from long to int  
int x = (int)8L;   // OK: explicit conversion to int  
```  
  
 Si verifica una conversione implicita predefinita da [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [byte](../../../csharp/language-reference/keywords/byte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md) o [char](../../../csharp/language-reference/keywords/char.md) in `long`.  
  
 Si noti inoltre che non esiste alcuna conversione implicita dai tipi a virgola mobile a `long`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
  
        long x = 3.0;         // Error: no implicit conversion from double  
long y = (long)3.0;   // OK: explicit conversion  
```  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.Int64>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)