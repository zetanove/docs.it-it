---
title: '#if (Riferimenti per C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#if'
dev_langs:
- CSharp
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
caps.latest.revision: 17
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
ms.sourcegitcommit: a780a11d8dd238187eb82933359bbb151bb3c333
ms.openlocfilehash: 4fc51446d297015d9e492703c9b1868c3b513c53
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="if-c-reference"></a>#if (Riferimenti per C#)
Quando il compilatore C# trova una direttiva `#if` seguita da una direttiva [#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md), compila il codice tra tali direttive solo se il simbolo specificato è definito.  A differenza di C e C++, non è possibile assegnare un valore numerico a un simbolo. L'istruzione #if in C# è booleana e consente di verificare solo se il simbolo è stato o meno definito. Ad esempio,  
  
```  
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
 È possibile usare gli operatori [==](../../../csharp/language-reference/operators/equality-comparison-operator.md) (uguaglianza), [!=](../../../csharp/language-reference/operators/not-equal-operator.md) (disuguaglianza) solo per verificare se una condizione è [true](../../../csharp/language-reference/keywords/true.md) o [false](../../../csharp/language-reference/keywords/false.md). True significa che il simbolo è definito. L'istruzione `#if DEBUG` ha lo stesso significato di `#if (DEBUG == true)`. È possibile usare gli operatori [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) (and), [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) (or) e [!](../../../csharp/language-reference/operators/logical-negation-operator.md) (not) per stabilire se sono stati definiti più simboli. È anche possibile raggruppare simboli e operatori tra parentesi.  
  
## <a name="remarks"></a>Note  
 `#if`, nsieme alle direttive [#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md), [#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md), [#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md), [#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) e [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md), consente di includere o escludere il codice in base all'esistenza di uno o più simboli. Questo può essere utile quando si compila il codice per una build di debug o per una configurazione specifica.  
  
 Una direttiva condizionale che inizia con `#if` deve terminare in modo esplicito con una direttiva `#endif`.  
  
 `#define` consente di definire un simbolo. In questo modo, usando il simbolo come espressione passata alla direttiva `#if`, l'espressione restituirà `true`.  
  
 Un simbolo può anche essere definito tramite l'opzione del compilatore [/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md). Per rimuovere la definizione di un simbolo, è possibile usare [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
 Un simbolo definito tramite `/define` o `#define` non provoca conflitti con una variabile avente lo stesso nome. Il nome di una variabile, infatti, non può essere passato a una direttiva del preprocessore e un simbolo può essere valutato solo da una direttiva del preprocessore.  
  
 L'ambito di un simbolo creato con `#define` è il file in cui è stato definito.  
  
## <a name="example"></a>Esempio  
  
```  
// preprocessor_if.cs  
#define DEBUG#define MYTEST  
using System;  
public class MyClass   
{  
    static void Main()   
    {  
#if (DEBUG && !MYTEST)  
        Console.WriteLine("DEBUG is defined");  
#elif (!DEBUG && MYTEST)  
        Console.WriteLine("MYTEST is defined");  
#elif (DEBUG && MYTEST)  
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else  
        Console.WriteLine("DEBUG and MYTEST are not defined");  
#endif  
    }  
}  
```  
  
 **Sono stati definiti DEBUG e MYTEST**   
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C#](../../../csharp/language-reference/preprocessor-directives/index.md)
