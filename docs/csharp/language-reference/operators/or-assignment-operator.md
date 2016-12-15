---
title: "Operatore |= (Riferimenti per C#) | Microsoft Docs"
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
  - "|=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "|= (operatore) (assegnazione OR) [C#]"
  - "operatore di assegnazione OR (|=) [C#]"
ms.assetid: 8315b8cf-dd15-402f-92f0-c7db931696ca
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore |= (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Operatore di assegnazione di OR.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `|=`, ad esempio  
  
```  
x |= y  
```  
  
 equivale a  
  
```  
x = x | y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  L'[operatore &#124;](../../../csharp/language-reference/operators/or-operator.md) esegue un'operazione di OR logico bit per bit sugli operandi integrali e di OR logico sugli operandi bool.  
  
 L'operatore `|=` non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore &#124;](../../../csharp/language-reference/operators/or-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#10](../../../csharp/language-reference/operators/codesnippet/CSharp/or-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)