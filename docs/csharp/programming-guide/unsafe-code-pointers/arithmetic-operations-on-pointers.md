---
title: "Operazioni aritmetiche sui puntatori (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatori [C#], operazioni aritmetiche"
ms.assetid: d4f0b623-827e-45ce-8649-cfcebc8692aa
caps.latest.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 18
---
# Operazioni aritmetiche sui puntatori (Guida per programmatori C#)
In questo argomento viene illustrato l'utilizzo degli operatori aritmetici `+` e **\-** per la gestione dei puntatori.  
  
> [!NOTE]
>  Non è possibile eseguire operazioni aritmetiche su puntatori a void.  
  
## Aggiunta e sottrazione di valori numerici a e da puntatori  
 È possibile aggiungere un valore `n` di tipo [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md) a un puntatore `p`, `` di qualsiasi tipo tranne `void*`.  Il `p+n` restituito è il puntatore risultante dall'aggiunta di `n * sizeof(p) to the address of p`.  Analogamente, `p-n` è il puntatore risultante dalla sottrazione di `n * sizeof(p)` dall'indirizzo di `p`.  
  
## Sottrazione di puntatori  
 È anche possibile sottrarre puntatori dello stesso tipo.  Il risultato è sempre di tipo `long`.  Se, ad esempio, `p1` e `p2` sono puntatori di tipo `pointer-type*`, l'espressione `p1-p2` determinerà il seguente risultato:  
  
 `((long)p1 - (long)p2)/sizeof(pointer_type)`  
  
 Quando l'operazione aritmetica causa un overflow del dominio del puntatore, non vengono generate eccezioni e il risultato dipende dall'implementazione.  
  
## Esempio  
 [!code-cs[csProgGuidePointers#14](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_1.cs)]  
  
 [!code-cs[csProgGuidePointers#15](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/CSharp/arithmetic-operations-on-pointers_2.cs)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Operatori](../../../csharp/language-reference/operators/index.md)   
 [Modifica dei puntatori](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)