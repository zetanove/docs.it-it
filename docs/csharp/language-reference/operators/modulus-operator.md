---
title: "Operatore % (Riferimenti per C#) | Microsoft Docs"
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
  - "%_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "% (operatore) [C#]"
  - "modulo (operatore) [C#]"
ms.assetid: 3b74f4f9-fd9c-45e7-84fa-c8d71a0dfad7
caps.latest.revision: 15
caps.handback.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore % (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'operatore di `%` calcola il resto dopo la divisione del primo operando dal secondo.  Tutti i tipi numerici dispongono predefinito gli operatori di altri elementi.  
  
## Note  
 I tipi definiti dall'utente possono eseguire l'overload dell'operatore `%`. Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#9](../../../csharp/language-reference/operators/codesnippet/CSharp/modulus-operator_1.cs)]  
  
## Commenti  
 Si notino gli errori di arrotondamento associati al tipo double.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)