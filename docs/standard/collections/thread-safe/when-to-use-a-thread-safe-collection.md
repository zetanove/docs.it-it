---
title: "Quando usare una raccolta thread-safe | Microsoft Docs"
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
  - "raccolte thread-safe, quando eseguire l'aggiornamento"
ms.assetid: a9babe97-e457-4ff3-b528-a1bc940d5320
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Quando usare una raccolta thread-safe
[!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] introduce cinque nuovi tipi di raccolte appositamente progettati per supportare le operazioni di aggiunta e rimozione multithreading.  Per ottenere la thread safety, questi nuovi tipi utilizzano vari tipi di blocchi efficienti e meccanismi di sincronizzazione senza blocco.  La sincronizzazione aumenta il sovraccarico di un'operazione.  La quantità di sovraccarico dipende dal tipo di sincronizzazione utilizzato, dal tipo di operazioni eseguite e da altri fattori quale il numero dei thread che tentano di accedere contemporaneamente alla raccolta.  
  
 In alcuni scenari, il sovraccarico della sincronizzazione è trascurabile e consente al tipo multithreading prestazioni significativamente più veloci e scalabilità migliorata rispetto all'equivalente non thread\-safe, se protetto da un blocco esterno.  In altri scenari, il sovraccarico può causare prestazioni e scalabilità del tipo thread\-safe pari o addirittura inferiori e più lente rispetto alla versione non thread\-safe bloccata esternamente del tipo.  
  
 Nelle sezioni che seguono vengono fornite indicazioni generali su quando utilizzare una raccolta thread\-safe e quando l'equivalente non thread\-safe, dotata di un blocco fornito dall'utente per le operazioni di lettura e scrittura.  Dal momento che le prestazioni possono variare in base a molti fattori, le indicazioni non sono specifiche e non sono necessariamente valide in ogni circostanza.  Se le prestazioni sono molto importanti, il modo migliore per stabilire quale tipo di raccolta utilizzare è misurare le prestazioni in base a configurazioni e carichi di computer rappresentativi.  Nel presente documento vengono utilizzati i seguenti termini:  
  
 *Scenario producer\-consumer puro*  
 Un thread specificato aggiunge o rimuove elementi, non entrambe le cose.  
  
 *Scenario producer\-consumer misto*  
 Un thread specificato aggiunge e rimuove elementi.  
  
 *Aumento di velocità*  
 Prestazione algoritmica più veloce rispetto a un altro tipo nello stesso scenario.  
  
 *Scalabilità*  
 Aumento delle prestazioni proporzionale al numero di core nel computer.  Le prestazioni di un algoritmo che ridimensiona sono più veloci in otto core che in due core.  
  
## ConcurrentQueue\(T\) vs. Queue\(T\)  
 Negli scenari producer\-consumer puri, dove il tempo di elaborazione per ogni elemento è molto breve \(poche istruzioni\), <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName> può offrire modesti vantaggi in termini di prestazioni rispetto a <xref:System.Collections.Generic.Queue%601?displayProperty=fullName> con blocco esterno.  In questo scenario, <xref:System.Collections.Concurrent.ConcurrentQueue%601> offre le prestazioni migliori quando un thread dedicato aggiunge elementi nella coda e un altro thread dedicato rimuove elementi dalla coda.  Se non si applica questa regola, le prestazioni di <xref:System.Collections.Generic.Queue%601> potrebbero persino essere leggermente più veloci rispetto a quelle di <xref:System.Collections.Concurrent.ConcurrentQueue%601> nei computer multicore.  
  
 Quando il tempo di elaborazione è all'incirca pari o superiore a 500 FLOPS \(operazioni a virgola mobile\), la regola dei due thread non si applica a <xref:System.Collections.Concurrent.ConcurrentQueue%601>, la cui scalabilità è molto buona.  <xref:System.Collections.Generic.Queue%601> non offre una buona scalabilità in questo scenario.  
  
 Negli scenari producer\-consumer misti, quando il tempo di elaborazione è molto breve, un oggetto <xref:System.Collections.Generic.Queue%601> con un blocco esterno offre una scalabilità migliore rispetto a <xref:System.Collections.Concurrent.ConcurrentQueue%601>.  Tuttavia, quando il tempo di elaborazione è all'incirca pari o superiore a 500 FLOPS, la scalabilità di <xref:System.Collections.Concurrent.ConcurrentQueue%601> è migliore.  
  
