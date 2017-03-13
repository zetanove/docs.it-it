---
title: "char (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "char"
  - "char_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "char (tipo di dati) [C#]"
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
caps.latest.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 27
---
# char (Riferimenti per C#)
La parola chiave di `char` utilizzata per dichiarare un'istanza della struttura di <xref:System.Char?displayProperty=fullName> di.NET Framework per rappresentare un carattere unicode.  Il valore di un oggetto di `Char` è un valore numerico a 16 bit \(ordinale\).  
  
 I caratteri unicode vengono utilizzati per rappresentare la maggior parte delle lingue scritte nel mondo intero.  
  
|Type|Intervallo|Dimensione|Tipo .NET Framework|  
|----------|----------------|----------------|-------------------------|  
|`char`|Da U\+0000 a U\+FFFF|Carattere Unicode a 16 bit|<xref:System.Char?displayProperty=fullName>|  
  
## Valori letterali  
 Le costanti del tipo `char` possono essere scritte come valori letterali carattere, sequenze di escape esadecimali o rappresentazioni Unicode.  È inoltre possibile impostare i codici con caratteri integrali.  Nell'esempio seguente quattro variabili `char` vengono inizializzate con lo stesso carattere `X`:  
  
 [!code-cs[csrefKeywordsTypes#19](../../../csharp/language-reference/keywords/codesnippet/CSharp/char_1.cs)]  
  
## Conversioni  
 Un tipo `char` può essere convertito in modo implicito in [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).  Non esiste tuttavia alcuna conversione implicita da questi tipi al tipo `char`.  
  
 Il tipo <xref:System.Char?displayProperty=fullName> fornisce diversi metodi statici da utilizzare con i valori `char`.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Char>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Stringhe](../../../csharp/programming-guide/strings/index.md)