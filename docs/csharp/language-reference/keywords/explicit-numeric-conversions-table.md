---
title: "Tabella delle conversioni numeriche esplicite (Riferimenti per C#) | Microsoft Docs"
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
  - "conversioni [C#], numeriche esplicite"
  - "conversioni numeriche esplicite [C#]"
  - "conversioni numeriche [C#], esplicita"
  - "tipi di dati numerici [C#]"
  - "conversione di tipi [C#], numeriche esplicite"
  - "tipi [C#], conversioni numeriche esplicite"
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Tabella delle conversioni numeriche esplicite (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La conversione numerica esplicita è utilizzata per convertire qualsiasi tipo numerico in qualsiasi altro tipo numerico, per il quale non esiste alcuna conversione implicita, utilizzando un'espressione cast.  Tali conversioni sono illustrate nella tabella che segue.  
  
 Per ulteriori informazioni sulle conversioni, vedere [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md).  
  
|Da|Per|  
|--------|---------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`byte`, `ushort`, `uint`, `ulong` oppure `char`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`Sbyte` o `char`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`sbyte`, `byte`, `ushort`, `uint`, `ulong` o  `char`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`sbyte`,  `byte`,  `short` o  `char`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`sbyte`, `byte`, `short`, `ushort`, `uint`, `ulong`, ``  o  `char`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`sbyte`,`byte`, `short`, `ushort`, `int` o  `char`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`sbyte`,  `byte`, `short`, `ushort`,  `int`, `uint`, `ulong` o  `char`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`sbyte`,  `byte`, `short`, `ushort`,  `int`, `uint`, `long` o  `char`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`sbyte`, `byte` o  `short`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, ``  o  `decimal`|  
|[double](../../../csharp/language-reference/keywords/double.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, ``  o  `decimal`|  
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float` o  `double`|  
  
## Note  
  
-   La conversione numerica esplicita può causare una perdita nella precisione o comportare la generazione di eccezioni.  
  
-   Quando si esegue una conversione da un valore `decimal` in un tipo integrale, il valore viene arrotondato al più vicino valore integrale in direzione dello zero.  Se il valore integrale risultante non è incluso nell'intervallo del tipo di destinazione, verrà generata un'eccezione <xref:System.OverflowException>.  
  
-   Quando si esegue una conversione da un valore `double` o `float` in un tipo integrale, il valore viene troncato.  Se il valore integrale restituito è esterno all'intervallo del valore di destinazione, il risultato dipende dal contesto di controllo dell'overflow.  In un contesto checked viene generata un'eccezione `OverflowException`, mentre in un contesto unckecked il risultato è un valore non specificato del tipo di destinazione.  
  
-   Per una conversione da `double` in `float`, il valore `double` viene arrotondato al valore `float` più vicino.  Se il valore `double` è troppo piccolo o troppo grande per essere contenuto nel tipo di destinazione, il risultato sarà zero o infinito.  
  
-   Per una conversione da `float` o `double` in `decimal`, il valore di origine viene convertito nella rappresentazione `decimal` e arrotondato al numero più vicino successivo alla ventottesima cifra decimale, se necessario.  A seconda dell'entità del valore di origine, è possibile che si verifichi uno dei seguenti risultati:  
  
    -   Se il valore di origine è troppo piccolo per essere rappresentato come `decimal`, il risultato sarà zero.  
  
    -   Se il valore di origine è NaN \(non numerico\), infinito o troppo grande per essere rappresentato come `decimal`, verrà generata un'eccezione `OverflowException`.  
  
-   Per una conversione da `decimal` in `float` o `double`, il valore `decimal` viene arrotondato al valore `double` o `float` più vicino.  
  
 Per ulteriori informazioni sulla conversione esplicita, vedere Explicit nella Specifica del linguaggio C\#.  Per ulteriori informazioni su come accedere alla specifica, vedere [Specifiche del linguaggio C\#](../../../csharp/language-reference/language-specification.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [Operatore \(\)](../../../csharp/language-reference/operators/invocation-operator.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)