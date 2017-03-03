---
title: Garbage Collection
description: Garbage Collection
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.devlang: dotnet
ms.assetid: db39a0f5-e363-490f-a7e6-adb9a6ff2a8c
translationtype: Human Translation
ms.sourcegitcommit: ffc0530b2263db0e073f351aac2d539de6701ead
ms.openlocfilehash: 4646a7e8c75315bb1a13bc5fddecd77888f6ae69
ms.lasthandoff: 01/18/2017

---

# <a name="garbage-collection"></a>Garbage Collection

Garbage Collection rappresenta una delle funzionalità più importanti della piattaforma .NET di codice gestito. Il Garbage Collector (GC) gestisce automaticamente le allocazioni e i rilasci di memoria. Non è necessario conoscere la procedura per allocare e rilasciare memoria o per gestire la durata degli oggetti che usano tale memoria. Un'allocazione viene eseguita ogni volta che si crea un _nuovo_ oggetto o che un tipo di valore è boxed. Le allocazioni in genere vengono eseguite molto rapidamente. Se non è presente memoria sufficiente per allocare un oggetto, il Garbage Collector deve raccogliere ed eliminare la memoria di garbage per rendere disponibile la memoria per eseguire nuove allocazioni. Questo processo è noto come "Garbage Collection".

Il Garbage Collector funge da gestore di memoria automatico, offrendo i seguenti vantaggi:

*   Consente di sviluppare un'applicazione senza alcun bisogno di liberare memoria.
*   Alloca gli oggetti nell'heap gestito in maniera efficiente.
*   Recupera gli oggetti inutilizzati, ne cancella la memoria e tiene la memoria a disposizione per le future allocazioni. Gli oggetti gestiti ottengono automaticamente contenuto pulito con il quale iniziare, pertanto i costruttori non devono inizializzare ogni campo dati.
*   Garantisce protezione per la memoria assicurando che un oggetto non possa usare il contenuto di un altro oggetto.

Il Garbage Collector .NET è generazionale e include tre generazioni. Ogni generazione ha il proprio heap che usa per l'archiviazione degli oggetti allocati. Esiste un principio fondamentale secondo il quale la maggior parte degli oggetti è di breve o di lunga durata. La generazione 0 è la prima generazione in cui gli oggetti vengono allocati. La durata degli oggetti spesso non va oltre la prima generazione, poiché nel momento in cui si verifica l'operazione di Garbage Collection successiva gli oggetti non sono più in uso (esterni all'ambito). La raccolta di generazione 0 viene eseguita rapidamente in quanto l'heap associato ha dimensioni ridotte. La generazione 1 è uno spazio di riserva. Gli oggetti che hanno breve durata ma che superano la raccolta di generazione 0 (spesso in base a una temporizzazione casuale) passano alla generazione 1\. Anche le raccolte di generazione 1 vengono eseguite rapidamente in quanto l'heap associato ha dimensioni ridotte. Le dimensioni dei primi due heap rimangono ridotte perché gli oggetti vengono raccolti oppure promossi all'heap della generazione successiva. La generazione 2 è la generazione in cui si trovano gli oggetti di lunga durata. L'heap di generazione 2 può raggiungere dimensioni notevoli, in quanto gli oggetti in esso contenuti possono durare a lungo e non esiste un heap di generazione 3 a cui promuoverli.

Il Garbage Collector ha un heap aggiuntivo per oggetti di grandi dimensioni chiamato heap degli oggetti grandi (LOH, Large Object Heap). È riservato per gli oggetti di dimensioni maggiori o uguali a 85.000 byte. Una matrice di byte (Byte[]) con elementi da 85 k rappresenta un esempio di un oggetto di grandi dimensioni. Gli oggetti di grandi dimensioni non vengono allocati negli heap generazionali, ma direttamente nell'Heap oggetto grande.

Le raccolte di generazione 2 e dell'Heap oggetto grande possono richiedere una notevole quantità di tempo per i programmi in esecuzione da molto tempo o che gestiscono grandi quantità di dati. I programmi server di grandi dimensioni notoriamente hanno heap dell'ordine di decine di GB. Il Garbage Collector usa varie tecniche per ridurre la quantità di tempo per cui l'esecuzione del programma resta bloccata. L'approccio principale consiste nell'eseguire il maggior numero possibile di operazioni di Garbage Collection in un thread in background, in modo da non interferire con l'esecuzione del programma. Il Garbage Collector espone anche alcuni modi per consentire agli sviluppatori di influenzarne il comportamento e ciò può essere molto utile per migliorare le prestazioni.

## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | ----------- 
[Gestione automatica della memoria e Garbage Collection](gc.md) | Illustra i concetti di base relativi alla gestione della memoria in .NET
[Principi fondamentali di Garbage Collection](fundamentals.md) | Descrive il funzionamento di Garbage Collection, la modalità di allocazione degli oggetti nell'heap gestito e altri concetti di base.
[Raccolte indotte](induced.md) | Descrive come eseguire un'operazione di Garbage Collection.
[Modalità di latenza](latency.md) | Descrive i modi per determinare l'ingerenza di Garbage Collection.
[Riferimenti deboli](weak-references.md) | Descrive i riferimenti che consentono al Garbage Collector di raccogliere un oggetto, pur senza impedire all'applicazione di accedervi.
 
## <a name="reference"></a>Riferimento

[System.GC](xref:System.GC)

[System.GCCollectionMode](xref:System.GCCollectionMode)

[System.Runtime.GCLatencyMode](xref:System.Runtime.GCLatencyMode)

[System.Runtime.GCSettings](xref:System.Runtime.GCSettings)

[GCSettings.LargeObjectHeapCompactionMode](xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode)

[Object.Finalize](xref:System.Object.Finalize)

[System.IDisposable](xref:System.IDisposable)

## <a name="see-also"></a>Vedere anche

[Pulizia delle risorse non gestite](unmanaged.md)


