---
title: "byte (Riferimenti per C#) | Microsoft Docs"
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
  - "byte"
  - "byte_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "byte (parola chiave) [C#]"
ms.assetid: 111f1db9-ca32-4f0e-b497-4783517eda47
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# byte (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `byte` denota un tipo integrale che archivia valori, come indicato nella tabella riportata di seguito.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`byte`|Da 0 a 255|Numero intero senza segno a 8 bit|<xref:System.Byte?displayProperty=fullName>|  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile `byte` come nell'esempio riportato di seguito.  
  
```  
byte myByte = 255;  
```  
  
 Nella precedente dichiarazione il valore letterale integer `255` è convertito in modo implicito da [int](../../../csharp/language-reference/keywords/int.md) a `byte`.  Se il valore letterale integer è esterno all'intervallo consentito per `byte`, viene generato un errore di compilazione.  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `byte` a [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Non è possibile convertire implicitamente in `byte` tipi numerici non letterali che richiedono un maggiore spazio in memoria.  Per ulteriori informazioni sullo spazio necessario per l'archiviazione di tipi integrali, vedere [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md).  Si considerino, ad esempio, le due variabili `byte` seguenti `x` e `y`:  
  
```  
  
byte x = 10, y = 20;  
```  
  
 L'istruzione di assegnazione riportata di seguito provocherà un errore di compilazione perché, per impostazione predefinita, l'espressione aritmetica sulla parte destra dell'operatore di assegnazione restituisce `int`.  
  
```  
// Error: conversion from int to byte:  
byte z = x + y;  
```  
  
 Per correggere l'errore, utilizzare un cast:  
  
```  
// OK: explicit conversion:  
byte z = (byte)(x + y);  
```  
  
 È tuttavia possibile utilizzare le seguenti istruzioni, in cui la variabile di destinazione ha dimensioni di archiviazione uguali o superiori:  
  
```  
int x = 10, y = 20;  
int m = x + y;  
long n = x + y;  
```  
  
 Non esiste inoltre alcuna conversione implicita dai tipi a virgola mobile a `byte`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
// Error: no implicit conversion from double:  
byte x = 3.0;   
// OK: explicit conversion:  
byte y = (byte)3.0;  
```  
  
 Quando si chiamano metodi di overload è necessario utilizzare un cast.  Si considerino, ad esempio, i seguenti metodi di overload che utilizzano parametri `byte` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(byte b) {}  
```  
  
 L'utilizzo del cast di `byte` garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
// Calling the method with the int parameter:  
SampleMethod(5);  
// Calling the method with the byte parameter:  
SampleMethod((byte)5);  
```  
  
 Per informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per ulteriori informazioni sulle regole di conversione numerica implicita, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.Byte>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)