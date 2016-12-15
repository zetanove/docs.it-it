---
title: "Tabella di formattazione dei risultati numerici (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "formattazione [C#]"
  - "formattazione di valori numerici [C#]"
  - "String.Format (metodo)"
  - "Console.Write (metodo)"
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Tabella di formattazione dei risultati numerici (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

È possibile formattare i risultati numerici utilizzando il metodo <xref:System.String.Format%2A?displayProperty=fullName> oppure tramite il metodo <xref:System.Console.Write%2A?displayProperty=fullName> o <xref:System.Console.WriteLine%2A?displayProperty=fullName>, che chiama `String.Format`.  Il formato viene specificato tramite le stringhe di formato.  Nella tabella che segue sono contenute le stringhe di formato standard supportate.  La stringa di formato accetta il formato seguente: `Axx`, dove `A` è l'identificatore di formato e `xx` è l'identificatore di precisione.  L'identificatore di formato controlla il tipo di formattazione applicato al valore numerico, mentre l'identificatore di precisione controlla il numero di cifre significative o decimali dell'output formattato.  Il valore dell'identificatore di precisione varia da 0 a 99.  
  
 Per ulteriori informazioni sulle stringhe di formattazione standard e personalizzate, vedere [Formattazione di tipi](../Topic/Formatting%20Types%20in%20the%20.NET%20Framework.md).  Per ulteriori informazioni sul metodo `String.Format`, vedere <xref:System.String.Format%2A?displayProperty=fullName>.  
  
|Identificatore di formato|Descrizione|Esempi|Output|  
|-------------------------------|-----------------|------------|------------|  
|C o c|Valuta|Console.Write\("{0:C}", 2.5\);<br /><br /> Console.Write\("{0:C}", \-2,5\);|$2.50<br /><br /> \($2.50\)|  
|D o d|Decimal|Console.Write\("{0:D5}", 25\);|00025|  
|E o e|Scientifico|Console.Write\("{0:E}", 250000\);|2.500000E\+005|  
|F o f|A virgola fissa|Console.Write\("{0:F2}", 25\);<br /><br /> Console.Write\("{0:F0}", 25\);|25.00<br /><br /> 25|  
|G o g|Generale|Console.Write\("{0:G}", 2.5\);|2.5|  
|N o n|Numero|Console.Write\("{0:N}", 2500000\);|2,500,000.00|  
|X o x|Esadecimale|Console.Write\("{0:X}", 250\);<br /><br /> Console.Write\("{0:X}", 0xffff\);|FA<br /><br /> FFFF|  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Stringhe di formato numerico standard](../Topic/Standard%20Numeric%20Format%20Strings.md)   
 [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [string](../../../csharp/language-reference/keywords/string.md)