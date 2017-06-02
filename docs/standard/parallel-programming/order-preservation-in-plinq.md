---
title: "Order Preservation in PLINQ | Microsoft Docs"
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
  - "PLINQ queries, order preservation"
ms.assetid: 10d202bc-19e1-4b5c-bbf1-9a977322a9ca
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Order Preservation in PLINQ
In PLINQ, l'obiettivo è ottimizzare le prestazioni senza tuttavia compromettere la correttezza.  Una query deve essere eseguita nel modo più veloce possibile e comunque produrre risultati corretti.  In alcuni casi la correttezza richiede la conservazione dell'ordine della sequenza di origine. Tuttavia, l'ordinamento può essere oneroso dal punto di vista del calcolo.  Pertanto, per impostazione predefinita, PLINQ non conserva l'ordine della sequenza di origine.  Sotto questo aspetto PLINQ assomiglia a [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)], ma differisce da LINQ to Objects, che invece conserva l'ordine.  
  
 Per eseguire l'override del comportamento predefinito è possibile attivare la conservazione dell'ordine tramite l'operatore <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> nella sequenza di origine.  La conservazione dell'ordine può quindi essere disattivata nella query in un secondo momento tramite il metodo <xref:System.Linq.ParallelEnumerable.AsUnordered%2A>.  Con entrambi i metodi, la domanda viene elaborata in base alle regole euristiche che determinano se l'esecuzione della query avverrà in modalità parallela o sequenziale.  Per ulteriori informazioni, vedere [Understanding Speedup in PLINQ](../../../docs/standard/parallel-programming/understanding-speedup-in-plinq.md).  
  
 Nell'esempio seguente viene mostrata una query parallela non ordinata che filtra tutti gli elementi che soddisfano una condizione, senza tentare di ordinare i risultati in alcun modo.  
  
 [!code-csharp[PLINQ#8](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#8)]
 [!code-vb[PLINQ#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#8)]  
  
 Questa query non produce necessariamente le prime 1000 città nella sequenza di origine che soddisfano la condizione, ma piuttosto un set di 1000 città che la soddisfano.  Gli operatori di query PLINQ eseguono il partizionamento della sequenza di origine in più sottosequenze che vengono elaborate come attività simultanee.  Se non è stata specificata la conservazione dell'ordine, i risultati di ogni partizione vengono passati alla fase successiva della query in un ordine arbitrario.  Inoltre, una partizione può produrre un subset dei propri risultati prima di continuare a elaborare gli elementi restanti.  È possibile che l'ordine risultante sia diverso ogni volta.  L'applicazione non può controllare questo comportamento perché dipende da come il sistema operativo pianifica i thread.  
  
 Nell'esempio seguente viene eseguito l'override del comportamento predefinito tramite l'operatore <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> nella sequenza di origine.  In questo modo si garantisce che il metodo <xref:System.Linq.ParallelEnumerable.Take%2A> restituisca le prime 1000 città nella sequenza di origine che soddisfano la condizione.  
  
 [!code-csharp[PLINQ#9](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#9)]
 [!code-vb[PLINQ#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#9)]  
  
 Tuttavia, questa query probabilmente presenta una velocità di esecuzione minore rispetto alla versione non ordinata. Infatti, deve tenere traccia dell'ordine originale in tutte le partizioni e, al momento dell'unione, garantire che l'ordine sia coerente.  Pertanto, è consigliabile utilizzare <xref:System.Linq.ParallelEnumerable.AsOrdered%2A> solo quando occorre e solo per quelle parti della query che lo richiedono.  Quando la conservazione dell'ordine non è più necessaria, utilizzare <xref:System.Linq.ParallelEnumerable.AsUnordered%2A> per disattivarla.  Nell'esempio seguente ciò si ottiene mediante la composizione di due query.  
  
 [!code-csharp[PLINQ#6](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#6)]
 [!code-vb[PLINQ#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinq2_vb.vb#6)]  
  
 Notare che PLINQ conserva per il resto della query l'ordine di una sequenza prodotta da operatori che impongono l'ordinamento.  In altre parole, gli operatori quali <xref:System.Linq.ParallelEnumerable.OrderBy%2A> e <xref:System.Linq.ParallelEnumerable.ThenBy%2A> vengono trattati come se fossero seguiti da una chiamata a <xref:System.Linq.ParallelEnumerable.AsOrdered%2A>.  
  
## Operatori di query e ordinamento  
 Gli operatori di query seguenti introducono la conservazione dell'ordine in tutte le operazioni successive in una query oppure finché non si chiama <xref:System.Linq.ParallelEnumerable.AsUnordered%2A>:  
  
-   <xref:System.Linq.ParallelEnumerable.OrderBy%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.ThenBy%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>  
  
 Gli operatori di query PLINQ seguenti in alcuni casi possono richiedere la produzione di risultati corretti da parte di sequenze di origine ordinate:  
  
-   <xref:System.Linq.ParallelEnumerable.Reverse%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.TakeWhile%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.SkipWhile%2A>  
  
-   <xref:System.Linq.ParallelEnumerable.Zip%2A>  
  
 Alcuni operatori di query PLINQ si comportano in modo diverso, a seconda che la sequenza di origine sia ordinata o non ordinata.  Questi operatori vengono elencati nella tabella seguente.  
  
|Operatore|Risultato quando la sequenza di origine è ordinata|Risultato quando la sequenza di origine non è ordinata|  
|---------------|--------------------------------------------------------|------------------------------------------------------------|  
|<xref:System.Linq.ParallelEnumerable.Aggregate%2A>|Output non deterministico per operazioni non associative o non commutative|Output non deterministico per operazioni non associative o non commutative|  
|<xref:System.Linq.ParallelEnumerable.All%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Any%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.AsEnumerable%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Average%2A>|Output non deterministico per operazioni non associative o non commutative|Output non deterministico per operazioni non associative o non commutative|  
|<xref:System.Linq.ParallelEnumerable.Cast%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Concat%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Count%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.DefaultIfEmpty%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Distinct%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.ElementAt%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.ElementAtOrDefault%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.Except%2A>|Risultati non ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.First%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.FirstOrDefault%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.ForAll%2A>|Viene eseguita in modo non deterministico e in parallelo|Viene eseguita in modo non deterministico e in parallelo|  
|<xref:System.Linq.ParallelEnumerable.GroupBy%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.GroupJoin%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Intersect%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Join%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Last%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.LastOrDefault%2A>|Restituisce l'elemento specificato|Elemento arbitrario|  
|<xref:System.Linq.ParallelEnumerable.LongCount%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Min%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.OrderBy%2A>|Riordina la sequenza|Inizia una nuova sezione ordinata|  
|<xref:System.Linq.ParallelEnumerable.OrderByDescending%2A>|Riordina la sequenza|Inizia una nuova sezione ordinata|  
|<xref:System.Linq.ParallelEnumerable.Range%2A>|Non applicabile \(stessa impostazione predefinita di <xref:System.Linq.ParallelEnumerable.AsParallel%2A> \)|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Repeat%2A>|Non applicabile \(stessa impostazione predefinita di <xref:System.Linq.ParallelEnumerable.AsParallel%2A>\)|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Reverse%2A>|Inverte|Nessuna operazione|  
|<xref:System.Linq.ParallelEnumerable.Select%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Select%2A> \(indicizzato\)|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.SelectMany%2A> \(indicizzato\)|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.SequenceEqual%2A>|Confronto ordinato|Confronto non ordinato|  
|<xref:System.Linq.ParallelEnumerable.Single%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.SingleOrDefault%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.Skip%2A>|Vengono ignorati i primi *n* elementi|Vengono ignorati *n* elementi qualsiasi|  
|<xref:System.Linq.ParallelEnumerable.SkipWhile%2A>|Risultati ordinati|Non deterministico  Esegue SkipWhile sull'ordine arbitrario corrente|  
|<xref:System.Linq.ParallelEnumerable.Sum%2A>|Output non deterministico per operazioni non associative o non commutative|Output non deterministico per operazioni non associative o non commutative|  
|<xref:System.Linq.ParallelEnumerable.Take%2A>|Accetta i primi `n` elementi|Accetta `n` elementi qualsiasi|  
|<xref:System.Linq.ParallelEnumerable.TakeWhile%2A>|Risultati ordinati|Non deterministico  Esegue TakeWhile sull'ordine arbitrario corrente|  
|<xref:System.Linq.ParallelEnumerable.ThenBy%2A>|Integra `OrderBy`|Integra `OrderBy`|  
|<xref:System.Linq.ParallelEnumerable.ThenByDescending%2A>|Integra `OrderBy`|Integra `OrderBy`|  
|<xref:System.Linq.ParallelEnumerable.ToArray%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.ToDictionary%2A>|Non applicabile|Non applicabile|  
|<xref:System.Linq.ParallelEnumerable.ToList%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.ToLookup%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Union%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Where%2A>|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Where%2A> \(indicizzato\)|Risultati ordinati|Risultati non ordinati|  
|<xref:System.Linq.ParallelEnumerable.Zip%2A>|Risultati ordinati|Risultati non ordinati|  
  
 I risultati non ordinati non vengono attivamente riordinati in sequenza casuale. Semplicemente a tali risultati non viene applicata una specifica logica di ordinamento.  In alcuni casi, una query non ordinata può mantenere l'ordinamento della sequenza di origine.  Per le query che utilizzano l'operatore Select indicizzato, PLINQ garantisce che gli elementi di output saranno riprodotti nell'ordine degli indici incrementali, ma non fornisce alcuna garanzia su quali indici verranno assegnati agli elementi.  
  
## Vedere anche  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)   
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)