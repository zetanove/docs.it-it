---
title: "decimal (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "decimal_CSharpKeyword"
  - "decimal"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "decimal (parola chiave) [C#]"
ms.assetid: b6522132-b5ee-4be3-ad13-3adfdb7de7a1
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 32
---
# decimal (Riferimenti per C#)
La parola chiave `decimal` indica un tipo di dati a 128 bit.  Rispetto ai tipi a virgola mobile, il tipo `decimal` è caratterizzato da una maggiore precisione e da un intervallo ridotto che lo rendono appropriato per calcoli finanziari e monetari.  Nella tabella riportata di seguito vengono indicati l'intervallo approssimativo e il grado di precisione del tipo `decimal`.  
  
|Tipo|Intervallo approssimativo|Precisione|Tipo .NET Framework|  
|----------|-------------------------------|----------------|-------------------------|  
|`decimal`|\(Da \-7,9 x 10<sup>28</sup> a 7,9 x 10<sup>28</sup>\) \/ \(da 10<sup>0 a 28</sup>\)|28\-29 cifre significative|<xref:System.Decimal?displayProperty=fullName>|  
  
## Valori letterali  
 Se si desidera che un valore letterale numerico reale venga gestito come `decimal`, utilizzare il suffisso m o M, ad esempio:  
  
```  
  
decimal myMoney = 300.5m;  
```  
  
 Senza il suffisso m, il numero viene infatti gestito come valore [double](../../../csharp/language-reference/keywords/double.md), provocando un errore di compilazione.  
  
## Conversioni  
 I tipi integrali vengono convertiti in modo implicito in `decimal` e il risultato restituisce `decimal`.  È pertanto possibile inizializzare una variabile decimale mediante un valore letterale Integer, senza il suffisso, ad esempio:  
  
```  
  
decimal myMoney = 300;  
```  
  
 Non esiste alcuna conversione implicita tra i tipi a virgola mobile e il tipo `decimal`. È pertanto necessario utilizzare un cast per operare una conversione tra questi due tipi.  Di seguito è riportato un esempio.  
  
```  
  
        decimal myMoney = 99.9m;  
double x = (double)myMoney;  
myMoney = (decimal)x;  
```  
  
 È inoltre possibile combinare tipi `decimal` e tipi integrali numerici nella stessa espressione.  Tuttavia, la combinazione di tipi `decimal` e tipi a virgola mobile senza un cast genera un errore di compilazione.  
  
 Per ulteriori informazioni sulle conversioni numeriche implicite, vedere [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Per ulteriori informazioni sulle conversioni numeriche esplicite, vedere [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
## Formattazione dell'output di tipo decimal  
 È possibile applicare il formato desiderato ai risultati utilizzando il metodo `String.Format` o mediante il metodo <xref:System.Console.Write%2A?displayProperty=fullName> che chiama `String.Format()`.  Il formato valuta viene specificato tramite la stringa di formato valuta standard "C" o "c", come illustrato nel secondo esempio riportato più avanti.  Per ulteriori informazioni sul metodo `String.Format`, vedere <xref:System.String.Format%2A?displayProperty=fullName>.  
  
## Esempio  
 L'esempio seguente genera un errore del compilatore tentando di aggiungere [double](../../../csharp/language-reference/keywords/double.md) e variabili `decimal`.  
  
```c#  
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
  
 Nell'esempio riportato di seguito vengono combinati nella stessa espressione un tipo `decimal` e un tipo [int](../../../csharp/language-reference/keywords/int.md).  Il risultato restituisce il tipo `decimal`.  
  
 [!code-cs[csrefKeywordsTypes#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_1.cs)]  
  
## Esempio  
 In questo esempio l'output viene formattato mediante la stringa del formato valuta \(in dollari\).  Si noti che `x` viene arrotondato perché le cifre decimali sono superiori a $ 0,99.  La variabile `y`, che rappresenta le cifre a precisione massima, viene invece visualizzata nel formato esatto.  
  
 [!code-cs[csrefKeywordsTypes#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/decimal_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Decimal>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)   
 [Stringhe di formato numerico standard](../Topic/Standard%20Numeric%20Format%20Strings.md)