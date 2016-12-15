---
title: "Confronto tra puntatori (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatori [C#], confronto"
ms.assetid: fcafd514-7405-4deb-8490-cc58efda5495
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Confronto tra puntatori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per confrontare puntatori di qualsiasi tipo, è possibile applicare gli operatori riportati di seguito:  
  
 **\=\=   \!\=   \<   \>   \<\=   \>\=**  
  
 Gli operatori di confronto consentono di confrontare gli indirizzi dei due operandi come se fossero Unsigned Integer.  
  
## Esempio  
 [!code-cs[csProgGuidePointers#16](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/pointer-comparison_1.cs)]  
  
 [!code-cs[csProgGuidePointers#17](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/pointer-comparison_2.cs)]  
  
## Esempio di output  
 `True`  
  
 `False`  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Modifica dei puntatori](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)