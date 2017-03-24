---
title: "Operatore -&gt; (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "->_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-> (operatore) (C#)"
  - "operatore di accesso a membri (->) [C#]"
ms.assetid: e39ccdc1-f1ff-4a92-bf1d-ac2c8c11316a
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# Operatore -&gt; (Riferimenti per C#)
L'operatore `->` può essere utilizzato per dereferenziare i puntatori e contemporaneamente accedere ai membri.  
  
## Note  
 Un'espressione con il seguente formato,  
  
```  
x->y  
```  
  
 dove `x` è puntatore di tipo `T*` e `y` è un membro di `T`, è equivalente a  
  
```  
(*x).y  
```  
  
 L'operatore `->` può essere utilizzato solo in codice contrassegnato come [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
 Non è possibile sottoporre l'operatore `->` a overload.  
  
## Esempio  
 [!code-cs[csRefOperators#15](../../../csharp/language-reference/operators/codesnippet/CSharp/dereference-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)