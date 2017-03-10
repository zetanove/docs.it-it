---
title: "Operatore | (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "|_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "| (operatore) [C#]"
  - "binario (operatore) (|) [C#]"
  - "operatore OR bit per bit [C#]"
ms.assetid: 82d6bb78-54c8-40bf-b679-531180ddaf70
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Operatore | (Riferimenti per C#)
Binary        `|`  sono già definiti per i tipi integrali e `bool`.  Per i tipi integrali,  `|`calcola l'operatore OR bit per bit dei suoi operandi.  Per gli operandi `bool`,  `|` calcola l'operatore OR logico degli operandi. Il risultato sarà pertanto `false` solo se entrambi gli operandi sono `false`.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore          `|` \(vedere [operator](../../../csharp/language-reference/keywords/operator.md)\).  
  
## Esempio  
 [!code-cs[csRefOperators#31](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#31)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)