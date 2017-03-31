---
title: 'Procedura: Eseguire codice di pulitura mediante istruzione finally (Guida per programmatori C#) | Microsoft Docs'
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- try/finally blocks [C#]
- exceptions [C#], try/finally block
- exception handling [C#], try/finally block
ms.assetid: 1b1e5aef-3f32-4a88-9d39-b5fffb33bdaf
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b9c22ca8ee9c83e6f1808520530c6d1912d8f4f1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-execute-cleanup-code-using-finally-c-programming-guide"></a>Procedura: eseguire codice di pulitura mediante finally (Guida per programmatori C#)
Lo scopo di un'istruzione `finally` consiste nel garantire che la pulizia necessaria di oggetti, in genere oggetti che contengono risorse esterne, venga eseguita immediatamente, anche se viene generata un'eccezione. Un esempio di questo tipo di pulitura è chiamare <xref:System.IO.Stream.Close%2A> su <xref:System.IO.FileStream> immediatamente dopo l'uso, anziché attendere che l'oggetto venga sottoposto a Garbage Collection da Common Language Runtime, come indicato di seguito:  
  
 [!code-cs[csProgGuideExceptions#16](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_1.cs)]  
  
## <a name="example"></a>Esempio  
 Per trasformare il codice precedente in un'istruzione `try-catch-finally`, il codice di pulitura viene separato dal codice di lavoro, come indicato di seguito.  
  
 [!code-cs[csProgGuideExceptions#17](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-execute-cleanup-code-using-finally_2.cs)]  
  
 Poiché può verificarsi un'eccezione in qualsiasi momento all'interno del blocco `try` prima della chiamata a `OpenWrite()`, oppure la chiamata a `OpenWrite()` stessa potrebbe non riuscire, non esiste alcuna garanzia che il file sia aperto quando si tenta di chiuderlo. Il blocco `finally` costituisce un controllo aggiuntivo per assicurarsi che l'oggetto <xref:System.IO.FileStream> non sia `null` prima di chiamare il metodo <xref:System.IO.Stream.Close%2A>. Senza il controllo `null`, il blocco `finally` potrebbe generare la propria eccezione <xref:System.NullReferenceException>, ma la generazione di eccezioni nei blocchi `finally` deve essere evitata laddove possibile.  
  
 Una connessione di database è un altro elemento ideale da chiudere in un blocco `finally`. Poiché il numero di connessioni consentite in un server di database è talvolta limitato, è necessario chiudere le connessioni di database il più rapidamente possibile. Se viene generata un'eccezione prima che la connessione venga chiusa, l'uso del blocco `finally` è preferibile rispetto all'attesa di Garbage Collection.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/index.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)   
 [Istruzione using](../../../csharp/language-reference/keywords/using-statement.md)   
 [try-catch](../../../csharp/language-reference/keywords/try-catch.md)   
 [try-finally](../../../csharp/language-reference/keywords/try-finally.md)   
 [try-catch-finally](../../../csharp/language-reference/keywords/try-catch-finally.md)
