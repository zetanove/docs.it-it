---
title: "?? Operatore (Riferimenti per C#) | Microsoft Docs"
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
  - "??_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operatore ?? [C#]"
  - "operatore coalesce [C#]"
  - "AND condizionale (operatore) (&&) [C#]"
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
caps.latest.revision: 17
caps.handback.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# ?? Operatore (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'operatore `??` viene chiamato operatore null\-coalescing.  Restituisce l'operando sinistro se non è Null. In caso contrario, restituisce l'operando destro.  
  
## Note  
 Un tipo nullable può rappresentare un valore dal dominio del tipo oppure il valore può essere indefinito, nel qual caso è Null.  È possibile utilizzare l'espressività sintattica dell'operatore `??` per restituire un valore appropriato \(l'operando destro\) quando l'operando sinistro è un tipo nullable il cui valore è Null.  Se si tenta di assegnare un tipo di valore nullable a un tipo non nullable senza utilizzare l'operatore `??`, verrà generato un errore in fase di compilazione.  Se si utilizza un cast e il tipo di valore nullable non è attualmente definito, verrà generata un'eccezione `InvalidOperationException`.  
  
 Per ulteriori informazioni, vedere [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md).  
  
 Il risultato di un operatore ?? non è considerato una costante anche se entrambi gli argomenti sono costanti.  
  
## Esempio  
 [!code-cs[csRefOperators#53](../../../csharp/language-reference/operators/codesnippet/CSharp/null-conditional-operator_1.cs)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Tipi nullable](../../../csharp/programming-guide/nullable-types/index.md)   
 [Cosa significa esattamente "elevato"?](http://go.microsoft.com/fwlink/?LinkID=112382)