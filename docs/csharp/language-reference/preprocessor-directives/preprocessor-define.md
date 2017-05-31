---
title: '#define (Riferimenti per C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '#define'
dev_langs:
- CSharp
helpviewer_keywords:
- '#define directive [C#]'
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
caps.latest.revision: 22
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
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 0db5a86fee1ed2139ae5046ada66121ffe8210b1
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="define-c-reference"></a>#define (Riferimenti per C#)
Si usa `#define` per definire un simbolo. Quando si usa il simbolo come espressione passata alla direttiva [#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md), l'espressione restituisce `true`, come illustrato nell'esempio seguente:  
  
 `#`  `define`   `DEBUG`  
  
## <a name="remarks"></a>Note  
  
> [!NOTE]
>  Non è possibile usare la direttiva `#define` per dichiarare valori costanti come in C e in C++. Le costanti in C# possono essere definite come membri statici di una classe o di uno struct. Se sono presenti più costanti di questo tipo, per usarle può essere utile creare una classe di costanti separata.  
  
 Per specificare le condizioni per la compilazione è possibile usare simboli. È possibile eseguire il test del simbolo tramite [#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) o [#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md). È anche possibile usare l'attributo `conditional` per eseguire una compilazione condizionale.  
  
 È possibile definire un simbolo ma non è possibile assegnare a questo un valore. La direttiva `#define` deve essere inserita in un file prima di usare istruzioni che non siano anche direttive del preprocessore.  
  
 Un simbolo può anche essere definito tramite l'opzione del compilatore [/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md). Per rimuovere la definizione di un simbolo, è possibile usare [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
 Un simbolo definito tramite `/define` o `#define` non provoca conflitti con una variabile avente lo stesso nome. Il nome di una variabile, infatti, non può essere passato a una direttiva del preprocessore e un simbolo può essere valutato solo da una direttiva del preprocessore.  
  
 L'ambito di un simbolo creato tramite `#define` è il file in cui il simbolo è stato definito.  
  
 Come illustrato nell'esempio seguente, è necessario inserire direttive `#define` all'inizio del file.  
  
```csharp  
#define DEBUG  
//#define TRACE  
#undef TRACE  
  
using System;  
  
public class TestDefine  
{  
    static void Main()  
    {  
#if (DEBUG)  
        Console.WriteLine("Debugging is enabled.");  
#endif  
  
#if (TRACE)  
     Console.WriteLine("Tracing is enabled.");  
#endif  
    }  
}  
// Output:  
// Debugging is enabled.  
```  
  
 Per un esempio su come annullare la definizione di un simbolo, vedere [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C#](../../../csharp/language-reference/preprocessor-directives/index.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [Procedura: Compilare in modo condizionale con traccia e debug](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)   
 [#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md)   
 [#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)
