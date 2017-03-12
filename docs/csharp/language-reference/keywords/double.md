---
title: "double (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "double"
  - "double_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "double (tipo di dati) [C#]"
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
caps.latest.revision: 26
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 26
---
# double (Riferimenti per C#)
La parola chiave `double` indica un tipo semplice che archivia valori a virgola mobile a 64 bit.  Nella tabella riportata di seguito sono indicati l'intervallo approssimativo e il grado di precisione del tipo `double`.  
  
|Type|Intervallo approssimativo|Precisione|Tipo .NET Framework|  
|----------|-------------------------------|----------------|-------------------------|  
|`double`|Da ±5.0 × 10<sup>−324</sup> a ±1.7 × 10<sup>308</sup>|15\-16 cifre|<xref:System.Double?displayProperty=fullName>|  
  
## Valori letterali  
 Per impostazione predefinita, un valore letterale numero reale a destra dell'operatore di assegnazione viene gestito come tipo `double`.  Se tuttavia si desidera che un numero integer venga gestito come `double`, utilizzare il suffisso d o D, ad esempio:  
  
```  
  
double x = 3D;  
```  
  
## Conversioni  
 È possibile combinare tipi integrali numerici e tipi a virgola mobile in una stessa espressione.  In questo caso i tipi integrali vengono convertiti in tipi a virgola mobile.  La valutazione dell'espressione viene eseguita in base ai criteri descritti di seguito.  
  
-   Se uno dei tipi a virgola mobile è `double`, l'espressione darà come risultato un valore `double` o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane.  
  
-   Se l'espressione non contiene alcun tipo `double`, darà come risultato un valore [float](../../../csharp/language-reference/keywords/float.md) o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane.  
  
 Un'espressione a virgola mobile può contenere i seguenti insiemi di valori:  
  
-   Zero positivo e negativo  
  
-   Infinito positivo e negativo  
  
-   Valore NaN \(non numerico\)  
  
-   L'insieme finito di valori diversi da zero  
  
 Per ulteriori informazioni su questi valori, vedere lo standard IEEE per l'aritmetica a virgola mobile binaria, disponibile sul sito Web [IEEE](http://go.microsoft.com/fwlink/?LinkId=26269).  
  
## Esempio  
 Nell'esempio riportato di seguito le parole chiave [int](../../../csharp/language-reference/keywords/int.md), [short](../../../csharp/language-reference/keywords/short.md), [float](../../../csharp/language-reference/keywords/float.md) e `double` vengono sommate per dare il risultato `double`.  
  
 [!code-cs[csrefKeywordsTypes#9](../../../csharp/language-reference/keywords/codesnippet/csharp/double_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella dei tipi a virgola mobile](../../../csharp/language-reference/keywords/floating-point-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)