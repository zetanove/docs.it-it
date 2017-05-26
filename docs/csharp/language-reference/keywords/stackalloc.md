---
title: stackalloc (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- stackalloc_CSharpKeyword
- stackalloc
dev_langs:
- CSharp
helpviewer_keywords:
- stackalloc keyword [C#]
ms.assetid: adc04c28-3ed2-4326-807a-7545df92b852
caps.latest.revision: 27
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
ms.openlocfilehash: 337a06daaf36a1eb265f66cd191fc48b80f0bae1
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="stackalloc-c-reference"></a>stackalloc (Riferimenti per C#)
La parola chiave `stackalloc` viene usata in un contesto di codice unsafe per allocare un blocco di memoria nello stack.  
  
```  
int* block = stackalloc int[100];  
```  
  
## <a name="remarks"></a>Note  
 La parola chiave è valida solo per gli inizializzatori di variabili locali. Il codice seguente causa errori di compilazione.  
  
```  
int* block;  
// The following assignment statement causes compiler errors. You  
// can use stackalloc only when declaring and initializing a local   
// variable.  
block = stackalloc int[100];  
```  
  
 Poiché vengono usati tipi puntatore, `stackalloc` richiede un contesto [unsafe](../../../csharp/language-reference/keywords/unsafe.md). Per altre informazioni, vedere [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md).  
  
 La parola chiave `stackalloc` è come [_alloca](https://docs.microsoft.com/cpp/c-runtime-library/reference/alloca) nella libreria di runtime del linguaggio C.  
  
 Nell'esempio seguente vengono calcolati e visualizzati i primi 20 numeri della sequenza di Fibonacci. Ogni numero corrisponde alla somma dei due numeri precedenti. Nel codice, un blocco di memoria di dimensioni sufficienti a contenere 20 elementi di tipo `int` viene allocato nello stack, non nell'heap. L'indirizzo del blocco è archiviato nel puntatore `fib`. Questa memoria non viene sottoposta alla procedura di Garbage Collection e non deve quindi essere bloccata con [fixed](../../../csharp/language-reference/keywords/fixed-statement.md). La durata del blocco di memoria è limitata alla durata del metodo che lo definisce. Non è possibile liberare la memoria prima della restituzione del metodo.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsOperator#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/stackalloc_1.cs)]  
  
## <a name="security"></a>Sicurezza  
 Il codice di tipo unsafe è meno sicuro delle alternative di tipo safe. Tuttavia, l'uso di `stackalloc` attiva automaticamente le funzionalità di rilevazione del sovraccarico del buffer in Common Language Runtime (CLR). Se viene rilevato un sovraccarico del buffer, il processo viene terminato il più rapidamente possibile per ridurre al minimo la possibilità che venga eseguito codice dannoso.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per gli operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
