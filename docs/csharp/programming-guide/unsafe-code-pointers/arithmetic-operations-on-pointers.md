---
title: Operazioni aritmetiche sui puntatori (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- pointers [C#], arithmetic operations
ms.assetid: d4f0b623-827e-45ce-8649-cfcebc8692aa
caps.latest.revision: 18
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
ms.openlocfilehash: fc675600526dcaa6afd488fdee57acdc577cf71f
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="arithmetic-operations-on-pointers-c-programming-guide"></a>Operazioni aritmetiche sui puntatori (Guida per programmatori C#)
Questo argomento illustra l'uso degli operatori aritmetici `+` e **-** per modificare i puntatori.  
  
> [!NOTE]
>  È possibile eseguire qualsiasi operazione aritmetica sui puntatori void.  
  
## <a name="adding-and-subtracting-numeric-values-to-or-from-pointers"></a>Aggiunta e sottrazione di valori numerici dai puntatori  
 È possibile aggiungere un valore `n` di tipo [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md) a un puntatore `p` di qualsiasi tipo, ad eccezione di `void*`. `p+n` è il puntatore risultante dall'aggiunta di `n * sizeof(p) to the address of p`. Analogamente, `p-n` è il puntatore risultante dalla sottrazione di `n * sizeof(p)` dall'indirizzo di `p`.  
  
## <a name="subtracting-pointers"></a>Sottrazione di puntatori  
 È anche possibile sottrarre puntatori dello stesso tipo. Il risultato è sempre il tipo `long`. Ad esempio, se `p1` e `p2` sono puntatori di tipo `pointer-type*`, l'espressione `p1-p2` è simile alla seguente:  
  
 `((long)p1 - (long)p2)/sizeof(pointer_type)`  
  
 Non viene generata nessuna eccezione quando l'operazione aritmetica supera il dominio del puntatore e il risultato dipende dall'implementazione.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csProgGuidePointers#14](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_1.cs)]  
  
 [!code-cs[csProgGuidePointers#15](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Codice di tipo unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Operatori di C#](../../../csharp/language-reference/operators/index.md)   
 [Modifica dei puntatori](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)   
 [Tipi di puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [unsafe](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
