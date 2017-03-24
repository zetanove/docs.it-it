---
title: "Tabella dei tipi incorporati (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "tipi C# incorporati"
  - "tipi [C#], incorporate"
ms.assetid: 54f901f2-bf2f-472c-ae8d-73e8ecfc57fe
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# Tabella dei tipi incorporati (Riferimenti per C#)
Nella tabella riportata di seguito sono indicate le parole chiave per i tipi incorporati di C\#, che rappresentano alias di tipi predefiniti nello spazio dei nomi <xref:System>.  
  
|Tipo C\#|Tipo .NET Framework|  
|--------------|-------------------------|  
|[bool](../../../csharp/language-reference/keywords/bool.md)|`System.Boolean`|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|`System.Byte`|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|`System.SByte`|  
|[char](../../../csharp/language-reference/keywords/char.md)|`System.Char`|  
|[decimal](../../../csharp/language-reference/keywords/decimal.md)|`System.Decimal`|  
|[double](../../../csharp/language-reference/keywords/double.md)|`System.Double`|  
|[float](../../../csharp/language-reference/keywords/float.md)|`System.Single`|  
|[int](../../../csharp/language-reference/keywords/int.md)|`System.Int32`|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|`System.UInt32`|  
|[long](../../../csharp/language-reference/keywords/long.md)|`System.Int64`|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|`System.UInt64`|  
|[object](../../../csharp/language-reference/keywords/object.md)|`System.Object`|  
|[short](../../../csharp/language-reference/keywords/short.md)|`System.Int16`|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|`System.UInt16`|  
|[string](../../../csharp/language-reference/keywords/string.md)|`System.String`|  
  
## Note  
 Tutti i tipi indicati nella tabella, ad eccezione di `object` e `string`, sono definiti come tipi semplici.  
  
 Le parole chiave dei tipi C\# e i corrispondenti alias sono interscambiabili.  È ad esempio possibile dichiarare una variabile intera utilizzando una delle seguenti dichiarazioni:  
  
```  
int x = 123;  
System.Int32 x = 123;  
```  
  
 Per visualizzare il tipo effettivo di qualsiasi tipo di C\#, utilizzare il metodo di sistema `GetType()`.  L'istruzione che segue, ad esempio, restituisce l'alias di sistema che rappresenta il tipo di `myVariable`:  
  
```  
Console.WriteLine(myVariable.GetType());  
```  
  
 È anche possibile utilizzare l'operatore [typeof](../../../csharp/language-reference/keywords/typeof.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi valore](../../../csharp/language-reference/keywords/value-types.md)   
 [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md)   
 [Tabella di formattazione dei risultati numerici](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)   
 [dynamic](../../../csharp/language-reference/keywords/dynamic.md)   
 [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md)