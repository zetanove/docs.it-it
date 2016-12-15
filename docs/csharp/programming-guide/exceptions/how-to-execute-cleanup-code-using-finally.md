---
title: "Procedura: eseguire codice di pulitura mediante finally (Guida per programmatori C#) | Microsoft Docs"
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
  - "gestione delle eccezioni [C#], blocco try/finally"
  - "eccezioni [C#], blocco try/finally"
  - "blocchi try/finally [C#]"
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
caps.latest.revision: 21
caps.handback.revision: 21
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: eseguire codice di pulitura mediante finally (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Lo scopo di un'istruzione `finally` è quello di garantire che venga eseguita immediatamente l'opportuna pulitura degli oggetti, in genere quelli che contengono risorse esterne, anche se viene generata un'eccezione.  Un esempio di questo tipo di pulitura consiste nel chiamare <xref:System.IO.Stream.Close%2A> su un oggetto <xref:System.IO.FileStream> immediatamente dopo l'utilizzo anziché attendere che venga sottoposto alla Garbage Collection da Common Language Runtime, come indicato di seguito:  
  
 [!code-cs[csProgGuideExceptions#16](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_1.cs)]  
  
## Esempio  
 Per trasformare il codice precedente in un'istruzione `try-catch-finally`, il codice di pulitura viene separato dal codice effettivo, come indicato di seguito.  
  
 [!code-cs[csProgGuideExceptions#17](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_2.cs)]  
  
 Poiché è possibile che in qualsiasi momento si verifichi un'eccezione all'interno del blocco `try` prima della chiamata `OpenWrite()` o che la chiamata a `OpenWrite()` non riesca, non esiste alcuna garanzia che il file sia aperto quando si tenta di chiuderlo.  Il blocco `finally` aggiunge un controllo per verificare che l'oggetto <xref:System.IO.FileStream> non sia `null` prima della chiamata al metodo <xref:System.IO.Stream.Close%2A>.  Senza il controllo di `null`, il blocco `finally` potrebbe infatti generare un'eccezione specifica <xref:System.NullReferenceException> ma la generazione di eccezioni in blocchi `finally` è da evitare, se possibile.  
  
 Una connessione a un database rappresenta un altro elemento ideale da chiudere in un blocco `finally`.  Poiché il numero di connessioni consentite a un server database è talvolta limitato, è importante chiudere le connessioni il più rapidamente possibile.  Se viene generata un'eccezione prima della chiusura di una connessione, anche in questo caso è preferibile utilizzare il blocco `finally` anziché attendere il processo di Garbage Collection.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)   
 [try\-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try...finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try...catch...finally](../../../csharp/language-reference/keywords/try-catch-finally.md)