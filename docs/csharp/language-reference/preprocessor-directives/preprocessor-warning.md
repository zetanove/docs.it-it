---
title: "#warning (Riferimenti per C#) | Microsoft Docs"
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
  - "#warning"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#warning (direttiva) [C#]"
ms.assetid: e6fb496d-bb8b-4018-baf6-5b60a0c8902b
caps.latest.revision: 9
caps.handback.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #warning (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#warning` consente di generare un avviso di livello uno da una posizione specifica del codice.  Di seguito è riportato un esempio:  
  
```  
#warning Deprecated code in this method.  
```  
  
## Note  
 `#warning` viene generalmente utilizzata in una direttiva condizionale.  Inoltre, è possibile generare un errore definito dall'utente tramite [\#error](../../../csharp/language-reference/preprocessor-directives/preprocessor-error.md).  
  
## Esempio  
  
```  
// preprocessor_warning.cs  
// CS1030 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#warning DEBUG is defined  
#endif  
    }  
}  
```  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)