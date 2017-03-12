---
title: "Operatore &gt;&gt; (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - ">>_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ">> (operatore) [C#]"
  - "operatore right shift (>>) [C#]"
ms.assetid: a07f8679-d318-4ef8-b38b-65903efb8056
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Operatore &gt;&gt; (Riferimenti per C#)
L'operatore di spostamento a destra \(`>>`\) sposta il primo operando verso destra in base al numero di bit specificati dal secondo operando.  
  
## Note  
 Se il primo operando è un tipo [int](../../../csharp/language-reference/keywords/int.md) o [uint](../../../csharp/language-reference/keywords/uint.md) \(quantità a 32 bit\), il conteggio dello spostamento verrà dato dai cinque bit meno significativi del secondo operando \(secondo operando & 0x1f\).  
  
 Se il primo operando è un tipo [long](../../../csharp/language-reference/keywords/long.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md) \(quantità a 64 bit\), il conteggio dello spostamento sarà dato dai sei bit meno significativi del secondo operando \(secondo operando & 0x3f\).  
  
 Se il primo operando è di tipo [int](../../../csharp/language-reference/keywords/int.md) o [long](../../../csharp/language-reference/keywords/long.md), lo spostamento verso destra sarà uno spostamento aritmetico, ovvero i bit vuoti più significativi vengono impostati come il bit del segno.  Se il primo operando è di tipo [uint](../../../csharp/language-reference/keywords/uint.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md), lo spostamento verso destra sarà uno spostamento logico, ovvero i bit più significativi vengono riempiti di zeri.  
  
 I tipi definiti dall'utente possono sottoporre a overload l'operatore `>>`. Il tipo del primo operando deve essere un tipo definito dall'utente, mentre il tipo del secondo operando deve essere [int](../../../csharp/language-reference/keywords/int.md).  Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#26](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#26)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)