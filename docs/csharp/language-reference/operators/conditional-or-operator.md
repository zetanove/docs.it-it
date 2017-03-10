---
title: "Operatore || (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "||_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "|| (operatore) [C#]"
  - "OR condizionale (operatore) (||) [C#]"
  - "OR logico (operatore) [C#]"
ms.assetid: 7d442d8e-400d-421f-b4d2-034bf82bcbdc
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# Operatore || (Riferimenti per C#)
L'operatore OR condizionale \(`||`\) esegue un oggetto OR logico dei propri operandi `bool`.  Se il primo operando valuta a `true`, il secondo operando non viene valutato.  Se il primo operando valuta a `false`, il secondo operatore OR determina se l'espressione viene valutato rispetto a `true` o a `false`.  
  
## Note  
 L'operazione  
  
```  
x || y  
```  
  
 corrisponde all'operazione  
  
```  
x | y  
```  
  
 ma se `x` è `true`, `y` non viene valutato perché l'operazione OR è `true` indipendentemente dal valore `y`.  Questo concetto è noto come “valutazione di valutazione short circuit„.  
  
 L'operatore OR condizionale non può essere sottoposta a overload, ma gli overload degli operatori logici normali e operatori [false](../../../csharp/language-reference/keywords/false.md) e [true](../../../csharp/language-reference/keywords/true.md), con alcune restrizioni, vengono considerati overload degli operatori logici condizionali.  
  
## Esempio  
 Negli esempi seguenti, l'espressione che utilizza `||` restituisce solo il primo operando.  l'espressione che utilizza `|`valuta entrambi gli operandi.  Nel secondo esempio, si verifica un'eccezione di runtime se entrambi gli operandi sono valutati.  
  
 [!code-cs[csRefOperators#52](../../../csharp/language-reference/operators/codesnippet/csharp/csrefOperators/csrefOperators.cs#52)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)