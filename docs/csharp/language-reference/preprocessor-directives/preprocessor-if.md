---
title: "#if (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "#if"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#if (direttiva) [C#]"
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #if (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Quando il compilatore C\# trova una direttiva `#if` seguita da una direttiva [\#endif\<\/legacyLink\>](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md), compila il codice tra le direttive solo se il simbolo specificato è definito.  A differenza di C e C\+\+, non è possibile assegnare un valore numerico a un simbolo. L'istruzione \#if in C\# è booleana e consente di verificare solo se il simbolo è stato o meno definito.  Di seguito è riportato un esempio:  
  
```  
#define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
 È possibile utilizzare gli operatori [\=\=](../../../csharp/language-reference/operators/equality-comparison-operator.md) \(uguaglianza\), [\!\=](../../../csharp/language-reference/operators/not-equal-operator.md) \(disuguaglianza\) solo per verificare se una condizione è [true](../../../csharp/language-reference/keywords/true.md) o [false](../../../csharp/language-reference/keywords/false.md) .  True significa che il simbolo è definito.  L'istruzione `#if DEBUG` ha lo stesso significato di `#if (DEBUG == true)`.  È possibile utilizzare gli operatori [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) \(e\), [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) \(o\), e [\!](../../../csharp/language-reference/operators/logical-negation-operator.md) \(non\) valutare se i simboli più definite.  È anche possibile raggruppare simboli e operatori tra parentesi.  
  
## Note  
 `#if`, insieme alle direttive [\#else](../../../csharp/language-reference/preprocessor-directives/preprocessor-else.md), [\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md), [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md), [\#define](../../../csharp/language-reference/preprocessor-directives/preprocessor-define.md) e [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md), consente di includere o escludere il codice in base all'esistenza di uno o più simboli.  Questo può essere utile quando si compila il codice per una build di debug o per una configurazione specifica.  
  
 Una direttiva condizionale che inizia con `#if` deve terminare in modo esplicito con una direttiva `#endif`.  
  
 `#define` consente di definire un simbolo. In questo modo, utilizzando il simbolo come espressione passata alla direttiva `#if`, l'espressione restituirà `true`.  
  
 Un simbolo può anche essere definito tramite l'opzione del compilatore [\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md).  Per rimuovere la definizione di un simbolo, è possibile utilizzare [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
 Un simbolo definito tramite `/define` o `#define` non provoca conflitti con una variabile avente lo stesso nome.  Il nome di una variabile, infatti, non può essere passato a una direttiva per il preprocessore e un simbolo può essere valutato solo da una direttiva per il preprocessore.  
  
 L'ambito di un simbolo creato con `#define` è il file in cui è stato definito.  
  
## Esempio  
  
```  
// preprocessor_if.cs  
#define DEBUG #define MYTEST  
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
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)