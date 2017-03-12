---
title: "Operatore &lt;= (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<= (operatore) [C#]"
  - "minore o uguale a (operatore) (<=) [C#]"
ms.assetid: bb0caec9-d253-4105-b8bc-5252233251e4
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Operatore &lt;= (Riferimenti per C#)
Tutti i tipi numerici e i tipi di enumerazione definiscono un operatore relazionale "minore o uguale a" \(`<=`\) che restituisce `true` se il primo operando è minore o uguale al secondo e `false` in caso contrario.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `<=`.  Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Se si esegue l'overload dell'operatore `<=`, è necessario sottoporre a overload anche l'operatore [\>\=](../../../csharp/language-reference/operators/greater-than-equal-operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#32](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#32)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [esplicita](../../../csharp/language-reference/keywords/explicit.md)