---
title: Utilizzo di eccezioni (Guida per programmatori C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- exception handling [C#], about exception handling
- exceptions [C#], about exceptions
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
caps.latest.revision: 15
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
ms.translationtype: Human Translation
ms.sourcegitcommit: a5ed524a1b17f7be8903f998cbd732594faab831
ms.openlocfilehash: a8c29002ae2287df60996ed2b23068eec1e2739b
ms.contentlocale: it-it
ms.lasthandoff: 05/15/2017

---
# <a name="using-exceptions-c-programming-guide"></a>Utilizzo di eccezioni (Guida per programmatori C#)
In C# gli errori del programma in fase di esecuzione vengono propagati attraverso il programma usando il meccanismo delle eccezioni. Le eccezioni vengono generate dal codice che rileva un errore e intercettate dal codice in grado di correggere l'errore. Le eccezioni possono essere generate da Common Language Runtime (CLR) in .NET Framework o dal codice in un programma. Quando viene generata un'eccezione, si propaga nello stack di chiamate finché non viene trovata un'istruzione `catch` per l'eccezione. Le eccezioni non rilevate vengono gestite da un gestore di eccezioni generico del sistema che visualizza una finestra di dialogo.  
  
 Le eccezioni sono rappresentate dalle classi derivate da <xref:System.Exception>. Questa classe identifica il tipo di eccezione e contiene proprietà con informazioni sull'eccezione. Generare un'eccezione implica la creazione un'istanza di una classe derivata dall'eccezione, la configurazione, se necessaria, delle proprietà dell'eccezione e la generazione dell'oggetto usando la parola chiave `throw`. Ad esempio:  
  
 [!code-cs[csProgGuideExceptions#1](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_1.cs)]  
  
 Dopo la generazione di un'eccezione, il runtime controlla l'istruzione corrente per verificare se si trova all'interno di un blocco `try`. In questo caso tutti i blocchi `catch` associati al blocco `try` vengono controllati per verificare se è possibile intercettare l'eccezione. I blocchi `Catch` normalmente specificano i tipi di eccezione. Se il tipo del blocco `catch` è lo stesso tipo dell'eccezione o di una classe di base dell'eccezione, il blocco `catch` può gestire il metodo. Ad esempio:  
  
 [!code-cs[csProgGuideExceptions#2](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_2.cs)]  
  
 Se l'istruzione che genera un'eccezione non è in un blocco `try` oppure se il blocco `try` che la contiene non corrisponde ad alcun blocco `catch`, il runtime controlla il metodo di chiamata per un'istruzione `try` e i blocchi `catch`. Il runtime continua a risalire lo stack di chiamate alla ricerca di un blocco `catch` compatibile. Quando il blocco `catch` viene trovato ed eseguito, il controllo passa all'istruzione successiva dopo quel blocco `catch`.  
  
 Un'istruzione `try` può contenere più di un blocco `catch`. Viene eseguita la prima istruzione `catch` in grado di gestire l'eccezione ed eventuali istruzioni`catch` successive, anche se compatibili, vengono ignorate. Di conseguenza, i blocchi catch devono sempre essere ordinati dal più specifico, o più derivato, al meno specifico. Ad esempio:  
  
 [!code-cs[csProgGuideExceptions#3](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_3.cs)]  
  
 Prima dell'esecuzione del blocco `catch` il runtime cerca i blocchi `finally`. I blocchi `Finally` consentono al programmatore di eliminare eventuali stati ambigui che possono essere rimasti dopo un blocco `try` interrotto o di rilasciare eventuali risorse esterne, ad esempio handle di grafica, connessioni al database o flussi di file, senza attendere che il Garbage Collector del runtime finalizzi gli oggetti. Ad esempio:  
  
 [!code-cs[csProgGuideExceptions#4](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/using-exceptions_4.cs)]  
  
 Se `WriteByte()` ha generato un'eccezione, il codice nel secondo blocco `try` che tenti di riaprire il file avrebbe esito negativo se non viene chiamata `file.Close()` e il file rimarrebbe bloccato. Poiché i blocchi `finally` vengono eseguiti anche se viene generata un'eccezione, il blocco `finally` dell'esempio precedente consente di chiudere correttamente il file e di evitare un errore.  
  
 Se non viene trovato alcun blocco `catch` compatibile nello stack di chiamate dopo la generazione di un'eccezione, si verifica una delle tre situazioni seguenti:  
  
-   Se l'eccezione è all'interno di un finalizzatore, il finalizzatore viene interrotto e viene chiamato il finalizzatore di base, se presente.  
  
-   Se lo stack di chiamate contiene un costruttore statico o un inizializzatore di campo statico, viene generata <xref:System.TypeInitializationException> con l'eccezione originale assegnata alla proprietà <xref:System.Exception.InnerException%2A> della nuova eccezione.  
  
-   Se viene raggiunto l'inizio del thread, il thread viene terminato.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/index.md)
