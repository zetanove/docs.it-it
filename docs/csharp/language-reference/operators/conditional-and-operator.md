---
title: "Operatore &amp;&amp; (Riferimenti per C#) | Microsoft Docs"
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
  - "&&_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "&& (operatore) [C#]"
  - "AND logico (operatore) [C#]"
ms.assetid: 2e4f0a1c-92a3-40f8-8e3b-17b607f20c31
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore &amp;&amp; (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'operatore AND condizionale \(`&&`\) esegue un AND logico degli operandi `bool`, ma valuta il secondo operando solo se necessario.  
  
## Note  
 L'operazione  
  
```  
x && y  
```  
  
 corrisponde all'operazione  
  
```  
x & y  
```  
  
 ma se `x`viene  `false`,  `y` non viene valutato, poiché il risultato dell'operazione di AND viene  `false` indipendentemente dal valore di  `y` è.  Questa condizione viene denominata anche valutazione "short circuit".  
  
 L'operatore AND condizionale non può essere sottoposto a overload. Tuttavia, anche gli overload dei normali operatori logici e degli operatori [true](../../../csharp/language-reference/keywords/true.md) e [false](../../../csharp/language-reference/keywords/false.md) vengono considerati, con qualche limitazione, overload degli operatori logici condizionali.  
  
## Esempio  
 Nell'esempio seguente, l'espressione condizionale nella seconda `if` l'istruzione restituisce solo il primo operando perché restituisce un valore di operando  `false`.  
  
 [!code-cs[csRefOperators#48](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-and-operator_1.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)