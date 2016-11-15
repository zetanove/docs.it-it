---
title: Raccolte thread-safe
description: Raccolte thread-safe
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 92d5515d-f5d6-4a09-8bbb-31865d678643
translationtype: Human Translation
ms.sourcegitcommit: cfe65fcba1b3fdc09ffcac704a760d8ce29ea60b
ms.openlocfilehash: 421d46585b5d83f5772fa6596ad581c8c6acbf71

---

# <a name="threadsafe-collections"></a>Raccolte thread-safe

Lo spazio dei nomi [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) include diverse classi di raccolta thread-safe e scalabili. Più thread possono aggiungere o rimuovere elementi da queste raccolte in modo sicuro ed efficiente, senza richiedere una sincronizzazione aggiuntiva nel codice utente. Quando si scrive nuovo codice, usare le classi di raccolta simultanee ogni volta che la raccolta verrà scritta contemporaneamente su più thread. Se si prevede di leggere solo da una raccolta condivisa, è possibile usare le classi dello spazio dei nomi [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic). È consigliabile evitare di usare le classi di raccolta [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections) a meno che non sia necessario definire come destinazione il runtime di .NET Framework versione 1.1 o precedente.

## <a name="finegrained-locking-and-lockfree-mechanisms"></a>Blocco con granularità fine e meccanismi senza blocco

Alcuni tipi di raccolte simultanee usano meccanismi di sincronizzazione leggeri, ad esempio [SpinLock](https://docs.microsoft.com/dotnet/core/api/System.Threading.SpinLock), [SpinWait](https://docs.microsoft.com/dotnet/core/api/System.Threading.SpinWait), [SemaphoreSlim](https://docs.microsoft.com/dotnet/core/api/System.Threading.SemaphoreSlim) e [CountdownEvent](https://docs.microsoft.com/dotnet/core/api/System.Threading.CountdownEvent). Questi tipi di sincronizzazione usano in genere la rotazione con stato occupato per breve periodi di tempo prima di impostare il thread in uno stato `Wait` effettivo. Quando si prevedono tempi di attesa molto brevi, la rotazione è molto meno dispendiosa a livello di elaborazione rispetto all'attesa, che implica una transizione del kernel complessa. Per le classi di raccolta che usano la rotazione, questo livello di efficienza significa che più thread possono aggiungere e rimuovere elementi con una frequenza molto elevata.

Le classi [ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) e [ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) non usano i blocchi. Al contrario, si basano sulle operazioni con interlock per ottenere la thread safety.

> [!NOTE]
> Poiché supportano [ICollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection), le classi di raccolta simultanee forniscono implementazioni per le proprietà `IsSynchronized` e `SyncRoot`, anche se queste sono irrilevanti. `IsSynchronized` restituisce sempre `false` e `SyncRoot` è sempre null.

La tabella seguente elenca i tipi di raccolta nello spazio dei nomi [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent).

Tipo | Descrizione
---- | -----------
[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) | Fornisce la funzionalità di delimitazione e blocco per qualsiasi tipo che implementa [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1). Per altre informazioni, vedere [Panoramica di BlockingCollection](blockingcollection-overview.md).
[ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1) | Implementazione thread-safe di una raccolta non ordinata di elementi.
[ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) | Implementazione thread-safe di un dizionario di coppie chiave-valore.
[ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) | Implementazione thread-safe di una coda FIFO (First-In, First-Out).
[ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) | Implementazione thread-safe di una coda LIFO (Last-In, First-Out).
[IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1) | Interfaccia che un tipo deve implementare per essere usato in un oggetto `BlockingCollection`.

## <a name="thread-synchronization-in-the-net-framework-version-10-and-20-collections"></a>Sincronizzazione dei thread nelle raccolte di .NET Framework versione 1.0 e 2.0

Le raccolte introdotte inizialmente in .NET Framework versione 1.0 si trovano nello spazio dei nomi [System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections). Queste prime raccolte, che includono le raccolte [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList) e [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) comunemente usate, supportano la thread safety tramite la proprietà `Synchronized`, che restituisce un wrapper thread-safe per la raccolta. Il wrapper funziona bloccando l'intera raccolta in ogni operazione di aggiunta o rimozione. Pertanto, ogni thread che tenta di accedere alla raccolta deve attendere il proprio turno per acquisire l'unico blocco. Questa caratteristica non è scalabile e può causare un peggioramento delle prestazioni per le raccolte di grandi dimensioni. Inoltre, la progettazione non è completamente protetta da race condition. 

Le classi di raccolta introdotte inizialmente in .NET Framework versione 2.0 si trovano nello spazio dei nomi [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic). Queste classi includono [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1), [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e così via e forniscono maggiore indipendenza dai tipi e migliori prestazioni rispetto alle classi `System.Collections`. Tuttavia, le classi di raccolta `System.Collections.Generic` non forniscono la sincronizzazione dei thread. Quando gli elementi vengono aggiunti o rimossi contemporaneamente su più thread, la sincronizzazione deve essere gestita dal codice utente.

È quindi consigliabile usare le classi di raccolta `System.Collections.Concurrent` perché forniscono non solo l'indipendenza dai tipi delle classi di raccolta `System.Collections.Generic`, ma anche una thread safety più efficiente e completa rispetto alle raccolte `System.Collections`.

## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | -----------
[Panoramica di BlockingCollection](blockingcollection-overview.md) | Descrive la funzionalità fornita dal tipo `BlockingCollection<T>`.
[Quando usare una raccolta thread-safe](when-to-use-a-thread-safe-collection.md) | Illustra quando è opportuno usare una raccolta thread-safe.
[Procedura: Aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary](how-to-add-and-remove-items.md) | Descrive come aggiungere e rimuovere elementi da un oggetto `ConcurrentDictionary<TKey, TValue>`.
[Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](how-to-add-and-take-items.md) | Descrive come aggiungere e recuperare elementi da una raccolta di blocco senza usare l'enumeratore di sola lettura.
[Procedura: Aggiungere funzionalità di delimitazione e blocco a una raccolta](how-to-add-bounding-and-blocking.md ) | Descrive come usare una classe di raccolta come meccanismo di archiviazione sottostante per una raccolta `IProducerConsumerCollection<T>;`.
[Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection](how-to-use-foreach-to-remove.md ) | Descrive come usare `foreach` per rimuovere tutti gli elementi in una raccolta di blocco.
[Procedura: utilizzare matrici di raccolte di blocco in una pipeline](how-to-use-arrays-of-blockingcollections.md) | Descrive come usare più raccolte di blocco contemporaneamente per implementare una pipeline.
[Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag](how-to-create-an-object-pool.md) | Illustra come usare un contenitore simultaneo per migliorare le prestazioni negli scenari in cui è possibile riutilizzare gli oggetti anziché crearne continuamente di nuovi.

## <a name="reference"></a>Riferimento

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)






 





<!--HONumber=Nov16_HO3-->