## ConcurrentStack vs. Stack  
 Negli scenari producer\-consumer puri, quando il tempo di elaborazione è molto breve, <xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName> e <xref:System.Collections.Generic.Stack%601?displayProperty=fullName> con blocco esterno offrono presumibilmente prestazioni analoghe, con un thread di push dedicato e un thread di pop dedicato.  Tuttavia, quando il numero dei thread aumenta, entrambi i tipi subiscono un rallentamento a causa di un aumento del conflitto, e le prestazioni di <xref:System.Collections.Generic.Stack%601> potrebbero essere migliori rispetto a quelle di <xref:System.Collections.Concurrent.ConcurrentStack%601>.  Quando il tempo di elaborazione è all'incirca pari o superiore a 500 FLOPS, la frequenza di scalabilità è pressoché analoga per entrambi i tipi.  
  
 Negli scenari producer\-consumer misti, <xref:System.Collections.Concurrent.ConcurrentStack%601> è più veloce sia per i carichi di lavoro piccoli che per quelli grandi.  
  
 L'utilizzo di <xref:System.Collections.Concurrent.ConcurrentStack%601.PushRange%2A> e <xref:System.Collections.Concurrent.ConcurrentStack%601.TryPopRange%2A> può accelerare notevolmente i tempi di accesso.  
  
## ConcurrentDictionary vs. Dizionario  
 In generale, utilizzare un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> negli scenari in cui si aggiungono e aggiornano chiavi o valori contemporaneamente da più thread.  Negli scenari che implicano aggiornamenti frequenti e un numero di letture relativamente basso, <xref:System.Collections.Concurrent.ConcurrentDictionary%602> offre in genere modesti vantaggi.  Negli scenari che implicano molte letture e molti aggiornamenti, <xref:System.Collections.Concurrent.ConcurrentDictionary%602> è in genere molto più veloce nei computer con un numero di core indefinito.  
  
 Negli scenari che implicano aggiornamenti frequenti, è possibile aumentare il grado di concorrenza in <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, quindi eseguire una misurazione per vedere se le prestazioni aumentano nei computer multicore.  Se si modifica il livello di concorrenza, evitare il più possibile operazioni globali.  
  
 In caso di semplice lettura di chiavi o valori, <xref:System.Collections.Generic.Dictionary%602> è più veloce in quanto, se il dizionario non viene modificato da alcun thread, non sarà necessaria alcuna sincronizzazione.  
  
## ConcurrentBag  
 Negli scenari producer\-consumer puri, le prestazioni di <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName> saranno probabilmente più lente rispetto a quelle degli altri tipi di raccolte simultanei.  
  
 Negli scenari producer\-consumer misti, <xref:System.Collections.Concurrent.ConcurrentBag%601> è in genere molto più veloce e più scalabile di qualunque altro tipo di raccolta simultaneo, sia per carichi di lavoro grandi che piccoli.  
  
## BlockingCollection  
 Nei casi che richiedono la semantica di delimitazione e blocco, le prestazioni di <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> saranno presumibilmente più veloci rispetto a qualsiasi implementazione personalizzata.  Supporta inoltre l'annullamento, l'enumerazione e la gestione di eccezioni dettagliati.  
  
## Vedere anche  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [Raccolte thread\-safe](../../../../docs/standard/collections/thread-safe/index.md)   
 [Parallel Programming](../../../../docs/standard/parallel-programming/index.md)