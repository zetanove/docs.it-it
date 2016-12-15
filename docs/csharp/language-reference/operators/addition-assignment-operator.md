---
title: "Operatore += (Riferimenti per C#) | Microsoft Docs"
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
  - "+=_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "+= (operatore) [C#]"
  - "assegnazione di addizione (operatore) (+=) [C#]"
ms.assetid: 9cdf97e6-331d-492b-85e1-3ec3171484e9
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operatore += (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Operatore di assegnazione di addizione.  
  
## Note  
 Un'espressione che utilizza l'operatore di assegnazione `+=`, ad esempio  
  
```  
x += y  
```  
  
 equivale a  
  
```  
x = x + y  
```  
  
 con la differenza che `x` viene valutato solo una volta.  Il significato dell'[operatore \+](../../../csharp/language-reference/operators/addition-operator.md) varia a seconda dei tipi di `x` e `y`, somma per gli operandi numerici, concatenazione per gli operandi string e così via.  
  
 L'operatore `+=` non può essere sottoposto direttamente a overload; tuttavia, i tipi definiti dall'utente possono eseguire l'overload dell'[operatore \+](../../../csharp/language-reference/operators/addition-operator.md). Per ulteriori informazioni, vedere [operator](../../../csharp/language-reference/keywords/operator.md).  
  
 L'operatore `+=` viene inoltre utilizzato per specificare un metodo che verrà chiamato in risposta a un evento. Tali metodi sono denominati gestori dell'evento.  L'utilizzo dell'operatore `+=` in questo contesto viene definito *sottoscrizione di un evento*.  Per ulteriori informazioni, vedere [Procedura: eseguire e annullare la sottoscrizione a eventi](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).  e [Delegati](../../../csharp/programming-guide/delegates/index.md).  
  
## Esempio  
 [!code-cs[csRefOperators#35](../../../csharp/language-reference/operators/codesnippet/CSharp/addition-assignment-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)