---
title: "How to: Write a Simple Parallel.ForEach Loop | Microsoft Docs"
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
  - "foreach, parallel version"
  - "parallel programming, foreach"
ms.assetid: cb5fab92-1c19-499e-ae91-8b7525dd875f
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# How to: Write a Simple Parallel.ForEach Loop
In questo esempio viene mostrato come utilizzare un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> per applicare il parallelismo dei dati su qualsiasi origine dati <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>.  
  
> [!NOTE]
>  Questa documentazione utilizza espressioni lambda per definire delegati in PLINQ.  Se non si ha familiarità con le espressioni lambda in C\# o Visual Basic, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
## Esempio  
 [!code-csharp[TPL_Parallel#03](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/simpleforeach.cs#03)]
 [!code-vb[TPL_Parallel#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/simpleforeach.vb#03)]  
  
 Un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A> funziona come un ciclo <xref:System.Threading.Tasks.Parallel.For%2A>.  La raccolta di origine viene partizionato e il lavoro viene pianificato in più thread in base all'ambiente di sistema.  Quanto maggiore è il numero di processori nel sistema, tanto più veloce sarà l'esecuzione del metodo in parallelo.  Per alcune raccolte di origine, a seconda della dimensione dell'origine e del tipo di lavoro eseguito, è possibile che un ciclo sequenziale sia più veloce.  Per ulteriori informazioni sulle prestazioni, vedere [Potential Pitfalls in Data and Task Parallelism](../../../docs/standard/parallel-programming/potential-pitfalls-in-data-and-task-parallelism.md).  
  
 Per ulteriori informazioni sui cicli paralleli, vedere [How to: Write a Simple Parallel.For Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md).  
  
 Per utilizzare <xref:System.Threading.Tasks.Parallel.ForEach%2A> con una raccolta non generica, è possibile utilizzare il metodo di estensione <xref:System.Linq.Enumerable.Cast%2A> per convertire la raccolta in una raccolta generica, come illustrato nell'esempio seguente:  
  
 [!code-csharp[TPL_Parallel#07](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/nongeneric.cs#07)]
 [!code-vb[TPL_Parallel#07](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/nongeneric.vb#07)]  
  
 È inoltre possibile utilizzare Parallel LINQ \(PLINQ\) per parallelizzare l'elaborazione delle origini dati <xref:System.Collections.Generic.IEnumerable%601>.  PLINQ consente di utilizzare una sintassi di query dichiarativa per esprimere il comportamento dei cicli.  Per ulteriori informazioni, vedere [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## Compilazione del codice  
  
-   Copiare e incollare questo codice in un progetto di applicazione console di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 2010 e premere F5.  
  
-   Aggiungere un riferimento a System.Drawing.dll  
  
-   Premere F5  
  
## Vedere anche  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)   
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)