---
title: delegate (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- delegate_CSharpKeyword
- delegate
- CS0123
dev_langs:
- CSharp
helpviewer_keywords:
- delegate keyword [C#]
- function pointers [C#]
ms.assetid: 0bb8cb6d-2f87-47c7-9d1f-d65c1cd01e9f
caps.latest.revision: 24
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
ms.openlocfilehash: cf100a5ad3adf001d5435ef6f67e2aa670456649
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="delegate-c-reference"></a>delegate (Riferimenti per C#)
La dichiarazione di un tipo delegato è simile alla firma di un metodo. Ha un valore restituito e una serie di parametri di qualsiasi tipo:  
  
```  
public delegate void TestDelegate(string message);  
public delegate int TestDelegate(MyType m, long num);  
```  
  
 `delegate` è un tipo riferimento che può essere usato per incapsulare un metodo denominato o anonimo. I delegati sono simili ai puntatori a funzioni in C++, ma sono indipendenti dai tipi e protetti. Per le applicazioni dei delegati, vedere  [Delegati](../../../csharp/programming-guide/delegates/index.md) e [Delegati generici](../../../csharp/programming-guide/generics/generic-delegates.md).  
  
## <a name="remarks"></a>Note  
 I delegati sono la base degli [eventi](../../../csharp/programming-guide/events/index.md).  
  
 È possibile creare un'istanza di un delegato associandolo a un metodo denominato o anonimo. Per altre informazioni, vedere [Metodi denominati](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md) e [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  
  
 È necessario creare un'istanza del delegato con un metodo o un'espressione lambda con tipo restituito compatibile e parametri di input. Per altre informazioni sul grado di varianza consentito nella firma del metodo, vedere [Varianza nei delegati](http://msdn.microsoft.com/library/e3b98197-6c5b-4e55-9c6e-9739b60645ca). Per l'uso con i metodi anonimi, è necessario dichiarare insieme il delegato e il codice da associare ad esso. In questa sezione sono descritti entrambi i metodi per la creazione di istanze di delegati.  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsTypes#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/delegate_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Eventi](../../../csharp/programming-guide/events/index.md)   
 [Delegati con metodi denominati e anonimi](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)   
 [Metodi anonimi](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)
