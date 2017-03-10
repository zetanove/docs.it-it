---
title: "Conversioni di puntatori (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "puntatori [C#], conversioni"
ms.assetid: f0e87502-477a-4ede-a31f-7a3e262e46fb
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Conversioni di puntatori (Guida per programmatori C#)
Nella tabella che segue sono illustrate le conversioni di puntatori implicite già definite.  Le conversioni implicite possono avere luogo in numerose situazioni, incluse le chiamate a metodi e le istruzioni di assegnazione.  
  
## Conversioni di puntatori implicite  
  
|Da|Per|  
|--------|---------|  
|Qualsiasi tipo di puntatore|void\*|  
|null|Qualsiasi tipo di puntatore|  
  
 La conversione di puntatori esplicita consente di eseguire conversioni in puntatori per i quali non esiste alcuna conversione implicita, utilizzando un'espressione cast.  Tali conversioni sono illustrate nella tabella che segue.  
  
## Conversioni di puntatori esplicite  
  
|Da|Per|  
|--------|---------|  
|Qualsiasi tipo di puntatore|Qualsiasi altro tipo di puntatore|  
|sbyte, byte, short, ushort, int, uint, long oppure ulong|Qualsiasi tipo di puntatore|  
|Qualsiasi tipo di puntatore|sbyte, byte, short, ushort, int, uint, long oppure ulong|  
  
## Esempio  
 Nell'esempio riportato di seguito un puntatore a `int` viene convertito in un puntatore a `byte`.  Si noti che il puntatore punta al byte della variabile con l'indirizzo più basso.  Quando si incrementa successivamente il risultato, fino a raggiungere la dimensione di `int` \(4 byte\), è possibile visualizzare i byte rimanenti della variabile.  
  
 [!code-cs[csProgGuidePointers#3](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers2.cs#3)]  
  
 [!code-cs[csProgGuidePointers#4](../../../csharp/programming-guide/unsafe-code-pointers/codesnippet/csharp/Pointers/Pointers.cs#4)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni puntatore](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)   
 [Tipi di puntatori](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)   
 [Tipi](../../../csharp/language-reference/keywords/types.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Istruzione fixed](../../../csharp/language-reference/keywords/fixed-statement.md)   
 [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)