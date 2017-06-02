---
title: where (vincolo di tipo generico) (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.assetid: d7aa871b-0714-416a-bab2-96f87ada4310
caps.latest.revision: 10
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
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: e5baa75c55d58a4d975fc42472f90ff4125cbb5c
ms.contentlocale: it-it
ms.lasthandoff: 03/24/2017

---
# <a name="where-generic-type-constraint-c-reference"></a>where (vincolo di tipo generico) (Riferimenti per C#)
In una definizione di tipo generico, la clausola `where` viene usata per specificare i vincoli per i tipi che possono essere usati come argomenti per un parametro di tipo definito in una dichiarazione generica. Ad esempio, è possibile dichiarare una classe generica, `MyGenericClass`, in modo tale che il parametro di tipo `T` implementi l'interfaccia <xref:System.IComparable%601>:  
  
```csharp  
public class MyGenericClass<T> where T:IComparable { }  
```  
  
> [!NOTE]
>  Per altre informazioni sulla clausola where in un'espressione di query, vedere [Clausola where](../../../csharp/language-reference/keywords/where-clause.md).  
  
 Oltre ai vincoli di interfaccia, una clausola `where` può includere un vincolo di classe di base, che stabilisce che un tipo deve usare la classe specificata come classe di base (o essere la classe stessa) per poter essere usato come argomento di tipo per tale tipo generico. Se viene usato tale vincolo, deve apparire prima di tutti gli altri vincoli per quel parametro di tipo.  
  
 [!code-cs[csrefKeywordsContextual#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_1.cs)]  
  
 La clausola `where` può anche includere un vincolo di costruttore. È possibile creare un'istanza di un parametro di tipo usando l'operatore new. Tuttavia, per poter eseguire questa operazione, è necessario che il parametro di tipo sia vincolato dal vincolo di costruttore, `new()`. Il [vincolo new()](../../../csharp/language-reference/keywords/new-constraint.md) consente al compilatore di sapere che ogni argomento di tipo specificato deve usare un costruttore accessibile senza parametri o predefinito. Ad esempio:  
  
 [!code-cs[csrefKeywordsContextual#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_2.cs)]  
  
 Il vincolo `new()` viene visualizzato per ultimo nella clausola `where`.  
  
 Con più parametri di tipo, usare una clausola `where` per ogni parametro di tipo, ad esempio:  
  
 [!code-cs[csrefKeywordsContextual#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/where-generic-type-constraint_3.cs)]  
  
 È anche possibile associare vincoli ai parametri di tipo di metodi generici, come indicato di seguito:  
  
```csharp  
public bool MyMethod<T>(T t) where T : IMyInterface { }  
```  
  
 Si noti che la sintassi usata per descrivere i vincoli dei parametri di tipo per i delegati è uguale a quella dei metodi:  
  
```csharp  
delegate T MyDelegate<T>() where T : new()  
```  
  
 Per informazioni sui delegati generici, vedere [Delegati generici](../../../csharp/programming-guide/generics/generic-delegates.md).  
  
 Per informazioni dettagliate sulla sintassi e sull'uso dei vincoli, vedere [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md).  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Introduzione ai generics](../../../csharp/programming-guide/generics/introduction-to-generics.md)   
 [Vincolo new](../../../csharp/language-reference/keywords/new-constraint.md)   
 [Vincoli sui parametri di tipo](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)
