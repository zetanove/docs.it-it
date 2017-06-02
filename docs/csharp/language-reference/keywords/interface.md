---
title: interface (Riferimenti per C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- interface_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- interface keyword [C#]
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
caps.latest.revision: 29
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
ms.openlocfilehash: 84759153ebfc77ba6d39e1b3c47a00a083f267c0
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="interface-c-reference"></a>interface (Riferimenti per C#)
Un'interfaccia contiene solo le firme di [metodi](../../../csharp/programming-guide/classes-and-structs/methods.md), [proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md), [eventi](../../../csharp/programming-guide/events/index.md) o [indicizzatori](../../../csharp/programming-guide/indexers/index.md). Una classe o uno struct che implementa l'interfaccia deve implementarne i membri specificati nella definizione dell'interfaccia stessa. Nell'esempio seguente, la classe `ImplementationClass` deve implementare un metodo denominato `SampleMethod` che è privo di parametri e restituisce `void`.  
  
 Per altre informazioni e altri esempi, vedere [Interfacce](../../../csharp/programming-guide/interfaces/index.md).  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsTypes#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_1.cs)]  
  
 Un'interfaccia può essere membro di uno spazio dei nomi o di una classe e contenere firme dei seguenti membri:  
  
-   [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md)  
  
-   [Proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)  
  
-   [Indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)  
  
-   [Eventi](../../../csharp/language-reference/keywords/event.md)  
  
 Un'interfaccia può ereditare da una o più interfacce di base.  
  
 Quando un elenco di tipi di base contiene interfacce e una classe di base, la classe di base deve precedere le interfacce.  
  
 Una classe che implementa un'interfaccia può implementare in modo esplicito i membri di tale interfaccia. Non è possibile accedere a un membro implementato in modo esplicito tramite un'istanza di classe, ma solo tramite un'istanza dell'interfaccia.  
  
 Per altri dettagli e altri esempi di codice sull'implementazione esplicita delle interfacce, vedere [Implementazione esplicita dell'interfaccia](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata un'implementazione dell'interfaccia. In questo esempio l'interfaccia contiene la dichiarazione di proprietà e la classe contiene l'implementazione. Qualsiasi istanza di una classe che implementa `IPoint` presenta proprietà `x` e `y` di tipo Integer.  
  
 [!code-cs[csrefKeywordsTypes#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/interface_2.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Tipi di riferimento](../../../csharp/language-reference/keywords/reference-types.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)   
 [Uso delle proprietà](../../../csharp/programming-guide/classes-and-structs/using-properties.md)   
 [Uso degli indicizzatori](../../../csharp/programming-guide/indexers/using-indexers.md)   
 [class](../../../csharp/language-reference/keywords/class.md)   
 [struct](../../../csharp/language-reference/keywords/struct.md)   
 [Interfacce](../../../csharp/programming-guide/interfaces/index.md)
