---
title: "return (Riferimenti per C#) | Microsoft Docs"
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
  - "return_CSharpKeyword"
  - "return"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "return (parola chiave) [F#]"
  - "return (istruzione) [C#]"
ms.assetid: 6da6e152-5b58-4448-8f3f-470dd0617ecd
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# return (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'istruzione `return` termina l'esecuzione del metodo in cui è contenuta e restituisce il controllo al metodo di chiamata.  Può anche restituire un valore facoltativo.  Se il metodo è un tipo `void`, è possibile omettere l'istruzione `return`.  
  
 Se l'istruzione return si trova in un blocco `try`, il blocco `finally`, se esistente, verrà eseguito prima che il controllo ritorni al metodo chiamante.  
  
## Esempio  
 Nell'esempio seguente, il metodo `A()` restituisce la variabile `Area` sotto forma di valore [double](../../../csharp/language-reference/keywords/double.md).  
  
 [!code-cs[csrefKeywordsJump#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/return_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione return](/visual-cpp/cpp/return-statement-cpp)   
 [Istruzioni di spostamento](../../../csharp/language-reference/keywords/jump-statements.md)