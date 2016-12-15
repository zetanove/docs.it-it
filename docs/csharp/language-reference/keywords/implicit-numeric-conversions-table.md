---
title: "Tabella delle conversioni numeriche implicite (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "conversioni [C#], conversioni numeriche implicite"
  - "conversioni numeriche implicite [C#]"
  - "conversioni numeriche [C#], impliciti"
  - "tipi [C#], conversioni numeriche implicite"
ms.assetid: 72eb5a94-0491-48bf-8032-d7ebfdfeb8d8
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Tabella delle conversioni numeriche implicite (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Nella tabella che segue sono illustrate le conversioni numeriche implicite già definite.  Le conversioni implicite possono avere luogo in numerose situazioni, incluse le chiamate a metodi e le istruzioni di assegnazione.  
  
|Da|Per|  
|--------|---------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`short`,`int`,`long`,`float`,`double` o `decimal`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double` o `decimal`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`int`, `long`, `float`, `double` oppure `decimal`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`int`, `uint`, `long`, `ulong`, `float`, `double` o `decimal`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`long`, `float`, `double` o `decimal`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`long`, `ulong`, `float`, `double` oppure `decimal`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`float`, `double` o `decimal`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double` o `decimal`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`double`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`float`,  `double` o `decimal`|  
  
## Note  
  
-   Precisione, ma non la grandezza potrebbe andare persa le conversioni da `int`, `uint`, `long`, o `ulong` a `float` e da `long` o `ulong` a `double`.  
  
-   Non esiste alcuna conversione implicita verso il tipo `char`.  
  
-   Non esiste alcuna conversione implicita tra tipi a virgola mobile e il tipo `decimal`.  
  
-   Un'espressione costante di tipo `int` può essere convertita in`sbyte`, `byte`, `short`, `ushort`, `uint` o `ulong`, a condizione che il valore di tale espressione sia compreso nell'intervallo del tipo di destinazione.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md)