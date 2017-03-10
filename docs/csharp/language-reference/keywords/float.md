---
title: "float (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "float"
  - "float_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "float (parola chiave) [C#]"
  - "numeri a virgola mobile [C#], float (parola chiave)"
ms.assetid: 1e77db7b-dedb-48b7-8dd1-b055e96a9258
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# float (Riferimenti per C#)
La parola chiave `float` indica un tipo semplice che archivia valori a virgola mobile a 32 bit.  Nella tabella riportata di seguito sono indicati l'intervallo approssimativo e il grado di precisione del tipo `float`.  
  
|Type|Intervallo approssimativo|Precisione|Tipo .NET Framework|  
|----------|-------------------------------|----------------|-------------------------|  
|`float`|Da \-3,4 × 10<sup>38</sup>a \+3,4 × 10<sup>38</sup>|7 cifre|<xref:System.Single?displayProperty=fullName>|  
  
## Valori letterali  
 Per impostazione predefinita, un valore letterale numerico reale a destra dell'operatore di assegnazione viene gestito come tipo [double](../../../csharp/language-reference/keywords/double.md).  Per inizializzare una variabile float è quindi necessario utilizzare il suffisso `f` o `F`, come illustrato di seguito.  
  
```  
  
float x = 3.5F;  
```  
  
 Se nella precedente dichiarazione non si utilizza il suffisso, verrà generato un errore di compilazione poiché si sta tentando di archiviare un valore [double](../../../csharp/language-reference/keywords/double.md) in una variabile `float`.  
  
## Conversioni  
 È possibile combinare tipi integrali numerici e tipi a virgola mobile in una stessa espressione.  In questo caso i tipi integrali vengono convertiti in tipi a virgola mobile.  La valutazione dell'espressione viene eseguita in base ai criteri descritti di seguito.  
  
-   Se uno dei tipi a virgola mobile è [double](../../../csharp/language-reference/keywords/double.md), l'espressione darà come risultato un valore [double](../../../csharp/language-reference/keywords/double.md) o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane.  
  
-   Se l'espressione non contiene alcun tipo [double](../../../csharp/language-reference/keywords/double.md), darà come risultato un valore `float` o [bool](../../../csharp/language-reference/keywords/bool.md) nel caso di espressioni relazionali o booleane.  
  
 Un'espressione a virgola mobile può contenere i seguenti insiemi di valori:  
  
-   Zero positivo e negativo  
  
-   Infinito positivo e negativo  
  
-   Valore NaN \(non numerico\)  
  
-   L'insieme finito di valori diversi da zero  
  
 Per ulteriori informazioni su questi valori, vedere lo standard IEEE per l'aritmetica a virgola mobile binaria, disponibile sul sito Web [IEEE](http://go.microsoft.com/fwlink/?LinkId=26269).  
  
## Esempio  
 Nell'esempio riportato di seguito le parole chiave [int](../../../csharp/language-reference/keywords/int.md), [short](../../../csharp/language-reference/keywords/short.md) e `float` sono incluse in un'espressione matematica che dà come risultato un valore `float`.  Ricordare che `float` è un alias per il tipo <xref:System.Single?displayProperty=fullName>. Si noti che [double](../../../csharp/language-reference/keywords/double.md) non è presente nell'istruzione.  
  
 [!code-cs[csrefKeywordsTypes#13](../../../csharp/language-reference/keywords/codesnippet/csharp/float_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 <xref:System.Single>   
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei tipi integrali](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [Tabella dei tipi incorporati](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)