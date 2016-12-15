---
title: "Operatore &gt;&gt;= (Riferimenti per C#) | Microsoft Docs"
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
  - ">>=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ">>= (operatore) (assegnazione Right Shift) [C#]"
  - "operatore di assegnazione right shift (>>=) [C#]"
ms.assetid: b593778c-b9b4-440d-8b29-c1ac22cb81c0
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore &gt;&gt;= (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Operatore di assegnazione spostamento a destra.  
  
## Note  
 Un'espressione con il seguente formato:  
  
```  
x >>= y  
```  
  
 viene valutata come  
  
```  
x = x >> y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  L'[operatore \>\>](../../../csharp/language-reference/operators/right-shift-operator.md) sposta `x` verso destra in base al valore specificato da `y`.  
  
 L'operatore \>\>\= non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore \>\>](../../../csharp/language-reference/operators/right-shift-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#11](../../../csharp/language-reference/operators/codesnippet/CSharp/right-shift-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)