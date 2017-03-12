---
title: "Procedura: ottenere il valore di una variabile puntatore (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatore (espressioni) [C#], riferimento indiretto"
  - "puntatori [C#], * (operatore)"
  - "puntatori [C#], riferimento indiretto"
  - "variabili [C#], puntatori"
ms.assetid: 460a813a-4995-44c1-9de2-213b91dc7668
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Procedura: ottenere il valore di una variabile puntatore (Guida per programmatori C#)
L'operatore di riferimento indiretto a puntatore consente di ottenere la variabile nella posizione indicata da un puntatore.  L'espressione ha il seguente formato, dove  `p` è un tipo di puntatore:  
  
```  
*p;  
```  
  
 Non è possibile utilizzare l'operatore unario di riferimento indiretto o un'espressione di tipo diverso da puntatore,  né applicarlo a un puntatore [void](../../../csharp/language-reference/keywords/void.md).  
  
 Se l'operatore di riferimento indiretto viene applicato a un puntatore [null](../../../csharp/language-reference/keywords/null.md), il risultato dipende dall'implementazione.  
  
## Esempio  
 Nell'esempio riportato di seguito si accede a una variabile di tipo `char` utilizzando puntatori di tipi diversi.  Si noti che l'indirizzo di `theChar` varia da un'esecuzione all'altra, in quanto l'indirizzo fisico allocato a una variabile può subire modifiche.  
  
 [!code-cs[csProgGuidePointers#5](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#5)]  
  
 [!code-cs[csProgGuidePointers#6](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#6)]  
  
  **Valore di theChar \= Z**   
**Indirizzo di theChar \= 12F718**  
**Valore di pChar \= Z**   
**Valore di pInt \= 90**    
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)