---
title: try...finally (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- finally
- finally_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- finally keyword [C#]
- try-finally statement [C#]
ms.assetid: c27623fb-7261-4464-862c-7a369d3c8f0a
caps.latest.revision: 25
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
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3f7618aa6d4ae3535b2b6cb562349650b3eba1ed
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="try-finally-c-reference"></a>try...finally (Riferimenti per C#)
Usando un blocco `finally`, è possibile eliminare le risorse allocate in un blocco [try](../../../csharp/language-reference/keywords/try-catch.md) ed è possibile eseguire codice anche se viene generata un'eccezione di blocco `try`. In genere, le istruzioni di un blocco `finally` vengono eseguite quando il controllo lascia un'istruzione `try`. Il trasferimento del controllo può verificarsi come risultato dell'esecuzione normale, dell'esecuzione di un'istruzione `break`, `continue`, `goto` o `return` o della propagazione di un'eccezione dell'istruzione `try`.  
  
 All'interno di un'eccezione gestita, l'esecuzione del blocco `finally` associato è garantita. Tuttavia, se l'eccezione non è gestita, l'esecuzione del blocco `finally` dipende da come viene attivata l'operazione di rimozione dell'eccezione. Ciò, a sua volta, dipende da come viene configurato il computer. Per altre informazioni, vedere [Unhandled Exception Processing in the CLR](http://go.microsoft.com/fwlink/?LinkId=128371) (Elaborazione di eccezioni non gestite nel CLR).  
  
 In genere, quando un'eccezione non gestita termina un'applicazione non è importante sapere se il blocco `finally` è in esecuzione. Tuttavia, se si dispone di istruzioni in un blocco `finally` che deve essere eseguito anche in questo caso, una soluzione consiste nell'aggiungere un blocco `catch` all'istruzione `try`-`finally`. In alternativa, è possibile intercettare l'eccezione che potrebbe essere generata nel blocco `try` di un'istruzione `try`-`finally` in alto nello stack di chiamate. Vale a dire, è possibile intercettare l'eccezione nel metodo che chiama il metodo che contiene l'istruzione `try`-`finally`, nel metodo che chiama questo metodo o in qualsiasi metodo nello stack di chiamate. Se non viene rilevata l'eccezione, l'esecuzione del blocco `finally` varia a seconda che il sistema operativo scelga di generare un'operazione di rimozione dell'eccezione o meno.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente un'istruzione di conversione non valida causa un'eccezione `System.InvalidCastException`. L'eccezione viene non è gestita.  
  
 [!code-cs[csrefKeywordsExceptions#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-finally_1.cs)]  
  
 Nell'esempio seguente viene intercettata un'eccezione del metodo `TryCast` in un metodo nella parte più in alto dello stack di chiamate.  
  
 [!code-cs[csrefKeywordsExceptions#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-finally_2.cs)]  
  
 Per altre informazioni su `finally`, vedere [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md).  
  
 C# contiene anche l'[istruzione using](../../../csharp/language-reference/keywords/using-statement.md), che fornisce funzionalità simili agli oggetti <xref:System.IDisposable> con una sintassi comoda.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni try, throw e catch (C++)](https://docs.microsoft.com/cpp/cpp/try-throw-and-catch-statements-cpp)   
 [Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [Procedura: Come generare in modo esplicito le eccezioni](https://msdn.microsoft.com/library/xhcbs8fz)
