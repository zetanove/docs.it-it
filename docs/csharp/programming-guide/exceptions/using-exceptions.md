---
title: "Utilizzo di eccezioni (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "gestione delle eccezioni [C#], informazioni sulla gestione delle eccezioni"
  - "eccezioni [C#], informazioni"
ms.assetid: 71472c62-320a-470a-97d2-67995180389d
caps.latest.revision: 15
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 15
---
# Utilizzo di eccezioni (Guida per programmatori C#)
In C\# gli errori che si verificano nel programma in fase di esecuzione vengono propagati mediante il meccanismo delle eccezioni.  Le eccezioni vengono generate dal codice che riscontra un errore e intercettate dal codice che è in grado di correggere l'errore.  Le eccezioni possono essere generate da Common Language Runtime \(CLR\) di .NET Framework oppure dal codice di un programma.  Una volta generata, l'eccezione si propaga nello stack di chiamate finché non viene individuata un'istruzione `catch`.  Le eccezioni non intercettate vengono gestite da un gestore eccezioni generico fornito dal sistema, che visualizza una finestra di dialogo.  
  
 Le eccezioni sono rappresentate da classi derivate da <xref:System.Exception>.  Questa classe identifica il tipo di eccezione e contiene le proprietà con i dettagli relativi all'eccezione.  La generazione di un'eccezione implica la creazione di un'istanza di una classe derivata dall'eccezione, la configurazione facoltativa delle proprietà dell'eccezione e la generazione dell'oggetto con la parola chiave `throw`.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideExceptions#1](../../../csharp/programming-guide/exceptions/codesnippet/csharp/using-exceptions_1.cs)]  
  
 Dopo la generazione di un'eccezione, il runtime controlla l'istruzione corrente per verificare se si trova all'interno di un blocco `try`.  In caso affermativo, gli eventuali blocchi `catch` associati al blocco `try` vengono controllati per verificare se sono in grado di intercettare l'eccezione.  I blocchi `Catch` specificano i tipi di eccezione; se il tipo del blocco `catch` è identico a quello dell'eccezione o è una classe base dell'eccezione, il blocco `catch` è in grado di gestire il metodo.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideExceptions#2](../../../csharp/programming-guide/exceptions/codesnippet/csharp/using-exceptions_2.cs)]  
  
 Se l'istruzione che genera un'eccezione non si trova all'interno di un blocco `try` oppure se il blocco `try` che la racchiude non ha alcun blocco `catch` corrispondente, il runtime controlla il metodo chiamante per verificare la presenza di un'istruzione `try` e di blocchi `catch`.  Il runtime risale lo stack di chiamate, alla ricerca di un blocco `catch` compatibile.  Quando il blocco `catch` viene individuato ed eseguito, il controllo viene passato all'istruzione successiva dopo tale blocco `catch`.  
  
 Un'istruzione `try` può contenere più di un blocco `catch`.  La prima istruzione `catch` in grado di gestire l'eccezione viene eseguita. Le eventuali istruzioni `catch` seguenti, anche se compatibili, vengono ignorate.  Pertanto i blocchi catch dovrebbero sempre essere ordinati dal più specifico \(o più derivato\) al meno specifico.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideExceptions#3](../../../csharp/programming-guide/exceptions/codesnippet/csharp/using-exceptions_3.cs)]  
  
 Prima che venga eseguito il blocco `catch` il runtime verifica i blocchi `finally`.  I blocchi `Finally` consentono al programmatore di pulire qualsiasi stato ambiguo eventualmente rimasto da un blocco `try` interrotto o di rilasciare le risorse esterne \(ad esempio handle grafici, connessioni al database o flussi di file\) senza aspettare la finalizzazione degli oggetti da parte del Garbage Collector in fase di esecuzione.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideExceptions#4](../../../csharp/programming-guide/exceptions/codesnippet/csharp/using-exceptions_4.cs)]  
  
 Se `WriteByte()` ha generato un'eccezione, il tentativo di riaprire il file da parte del codice nel secondo blocco `try` avrà esito negativo se non si chiama `file.Close()` e il file rimarrà bloccato.  Poiché i blocchi `finally` vengono eseguiti indipendentemente dal fatto che venga o meno generata un'eccezione, il blocco `finally` dell'esempio precedente consente di chiudere il file correttamente e di evitare errori.  
  
 Se nello stack di chiamate non viene individuato alcun blocco `catch` compatibile dopo la generazione di un'eccezione, si verifica una delle tre situazioni seguenti:  
  
-   Se l'eccezione si trova all'interno di un distruttore, quest'ultimo verrà interrotto e verrà chiamato l'eventuale distruttore base.  
  
-   Se lo stack di chiamate contiene un costruttore statico oppure un inizializzatore di un campo statico, verrà generata un'eccezione <xref:System.TypeInitializationException> e l'eccezione originale verrà assegnata alla proprietà <xref:System.Exception.InnerException%2A> della nuova eccezione.  
  
-   Se si raggiunge l'inizio del thread, quest'ultimo verrà terminato.  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)