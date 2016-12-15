---
title: "#define (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "#define"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#define (direttiva) [C#]"
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #define (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per definire un simbolo, utilizzare `#define`.  Quando si utilizza il simbolo come espressione passata alla direttiva [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md), l'espressione restituirà `true`, come mostrato nel seguente esempio:  
  
 `#`  `define`   `DEBUG`  
  
## Note  
  
> [!NOTE]
>  Non è possibile utilizzare la direttiva `#define` per dichiarare valori costanti come in C e C\+\+.  Le costanti in C\# possono essere definite come membri statici di una classe o di una struttura.  Se sono presenti più costanti, può essere utile creare una classe di costanti separata per utilizzarle.  
  
 I simboli possono essere utilizzati per specificare le condizioni per la compilazione.  È possibile eseguire il test del simbolo tramite [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) o [\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md).  È inoltre possibile utilizzare l'attributo `conditional` per eseguire una compilazione condizionale.  
  
 È possibile definire un simbolo ma non assegnarvi un valore.  La direttiva `#define` deve essere inserita in un file prima di utilizzare istruzioni che non siano anche direttive del preprocessore.  
  
 Un simbolo può anche essere definito tramite l'opzione del compilatore [\/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md).  Per rimuovere la definizione di un simbolo, è possibile utilizzare [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
 Un simbolo definito tramite `/define` o `#define` non provoca conflitti con una variabile avente lo stesso nome.  Il nome di una variabile, infatti, non può essere passato a una direttiva per il preprocessore e un simbolo può essere valutato solo da una direttiva per il preprocessore.  
  
 L'ambito di un simbolo creato utilizzando `#define` è il file in cui il simbolo è stato definito.  
  
 Come illustrato nel seguente esempio, è necessario inserire direttive `#define` nella parte superiore del file.  
  
```c#  
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
  
 Per un esempio su come annullare la definizione di un simbolo, vedere [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)   
 [const](../../../csharp/language-reference/keywords/const.md)   
 [How to: Compile Conditionally with Trace and Debug](../Topic/How%20to:%20Compile%20Conditionally%20with%20Trace%20and%20Debug.md)   
 [\#undef](../../../csharp/language-reference/preprocessor-directives/preprocessor-undef.md)   
 [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md)