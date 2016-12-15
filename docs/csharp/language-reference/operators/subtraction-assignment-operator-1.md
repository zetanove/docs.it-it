---
title: "Operatore -= (Riferimenti per C#) | Microsoft Docs"
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
  - "-=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "-= (operatore) (assegnazione di sottrazione) [C#]"
  - "operatore di assegnazione di sottrazione (-=) [C#]"
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore -= (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Operatore di assegnazione di sottrazione.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `-=`, ad esempio  
  
```  
x -= y  
```  
  
 equivale a  
  
```  
x = x - y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  Il significato dell'[operatore \-](../../../csharp/language-reference/operators/subtraction-operator.md) varia a seconda dei tipi `x` e `y`: \(sottrazione per gli operandi numerici, rimozione del delegato per gli operandi delegati e così via.  
  
 L'operatore `-=` non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore \-](../../../csharp/language-reference/operators/subtraction-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
 L'operatore \-\= viene anche utilizzato in C\# per annullare la sottoscrizione di un evento.  Per ulteriori informazioni, vedere [Procedura: eseguire e annullare la sottoscrizione a eventi](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).  
  
## Esempio  
 [!code-cs[csRefOperators#6](../../../csharp/language-reference/operators/codesnippet/CSharp/subtraction-assignment-operator-1_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)