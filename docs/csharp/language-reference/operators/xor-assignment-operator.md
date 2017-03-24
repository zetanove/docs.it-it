---
title: "Operatore ^= (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "^=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "^= (operatore) [C#]"
ms.assetid: 3658ff9a-61cd-467e-ad6b-8fbf1cfbaae4
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Operatore ^= (Riferimenti per C#)
Operatore di assegnazione di OR esclusivo.  
  
## Note  
 Un'espressione con il seguente formato:  
  
```  
x ^= y  
```  
  
 viene valutata come  
  
```  
x = x ^ y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  L'[operatore ^](../../../csharp/language-reference/operators/xor-operator.md) esegue un'operazione con OR esclusivo bit per bit sugli operandi integrali e con OR esclusivo logico sugli operandi [bool](../../../csharp/language-reference/keywords/bool.md).  
  
 L'operatore ^\= non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore^](../../../csharp/language-reference/operators/xor-operator.md) \(vedere [operator](../../../csharp/language-reference/keywords/operator.md)\).  
  
## Esempio  
 [!code-cs[csRefOperators#23](../../../csharp/language-reference/operators/codesnippet/CSharp/xor-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)