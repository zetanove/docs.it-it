---
title: "operator (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "operator_CSharpKeyword"
  - "operator"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operator (parola chiave) [C#]"
ms.assetid: 59218cce-e90e-42f6-a6bb-30300981b86a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# operator (Riferimenti per C#)
Utilizzare la parola chiave `operator` per eseguire l'overload di un operatore incorporato o fornire una conversione definita dall'utente in una classe o una dichiarazione di struttura.  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzata una classe estremamente semplificata di numeri frazionari  in cui gli operatori \+ e \* vengono sottoposti a overload per eseguire addizioni e moltiplicazioni frazionarie. Viene inoltre definito un operatore che converte un tipo Fraction nel corrispondente tipo double.  
  
 [!code-cs[csrefKeywordsConversion#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/operator_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [impliciti](../../../csharp/language-reference/keywords/implicit.md)   
 [esplicita](../../../csharp/language-reference/keywords/explicit.md)   
 [Procedura: implementare conversioni tra struct definite dall'utente](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)