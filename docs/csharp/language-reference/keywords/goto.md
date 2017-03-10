---
title: "goto (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "goto_CSharpKeyword"
  - "goto"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "goto (parola chiave) [C#]"
ms.assetid: 2c03c9c1-8119-44ef-b740-fb3d287a42fe
caps.latest.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 22
---
# goto (Riferimenti per C#)
L'istruzione `goto` passa direttamente il controllo del programma a un'istruzione con etichetta.  
  
 L'istruzione `goto` viene generalmente utilizzata per trasferire il controllo a un'etichetta case specifica di un'istruzione switch o all'etichetta predefinita di un'istruzione `switch`.  
  
 L'istruzione `goto` viene inoltre utilizzata per uscire dai cicli annidati più interni.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo di `goto` in un'istruzione [switch](../../../csharp/language-reference/keywords/switch.md).  
  
 [!code-cs[csrefKeywordsJump#4](../../../csharp/language-reference/keywords/codesnippet/csharp/goto_1.cs)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come utilizzare l'istruzione `goto` per uscire dai cicli annidati.  
  
 [!code-cs[csrefKeywordsJump#5](../../../csharp/language-reference/keywords/codesnippet/csharp/goto_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzione goto](/visual-cpp/cpp/goto-statement-cpp)   
 [Istruzioni di spostamento](../../../csharp/language-reference/keywords/jump-statements.md)