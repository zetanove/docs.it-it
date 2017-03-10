---
title: "Tabella dei valori predefiniti (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "costruttori [C#], valori restituiti"
  - "parole chiave [C#], new"
  - "costruttore predefinito [C#]"
  - "impostazioni predefinite [C#]"
  - "tipi valore [C#], inizializzazione"
  - "variabili [C#], tipi valore"
  - "costruttori [C#], costruttore predefinito"
  - "tipi [C#], valori restituiti dal costruttore predefinito"
ms.assetid: 4af2c1df-9e3a-48c1-83ac-b192986fc5bc
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# Tabella dei valori predefiniti (Riferimenti per C#)
Nella tabella che segue sono riportati i valori predefiniti dei tipi di valore restituiti dai costruttori predefiniti.  I costruttori predefiniti vengono richiamati mediante l'operatore `new`, come riportato di seguito:  
  
```  
int myInt = new int();  
```  
  
 L'istruzione precedente ha lo stesso effetto dell'istruzione che segue:  
  
```  
int myInt = 0;  
```  
  
 Si tenga presente che in C\# non è consentito l'utilizzo di variabili non inizializzate.  
  
|Tipo di valore|Valore predefinito|  
|--------------------|------------------------|  
|[bool](../../../csharp/language-reference/keywords/bool.md)|`false`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|0|  
|[char](../../../csharp/language-reference/keywords/char.md)|'\\0'|  
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|0,0M|  
|[double](../../../csharp/language-reference/keywords/double.md)|0,0D|  
|[enum](../../../csharp/language-reference/keywords/enum.md)|Valore generato dall'espressione \(E\)0, dove E è l'identificatore dell'enumerazione.|  
|[float](../../../csharp/language-reference/keywords/float.md)|0,0F|  
|[int](../../../csharp/language-reference/keywords/int.md)|0|  
|[long](../../../csharp/language-reference/keywords/long.md)|0L|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|0|  
|[short](../../../csharp/language-reference/keywords/short.md)|0|  
|[struct](../../../csharp/language-reference/keywords/struct.md)|Valore generato dall'impostazione di tutti i campi associati a tipi che rappresentano un valore sui rispettivi valori predefiniti e di tutti i campi associati a tipi che rappresentano un riferimento su `null`.|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|0|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|0|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|0|  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tabella dei tipi di valore](../../../csharp/language-reference/keywords/value-types-table.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md)