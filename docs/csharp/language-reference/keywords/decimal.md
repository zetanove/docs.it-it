---
title: decimal (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- decimal_CSharpKeyword
- decimal
dev_langs:
- CSharp
helpviewer_keywords:
- decimal keyword [C#]
ms.assetid: b6522132-b5ee-4be3-ad13-3adfdb7de7a1
caps.latest.revision: 32
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f104657c66e067ffe657f8387fef2178e3b2e62b
ms.lasthandoff: 03/13/2017

---
# <a name="decimal-c-reference"></a>decimal (Riferimenti per C#)
La parola chiave `decimal` indica un tipo di dati a 128 bit. Rispetto ai tipi a virgola mobile, il tipo `decimal` è caratterizzato da una maggiore precisione e da un intervallo ridotto che lo rendono appropriato per calcoli finanziari e monetari. Nella tabella riportata di seguito vengono indicati l'intervallo approssimativo e il grado di precisione del tipo `decimal`.  
  
|Tipo|Intervallo approssimativo|Precisione|Tipo .NET Framework|  
|----------|-----------------------|---------------|-------------------------|  
|`decimal`|(Da -7,9 x 10<sup>28</sup> a 7,9 x 10<sup>28</sup>) / (da 10<sup>0 a 28</sup>)|28-29 cifre significative|<xref:System.Decimal?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali  
 Se si desidera che un valore letterale numerico reale venga gestito come `decimal`, utilizzare il suffisso m o M, ad esempio:  
  
```  
  
decimal myMoney = 300.5m;  
```  
  
 Senza il suffisso m, il numero viene gestito come valore [double](../../../csharp/language-reference/keywords/double.md) e genera un errore del compilatore.  
  
## <a name="conversions"></a>Conversioni  
 I tipi integrali vengono convertiti in modo implicito in `decimal` e il risultato restituisce `decimal`. È pertanto possibile inizializzare una variabile decimale mediante un valore letterale Integer, senza il suffisso, ad esempio:  
  
```  
  
decimal myMoney = 300;  
```  
  
 Non esiste alcuna conversione implicita tra i tipi a virgola mobile e il tipo `decimal`. È pertanto necessario utilizzare un cast per operare una conversione tra questi due tipi. Ad esempio:  
  
```  
  
      decimal myMoney = 99.9m;  
double x = (double)myMoney;  
myMoney = (decimal)x;  
```  
  
 È inoltre possibile combinare tipi `decimal` e tipi integrali numerici nella stessa espressione. Tuttavia, la combinazione di tipi `decimal` e tipi a virgola mobile senza un cast genera un errore di compilazione.  
  
 Per altre informazioni sulle conversioni numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Per altre informazioni sulle conversioni numeriche esplicite, vedere [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
## <a name="formatting-decimal-output"></a>Formattazione dell'output di tipo decimal  
 È possibile formattare i risultati usando il metodo `String.Format` o il metodo <xref:System.Console.Write%2A?displayProperty=fullName>, che chiama `String.Format()`. Il formato valuta viene specificato tramite la stringa di formato valuta standard "C" o "c", come illustrato nel secondo esempio riportato più avanti. Per altre informazioni sul metodo `String.Format`, vedere <xref:System.String.Format%2A?displayProperty=fullName>.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente causa un errore del compilatore tentando di aggiungere le variabili [double](../../../csharp/language-reference/keywords/double.md) e `decimal`.  
  
```csharp  
double dub = 9;  
// The following line causes an error that reads "Operator '+' cannot be applied to   
// operands of type 'double' and 'decimal'"  
Console.WriteLine(dec + dub);   
  
// You can fix the error by using explicit casting of either operand.  
Console.WriteLine(dec + (decimal)dub);  
Console.WriteLine((double)dec + dub);  
  
```  
  
 Viene restituito l'errore seguente:  
  
 `Operator '+' cannot be applied to operands of type 'double' and 'decimal'`  
  
 In questo esempio `decimal` e [int](../../../csharp/language-reference/keywords/int.md) sono combinate nella stessa espressione. Il risultato restituisce il tipo `decimal`.  
  
 [!code-cs[csrefKeywordsTypes#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_1.cs)]  
  
## <a name="example"></a>Esempio  
 In questo esempio l'output viene formattato mediante la stringa del formato valuta (in dollari). Si noti che `x` viene arrotondato perché le cifre decimali sono superiori a $ 0,99. La variabile `y`, che rappresenta le cifre a precisione massima, viene invece visualizzata nel formato esatto.  
  
 [!code-cs[csrefKeywordsTypes#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Decimal>   
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [Stringhe di formato numerico standard](http://msdn.microsoft.com/library/580e57eb-ac47-4ffd-bccd-3a1637c2f467)
