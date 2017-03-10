---
title: "Operatore &lt;&lt; (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<<_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<< (operatore) [C#]"
  - "operatore left shift (<<) [C#]"
ms.assetid: a654eb56-1ff7-4bf3-9064-b631be0cdccc
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Operatore &lt;&lt; (Riferimenti per C#)
L'operatore di spostamento a sinistra \(`<<`\) sposta il primo operando verso sinistra in base al numero di bit specificati nel secondo operando.  Il tipo del secondo operando deve essere un [int](../../../csharp/language-reference/keywords/int.md) o un tipo avente una conversione numerica implicita predefinita su `int`.  
  
## Note  
 Se il primo operando è un tipo [int](../../../csharp/language-reference/keywords/int.md) o [uint](../../../csharp/language-reference/keywords/uint.md) \(quantità a 32 bit\), il conteggio dello spostamento sarà dato dai cinque bit meno significativi del secondo operando.  Ovvero, il calcolo shift effettivo è compreso tra 0 e 31 bit.  
  
 Se il primo operando è un tipo [long](../../../csharp/language-reference/keywords/long.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md) \(quantità a 64 bit\), il conteggio dello spostamento sarà dato dai sei bit meno significativi del secondo operando.  Ovvero, il calcolo shift effettivo è compreso tra 0 e 63 bit.  
  
 Tutti i bit più significativi che non rientrano nell'intervallo del tipo del primo operando dopo lo spostamento vengono scartati, mentre i bit vuoti meno significativi vengono riempiti di zeri.  Le operazioni di spostamento non provocano mai overflow.  
  
 I tipi definiti dall'utente possono sottoporre a overload l'operatore `<<` \(per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md)\). Il tipo del primo operando deve essere un tipo definito dall'utente, mentre il tipo del secondo operando deve essere `int`.  Quando si esegue l'overload di un operatore binario, viene eseguito in modo implicito anche l'overload dell'eventuale operatore di assegnazione corrispondente.  
  
## Esempio  
 [!code-cs[csRefOperators#14](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#14)]  
  
## Commenti  
 Si noti che `i<<1` e `i<<33` generano lo stesso risultato, in quanto 1 e 33 hanno gli stessi cinque bit meno significativi.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)