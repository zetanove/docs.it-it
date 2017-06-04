---
title: "How to: Use Parallel.Invoke to Execute Parallel Operations | Microsoft Docs"
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
  - "task parallelism in .NET"
  - "parallel programming, task parallelism"
ms.assetid: 6b3ecd79-dec9-4ce1-abf4-62e5392a59c6
caps.latest.revision: 22
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# How to: Use Parallel.Invoke to Execute Parallel Operations
Questo esempio mostra come parallelizzare le operazioni usando <xref:System.Threading.Tasks.Parallel.Invoke%2A> in Task Parallel Library.  Vengono eseguite tre operazioni in un'origine dati condivisa.  Poiché nessuna delle operazioni modifica l'origine, possono essere eseguite in parallelo in modo semplice.  
  
> [!NOTE]
>  Questa documentazione usa espressioni lambda per definire delegati in TPL.  Se non si ha familiarità con le espressioni lambda in C\# o Visual Basic, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## Esempio  
 [!code-csharp[TPL_Parallel#06](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallelinvoke.cs#06)]
 [!code-vb[TPL_Parallel#06](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/parallelinvoke.vb#06)]  
  
 Si noti che con <xref:System.Threading.Tasks.Parallel.Invoke%2A>, basta indicare le azioni che si desidera eseguire simultaneamente e il runtime gestisce tutti i dettagli di pianificazione dei thread, tra cui l'adattamento automatico al numero di core nel computer host.  
  
 Questo esempio parallelizza le operazioni, ma non i dati.  Come approccio alternativo, è possibile parallelizzare le query LINQ usando PLINQ ed eseguire le query in sequenza.  In alternativa, è possibile parallelizzare i dati usando PLINQ.  Un'altra possibilità consiste nel parallelizzare sia le query che le attività.  Anche se il sovraccarico risultante potrebbe comportare problemi di prestazioni nei computer host con un numero relativamente basso di processori, la scalabilità sarebbe decisamente migliore nei computer con molti processori.  
  
## Compilazione del codice  
  
-   Copiare e incollare l'esempio completo in un progetto di Microsoft Visual Studio 2010 e premere F5.  
  
## Vedere anche  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [How to: Wait on One or More Tasks to Complete](../Topic/How%20to:%20Wait%20on%20One%20or%20More%20Tasks%20to%20Complete.md)   
 [How to: Cancel a Task and Its Children](../../../docs/standard/parallel-programming/how-to-cancel-a-task-and-its-children.md)   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)