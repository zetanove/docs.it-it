---
title: "break (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "break"
  - "break_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "break (parola chiave) [C#]"
ms.assetid: be2571ed-efb0-4965-b122-81e5b09db0b9
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# break (Riferimenti per C#)
L'istruzione `break` termina il ciclo di inclusione più vicino o l'istruzione [switch](../../../csharp/language-reference/keywords/switch.md) in cui è contenuta.  Il controllo viene passato all'istruzione che segue l'istruzione terminata, se presente.  
  
## Esempio  
 In questo esempio l'istruzione condizionale contiene un contatore che dovrebbe contare da 1 a 100. L'istruzione `break` viene tuttavia utilizzata per terminare il ciclo dopo 4 conteggi.  
  
 [!code-cs[csrefKeywordsJump#1](../../../csharp/language-reference/keywords/codesnippet/csharp/break_1.cs)]  
  
## Esempio  
 In questo esempio, l'istruzione `break` viene utilizzata per interrompere un ciclo annidato interno e restituire il controllo al ciclo esterno.  
  
 [!code-cs[csrefKeywordsJump#7](../../../csharp/language-reference/keywords/codesnippet/csharp/break_2.cs)]  
  
## Esempio  
 In questo esempio viene illustrato l'utilizzo di `break` in un'istruzione [switch](../../../csharp/language-reference/keywords/switch.md).  
  
 [!code-cs[csrefKeywordsJump#2](../../../csharp/language-reference/keywords/codesnippet/csharp/break_3.cs)]  
  
 Se si inserisse `4`, si otterrebbe il seguente output:  
  
```  
Enter your selection (1, 2, or 3): 4  
Sorry, invalid selection.  
```  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [switch](../../../csharp/language-reference/keywords/switch.md)   
 [Istruzioni di spostamento](../../../csharp/language-reference/keywords/jump-statements.md)   
 [Istruzioni di iterazione](../../../csharp/language-reference/keywords/iteration-statements.md)