---
title: "Merge Options in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, merge options"
ms.assetid: e8f7be3b-88de-4f33-ab14-dc008e76c1ba
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# Merge Options in PLINQ
Quando una query viene eseguita in parallelo, PLINQ esegue il partizionamento della sequenza di origine in modo che più thread possano funzionare simultaneamente su parti diverse, in genere in thread separati.  Se è necessario utilizzare i risultati in un solo thread, ad esempio in un ciclo `foreach` \(`For Each` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\), i risultati di ogni thread devono essere riuniti in un'unica sequenza.  Il tipo di unione eseguito da PLINQ dipende dagli operatori presenti nella query.  Ad esempio, gli operatori che impongono un nuovo ordine dei risultati devono memorizzare nel buffer tutti gli elementi di tutti i thread.  Dal punto di vista del thread consumer \(che è anche il thread dell'utente dell'applicazione\), è possibile che una query memorizzata completamente nel buffer resti in esecuzione per un notevole periodo di tempo prima di produrre il primo risultato.  Altri operatori, per impostazione predefinita, vengono memorizzati nel buffer solo in parte e producono risultati in batch.  L'operatore <xref:System.Linq.ParallelEnumerable.ForAll%2A> è l'unico a non essere memorizzato nel buffer per impostazione predefinita.  Produce immediatamente tutti gli elementi di tutti i thread.  
  
 Tramite il metodo <xref:System.Linq.ParallelEnumerable.WithMergeOptions%2A>, come illustrato nell'esempio seguente, è possibile fornire a PLINQ un suggerimento che indica il tipo di unione da eseguire.  
  
 [!code-csharp[PLINQ#26](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#26)]
 [!code-vb[PLINQ#26](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#26)]  
  
 Per l'esempio completo, vedere [How to: Specify Merge Options in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md).  
  
 Se una determinata query non può supportare l'opzione richiesta, quest'ultima verrà semplicemente ignorata.  Nella maggior parte dei casi non è necessario specificare un'opzione di unione per una query PLINQ.  Tuttavia, in alcuni casi è possibile scoprire tramite test e misurazioni che l'esecuzione della query risulta più efficiente in una modalità non predefinita.  Questa opzione viene spesso utilizzata per forzare un operatore di fusione di blocchi a eseguire lo streaming dei propri risultati allo scopo di fornire un'interfaccia utente avente una capacità di risposta maggiore.  
  
## ParallelMergeOptions  
 L'enumerazione <xref:System.Linq.ParallelMergeOptions> include le opzioni seguenti che specificano, per le forme di query supportate, come viene prodotto l'output finale della query quando i risultati vengono utilizzati in un unico thread:  
  
-   `Not Buffered`  
  
     L'opzione <xref:System.Linq.ParallelMergeOptions> fa in modo che ogni elemento elaborato venga restituito da ogni thread appena viene prodotto.  Questo comportamento è analogo a uno "streaming" dell'output.  Se l'operatore <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> è presente nella query, `NotBuffered` conserva l'ordine degli elementi di origine.  Benché quando si usa `NotBuffered` i risultati vengano prodotti appena sono disponibili, il tempo complessivo per produrre tutti i risultati potrebbe comunque risultare maggiore rispetto al tempo che occorrerebbe utilizzando una delle altre opzioni di unione.  
  
-   `Auto Buffered`  
  
     Quando si utilizza l'opzione <xref:System.Linq.ParallelMergeOptions> la query raccoglie gli elementi in un buffer, quindi passa periodicamente il contenuto del buffer in un unico blocco al thread consumer.  Questo comportamento è analogo alla produzione dei dati di origine in "blocchi" anziché mediante lo "streaming" menzionato per l'opzione `NotBuffered`.  È possibile che `AutoBuffered` richieda più tempo di `NotBuffered` per rendere disponibile il primo elemento nel thread consumer.  La dimensione del buffer e l'esatto comportamento di produzione non sono configurabili e possono variare a seconda di vari fattori correlati alla query.  
  
-   `FullyBuffered`  
  
     Quando si utilizza l'opzione <xref:System.Linq.ParallelMergeOptions> non viene prodotto alcun elemento finché l'output dell'intera query non è stato memorizzato nel buffer.  Benché quando si utilizza questa opzione sia possibile che occorrano tempi ancora più lunghi affinché il primo elemento sia disponibile nel thread consumer, è comunque possibile che i risultati completi vengano prodotti più velocemente rispetto a quando si utilizzano le altre opzioni.  
  
## Operatori di query che supportano le opzioni di unione  
 Nella tabella seguente vengono elencati gli operatori che supportano tutte le modalità delle opzioni di unione, con le limitazioni specificate.  
  
|Operatore|Restrizioni|  
|---------------|-----------------|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|Solo query non ordinate che presentano un'origine di tipo Array o List.|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.OfType%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|Solo query non ordinate che presentano un'origine di tipo Array o List.|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|None|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|None|  
  
 Tutti gli altri operatori di query PLINQ possono ignorare le opzioni di unione fornite dall'utente.  Alcuni operatori di query, ad esempio <xref:System.Linq.ParallelEnumerable.Reverse%2A> e <xref:System.Linq.ParallelEnumerable.OrderBy%2A>, possono produrre elementi solo dopo che tutti gli elementi sono stati prodotti e riordinati.  Pertanto, quando <xref:System.Linq.ParallelMergeOptions> viene utilizzato in una query che contiene anche un operatore quale <xref:System.Linq.ParallelEnumerable.Reverse%2A>, il comportamento dell'unione verrà applicato nella query solo dopo che tale operatore avrà prodotto i propri risultati.  
  
 La capacità di alcuni operatori di gestire le opzioni di unione dipende dal tipo della sequenza di origine e dall'eventuale uso precedente dell'operatore <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> nella query.  <xref:System.Linq.ParallelEnumerable.ForAll%2A> è sempre <xref:System.Linq.ParallelMergeOptions>. Produce immediatamente i propri elementi.  <xref:System.Linq.ParallelEnumerable.OrderBy%2A> è sempre <xref:System.Linq.ParallelMergeOptions>. Deve ordinare l'intero elenco prima di produrre elementi.  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [How to: Specify Merge Options in PLINQ](../../../docs/standard/parallel-programming/how-to-specify-merge-options-in-plinq.md)