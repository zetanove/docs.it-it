---
title: throw (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-03-02
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- throw
- throw_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- throw statement [C#]
- throw expression [C#]
- throw keyword [C#]
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 095a86f5ab2ce50f5931643161a44b5759583e4e
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="throw-c-reference"></a>throw (Riferimenti per C#)
Segnala l'occorrenza di un'eccezione durante l'esecuzione del programma.  
  
## <a name="remarks"></a>Note

La sintassi di `throw` è:

```csharp
throw [e]
```
dove `e` è un'istanza di una classe derivata da <xref:System.Exception?displayProperty=fullName>. Nell'esempio seguente l'istruzione `throw` viene usata per generare una @System.IndexOutOfRangeException, se l'argomento passato a un metodo denominato `GetNumber` non corrisponde a un indice valido di una matrice interna.

[!code-cs[csrefKeyword#1](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#1)]  

I caller al metodo usano quindi un blocco `try-catch` o `try-catch-finally` per gestire l'eccezione generata. L'esempio seguente gestisce l'eccezione generata dal metodo `GetNumber`.

[!code-cs[csrefKeyword#2](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#2)]  

## <a name="re-throwing-an-exception"></a>Nuova generazione di un'eccezione

È possibile anche usare `throw` in un blocco `catch` per generare nuovamente un'eccezione gestita in un blocco `catch`.  In questo caso, `throw` non accetta un operando di eccezione. È particolarmente utile quando un metodo passa un argomento da un caller a un altro metodo di raccolta e il metodo di raccolta genera un'eccezione che deve essere passata al caller. Nell'esempio seguente viene generata nuovamente una @System.NullReferenceException, che viene generata quando si tenta di recuperare il primo carattere di una stringa non inizializzata. 

[!code-cs[csrefKeyword#3](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-3.cs#3)]  

> [!IMPORTANT]
> È possibile anche usare la sintassi `throw e` in un blocco `catch` per creare un'istanza di una nuova eccezione da passare al caller. In questo caso non viene mantenuta la traccia dello stack dell'eccezione originale, che è disponibile dalla proprietà @System.Exception.Stacktrace.
 
## <a name="the-throw-expression"></a>Espressione `throw`

A partire da C# 7 è possibile usare `throw` come espressione e come istruzione. Ciò consente di generare un'eccezione in contesti non supportati in precedenza. Sono inclusi:

- [L'operatore condizionale](../operators/conditional-operator.md). Nell'esempio seguente viene usata un'espressione `throw` per generare una @System.ArgumentException se a un metodo viene passato una matrice di stringa vuota. Prima di C# 7, la logica avrebbe dovuto usare un'istruzione `if` / `else`.

   [!code-cs[csrefKeyword#4](../../../../samples/snippets/csharp/language-reference/keywords/throw/conditional.cs#1)]  
  
- [L'operatore null-coalescing](../operators/null-conditional-operator.md). Nell'esempio seguente viene usata un'espressione `throw` con un operatore null-coalescing per generare un'eccezione, se la stringa assegnata a una proprietà `Name` è `null`.
 
   [!code-cs[csrefKeyword#5](../../../../samples/snippets/csharp/language-reference/keywords/throw/coalescing.cs#1)]  
 
- [lambda](../../lambda-expressions.md) o metodo con corpo di espressione. L'esempio seguente illustra un metodo con corpo di espressione che genera una @System.InvalidCastException perché non è supportata una conversione in un valore @System.DateTime.
 
   [!code-cs[csrefKeyword#6](../../../../samples/snippets/csharp/language-reference/keywords/throw/exp-bodied.cs#1)]  
 
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [Istruzioni try, catch e throw in C++](../../../csharp/language-reference/keywords/try-catch.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [Procedura: Come generare in modo esplicito le eccezioni](https://msdn.microsoft.com/library/xhcbs8fz)
