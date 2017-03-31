---
title: sbyte (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- sbyte_CSharpKeyword
- sbyte
dev_langs:
- CSharp
helpviewer_keywords:
- sbyte keyword [C#]
ms.assetid: 1a9c7b48-73d1-4d33-b485-c4faf0a816bc
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: df57296bb285441aeddc596289d82d1e458dc278
ms.lasthandoff: 03/13/2017

---
# <a name="sbyte-c-reference"></a>sbyte (Riferimenti per C#)
La parola chiave `sbyte` indica un tipo integrale che memorizza valori in base alla dimensione e all'intervallo indicati nella seguente tabella.  
  
|Tipo|Intervallo|Dimensioni|Tipo .NET Framework|  
|----------|-----------|----------|-------------------------|  
|`sbyte`|Da -128 a 127|Valore intero con segno a 8 bit|<xref:System.SByte?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali  
 È possibile dichiarare e inizializzare una variabile `sbyte` come riportato di seguito:  
  
```  
  
sbyte sByte1 = 127;  
```  
  
 Nella precedente dichiarazione il valore letterale intero 127 viene convertito in modo implicito da [int](../../../csharp/language-reference/keywords/int.md) a `sbyte`. Se il valore letterale intero supera l'intervallo di `sbyte`, si verifica un errore di compilazione.  
  
 È necessario usare un cast quando si chiamano metodi di overload. Considerare, ad esempio, i metodi seguenti di overload che usano i parametri `sbyte` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(sbyte b) {}  
```  
  
 L'uso del cast `sbyte` garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the sbyte parameter:  
SampleMethod((sbyte)5);  
```  
  
## <a name="conversions"></a>Conversioni  
 Si verifica una conversione implicita predefinita da `sbyte` a [short](../../../csharp/language-reference/keywords/short.md), [int](../../../csharp/language-reference/keywords/int.md), [long](../../../csharp/language-reference/keywords/long.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non è possibile convertire in modo implicito tipi numerici non letterali che necessitano di maggiore spazio in memoria in `sbyte`. Per informazioni sullo spazio necessario per l'archiviazione dei tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md). Considerare, ad esempio, le due variabili `sbyte` seguenti, `x` e `y`:  
  
```  
  
sbyte x = 10, y = 20;  
```  
  
 L'istruzione di assegnazione che segue provocherà un errore di compilazione poiché, per impostazione predefinita, l'espressione aritmetica a destra dell'operatore di assegnazione restituisce [int](../../../csharp/language-reference/keywords/int.md).  
  
```  
  
sbyte z = x + y;   // Error: conversion from int to sbyte  
```  
  
 Per risolvere il problema, eseguire il cast dell'espressione come nell'esempio seguente:  
  
```  
  
sbyte z = (sbyte)(x + y);   // OK: explicit conversion  
```  
  
 È possibile tuttavia usare le istruzioni seguenti dove la variabile di destinazione ha la stessa dimensione di archiviazione o una dimensione maggiore:  
  
```  
  
      sbyte x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 Si noti inoltre che non avviene alcuna conversione implicita dai tipi a virgola mobile in `sbyte`. Ad esempio, l'istruzione seguente genera un errore del compilatore, a meno che non venga usato un cast esplicito:  
  
```  
  
      sbyte x = 3.0;         // Error: no implicit conversion from double  
sbyte y = (sbyte)3.0;  // OK: explicit conversion  
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per altre informazioni sulle regole di conversione numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.SByte>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
