---
title: "#endif (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#endif"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#endif (direttiva) [C#]"
ms.assetid: 6a5fca55-5aee-441f-86f6-1c99fbe9ec05
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# #endif (Riferimenti per C#)
`#endif` specifica la fine di una direttiva condizionale iniziata con la direttiva [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md).  Di seguito è riportato un esempio:  
  
```  
  
      #define DEBUG  
// ...  
#if DEBUG  
    Console.WriteLine("Debug version");  
#endif  
```  
  
## Note  
 Una direttiva condizionale che inizia con `#if` deve esplicitamente terminare con una direttiva `#endif`.  Per un esempio sull'utilizzo di `#endif`, vedere [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)