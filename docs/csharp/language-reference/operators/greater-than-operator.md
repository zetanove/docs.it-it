---
title: "Operatore &gt; (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - ">_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "> (operatore) [C#]"
  - "maggiore di (operatore) (>) [C#]"
ms.assetid: 26d3cb69-9c0b-4cc5-858b-5be1abd6659d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Operatore &gt; (Riferimenti per C#)
Tutti i tipi numerici e di enumerazione definiscono un operatore relazionale "maggiore di" \(`>`\) che restituisce `true` se il primo operando è maggiore del secondo e `false` in caso contrario.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `>`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Se si esegue l'overload dell'operatore `>`, è necessario sottoporre a overload anche l'operatore [\<](../../../csharp/language-reference/operators/less-than-operator.md).  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#29](../../../csharp/language-reference/operators/codesnippet/CSharp/greater-than-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [esplicita](../../../csharp/language-reference/keywords/explicit.md)