---
title: "Creazione e generazione di eccezioni (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
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
  - "intercettazione di eccezioni [C#]"
  - "eccezioni [C#], creazione"
  - "eccezioni [C#], generazione"
  - "generazione di eccezioni [C#]"
ms.assetid: 6bbba495-a115-4c6d-90cc-1f4d7b5f39e2
caps.latest.revision: 28
caps.handback.revision: 28
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Creazione e generazione di eccezioni (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Le eccezioni vengono utilizzate per indicare che si è verificato un errore durante l'esecuzione di un programma.  Gli oggetti eccezione che descrivono un errore vengono creati e quindi *generati* con la parola chiave [throw](../../../csharp/language-reference/keywords/throw.md).  Il runtime ricerca quindi il gestore eccezioni maggiormente compatibile.  
  
 I programmatori devono generare eccezioni se almeno una delle condizioni seguenti è vera:  
  
-   Il metodo non è in grado di completare la funzionalità definita.  
  
     Se ad esempio un parametro di un metodo contiene un valore non valido:  
  
     [!code-cs[csProgGuideExceptions#12](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_1.cs)]  
  
-   Viene effettuata una chiamata non appropriata a un oggetto, in base allo stato di un oggetto.  
  
     Un esempio potrebbe essere la scrittura in un file di sola lettura.  Nei casi in cui lo stato di un oggetto non consente un'operazione, generare un'istanza di <xref:System.InvalidOperationException> o un oggetto basato su una derivazione di questa classe.  Di seguito viene riportato un esempio di un metodo che genera un oggetto <xref:System.InvalidOperationException>:  
  
     [!code-cs[csProgGuideExceptions#13](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_2.cs)]  
  
-   Quando un argomento di un metodo genera un'eccezione.  
  
     In questo caso è necessario intercettare l'eccezione originale e creare un'istanza di <xref:System.ArgumentException>.  L'eccezione originale deve essere passata al costruttore dell'oggetto <xref:System.ArgumentException> come il parametro <xref:System.Exception.InnerException%2A>:  
  
     [!code-cs[csProgGuideExceptions#14](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_3.cs)]  
  
 Le eccezioni contengono una proprietà denominata <xref:System.Exception.StackTrace%2A>.  Questa stringa contiene il nome dei metodi sullo stack di chiamate correnti, oltre al nome del file e al numero di riga in cui è stata generata l'eccezione per ciascun metodo.  Un oggetto <xref:System.Exception.StackTrace%2A> viene creato automaticamente da Common Language Runtime \(CLR\) a partire dal punto dell'istruzione `throw`, quindi le eccezioni devono essere generate a partire dal punto in cui deve iniziare la traccia dello stack.  
  
 Tutte le eccezioni contengono una proprietà denominata <xref:System.Exception.Message%2A>.  Questa stringa deve essere impostata in modo da descrivere il motivo dell'eccezione.  Si noti che nel testo del messaggio non devono essere inserite informazioni riservate.  Oltre a <xref:System.Exception.Message%2A>, <xref:System.ArgumentException> contiene una proprietà denominata <xref:System.ArgumentException.ParamName%2A> che deve essere impostata sul nome dell'argomento che ha causato la generazione dell'eccezione.  Nel caso di un metodo per l'impostazione di proprietà, <xref:System.ArgumentException.ParamName%2A> deve essere impostata su `value`.  
  
 I membri di metodi pubblici e protetti devono generare eccezioni ogni volta che non sono in grado di completare le funzioni previste.  La classe di eccezioni generata deve corrispondere all'eccezione più specifica disponibile che sia adatta alle condizioni di errore.  Queste eccezioni devono essere documentate come parte della funzionalità della classe e le classi derivate o gli aggiornamenti della classe originale devono conservare lo stesso comportamento per la compatibilità con le versioni precedenti.  
  
## Azioni da evitare quando vengono generate le eccezioni  
 Nell'elenco seguente vengono riportate le procedure da evitare quando vengono generate le eccezioni:  
  
-   Le eccezioni non devono essere utilizzate per modificare il flusso di un programma come parte della normale esecuzione.  Le eccezioni devono essere utilizzate solo per segnalare e gestire le condizioni di errore.  
  
-   Le eccezioni non devono essere restituite come valore o parametro restituito anziché essere generate.  
  
-   Non generare intenzionalmente <xref:System.Exception?displayProperty=fullName>, <xref:System.SystemException?displayProperty=fullName>, <xref:System.NullReferenceException?displayProperty=fullName> o <xref:System.IndexOutOfRangeException?displayProperty=fullName> dal codice sorgente personalizzato.  
  
-   Non creare eccezioni che possono essere generate in modalità di debug ma non in modalità di rilascio.  Per identificare gli errori di runtime durante la fase di sviluppo, utilizzare invece il metodo Debug Assert.  
  
## Definizione delle classi di eccezioni  
 I programmi possono generare una classe di eccezioni predefinite disponibile nello spazio dei nomi <xref:System> \(tranne nei casi indicati in precedenza\) oppure creare classi di eccezioni specifiche derivandole da <xref:System.Exception>.  Le classi derivate devono definire almeno quattro costruttori: uno predefinito, uno che imposta la proprietà Message e uno che imposta sia la proprietà <xref:System.Exception.Message%2A> che la proprietà <xref:System.Exception.InnerException%2A>.  Il quarto costruttore viene utilizzato per serializzare l'eccezione.  Le nuove classi di eccezioni devono essere serializzabili.  Di seguito è riportato un esempio:  
  
 [!code-cs[csProgGuideExceptions#15](../../../csharp/programming-guide/exceptions/codesnippet/CSharp/creating-and-throwing-exceptions_4.cs)]  
  
 Le nuove proprietà devono essere aggiunte alla classe di eccezioni solo quando i dati che forniscono sono utili per risolvere l'eccezione.  Se le nuove proprietà vengono aggiunte alla classe di eccezioni derivata, è necessario eseguire l'override di `ToString()` in modo che restituisca le informazioni aggiunte.  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Eccezioni e gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exceptions-and-exception-handling.md)   
 [Gerarchia delle eccezioni](../Topic/Exception%20Hierarchy.md)   
 [Gestione delle eccezioni](../../../csharp/programming-guide/exceptions/exception-handling.md)