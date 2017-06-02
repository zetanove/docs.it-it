---
title: "Data Parallelism (Task Parallel Library) | Microsoft Docs"
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
  - "parallelism, data"
ms.assetid: 3f05f33f-f1da-4b16-81c2-9ceff1bef449
caps.latest.revision: 25
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 25
---
# Data Parallelism (Task Parallel Library)
Con l'espressione *parallelismo dei dati* ci si riferisce a scenari in cui la stessa operazione viene eseguita contemporaneamente \(ovvero in parallelo\) sugli elementi di una matrice o una raccolta di origine.  Nelle operazioni in parallelo su dati la raccolta di origine viene suddivisa in partizioni in modo che più thread possano agire simultaneamente su segmenti diversi.  
  
 La libreria Task Parallel Library \(TPL\) supporta il parallelismo dei dati tramite la classe <xref:System.Threading.Tasks.Parallel?displayProperty=fullName>.  Questa classe fornisce le implementazioni in parallelo basate su metodo dei cicli [for](../Topic/for%20\(C%23%20Reference\).md) e [foreach](../Topic/foreach,%20in%20\(C%23%20Reference\).md) \(`For`  e `For Each` in Visual Basic\).  La scrittura della logica di un ciclo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> o <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> è molto simile a quella della logica di un ciclo sequenziale.  Non è necessario creare thread o accodare elementi di lavoro.  Nei cicli di base non è necessario acquisire blocchi.  La libreria TPL gestisce automaticamente tutto il lavoro di basso livello.  Per informazioni dettagliate sull'uso di <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName>, scaricare il documento [Modelli di programmazione parallela: Comprendere e applicare modelli paralleli con .NET Framework 4](http://www.microsoft.com/download/details.aspx?id=19222).  L'esempio di codice seguente mostra un ciclo `foreach` semplice e il relativo equivalente parallelo.  
  
> [!NOTE]
>  Questa documentazione usa espressioni lambda per definire delegati in TPL.  Se non si ha familiarità con le espressioni lambda in C\# o Visual Basic, vedere [Lambda Expressions in PLINQ and TPL](../../../docs/standard/parallel-programming/lambda-expressions-in-plinq-and-tpl.md).  
  
 [!code-csharp[TPL#20](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#20)]
 [!code-vb[TPL#20](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/tpl_vb.vb#20)]  
  
 Quando viene eseguito un ciclo parallelo, la libreria TPL esegue il partizionamento dell'origine dati in modo che il ciclo possa agire simultaneamente su più parti.  L'utilità di pianificazione esegue automaticamente il partizionamento dell'attività in base alle risorse di sistema e al carico di lavoro.  Quando risulta possibile, se si verifica uno sbilanciamento del carico di lavoro, l'utilità di pianificazione ridistribuisce il lavoro fra più thread e processori.  
  
> [!NOTE]
>  È anche possibile fornire un partitioner o un'utilità di pianificazione personalizzata,  Per altre informazioni, vedere [Custom Partitioners for PLINQ and TPL](../../../docs/standard/parallel-programming/custom-partitioners-for-plinq-and-tpl.md) e [Task Schedulers](../Topic/Task%20Schedulers.md).  
  
 Sia il metodo <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName> sia il metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> presentano vari overload che consentono di arrestare o interrompere l'esecuzione del ciclo, monitorare lo stato del ciclo in altri thread, gestire lo stato di thread locale, completare gli oggetti di thread locali, controllare il livello di concorrenza e così via.  I tipi di supporto che consentono di usare queste funzionalità prevedono <xref:System.Threading.Tasks.ParallelLoopState>, <xref:System.Threading.Tasks.ParallelOptions>, <xref:System.Threading.Tasks.ParallelLoopResult>, <xref:System.Threading.CancellationToken> e <xref:System.Threading.CancellationTokenSource>.  
  
 Per altre informazioni, vedere la pagina relativa ai [modelli di programmazione parallela](http://go.microsoft.com/fwlink/p/?LinkId=265491).  
  
 Il parallelismo dei dati con sintassi dichiarativa o di tipo query è supportato da PLINQ.  Per altre informazioni, vedere [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[How to: Write a Simple Parallel.For Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-for-loop.md)|Descrive come scrivere un ciclo <xref:System.Threading.Tasks.Parallel.For%2A> su qualsiasi matrice o raccolta dell'origine <xref:System.Collections.Generic.IEnumerable%601> indicizzabile.|  
|[How to: Write a Simple Parallel.ForEach Loop](../../../docs/standard/parallel-programming/how-to-write-a-simple-parallel-foreach-loop.md)|Descrive come scrivere un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A> su qualsiasi raccolta di origine <xref:System.Collections.Generic.IEnumerable%601>.|  
|[How to: Stop or Break from a Parallel.For Loop](http://msdn.microsoft.com/it-it/de52e4f1-9346-4ad5-b582-1a4d54dc7f7e)|Descrive come arrestare o interrompere un ciclo parallelo in modo che tutti i thread siano informati dell'azione.|  
|[How to: Write a Parallel.For Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md)|Descrive come scrivere un ciclo <xref:System.Threading.Tasks.Parallel.For%2A> in cui ogni thread gestisce una variabile privata che non è visibile a qualsiasi altro thread e come sincronizzare i risultati di tutti i thread quando il ciclo viene completato.|  
|[How to: Write a Parallel.ForEach Loop with Thread\-Local Variables](../../../docs/standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-thread-local-variables.md)|Descrive come scrivere un ciclo <xref:System.Threading.Tasks.Parallel.ForEach%2A> in cui ogni thread gestisce una variabile privata che non è visibile a qualsiasi altro thread e come sincronizzare i risultati di tutti i thread quando il ciclo viene completato.|  
|[How to: Cancel a Parallel.For or ForEach Loop](../../../docs/standard/parallel-programming/how-to-cancel-a-parallel-for-or-foreach-loop.md)|Descrive come annullare un ciclo parallelo tramite un oggetto <xref:System.Threading.CancellationToken?displayProperty=fullName>.|  
|[How to: Speed Up Small Loop Bodies](../../../docs/standard/parallel-programming/how-to-speed-up-small-loop-bodies.md)|Descrive come aumentare la velocità di esecuzione nel caso di un corpo di ciclo molto piccolo.|  
|[Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)|Contiene la panoramica di Task Parallel Library.|  
|[Parallel Programming](../../../docs/standard/parallel-programming/index.md)|Introduce la Programmazione parallela in .NET Framework.|  
  
## Vedere anche  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)