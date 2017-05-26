---
title: if-else (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- if_CSharpKeyword
- else
- else_CSharpKeyword
- if
dev_langs:
- CSharp
helpviewer_keywords:
- else keyword [C#]
- if keyword [C#]
ms.assetid: d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2
caps.latest.revision: 32
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e4016ee35ed487fd2ca48074d2e483778719dff3
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="if-else-c-reference"></a>if-else (Riferimenti per C#)
Un'istruzione `if` identifica quale istruzione eseguire in base al valore di un'espressione `Boolean` . Nell'esempio seguente la variabile `Boolean` `result` viene impostata su `true` e quindi archiviata nell'istruzione `if` . L'output è `The condition is true`.  
  
 [!code-cs[csrefKeywordsSelection#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_1.cs)]  
  
 È possibile eseguire gli esempi di questo argomento posizionandoli nel metodo `Main` di un'app console.  
  
 Un'istruzione `if` in C# può essere usata in due modi, come illustrato nell'esempio seguente.  
  
```csharp  
// if-else statement  
if (condition)  
{  
    then-statement;  
}  
else  
{  
    else-statement;  
}  
// Next statement in the program.  
  
// if statement without an else  
if (condition)  
{  
    then-statement;  
}  
// Next statement in the program.  
```  
  
 In un'istruzione `if-else` se `condition` restituisce true, viene eseguito `then-statement` . Se `condition` è false, viene eseguito `else-statement` . Poiché `condition` non può essere contemporaneamente true e false, `then-statement` e `else-statement` di un'istruzione `if-else` non possono mai essere eseguiti insieme. Dopo l'esecuzione di `then-statement` o `else-statement` il controllo viene trasferito all'istruzione successiva dopo l'istruzione `if` .  
  
 In un'istruzione `if` che non include un'istruzione `else` , se `condition` è true, viene eseguito `then-statement` . Se `condition` è false, il controllo viene trasferito all'istruzione successiva dopo l'istruzione `if` .  
  
 `then-statement` e `else-statement` possono essere entrambi costituiti da una singola istruzione o da più istruzioni racchiuse tra parentesi graffe (`{}`). Per una singola istruzione le parentesi graffe sono facoltative ma consigliate.  
  
 L'istruzione o le istruzioni in `then-statement` e `else-statement` possono essere di qualsiasi tipo, compresa un'altra istruzione `if` annidata all'interno dell'istruzione `if` originale. Nelle istruzioni `if` annidate ogni clausola `else` appartiene all'ultima istruzione `if` che non ha un'istruzione `else`corrispondente. Nell'esempio seguente viene visualizzato `Result1` se `m > 10` e `n > 20` restituiscono entrambi true. Se `m > 10` è true ma `n > 20` è false, viene visualizzato `Result2` .  
  
 [!code-cs[csrefKeywordsSelection#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_2.cs)]  
  
 Se invece si vuole che venga visualizzato `Result2` quando `(m > 10)` è false, è possibile specificare tale associazione usando le parentesi graffe per stabilire l'inizio e la fine dell'istruzione `if` annidata, come illustrato nell'esempio seguente.  
  
 [!code-cs[csrefKeywordsSelection#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_3.cs)]  
  
 `Result2` viene visualizzato se la condizione `(m > 10)` restituisce false.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente si immette un carattere dalla tastiera e il programma usa un'istruzione `if` annidata per determinare se il carattere di input è un carattere alfabetico. Se il carattere di input è un carattere alfabetico, il programma verifica se il carattere di input è maiuscolo o minuscolo. Viene visualizzato un messaggio per ogni situazione.  
  
 [!code-cs[csrefKeywordsSelection#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_4.cs)]  
  
## <a name="example"></a>Esempio  
 È anche possibile annidare un'istruzione `if` all'interno di un blocco else, come illustrato nella parte di codice seguente. Nell'esempio le istruzioni `if` vengono annidate all'interno di due blocchi else e di un blocco then. I commenti specificano che le condizioni sono true o false in ogni blocco.  
  
 [!code-cs[csrefKeywordsSelection#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_5.cs)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente determina se un carattere di input è una lettera minuscola, una lettera maiuscola o un numero. Se tutte e tre le condizioni sono false, il carattere non è un carattere alfanumerico. Nell'esempio viene visualizzato un messaggio per ogni situazione.  
  
 [!code-cs[csrefKeywordsSelection#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/if-else_6.cs)]  
  
 Come per un'istruzione nel blocco else o nel blocco then è possibile usare qualsiasi istruzione valida, allo stesso modo per la condizione è possibile usare qualsiasi espressione booleana valida. È possibile usare operatori logici quali [&&](../../../csharp/language-reference/operators/conditional-and-operator.md), [&](../../../csharp/language-reference/operators/and-operator.md), [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md), [&#124;](../../../csharp/language-reference/operators/or-operator.md) e [!](../../../csharp/language-reference/operators/logical-negation-operator.md) . Il codice seguente illustra alcuni esempi.  
  
```csharp  
// NOT  
bool result = true;  
if (!result)  
{  
    Console.WriteLine("The condition is true (result is false).");  
}  
else  
{  
    Console.WriteLine("The condition is false (result is true).");  
}  
  
// Short-circuit AND  
int m = 9;  
int n = 7;  
int p = 5;  
if (m >= n && m >= p)  
{  
    Console.WriteLine("Nothing is larger than m.");  
}  
  
// AND and NOT  
if (m >= n && !(p > m))  
{  
    Console.WriteLine("Nothing is larger than m.");  
}  
  
// Short-circuit OR  
if (m > n || m > p)  
{  
    Console.WriteLine("m isn't the smallest.");  
}  
  
// NOT and OR  
m = 4;  
if (!(m >= n || m >= p))  
{  
    Console.WriteLine("Now m is the smallest.");  
}  
// Output:  
// The condition is false (result is true).  
// Nothing is larger than m.  
// Nothing is larger than m.  
// m isn't the smallest.  
// Now m is the smallest.  
```  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Operatore ?: ](../../../csharp/language-reference/operators/conditional-operator.md)   
 [Istruzione if-else (C++)](https://docs.microsoft.com/cpp/cpp/if-else-statement-cpp)   
 [switch](../../../csharp/language-reference/keywords/switch.md)

