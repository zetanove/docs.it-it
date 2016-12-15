---
title: "Procedura: incrementare e decrementare i puntatori (Guida per programmatori C#) | Microsoft Docs"
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
  - "puntatore (espressioni) [C#], incremento e decremento"
  - "puntatori [C#], incremento e decremento"
ms.assetid: 1b8b9281-44ee-485a-9045-3db38a4b4b89
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: incrementare e decrementare i puntatori (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli operatori di incremento e decremento `++` e `--` consentono di modificare la posizione del puntatore in base a [sizeof](../../../csharp/language-reference/keywords/sizeof.md) \(`pointer-type`\), nel caso di un puntatore di tipo pointer\-type\*.  Il formato delle espressioni di incremento e decremento è il seguente:  
  
```  
++p;  
p++;  
--p;  
p--;  
```  
  
 È possibile applicare gli operatori di incremento e decremento ai puntatori di qualsiasi tipo, ad eccezione del tipo `void*`.  
  
 Quando si applica l'operatore di incremento a un puntatore di tipo `pointer-type`, [sizeof](../../../csharp/language-reference/keywords/sizeof.md) \(`pointer-type`\) viene aggiunto all'indirizzo contenuto nella variabile del puntatore.  
  
 Quando si applica l'operatore di decremento a un puntatore di tipo `pointer-type`, `sizeof` \(`pointer-type`\) viene sottratto dall'indirizzo contenuto nella variabile del puntatore.  
  
 Quando l'operazione causa un overflow del dominio del puntatore, non vengono generate eccezioni e il risultato dipende dall'implementazione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come passare da un elemento di una matrice all'altro incrementando il puntatore della dimensione di `int`.  A ogni passaggio verranno visualizzati l'indirizzo e il contenuto dell'elemento della matrice.  
  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-increment-and-decrement-pointers_1.cs)]  
  
 [!code-cs[csProgGuidePointers#13](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/how-to-increment-and-decrement-pointers_2.cs)]  
  
  **Valore: 0 @ indirizzo 12860272**  
**Valore: 1 @ indirizzo: 12860276**  
**Valore: 2 @ indirizzo: 12860280**  
**Valore: 3 @ indirizzo: 12860284**  
**Valore: 4 @ indirizzo 12860288**   
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Modifica dei puntatori](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)