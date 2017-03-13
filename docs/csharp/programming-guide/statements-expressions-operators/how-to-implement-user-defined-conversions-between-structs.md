---
title: "Procedura: implementare conversioni tra struct definite dall&#39;utente (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "conversioni definite dall'utente [C#]"
ms.assetid: 97839aef-8fbc-40d5-9769-6b569bc2710b
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# Procedura: implementare conversioni tra struct definite dall&#39;utente (Guida per programmatori C#)
In questo esempio vengono definite due struct, `RomanNumeral` e `BinaryNumeral`, e vengono mostrate delle conversioni tra esse.  
  
## Esempio  
 [!code-cs[csProgGuideStatements#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-user-defined-conversions-between-structs_1.cs)]  
  
## Programmazione efficiente  
  
-   Nell'esempio precedente l'istruzione:  
  
     [!code-cs[csProgGuideStatements#14](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-user-defined-conversions-between-structs_2.cs)]  
  
     esegue una conversione da `RomanNumeral` a `BinaryNumeral`.  Dal momento che non esiste alcuna conversione diretta da `RomanNumeral` a `BinaryNumeral`, utilizzare un cast per la conversione da `RomanNumeral` a `int` e un altro cast per la conversione da `int` a `BinaryNumeral`.  
  
-   L'istruzione:  
  
     [!code-cs[csProgGuideStatements#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-user-defined-conversions-between-structs_3.cs)]  
  
     esegue una conversione da `BinaryNumeral` a `RomanNumeral`.  Dal momento che `RomanNumeral` definisce una conversione implicita da `BinaryNumeral`, non è necessario alcun cast.  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori di conversione](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)