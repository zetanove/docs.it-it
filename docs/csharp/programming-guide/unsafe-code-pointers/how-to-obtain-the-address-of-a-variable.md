---
title: "Procedura: ottenere l&#39;indirizzo di una variabile (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatore (espressioni) [C#], address-of (operatore)"
  - "puntatori [C#], & (operatore)"
  - "variabili [C#], address-of."
ms.assetid: 44fe2cd9-a64f-4ef5-be2a-09ce807c0182
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: ottenere l&#39;indirizzo di una variabile (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Per ottenere l'indirizzo di un'espressione unaria, che restituisce una variabile fissa, utilizzare l'operatore address\-of:  
  
```  
int number;  
int* p = &number; //address-of operator &  
```  
  
 L'operatore address\-of può essere applicato solo a una variabile.  Se la variabile è spostabile, è possibile utilizzare l' [istruzione fissa](../../../csharp/language-reference/keywords/fixed-statement.md) per correggere temporaneamente la variabile prima di ottenerne l'indirizzo.  
  
 È compito del programmatore garantire che la variabile venga inizializzata.  Il compilatore non genererà un messaggio di errore se la variabile non è inizializzata.  
  
 Non è possibile ottenere l'indirizzo di una costante o di un valore.  
  
## Esempio  
 In questo esempio viene dichiarato un puntatore a `int`, `p`, a cui viene assegnato l'indirizzo di una variabile integer `number`.  La variabile `number` viene inizializzata in seguito all'assegnazione a \*p.  Se si trasforma l'istruzione di assegnazione in un commento, verrà rimossa l'inizializzazione della variabile `number`, ma non verrà generato alcun errore in fase di compilazione.  Si noti l'utilizzo dell'operatore di [accesso ai membri](../../../csharp/programming-guide/unsafe-code-pointers/how-to-access-a-member-with-a-pointer.md) `->` per ottenere e visualizzare l'indirizzo archiviato nel puntatore.  
  
 [!code-cs[csProgGuidePointers#7](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-obtain-the-address-of-a-variable_1.cs)]  
  
 [!code-cs[csProgGuidePointers#8](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-obtain-the-address-of-a-variable_2.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)