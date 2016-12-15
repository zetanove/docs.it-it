---
title: "while (Riferimenti per C#) | Microsoft Docs"
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
  - "while_CSharpKeyword"
  - "while"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "while (parola chiave) [C#]"
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# while (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'istruzione `while` esegue un'istruzione o un blocco di istruzioni finché un'espressione specificata non restituisce `false`.  
  
## Esempio  
 [!code-cs[csrefKeywordsIteration#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_1.cs)]  
  
## Esempio  
 [!code-cs[csrefKeywordsIteration#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_2.cs)]  
  
## Esempio  
 Poiché il test dell'espressione `while` avviene prima di ogni esecuzione del ciclo, un ciclo `while` viene eseguito zero o più volte.  Il ciclo [do](../../../csharp/language-reference/keywords/do.md) è differente, in quanto viene eseguito una o più volte.  
  
 Un ciclo `while` termina quando un'istruzione [break](../../../csharp/language-reference/keywords/break.md), [goto](../../../csharp/language-reference/keywords/goto.md), [return](../../../csharp/language-reference/keywords/return.md) o [throw](../../../csharp/language-reference/keywords/throw.md) trasferisce il controllo all'esterno del ciclo.  Per trasferire il controllo all'iterazione successiva senza uscire dal ciclo, utilizzare l'istruzione [continue](../../../csharp/language-reference/keywords/continue.md).  Si noti la differenza di output nei tre esempi precedenti, che dipende dalla posizione in cui viene incrementato `int n`.  Nell'esempio riportato di seguito non viene generato alcun output.  
  
 [!code-cs[csrefKeywordsIteration#7](../../../csharp/language-reference/keywords/codesnippet/CSharp/while_3.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione while \(C\+\+\)](/visual-cpp/cpp/while-statement-cpp)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)