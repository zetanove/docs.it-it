---
title: "Operatore &gt;= (Riferimenti per C#) | Microsoft Docs"
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
  - ">=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ">= (operatore) [C#]"
  - "maggiore o uguale a (operatore) (>=) [C#]"
ms.assetid: 0db4dcaf-56a3-4884-a7ad-35f64978a58d
caps.latest.revision: 16
caps.handback.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore &gt;= (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Tutti i tipi numerici e di enumerazione definiscono un operatore relazionale "maggiore o uguale a" \(`>=`\) che restituisce `true` se il primo operando è maggiore o uguale al secondo e `false` in caso contrario.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `>=`.  Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Se si esegue l'overload dell'operatore `>=`, è necessario sottoporre a overload anche l'operatore [\<\=](../../../csharp/language-reference/operators/less-than-equal-operator.md).  Le operazioni sui tipi integrali sono generalmente consentite sull'enumerazione.  
  
## Esempio  
 [!code-cs[csRefOperators#39](../../../csharp/language-reference/operators/codesnippet/CSharp/greater-than-equal-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)