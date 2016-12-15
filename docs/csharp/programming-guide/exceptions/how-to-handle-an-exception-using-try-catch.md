---
title: "Procedura: gestire un&#39;eccezione utilizzando Try/Catch (Guida per programmatori C#) | Microsoft Docs"
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
  - "gestione delle eccezioni [C#], blocchi try/catch"
  - "eccezioni [C#], blocchi try/catch"
  - "try/catch (blocchi) [C#]"
ms.assetid: ca8e3773-980e-4767-8633-7408540e9818
caps.latest.revision: 14
caps.handback.revision: 14
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Procedura: gestire un&#39;eccezione utilizzando Try/Catch (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Lo scopo di un blocco [try\-catch](../../../csharp/language-reference/keywords/try-catch.md) è di intercettare e gestire un'eccezione generata da codice effettivo.  Alcune eccezioni possono essere gestite in un blocco `catch` e il problema viene risolto senza generare di nuovo l'eccezione. Molto spesso, tuttavia, è possibile solo assicurarsi che venga generata l'eccezione appropriata.  
  
## Esempio  
 In questo esempio, <xref:System.IndexOutOfRangeException> non è l'eccezione più appropriata. <xref:System.ArgumentOutOfRangeException> è più adatta al metodo perché l'errore è causato dall'argomento `index` passato dal chiamante.  
  
 [!code-cs[csProgGuideExceptions#5](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/how-to-handle-an-exception-using-try-catch_1.cs)]  
  
## Commenti  
 Il codice che genera un'eccezione è racchiuso nel blocco `try`.  Subito dopo viene aggiunta un'istruzione `catch` per gestire l'eventuale `IndexOutOfRangeException`.  Il blocco `catch` gestisce l'eccezione `IndexOutOfRangeException` e genera l'eccezione `ArgumentOutOfRangeException` più appropriata.  Per fornire al chiamante le maggiori informazioni possibili, specificare l'eccezione originale come proprietà <xref:System.Exception.InnerException%2A> della nuova eccezione.  Poiché la proprietà <xref:System.Exception.InnerException%2A> è [readonly](../../../csharp/language-reference/keywords/readonly.md), è necessario assegnarla nel costruttore della nuova eccezione.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)