---
title: double (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- double
- double_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- double data type [C#]
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
caps.latest.revision: 26
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
ms.openlocfilehash: ccdd29c78a3cdc9d32fa08b1be94eecd717418fc
ms.lasthandoff: 03/13/2017

---
# <a name="double-c-reference"></a>double (Riferimenti per C#)
La parola chiave `double` indica un tipo semplice che archivia valori a virgola mobile a 64 bit. Nella tabella riportata di seguito sono indicati l'intervallo approssimativo e il grado di precisione del tipo `double`.  
  
|Tipo|Intervallo approssimativo|Precisione|Tipo .NET Framework|  
|----------|-----------------------|---------------|-------------------------|  
|`double`|Compreso tra ±5,0 × 10<sup>−324</sup> e ±1,7 × 10<sup>308</sup>|15-16 cifre|<xref:System.Double?displayProperty=fullName>|  
  
## <a name="literals"></a>Valori letterali  
 Per impostazione predefinita, un valore letterale numerico reale a destra dell'operatore di assegnazione viene gestito come tipo `double`. Se invece un numero intero deve essere trattato come `double`, usare il suffisso d o D, ad esempio:  
  
```  
  
double x = 3D;  
```  
  
## <a name="conversions"></a>Conversioni  
 In una stessa espressione è possibile combinare tipi integrali numerici e tipi a virgola mobile. In questo caso i tipi integrali vengono convertiti in tipi a virgola mobile. La valutazione dell'espressione viene eseguita in base alle regole seguenti:  
  
-   Se uno dei tipi a virgola mobile è `double`, l'espressione restituirà un valore `double` o [bool](../../../csharp/language-reference/keywords/bool.md) in caso di espressioni relazionali o booleane.  
  
-   Se l'espressione non contiene alcun tipo `double` restituirà un valore [float](../../../csharp/language-reference/keywords/float.md) o [bool](../../../csharp/language-reference/keywords/bool.md) in caso di espressioni relazionali o booleane.  
  
 Un'espressione a virgola mobile può contenere gli insiemi di valori seguenti:  
  
-   Zero positivo e negativo.  
  
-   Infinito positivo e negativo.  
  
-   Non un numero (NaN).  
  
-   Insieme finito di valori diversi da zero.  
  
 Per altre informazioni su questi valori, vedere lo standard IEEE per l'aritmetica a virgola mobile binaria, disponibile nel sito Web [IEEE](http://go.microsoft.com/fwlink/?LinkId=26269).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, i valori [int](../../../csharp/language-reference/keywords/int.md), [short](../../../csharp/language-reference/keywords/short.md), [float](../../../csharp/language-reference/keywords/float.md), e `double` vengono sommati per restituire un risultato `double`.  
  
 [!code-cs[csrefKeywordsTypes#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/double_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tabella dei valori predefiniti](../../../csharp/language-reference/keywords/default-values-table.md)   
 [Tabella dei tipi predefiniti](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [Tabella dei tipi a virgola mobile](../../../csharp/language-reference/keywords/floating-point-types-table.md)   
 [Tabella delle conversioni numeriche implicite](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [Tabella delle conversioni numeriche esplicite](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
