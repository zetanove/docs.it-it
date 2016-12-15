---
title: "#error (Riferimenti per C#) | Microsoft Docs"
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
  - "#error"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#error (direttiva) [C#]"
ms.assetid: f2a7f3af-4cf9-4111-b369-70204d24b26b
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #error (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#error` consente di generare un errore da una posizione specifica nel codice.  Di seguito è riportato un esempio:  
  
```  
#error Deprecated code in this method.  
```  
  
## Note  
 La direttiva `#error` viene generalmente utilizzata nelle direttive condizionali.  
  
 Inoltre, è possibile generare un avviso definito dall'utente tramite [\#warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-warning.md).  
  
## Esempio  
  
```  
// preprocessor_error.cs  
// CS1029 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#error DEBUG is defined  
#endif  
    }  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)