---
title: "Operatore | (Riferimenti per C#) | Microsoft Docs"
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
  - "|_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "| (operatore) [C#]"
  - "binario (operatore) (|) [C#]"
  - "operatore OR bit per bit [C#]"
ms.assetid: 82d6bb78-54c8-40bf-b679-531180ddaf70
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore | (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Binary        `|`  sono già definiti per i tipi integrali e `bool`.  Per i tipi integrali,  `|`calcola l'operatore OR bit per bit dei suoi operandi.  Per gli operandi `bool`,  `|` calcola l'operatore OR logico degli operandi. Il risultato sarà pertanto `false` solo se entrambi gli operandi sono `false`.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore          `|` \(vedere [operator](../../../csharp/language-reference/keywords/operator.md)\).  
  
## Esempio  
 [!code-cs[csRefOperators#31](../../../csharp/language-reference/operators/codesnippet/CSharp/or-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)