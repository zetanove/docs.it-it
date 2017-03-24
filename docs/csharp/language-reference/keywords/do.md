---
title: "do (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "do_CSharpKeyword"
  - "do"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "do (parola chiave) [C#]"
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# do (Riferimenti per C#)
L'istruzione `do` esegue ripetutamente un'istruzione o un blocco di istruzioni finché un'espressione specificata non restituisce `false`.  Il corpo del ciclo deve essere racchiuso tra parentesi graffe `{}`, a meno che non consista in una singola istruzione.  In tal caso, le parentesi graffe sono facoltative.  
  
## Esempio  
 Nell'esempio riportato di seguito le istruzioni del ciclo `do-while` vengono eseguite purché la variabile `x` sia inferiore a 5.  
  
 [!code-cs[csrefKeywordsIteration#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/do_1.cs)]  
  
 A differenza dell'istruzione [while](../../../csharp/language-reference/keywords/while.md), un ciclo `do-while` viene eseguito una volta prima della valutazione dell'espressione condizionale.  
  
 In corrispondenza di qualsiasi posizione nel blocco `do-while`, è possibile uscire dal ciclo utilizzando l'istruzione [break](../../../csharp/language-reference/keywords/break.md).  È possibile passare direttamente all'istruzione di valutazione dell'espressione `while` utilizzando l'istruzione [continue](../../../csharp/language-reference/keywords/continue.md).  Se l'espressione `while` restituisce un valore true, l'esecuzione continua alla prima istruzione dopo il ciclo.  Se l'espressione restituisce un valore false, l'esecuzione continua alla prima istruzione dopo il ciclo `do-while`.  
  
 È inoltre possibile uscire da un ciclo `do-while` mediante le istruzioni [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) e [throw](../../../csharp/language-reference/keywords/throw.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione do\-while \(C\+\+\)](/visual-cpp/cpp/do-while-statement-cpp)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)