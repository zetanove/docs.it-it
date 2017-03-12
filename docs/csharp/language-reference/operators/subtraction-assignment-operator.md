---
title: "Operatore /= (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "/=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/= (operatore di assegnazione di divisione) [C#]"
  - "operatore di assegnazione di divisione (/=) [C#]"
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Operatore /= (Riferimenti per C#)
Operatore di assegnazione di divisione.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `/=`, ad esempio  
  
```  
x /= y  
```  
  
 equivale a  
  
```  
x = x / y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  Per i tipi numerici, l'[operatore \/](../../../csharp/language-reference/operators/division-operator.md) è già definito per l'esecuzione di divisioni.  
  
 L'operatore`/=` non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore \/](../../../csharp/language-reference/operators/division-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  Su tutti gli operatori di assegnazione composti, l'overload dell'operatore binario esegue in modo implicito l'overload dell'assegnazione composta equivalente.  
  
## Esempio  
 [!code-cs[csRefOperators#5](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#5)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)