---
title: "Operatore () (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "()_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "() (operatore) [C#]"
  - "cast (operatore) [C#]"
  - "conversione di tipi [C#], () (operatore)"
ms.assetid: 846e1f94-8a8c-42fc-a42c-fbd38e70d8cc
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# Operatore () (Riferimenti per C#)
Oltre a specificare l'ordine in cui devono essere eseguite le operazioni di un'espressione, le parentesi vengono utilizzate per eseguire le seguenti operazioni:  
  
1.  Specificare i cast, ovvero le conversioni di tipo.  
  
     [!code-cs[csRefOperators#1](../../../csharp/language-reference/operators/codesnippet/CSharp/invocation-operator_1.cs)]  
  
2.  Richiamare metodi o delegati.  
  
     [!code-cs[csRefOperators#2](../../../csharp/language-reference/operators/codesnippet/CSharp/invocation-operator_2.cs)]  
  
## Note  
 Un cast richiama l'operatore di conversione in modo esplicito da un tipo a un altro. Se tale operatore di conversione non viene definito, il cast non sarà eseguito correttamente.  Per informazioni sulla definizione di un operatore di conversione, vedere [explicit](../../../csharp/language-reference/keywords/explicit.md) e [implicit](../../../csharp/language-reference/keywords/implicit.md).  
  
 Non è possibile sottoporre l'operatore `()` a overload.  
  
 Per ulteriori informazioni, vedere [Cast e conversioni di tipi \(C\#\)](../../../csharp/programming-guide/types/casting-and-type-conversions.md).  
  
 Un'espressione cast può determinare una sintassi ambigua.  Ad esempio, l'espressione `(x)–y` potrebbe essere interpretata come espressione cast \(un cast di –y sul tipo x\) oppure come espressione di addizione combinata con un'espressione tra parentesi che calcola il valore x – y.  
  
 Per ulteriori informazioni sulla chiamata del metodo, vedere [Metodi](../../../csharp/programming-guide/classes-and-structs/methods.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)