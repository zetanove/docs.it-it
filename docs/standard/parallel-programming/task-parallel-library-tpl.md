---
title: "Task Parallel Library (TPL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET, concurrency in"
  - ".NET, parallel programming in"
  - "Parallel Programming"
ms.assetid: b8f99f43-9104-45fd-9bff-385a20488a23
caps.latest.revision: 37
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 37
---
# Task Parallel Library (TPL)
La libreria Task Parallel Library \(TPL\) è un set di tipi e API pubblici negli spazi dei nomi <xref:System.Threading?displayProperty=fullName> e <xref:System.Threading.Tasks?displayProperty=fullName>.  Lo scopo di TPL è di rendere gli sviluppatori più produttivi mediante la semplificazione del processo di aggiunta di parallelismo e concorrenza alle applicazioni.  La libreria TPL ridimensiona il grado di concorrenza dinamicamente per utilizzare in modo efficace tutti i processori disponibili.  La libreria TPL gestisce inoltre il partizionamento del lavoro, la pianificazione dei thread in <xref:System.Threading.ThreadPool>, il supporto per l'annullamento, la gestione dello stato e altri dettagli di basso livello.  Quando si utilizza TPL, è possibile ottimizzare le prestazioni del codice concentrandosi sulle operazioni per cui il programma è stato progettato.  
  
 A partire da [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], TPL è la modalità preferita per scrivere il codice multithreading e parallelo.  Tuttavia, non tutto il codice è adatto per la parallelizzazione; ad esempio, se un ciclo esegue solo una piccola parte di lavoro in ciascuna iterazione o non viene eseguito per molte iterazioni, il sovraccarico della parallelizzazione potrebbe provocare un rallentamento dell'esecuzione del codice.  Inoltre, la parallelizzazione come qualsiasi codice multithreading, aggiunge complessità all'esecuzione del programma.  Benché la libreria TPL semplifichi gli scenari multithreading, è consigliabile avere una conoscenza di base dei concetti relativi all'utilizzo dei thread, ad esempio blocchi, deadlock e race condition. Infatti, ciò consentirà di utilizzare la libreria TPL in modo più efficace.  
  
## Argomenti correlati  
  
|||  
|-|-|  
|Titolo|Descrizione|  
|[Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)|Viene descritto come creare cicli `for` e `foreach` paralleli \(`For` e `For Each` in Visual Basic\).|  
|[Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)|Viene descritto come creare ed eseguire attività tramite <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=fullName> in modo implicito o direttamente tramite oggetti <xref:System.Threading.Tasks.Task> in modo esplicito.|  
|[Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)|Viene descritto come utilizzare i componenti del flusso di dati nella libreria del flusso di dati TPL per gestire più operazioni che devono comunicare tra loro o elaborare dati man mano che diventano disponibili.|  
|[Using TPL with Other Asynchronous Patterns](../../../docs/standard/parallel-programming/using-tpl-with-other-asynchronous-patterns.md)|Viene descritto come utilizzare TPL con altri modelli asincroni in .NET|  
|[Potential Pitfalls in Data and Task Parallelism](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md)|Vengono descritti alcuni problemi comuni e il modo per evitarli.|  
|[Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)|Viene descritto come realizzare il parallelismo dei dati con le query LINQ.|  
|[Parallel Programming](../../../docs/standard/parallel-programming/index.md)|Nodo di livello superiore per la programmazione parallela di .NET.|  
  
## Vedere anche  
 [Esempi di programmazione parallela con .NET Framework](http://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)