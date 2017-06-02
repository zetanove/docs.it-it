---
title: 'Procedura: Convertire una stringa in un numero (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
caps.latest.revision: 34
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
ms.translationtype: Human Translation
ms.sourcegitcommit: be7974018ce3195dc7344192d647fe64fb2ebcc4
ms.openlocfilehash: d406f1731db1e0979be8bba8d10301e57a2281e9
ms.contentlocale: it-it
ms.lasthandoff: 05/14/2017

---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>Procedura: convertire una stringa in un numero (Guida per programmatori C#)
È possibile convertire una [stringa`TryParse` in un numero usando i metodi della classe ](../../../csharp/language-reference/keywords/string.md) o usando il metodo <xref:System.Convert> presente nei diversi tipi numerici (int, long, float e così via).  
  
 Se si dispone di una stringa, è leggermente più efficiente e semplice chiamare un metodo `TryParse` (ad esempio, `int.TryParse("11")`).  L'uso di un metodo `Convert` è più utile per gli oggetti generali che implementano <xref:System.IConvertible>.  
  
 È possibile usare i metodi `Parse` o `TryParse` sul tipo numerico che si prevede sia contenuto nella stringa, ad esempio il tipo <xref:System.Int32?displayProperty=fullName>.  Il metodo <xref:System.Convert.ToUInt32%2A?displayProperty=fullName> utilizza il metodo <xref:System.Int32.Parse%2A> internamente.  Se il formato della stringa non è valido, il metodo `Parse` genera un'eccezione, mentre il metodo `TryParse` restituisce [false](../../../csharp/language-reference/keywords/false.md).  
  
## <a name="example"></a>Esempio  
 I metodi `Parse` e `TryParse` ignorano lo spazio vuoto all'inizio e alla fine della stringa, ma tutti gli altri devono essere caratteri che costituiscono il tipo numerico appropriato (int, long, ulong, float, decimal e così via).  Gli spazi vuoti all'interno di caratteri che costituiscono il numero generano un errore.  Ad esempio, è possibile usare `decimal.TryParse` per analizzare "10", "10,3", "  10  ", ma non è possibile usare questo metodo per analizzare 10 in "10X", "1 0" (si noti lo spazio), "10 ,3" (si noti lo spazio), "10e1" (in questo caso funziona `float.TryParse`) e così via.  
  
 Negli esempi riportati di seguito vengono illustrate chiamate con esito positivo e negativo ai metodi `Parse` e `TryParse`.  
  
 [!code-cs[csProgGuideTypes#5555](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_1.cs)]  
[!code-cs[csProgGuideTypes#25](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_2.cs)]  
[!code-cs[csProgGuideTypes#26](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_3.cs)]  
[!code-cs[csProgGuideTypes#27](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_4.cs)]  
[!code-cs[csProgGuideTypes#28](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_5.cs)]  
[!code-cs[csProgGuideTypes#100](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_6.cs)]  
  
## <a name="example"></a>Esempio  
 Nella tabella seguente sono elencati alcuni dei metodi della classe <xref:System.Convert> che è possibile usare.  
  
|Tipo numerico|Metodo|  
|------------------|------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 In questo esempio viene chiamato il metodo <xref:System.Convert.ToInt32%28System.String%29?displayProperty=fullName> per convertire un tipo [string](../../../csharp/language-reference/keywords/string.md) di input in un tipo [int](../../../csharp/language-reference/keywords/int.md). Il codice rileva le due eccezioni più comuni che possono essere generate da questo metodo, <xref:System.FormatException> e <xref:System.OverflowException>. Se è possibile incrementare il numero senza provocare l'overflow nella posizione di archiviazione di Integer, il programma aggiunge 1 al risultato e stampa l'output.  
  
 [!code-cs[csProgGuideTypes#5555](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_1.cs)]  
[!code-cs[csProgGuideTypes#24](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/how-to-convert-a-string-to-a-number_7.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi](../../../csharp/programming-guide/types/index.md)   
 [Procedura: Determinare se una stringa rappresenta un valore numerico](../../../csharp/programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)   
 [.NET Framework 4 Formatting Utility](http://code.msdn.microsoft.com/NET-Framework-4-Formatting-9c4dae8d) (Utilità di formattazione in .NET Framework 4)
