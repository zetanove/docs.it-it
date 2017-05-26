---
title: Quando usare una raccolta thread-safe | Documenti di Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, when to upgrade
ms.assetid: a9babe97-e457-4ff3-b528-a1bc940d5320
caps.latest.revision: 9
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 87898a4a6ba3d3ef4c53fd1c6b8f94ff353f10e4
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="when-to-use-a-thread-safe-collection"></a>Quando utilizzare una raccolta thread-safe
[!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] introduce cinque nuovi tipi di raccolta creati specificamente per il supporto di operazioni di aggiunta e rimozione multithread. Per ottenere la thread safety, questi nuovi tipi usano vari nuovi meccanismi di sincronizzazione, sia di blocco che senza blocco. La sincronizzazione aggiunge sovraccarico a un'operazione. La quantità di sovraccarico dipende dal tipo di sincronizzazione usato, dal tipo di operazioni eseguite e da altri fattori, quali il numero di thread che provano ad accedere contemporaneamente alla raccolta.  
  
 In determinati scenari il sovraccarico della sincronizzazione è trascurabile e consente al tipo con multithread un'elaborazione molto più rapida e una miglior scalabilità rispetto al tipo equivalente non thread-safe se protetto da un blocco esterno. In altri scenari il sovraccarico può far sì che la scalabilità e le prestazioni del tipo thread-safe risultino uguali o più lente rispetto alla versione del tipo non thread-safe con blocco esterno.  
  
 Le sezioni seguenti offrono indicazioni generali su quando usare una raccolta thread-safe o una raccolta non thread-safe equivalente e provvista di un blocco specificato dall'utente per le operazioni di lettura e scrittura. Dato che le prestazioni possono variare in base a molti fattori, le indicazioni non sono specifiche e non sono necessariamente valide in qualsiasi circostanza. Se le prestazioni sono molto importanti, il modo migliore per determinare il tipo di raccolta da usare è la misurazione delle prestazioni in base alle configurazioni e ai carichi di lavoro di computer campione. In questo documento vengono usati i seguenti termini:  
  
 *Scenario producer-consumer puro*  
 Un qualsiasi thread esegue l'aggiunta o la rimozione di elementi, ma non entrambe le operazioni.  
  
 *Scenario producer-consumer misto*  
 Un qualsiasi thread esegue sia l'aggiunta che la rimozione di elementi.  
  
 *Aumento della velocità*  
 Prestazioni algoritmiche più veloci rispetto a un altro tipo nello stesso scenario.  
  
 *Scalabilità*  
 Miglioramento delle prestazioni proporzionale al numero di core nel computer. Un algoritmo con scalabilità viene eseguito più velocemente su otto core che su due core.  
  
## <a name="concurrentqueuet-vs-queuet"></a>Confronto tra ConcurrentQueue(T) e Queue(T)  
 Negli scenari producer-consumer puri, in cui il tempo di elaborazione per ogni elemento è molto ridotto (poche istruzioni), <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName> offre vantaggi di prestazioni modesti rispetto a <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> con blocco esterno. In questo scenario, <xref:System.Collections.Concurrent.ConcurrentQueue%601> offre le prestazioni migliori quando un thread dedicato aggiunge elementi alla coda e un altro thread dedicato rimuove elementi dalla coda. Se non si applica questa regola, le prestazioni di <xref:System.Collections.Generic.Queue%601> potrebbe persino risultare leggermente più veloci di quelle di <xref:System.Collections.Concurrent.ConcurrentQueue%601> nei computer che dispongono di più core.  
  
 Quando il tempo di elaborazione è pari o superiore a circa 500 FLOPS (floating point operations, operazioni a virgola mobile), la regola dei due thread non è più valida per <xref:System.Collections.Concurrent.ConcurrentQueue%601>, che in questo caso registra una scalabilità ottimale. <xref:System.Collections.Generic.Queue%601> non presenta una scalabilità ottimale in questo scenario.  
  
 Negli scenari producer-consumer misti, quando il tempo di elaborazione è molto breve, un <xref:System.Collections.Generic.Queue%601> provvisto di blocco esterno offre una scalabilità migliore rispetto a <xref:System.Collections.Concurrent.ConcurrentQueue%601>. Tuttavia, quando il tempo di elaborazione è pari o superiore a 500 FLOPS, <xref:System.Collections.Concurrent.ConcurrentQueue%601> offre una scalabilità migliore.  
  
