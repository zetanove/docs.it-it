---
title: readonly (Riferimenti per C#) | Documentazione Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- readonly_CSharpKeyword
- readonly
dev_langs:
- CSharp
helpviewer_keywords:
- readonly keyword [C#]
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
caps.latest.revision: 16
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
ms.openlocfilehash: e915ac4621d2514e1efcaa8bdb4df698e6a66a72
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="readonly-c-reference"></a>readonly (Riferimenti per C#)
La parola chiave `readonly` è un modificatore utilizzabile nei campi. Quando una dichiarazione di campo include un modificatore `readonly`, le assegnazioni ai campi introdotte dalla dichiarazione possono verificarsi solo come parte della dichiarazione o in un costruttore della stessa classe.  
  
## <a name="example"></a>Esempio  
 In questo esempio, il valore del campo `year` non può essere modificato nel metodo `ChangeYear`, anche se gli viene assegnato un valore nel costruttore della classe:  
  
 [!code-cs[csrefKeywordsModifiers#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_1.cs)]  
  
 È possibile assegnare un valore a un campo `readonly` solo nei contesti seguenti:  
  
-   Quando la variabile viene inizializzata nella dichiarazione, ad esempio:  
  
    ```  
    public readonly int y = 5;  
    ```  
  
-   Per un campo di istanza, nei costruttori di istanza della classe che contiene la dichiarazione del campo, o per un campo statico, nel costruttore statico della classe che contiene la dichiarazione del campo. Questi sono anche gli unici contesti in cui è possibile passare un campo `readonly` come parametro [out](../../../csharp/language-reference/keywords/out.md) o [ref](../../../csharp/language-reference/keywords/ref.md).  
  
> [!NOTE]
>  La parola chiave `readonly` è diversa dalla parola chiave [const](../../../csharp/language-reference/keywords/const.md). Un campo `const` può essere inizializzato solo nella dichiarazione del campo. Un campo `readonly` può essere inizializzato nella dichiarazione o in un costruttore. I campi `readonly` possono quindi presentare valori diversi a seconda del costruttore usato. Inoltre, mentre un campo `const` rappresenta una costante in fase di compilazione, il campo `readonly` può essere usato per le costanti in fase di esecuzione, come nell'esempio seguente:  
  
```  
public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;  
```  
  
## <a name="example"></a>Esempio  
 [!code-cs[csrefKeywordsModifiers#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/readonly_2.cs)]  
  
 Nell'esempio precedente, se si usa un'istruzione simile alla seguente:  
  
 `p2.y = 66;        // Error`  
  
 si otterrà il messaggio di errore del compilatore:  
  
 `The left-hand side of an assignment must be an l-value`  
  
 ovvero lo stesso errore che si ottiene quando si tenta di assegnare un valore a una costante.  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)   
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [Campi](../../../csharp/programming-guide/classes-and-structs/fields.md)
