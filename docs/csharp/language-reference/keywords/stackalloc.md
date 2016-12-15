---
title: "stackalloc (Riferimenti per C#) | Microsoft Docs"
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
  - "stackalloc_CSharpKeyword"
  - "stackalloc"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "stackalloc (parola chiave) [C#]"
ms.assetid: adc04c28-3ed2-4326-807a-7545df92b852
caps.latest.revision: 27
caps.handback.revision: 27
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# stackalloc (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La parola chiave `stackalloc` viene utilizzata in un contesto di codice unsafe per allocare un blocco di memoria nello stack.  
  
```  
int* block = stackalloc int[100];  
```  
  
## Note  
 La parola chiave è valida solo per gli inizializzatori di variabili locali.  Il codice seguente causa errori di compilazione.  
  
```  
int* block;  
// The following assignment statement causes compiler errors. You  
// can use stackalloc only when declaring and initializing a local   
// variable.  
block = stackalloc int[100];  
```  
  
 Poiché vengono utilizzati tipi puntatore, `stackalloc` richiede un contesto [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  Per ulteriori informazioni, vedere [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md).  
  
 La parola chiave `stackalloc` è simile a [\_alloca](/visual-cpp/c-runtime-library/reference/alloca) nella libreria di runtime del linguaggio C.  
  
 Nell'esempio riportato di seguito vengono calcolati e visualizzati i primi 20 numeri della sequenza di Fibonacci.  Ogni numero corrisponde alla somma dei due numeri precedenti.  Nel codice, un blocco di memoria di dimensioni sufficienti a contenere 20 elementi di tipo `int` viene allocato nello stack, non nell'heap.  L'indirizzo del blocco è archiviato nel puntatore `fib`.  Questa memoria non viene sottoposta alla procedura di Garbage Collection e non deve pertanto essere bloccata tramite [fixed](../../../csharp/language-reference/keywords/fixed-statement.md).  La durata del blocco di memoria è limitata alla durata del metodo che lo definisce.  Non è possibile liberare la memoria prima della restituzione del metodo.  
  
## Esempio  
 [!code-cs[csrefKeywordsOperator#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/stackalloc_1.cs)]  
  
## Sicurezza  
 Il codice unsafe è per definizione meno sicuro delle alternative sicure.  Tuttavia, l'utilizzo di `stackalloc` attiva automaticamente le funzionalità di rilevazione del sovraccarico del buffer in Common Language Runtime \(CLR\).  Se viene rilevato un sovraccarico del buffer, il processo viene terminato il più rapidamente possibile per ridurre al minimo la possibilità che venga eseguito codice dannoso.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Parole chiave per operatori](../../../csharp/language-reference/keywords/operator-keywords.md)   
 [Codice unsafe e puntatori](../../../csharp/programming-guide/unsafe-code-pointers/index.md)