---
title: "try...finally (Riferimenti per C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "finally"
  - "finally_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "finally (parola chiave) [C#]"
  - "try-finally (istruzioni) [C#]"
ms.assetid: c27623fb-7261-4464-862c-7a369d3c8f0a
caps.latest.revision: 25
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 25
---
# try...finally (Riferimenti per C#)
Utilizzando un blocco `finally`, è possibile liberare le risorse allocate in un blocco [try](../../../csharp/language-reference/keywords/try-catch.md), quindi eseguire il codice anche se viene generata un'eccezione in tale blocco `try`.  In genere, le istruzioni di un blocco `finally` vengono eseguite quando il controllo lascia un'istruzione `try`.  Il trasferimento di controllo può verificarsi come risultato della normale esecuzione, dell'esecuzione di un'istruzione `break`, `continue`, `goto` o `return` o della propagazione di un'eccezione al di fuori dell'istruzione `try`.  
  
 In un'eccezione gestita, il blocco `finally` associato viene sicuramente eseguito.  Tuttavia, se l'eccezione non è gestita, l'esecuzione del blocco `finally` dipende da come viene attivata l'operazione di rimozione eccezione.  Questa, a sua volta, dipende dalla configurazione del computer.  Per ulteriori informazioni, vedere [Elaborazione delle eccezioni non gestite in CRL](http://go.microsoft.com/fwlink/?LinkId=128371).  
  
 In genere, quando un'eccezione non gestita termina un'applicazione, che il blocco `finally` sia eseguito o meno non è importante.  Tuttavia, se si dispone di istruzioni in un blocco `finally` che devono essere eseguite anche in tale situazione, una soluzione è di aggiungere un blocco `catch` all'istruzione `try`\-`finally`.  In alternativa, è possibile rilevare l'eccezione che può essere generata nel blocco `try` di un'istruzione `try`\-`finally` collocata nella parte superiore dello stack di chiamate.  È possibile rilevare l'eccezione nel metodo che chiama il metodo contenente l'istruzione `try`\-`finally` o nel metodo che chiama quel metodo o in qualsiasi metodo dello stack di chiamate.  Se l'eccezione non viene rilevata, l'esecuzione del blocco `finally` dipende dall'attivazione o meno da parte del sistema operativo dell'operazione di rimozione eccezione.  
  
## Esempio  
 In questo esempio un'istruzione di conversione non valida genera un'eccezione `System.InvalidCastException`.  L'eccezione non è gestita.  
  
 [!code-cs[csrefKeywordsExceptions#4](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-finally_1.cs)]  
  
 Nell'esempio seguente, viene rilevata un'eccezione dal metodo `TryCast` in un metodo allocato nello stack di chiamata.  
  
 [!code-cs[csrefKeywordsExceptions#6](../../../csharp/language-reference/keywords/codesnippet/CSharp/try-finally_2.cs)]  
  
 Per ulteriori informazioni su `finally`, vedere [try\-catch\-finally](../../../csharp/language-reference/keywords/try-catch-finally.md).  
  
 C\# contiene anche l'[istruzione using](../../../csharp/language-reference/keywords/using-statement.md), la quale fornisce una funzionalità simili per gli oggetti <xref:System.IDisposable> con sintassi di facile utilizzo.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec-md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni try, throw e catch \(C\+\+\)](/visual-cpp/cpp/try-throw-and-catch-statements-cpp)   
 [Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [throw](../../../csharp/language-reference/keywords/throw.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [Procedura: generare eccezioni in modo esplicito](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)