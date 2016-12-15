---
title: "ushort (Riferimenti per C#) | Microsoft Docs"
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
  - "ushort"
  - "ushort_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "ushort (parola chiave) [C#]"
ms.assetid: 1a7dbaae-b7a0-4111-872a-c88a6d3981ac
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ushort (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `ushort` indica un tipo di dati integrale che memorizza valori in base alla dimensione e all'intervallo indicati nella seguente tabella.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`ushort`|Da 0 a 65.535|Numero intero senza segno a 16 bit|<xref:System.UInt16?displayProperty=fullName>|  
  
## Valori letterali  
 È possibile dichiarare e inizializzare una variabile `ushort` come nell'esempio riportato di seguito:  
  
```  
  
ushort myShort = 65535;  
```  
  
 Nella precedente dichiarazione il valore letterale integer `65535` viene convertito in modo implicito da [int](../../../csharp/language-reference/keywords/int.md) a `ushort`.  Se il valore letterale integer è esterno all'intervallo consentito per `ushort`, viene generato un errore di compilazione.  
  
 Quando si chiamano metodi di overload, è necessario utilizzare un cast.  Si considerino, ad esempio, i seguenti metodi di overload che utilizzano parametri `ushort` e [int](../../../csharp/language-reference/keywords/int.md):  
  
```  
public static void SampleMethod(int i) {}  
public static void SampleMethod(ushort s) {}  
```  
  
 L'utilizzo del cast di `ushort` garantisce che venga chiamato il tipo corretto, ad esempio:  
  
```  
// Calls the method with the int parameter:  
SampleMethod(5);  
// Calls the method with the ushort parameter:  
SampleMethod((ushort)5);    
```  
  
## Conversioni  
 Si verifica una conversione implicita predefinita da `ushort` in [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  
  
 Si verifica una conversione implicita predefinita da [byte](../../../csharp/language-reference/keywords/byte.md) o [char](../../../csharp/language-reference/keywords/char.md) in `ushort`.  In tutti gli altri casi è necessario ricorrere a un cast per eseguire una conversione esplicita.  Si considerino, ad esempio, le due variabili `ushort` seguenti `x` e `y`:  
  
```  
  
ushort x = 5, y = 12;  
```  
  
 L'istruzione di assegnazione che segue provocherà un errore di compilazione poiché, per impostazione predefinita, l'espressione aritmetica a destra dell'operatore di assegnazione restituisce `int`.  
  
```  
  
ushort z = x + y;   // Error: conversion from int to ushort  
```  
  
 Per correggere l'errore, utilizzare un cast:  
  
```  
  
ushort z = (ushort)(x + y);   // OK: explicit conversion   
```  
  
 È tuttavia possibile utilizzare le seguenti istruzioni, in cui la variabile di destinazione ha dimensioni di archiviazione uguali o superiori:  
  
```  
int m = x + y;  
long n = x + y;  
```  
  
 Si noti inoltre che non esiste alcuna conversione implicita dai tipi a virgola mobile a `ushort`.  L'istruzione seguente, ad esempio, genera un errore di compilazione, a meno che non venga utilizzato un cast esplicito:  
  
```  
// Error -- no implicit conversion from double:  
ushort x = 3.0;   
// OK -- explicit conversion:  
ushort y = (ushort)3.0;  
```  
  
 Per ulteriori informazioni sulle espressioni aritmetiche con tipi a virgola mobile e tipi integrali, vedere [float](../../../csharp/language-reference/keywords/float.md) e [double](../../../csharp/language-reference/keywords/double.md).  
  
 Per ulteriori informazioni sulle regole di conversione numerica implicita, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 <xref:System.UInt16>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)