---
title: Operatore -= (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- -=_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- subtraction assignment operator (-=) [C#]
- -= operator (subtraction assignment ) [C#]
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
caps.latest.revision: 19
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
ms.openlocfilehash: d9ffcfe9b42f7ca65801a58338c8e40a37c90316
ms.lasthandoff: 03/13/2017

---
# <a name="--operator-c-reference"></a>Operatore -= (Riferimenti per C#)
Operatore di assegnazione di sottrazione.  
  
## <a name="remarks"></a>Note  
 Un'espressione che usa l'operatore di assegnazione `-=`, ad esempio  
  
```  
x -= y  
```  
  
 equivale a  
  
```  
x = x - y  
```  
  
 con la differenza che `x` viene valutato una sola volta. Il significato dell'[operatore -](../../../csharp/language-reference/operators/subtraction-operator.md) dipende dai tipi di `x` e `y` (sottrazione per gli operandi numerici, rimozione del delegato per gli operandi delegati e così via).  
  
 L'operatore `-=` non può essere sottoposto direttamente a overload. I tipi definiti dall'utente, tuttavia, possono eseguire l'overload dell'[operatore -](../../../csharp/language-reference/operators/subtraction-operator.md) (vedere [operator](../../../csharp/language-reference/keywords/operator.md)).  
  
 L'operatore -= viene anche usato in C# per annullare la sottoscrizione a un evento. Per altre informazioni, vedere [Procedura: sottoscrivere e annullare la sottoscrizione di eventi](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).  
  
## <a name="example"></a>Esempio  
 [!code-cs[csRefOperators#6](codesnippet/CSharp/subtraction-assignment-operator_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Operatori C#](../../../csharp/language-reference/operators/index.md)

