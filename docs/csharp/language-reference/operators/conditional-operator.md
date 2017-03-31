---
title: 'Operatore ?: (Riferimenti per C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ?:_CSharpKeyword
- ?_CSharpKeyword
- :_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- '?: operator [C#]'
- conditional operator (?:) [C#]
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
caps.latest.revision: 23
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3e60516d1f443528c357eb12612b6149f34c1f7e
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-c-reference"></a>Operatore ?: (Riferimenti per C#)
L'operatore condizionale (`?:`) restituisce uno tra due valori in base al valore di un'espressione booleana. Di seguito è riportata la sintassi per l'operatore condizionale.  
  
```  
condition ? first_expression : second_expression;  
```  
  
## <a name="remarks"></a>Note  
 L' oggetto `condition` deve restituire `true` o `false`. Se `condition` è `true`, `first_expression` viene valutato e diventa il risultato. Se `condition` è `false`, `second_expression` viene valutato e diventa il risultato. Viene valutata soltanto una delle due espressioni.  
  
 Il tipo di `first_expression` e di `second_expression` deve essere lo stesso o deve esistere una conversione implicita da un tipo a un altro.  
  
 I calcoli che richiedono una costruzione `if-else` possono essere espressi più concisamente mediante l'operatore condizionale. Ad esempio, il codice seguente viene utilizzato prima un'istruzione `if`, quindi un operatore condizionale per classificare un integer come positivo o negativo.  
  
```  
  
int input = Convert.ToInt32(Console.ReadLine());  
string classify;  
  
// if-else construction.  
if (input > 0)  
    classify = "positive";  
else  
    classify = "negative";  
  
// ?: conditional operator.  
classify = (input > 0) ? "positive" : "negative";  
  
```  
  
 L'operatore condizionale si associa all'operando a destra. L'espressione `a ? b : c ? d : e` viene valutata come `a ? b : (c ? d : e)`, non come `(a ? b : c) ? d : e`.  
  
 Non è possibile eseguire l'overload dell'operatore condizionale.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csRefOperators#41](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-operator_1.cs)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Operatori C#](../../../csharp/language-reference/operators/index.md)   
 [if-else](../../../csharp/language-reference/keywords/if-else.md)   
 [Operatori ?. e ?](../../../csharp/language-reference/operators/null-conditional-operators.md)   
 [?? (operatore)](../../../csharp/language-reference/operators/null-conditional-operator.md)
