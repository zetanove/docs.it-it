---
title: "Operatore *= (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "*=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "*= (operatore) [C#]"
  - "assegnazione di moltiplicazione (operatore binario) (*=) [C#]"
ms.assetid: 2e472155-59db-4dbf-bb94-bcccfa1a794d
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Operatore *= (Riferimenti per C#)
Operatore di assegnazione di moltiplicazione binario.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `*=`, ad esempio  
  
```  
x *= y  
```  
  
 equivale a  
  
```  
x = x * y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  Per i tipi numerici, l'[operatore \*](../../../csharp/language-reference/operators/multiplication-operator.md) è già definito per l'esecuzione di moltiplicazioni.  
  
 L'operatore `*=` non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore \*](../../../csharp/language-reference/operators/multiplication-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
## Esempio  
 [!code-cs[csRefOperators#13](../../../csharp/language-reference/operators/codesnippet/CSharp/multiplication-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)