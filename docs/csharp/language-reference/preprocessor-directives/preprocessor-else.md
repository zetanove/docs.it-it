---
title: "#else (Riferimenti per C#) | Microsoft Docs"
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
  - "#else"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#else (direttiva) [C#]"
ms.assetid: 6a347322-cfa2-4a86-98f8-ddfa2cb7d4db
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# #else (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

`#else` consente di creare una direttiva condizionale composita. In questo modo, se nessuna delle espressioni delle direttive [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md) o [\#elif](../../../csharp/language-reference/preprocessor-directives/preprocessor-elif.md) \(facoltativa\) precedenti ha restituito `true`, il compilatore valuterà tutto il codice tra `#else` e l'espressione `#endif` successiva.  
  
## Note  
 La direttiva per il preprocessore `#else` deve essere seguita da [\#endif](../../../csharp/language-reference/preprocessor-directives/preprocessor-endif.md).  Per un esempio dell'utilizzo di `#else` vedere [\#if](../../../csharp/language-reference/preprocessor-directives/preprocessor-if.md).  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Direttive per il preprocessore C\#](../../../csharp/language-reference/preprocessor-directives/index.md)