---
title: "Operatore &amp;= (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "&=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "&= (operatore) [C#]"
  - "AND (operatore di assegnazione) (&=) [C#]"
ms.assetid: e8d58f3f-72dd-4b5a-b995-452fcce7e6bb
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Operatore &amp;= (Riferimenti per C#)
Operatore di assegnazione di AND.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `&=`, ad esempio  
  
```  
x &= y  
```  
  
 equivale a  
  
```  
x = x & y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  L'[operatore &](../../../csharp/language-reference/operators/and-operator.md) esegue un'operazione AND logico bit per bit sugli operandi integrali e AND logico sugli operandi `bool`.  
  
 L'operatore `&=` non può essere sottoposto a overload direttamente; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore &](../../../csharp/language-reference/operators/and-operator.md) binario. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#34](../../../csharp/language-reference/operators/codesnippet/CSharp/and-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)