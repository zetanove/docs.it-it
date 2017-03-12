---
title: "Istruzione fixed (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "fixed_CSharpKeyword"
  - "fixed"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "fixed (parola chiave) [C#]"
ms.assetid: 7ea6db08-ad49-4a7a-b934-d8c4acad1c3a
caps.latest.revision: 24
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 24
---
# Istruzione fixed (Riferimenti per C#)
L'istruzione `fixed` impedisce che il Garbage Collector esegua la rilocazione di una variabile mobile.  L'istruzione `fixed` è consentita solo in un contesto di tipo [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  `Fixed` può essere utilizzato anche per creare [buffer di dimensione fissa](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md).  
  
 L'istruzione `fixed` imposta un puntatore a una variabile gestita e blocca quest'ultima durante l'esecuzione dell'istruzione.  Senza l'istruzione `fixed`, i puntatori alle variabili gestite mobili risulterebbero poco utili poiché la procedura di Garbage Collection potrebbe eseguire una rilocazione delle variabili in qualsiasi momento.  Il compilatore C\# consente di assegnare un solo puntatore a una variabile gestita in un'istruzione `fixed`.  
  
 [!code-cs[csrefKeywordsFixedLock#1](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#1)]  
  
 È possibile inizializzare un puntatore utilizzando una matrice, una stringa, un buffer a dimensione fissa o l'indirizzo di una variabile.  Nell'esempio riportato di seguito viene illustrato l'utilizzo di indirizzi, matrici e stringhe variabili.  Per ulteriori informazioni sui buffer di dimensioni fisse, vedere [Buffer a dimensione fissa](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md).  
  
 [!code-cs[csrefKeywordsFixedLock#2](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#2)]  
  
 È possibile inizializzare più puntatori purché siano tutti dello stesso tipo, ad esempio.  
  
```  
fixed (byte* ps = srcarray, pd = dstarray) {...}  
```  
  
 Per inizializzare i puntatori di tipi diversi, annidare semplicemente le istruzioni `fixed` come illustrato nell'esempio seguente.  
  
 [!code-cs[csrefKeywordsFixedLock#3](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#3)]  
  
 Dopo l'esecuzione del codice nell'istruzione, tutte le variabili bloccate vengono sbloccate e sottoposte alla procedura di Garbage Collection.  Di conseguenza, evitare di puntare a quelle variabili esterne all'istruzione `fixed`.  
  
> [!NOTE]
>  I puntatori inizializzati nelle istruzioni fixed non possono essere modificati.  
  
 In modalità non protetta, è possibile allocare memoria nello stack, che non è necessario bloccare perché lo stack non viene sottoposto alla procedura di Garbage Collection.  Per ulteriori informazioni, vedere [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md).  
  
## Esempio  
 [!code-cs[csrefKeywordsFixedLock#4](../../../csharp/language-reference/keywords/codesnippet/csharp/csrefFixedLock/csrefKeywordsFixedLock.cs#4)]  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [non protette](../../../csharp/language-reference/keywords/unsafe.md)   
 [Buffer a dimensione fissa](../../../csharp/programming-guide/unsafe-code-pointers/fixed-size-buffers.md)