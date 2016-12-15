---
title: "throw (Riferimenti per C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "throw"
  - "throw_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "throw (parola chiave) [C#]"
  - "throw (istruzione) [C#]"
ms.assetid: 5ac4feef-4b1a-4c61-aeb4-61d549e5dd42
caps.latest.revision: 22
caps.handback.revision: 22
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# throw (Riferimenti per C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'istruzione `throw` viene utilizzata per segnalare la presenza di una situazione anomala, denominata eccezione, durante l'esecuzione di un programma.  
  
## Note  
 L'eccezione generata è un oggetto la cui classe è derivata da <xref:System.Exception?displayProperty=fullName>, come illustrato nell'esempio seguente.  
  
```  
class MyException : System.Exception {}  
// ...  
throw new MyException();  
```  
  
 L'istruzione `throw` è in genere utilizzata insieme all'istruzione `try-catch` o `try-finally`.  Un'istruzione [throw](../../../csharp/language-reference/keywords/throw.md) può essere utilizzata in un blocco `catch` per rigenerare l'eccezione intercettata dal blocco `catch`.  In questo caso, l'istruzione [throw](../../../csharp/language-reference/keywords/throw.md) non accetta un operando di eccezione.  Per ulteriori informazioni ed esempi, vedere [try\-catch](../../../csharp/language-reference/keywords/try-catch.md) e [Procedura: generare eccezioni in modo esplicito](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md).  
  
## Esempio  
 In questo esempio viene illustrato come generare un'eccezione utilizzando l'istruzione `throw`.  
  
 [!code-cs[csrefKeywordsExceptions#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/throw_1.cs)]  
  
## Esempio di codice  
 Vedere gli esempi in [try\-catch](../../../csharp/language-reference/keywords/try-catch.md) e [Procedura: generare eccezioni in modo esplicito](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md).  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Riferimenti per C\#](../../../csharp/language-reference/index.md)   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [Istruzioni try, catch e throw in C\+\+](../../../csharp/language-reference/keywords/try-catch.md)   
 [Parole chiave di C\#](../../../csharp/language-reference/keywords/index.md)   
 [Istruzioni di gestione delle eccezioni](../../../csharp/language-reference/keywords/exception-handling-statements.md)   
 [Procedura: generare eccezioni in modo esplicito](../Topic/How%20to:%20Explicitly%20Throw%20Exceptions.md)