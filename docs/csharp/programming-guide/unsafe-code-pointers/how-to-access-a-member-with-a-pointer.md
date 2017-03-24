---
title: "Procedura: accedere a un membro mediante un puntatore (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatori [C#], accesso a membri"
ms.assetid: 1e998498-8c85-4a78-8ce2-4d8c20f08342
caps.latest.revision: 16
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 16
---
# Procedura: accedere a un membro mediante un puntatore (Guida per programmatori C#)
Per accedere a un membro di una struttura dichiarata all'interno di un contesto unsafe, è possibile utilizzare l'operatore di accesso ai membri come illustrato nell'esempio seguente in cui `p` è un puntatore a una [struttura](../../../csharp/language-reference/keywords/struct.md) contenente la coordinata `x` del membro.  
  
```  
CoOrds* p = &home;  
p -> x = 25; //member access operator ->  
```  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarata un oggetto [struttura](../../../csharp/language-reference/keywords/struct.md), `CoOrds`, che contiene le due coordinate, `x` e `y`, e viene creata un'istanza di tale oggetto.  Utilizzando l'operatore di accesso ai membri `->` e un puntatore all'istanza `home`, vengono assegnati i valori a `x` e `y`.  
  
> [!NOTE]
>  L'espressione `p->x` è equivalente a `(*p).x` ed è possibile ottenere lo stesso risultato utilizzando una delle due espressioni.  
  
 [!code-cs[csProgGuidePointers#9](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-a-member-with-a-pointer_1.cs)]  
  
 [!code-cs[csProgGuidePointers#10](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-access-a-member-with-a-pointer_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)