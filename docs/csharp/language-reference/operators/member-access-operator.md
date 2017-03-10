---
title: ". Operatore (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "._CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - ". operatore [C#]"
  - "punto (.) (operatore) [C#]"
  - "operatore di accesso al membro (.) [C#]"
ms.assetid: a1f54b52-b686-4ae5-a48e-a2a9ebd0eb7b
caps.latest.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 21
---
# . Operatore (Riferimenti per C#)
L'operatore punto \(`.`\) viene utilizzato per l'accesso ai membri.  L'operatore punto specifica un membro di un tipo o di uno spazio dei nomi.  Ad esempio, l'operatore punto viene utilizzato per accedere a metodi specifici all'interno delle librerie di classi di .NET Framework:  
  
 [!code-cs[csRefOperators#16](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#16)]  
  
 Si consideri ad esempio la seguente classe:  
  
 [!code-cs[csRefOperators#17](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#17)]  
  
 [!code-cs[csRefOperators#18](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#18)]  
  
 La variabile `s` ha due membri: `a` e `b`. Per accedervi, utilizzare l'operatore punto, come mostrato nell'esempio.  
  
 [!code-cs[csRefOperators#19](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#19)]  
  
 Il punto viene inoltre utilizzato per formare nomi completi, ovvero nomi che specificano, ad esempio, lo spazio dei nomi o l'interfaccia a cui appartengono.  
  
 [!code-cs[csRefOperators#20](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#20)]  
  
 La direttiva using rende facoltativa la qualificazione di alcuni nomi:  
  
 [!code-cs[csRefOperators#21](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#21)]  
  
 Tuttavia, se l'identificatore è ambiguo, dovrà essere qualificato:  
  
 [!code-cs[csRefOperators#22](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#22)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)