## <a name="concurrentstack-vs-stack"></a>Confronto tra ConcurrentStack e Stack  
 Negli scenari producer-consumer puri, quando il tempo di elaborazione è molto ridotto, è probabile che <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName> e <xref:System.Collections.Generic.Stack%601?displayProperty=fullName> con un blocco esterno abbiano prestazioni simili con un thread push dedicato e un thread pop dedicato. Se tuttavia il numero di thread aumenta, le prestazioni di entrambi i tipi rallentano per l'incremento dei conflitti e <xref:System.Collections.Generic.Stack%601> potrebbe registrare prestazioni migliori di <xref:System.Collections.Concurrent.ConcurrentStack%601>. Quando il tempo di elaborazione è pari o superiore a 500 FLOPS, la velocità di scalabilità dei due tipi è circa la stessa.  
  
 Negli scenari producer-consumer misti <xref:System.Collections.Concurrent.ConcurrentStack%601> è più veloce per i carichi di lavoro sia piccoli che grandi.  
  
 L'uso di <xref:System.Collections.Concurrent.ConcurrentStack%601.PushRange%2A> e <xref:System.Collections.Concurrent.ConcurrentStack%601.TryPopRange%2A> può accelerare notevolmente i tempi di accesso.  
  
## <a name="concurrentdictionary-vs-dictionary"></a>Confronto tra ConcurrentDictionary e Dizionario  
 In generale, è consigliabile usare <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> negli scenari in cui si aggiungono e aggiornano chiavi o valori da più thread simultaneamente. Negli scenari che presentano aggiornamenti frequenti e letture poco frequenti, <xref:System.Collections.Concurrent.ConcurrentDictionary%602> offre in genere moderati vantaggi. Negli scenari che presentano molte letture e molti aggiornamenti, <xref:System.Collections.Concurrent.ConcurrentDictionary%602> è in genere molto più rapida su computer con un numero qualsiasi di core.  
  
 Negli scenari con aggiornamenti frequenti è possibile aumentare il livello di concorrenza di <xref:System.Collections.Concurrent.ConcurrentDictionary%602> e quindi effettuare una misurazione per quantificare eventuali incrementi delle prestazioni nei computer con più core. Se si modifica il livello di concorrenza, evitare per quanto possibile le operazioni globali.  
  
 Se si esegue solo la lettura di chiavi o valori, <xref:System.Collections.Generic.Dictionary%602> è più veloce, perché non è richiesta alcuna sincronizzazione se il dizionario non viene modificato da nessun thread.  
  
## <a name="concurrentbag"></a>ConcurrentBag  
 Negli scenari producer-consumer puri, è probabile che l'esecuzione di <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName> risulti più lenta di quella di altri tipi di raccolta simultanea.  
  
 Negli scenari producer-consumer misti, <xref:System.Collections.Concurrent.ConcurrentBag%601> è in genere molto più veloce e più scalabile di qualsiasi altro tipo di raccolta simultanea per carichi di lavoro sia piccoli che grandi.  
  
## <a name="blockingcollection"></a>BlockingCollection  
 Quando è necessaria la semantica di delimitazione e blocco, è probabile che l'esecuzione di <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> risulti più rapida di quella di qualsiasi implementazione personalizzata. Supporta anche funzionalità complete di annullamento, enumerazione e gestione eccezioni.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread-safe](../../../../docs/standard/collections/thread-safe/index.md)   
 [Programmazione parallela](../../../../docs/standard/parallel-programming/index.md)
