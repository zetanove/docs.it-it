---
title: "Operatore &lt; (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "< (operatore) [C#]"
  - "minore di (operatore) (<) [C#]"
ms.assetid: 38cb91e6-79a6-48ec-9c1e-7b71fd8d2b41
caps.latest.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 14
---
# Operatore &lt; (Riferimenti per C#)
Tutti i tipi numerici e di enumerazione definiscono un operatore relazionale "minore di" \(`<`\) che restituisce `true` se il primo operando è minore del secondo e `false` in caso contrario.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `<`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Se si esegue l'overload dell'operatore `<`, è necessario sottoporre a overload anche l'operatore [\>](../../../csharp/language-reference/operators/greater-than-operator.md).  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#24](../../../csharp/language-reference/operators/codesnippet/CSharp/less-than-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)