---
title: Tabella di formattazione dei risultati numerici (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- formatting [C#]
- numeric formatting [C#]
- String.Format method
- Console.Write method
ms.assetid: 120ba537-4448-4c62-8676-7a8fdd98f496
caps.latest.revision: 14
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: a3e5d2eef3f0a76fc8e3faa52feca827070a9cab
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="formatting-numeric-results-table-c-reference"></a>Tabella di formattazione dei risultati numerici (Riferimenti per C#)
È possibile formattare i risultati numerici usando il metodo <xref:System.String.Format%2A?displayProperty=fullName> o con il metodo <xref:System.Console.Write%2A?displayProperty=fullName> o <xref:System.Console.WriteLine%2A?displayProperty=fullName> che chiama `String.Format`. Il formato è specificato dalle stringhe di formato. La tabella seguente contiene le stringhe di formato standard supportate. La stringa di formato ha questo aspetto: `Axx`, dove `A` è l'identificatore del formato e `xx` è l'identificatore della precisione. L'identificatore del formato controlla il tipo di formattazione applicato al valore numerico e l'identificatore della precisione controlla il numero di cifre significative o di decimali dell'output formattato. Il valore dell'identificatore della precisione è compreso tra 0 e 99.  
  
 Per altre informazioni sulle stringhe di formato numerico standard, vedere [Formattazione di tipi](../../../standard/base-types/formatting-types.md). Per ulteriori informazioni sul metodo `String.Format`, vedere <xref:System.String.Format%2A?displayProperty=fullName>.  
  
|Identificatore di formato|Descrizione|Esempi|Output|  
|----------------------|-----------------|--------------|------------|  
|C o c|Valuta|Console.Write("{0:C}", 2.5);<br /><br /> Console.Write("{0:C}", -2.5);|$2.50<br /><br /> ($2.50)|  
|D o d|Decimal|Console.Write("{0:D5}", 25);|00025|  
|E o e|Scientifico|Console.Write("{0:E}", 250000);|2.500000E+005|  
|F o f|A virgola fissa|Console.Write("{0:F2}", 25);<br /><br /> Console.Write("{0:F0}", 25);|25.00<br /><br /> 25|  
|G o g|Generale|Console.Write("{0:G}", 2.5);|2.5|  
|N o n|Number|Console.Write("{0:N}", 2500000);|2,500,000.00|  
|X o x|Esadecimale|Console.Write("{0:X}", 250);<br /><br /> Console.Write("{0:X}", 0xffff);|FA<br /><br /> FFFF|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Stringhe di formato numerico standard](../../../standard/base-types/standard-numeric-format-strings.md)   
 [Tabelle di riferimento per i tipi](../../../csharp/language-reference/keywords/reference-tables-for-types.md)   
 [string](../../../csharp/language-reference/keywords/string.md)
