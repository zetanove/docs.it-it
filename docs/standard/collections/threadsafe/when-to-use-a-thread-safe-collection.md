---
title: Quando utilizzare una raccolta thread-safe
description: Quando utilizzare una raccolta thread-safe
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a2a42d44-f6a5-4f16-9000-026221d66349
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: b0b88a85cb4048849464381656a30e8c8ea694d8
ms.lasthandoff: 03/02/2017

---

# <a name="when-to-use-a-thread-safe-collection"></a>Quando utilizzare una raccolta thread-safe

I tipi di raccolta `ConcurrentQueue`, `ConcurrentStack`, `ConcurrentDictionary`, `ConcurrentBag` e `BlockingCollection` sono stati creati specificamente per il supporto di operazioni di aggiunta e rimozione multithread. Per ottenere la thread safety, questi nuovi tipi usano vari nuovi meccanismi di sincronizzazione, sia di blocco che senza blocco. La sincronizzazione aggiunge sovraccarico a un'operazione. La quantità di sovraccarico dipende dal tipo di sincronizzazione usato, dal tipo di operazioni eseguite e da altri fattori, quali il numero di thread che provano ad accedere contemporaneamente alla raccolta.

In determinati scenari il sovraccarico della sincronizzazione è trascurabile e consente al tipo con multithread un'elaborazione molto più rapida e una miglior scalabilità rispetto al tipo equivalente non thread-safe se protetto da un blocco esterno. In altri scenari il sovraccarico può far sì che la scalabilità e le prestazioni del tipo thread-safe risultino uguali o più lente rispetto alla versione del tipo non thread-safe con blocco esterno.

Le sezioni seguenti offrono indicazioni generali su quando usare una raccolta thread-safe o una raccolta non thread-safe equivalente e provvista di un blocco specificato dall'utente per le operazioni di lettura e scrittura. Dato che le prestazioni possono variare in base a molti fattori, le indicazioni non sono specifiche e non sono necessariamente valide in qualsiasi circostanza. Se le prestazioni sono molto importanti, il modo migliore per determinare il tipo di raccolta da usare è la misurazione delle prestazioni in base alle configurazioni e ai carichi di lavoro di computer campione. In questo documento vengono usati i seguenti termini:

*Scenario producer-consumer puro:* un qualsiasi thread esegue l'aggiunta o la rimozione di elementi, ma non entrambe le operazioni.

*Scenario producer-consumer misto:* un qualsiasi thread esegue sia l'aggiunta che la rimozione di elementi.

*Aumento di velocità:* prestazioni algoritmiche più veloci rispetto a un altro tipo nello stesso scenario.

*Scalabilità:* miglioramento delle prestazioni proporzionale al numero di core nel computer. Un algoritmo con scalabilità viene eseguito più velocemente su otto core che su due core.

## <a name="concurrentqueuelttgt-vs-queuelttgt"></a>Confronto tra ConcurrentQueue&lt;T&gt; e Queue&lt;T&gt;

Negli scenari producer-consumer puri, in cui il tempo di elaborazione per ogni elemento è molto ridotto (poche istruzioni), [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) offre vantaggi di prestazioni modesti rispetto a [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) con blocco esterno. In questo scenario, `ConcurrentQueue<T>` offre le prestazioni migliori quando un thread dedicato aggiunge elementi alla coda e un altro thread dedicato rimuove elementi dalla coda. Se non si applica questa regola, le prestazioni di `Queue<T>` potrebbe persino risultare leggermente più veloci di quelle di `ConcurrentQueue<T>` nei computer che dispongono di più core. 

Quando il tempo di elaborazione è pari o superiore a circa 500 FLOPS (floating point operations, operazioni a virgola mobile), la regola dei due thread non è più valida per `ConcurrentQueue<T>`, che in questo caso registra una scalabilità ottimale. `Queue<T>` non presenta una scalabilità ottimale in questo scenario.

Negli scenari producer-consumer misti, quando il tempo di elaborazione è molto breve, un `Queue<T>` provvisto di blocco esterno offre una scalabilità migliore rispetto a `ConcurrentQueue<T>`. Tuttavia, quando il tempo di elaborazione è pari o superiore a 500 FLOPS, `ConcurrentQueue<T>` offre una scalabilità migliore.

## <a name="concurrentstack-vs-stack"></a>Confronto tra ConcurrentStack e Stack

Negli scenari producer-consumer puri, quando il tempo di elaborazione è molto ridotto, è probabile che [System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) e [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) con un blocco esterno abbiano prestazioni simili con un thread push dedicato e un thread pop dedicato. Se tuttavia il numero di thread aumenta, le prestazioni di entrambi i tipi rallentano per l'incremento dei conflitti e `Stack<T>` potrebbe registrare prestazioni migliori di `ConcurrentStack<T>`. Quando il tempo di elaborazione è pari o superiore a 500 FLOPS, la velocità di scalabilità dei due tipi è circa la stessa. 

Negli scenari producer-consumer misti `ConcurrentStack<T>` è più veloce per i carichi di lavoro sia piccoli che grandi.

L'uso di `PushRange` e `TryPopRange` può accelerare notevolmente i tempi di accesso.

## <a name="concurrentdictionary-vs-dictionary"></a>Confronto tra ConcurrentDictionary e Dizionario

In generale, è consigliabile usare [System.Collections.Concurrent.ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) negli scenari in cui si aggiungono e aggiornano chiavi o valori da più thread simultaneamente. Negli scenari che presentano aggiornamenti frequenti e letture poco frequenti, `ConcurrentDictionary<TKey, TValue>` offre in genere moderati vantaggi. Negli scenari che presentano molte letture e molti aggiornamenti, `ConcurrentDictionary<TKey, TValue>` è in genere molto più rapida su computer con un numero qualsiasi di core.

Negli scenari con aggiornamenti frequenti è possibile aumentare il livello di concorrenza di `ConcurrentDictionary<TKey, TValue>` e quindi effettuare una misurazione per quantificare eventuali incrementi delle prestazioni nei computer con più core. Se si modifica il livello di concorrenza, evitare per quanto possibile le operazioni globali.

Se si esegue solo la lettura di chiavi o valori, [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) è più veloce, perché non è richiesta alcuna sincronizzazione se il dizionario non viene modificato da nessun thread.

## <a name="concurrentbag"></a>ConcurrentBag

Negli scenari producer-consumer puri, è probabile che l'esecuzione di [System.Collections.Concurrent.ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1) risulti più lenta di quella di altri tipi di raccolta simultanea.

Negli scenari producer-consumer misti, `ConcurrentBag<T>` è in genere molto più veloce e più scalabile di qualsiasi altro tipo di raccolta simultanea per carichi di lavoro sia piccoli che grandi.

## <a name="blockingcollection"></a>BlockingCollection

Quando è necessaria la semantica di delimitazione e blocco, è probabile che l'esecuzione [System.Collections.Concurrent.BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) risulti più rapida di quella di qualsiasi implementazione personalizzata. Supporta anche funzionalità complete di annullamento, enumerazione e gestione eccezioni.

## <a name="see-also"></a>Vedere anche

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[Raccolte thread-safe](index.md)

