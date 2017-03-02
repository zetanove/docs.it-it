---
title: Panoramica di BlockingCollection
description: Panoramica di BlockingCollection
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: a1a867de-53c2-49ca-9a1a-e5770a942724
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 8a770fb7143a547031daf231d1a0863322c3cfaa
ms.lasthandoff: 03/02/2017

---

# <a name="blockingcollection-overview"></a>Panoramica di BlockingCollection

[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) è una classe di raccolta thread-safe che offre le funzionalità seguenti:

*   Implementazione del modello Producer-Consumer.

*   Aggiunta e rimozione thread-safe di elementi da una raccolta.

*   Capacità massima facoltativa.

*   Operazioni di inserimento e rimozione che si bloccano quando la raccolta è vuota o piena.

*   Operazioni "prova" di inserimento e rimozione che non si bloccano o che si bloccano per un periodo di tempo specificato.

*   Incapsulamento di qualsiasi tipo di raccolta che implementi [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1).

*   Annullamento con token di annullamento.

*   Due tipi di enumerazione con `foreach`: 

    1. Enumerazione di sola lettura.
    
    2. Enumerazione che rimuove gli elementi quando vengono enumerati.
    
## <a name="bounding-and-blocking-support"></a>Supporto di delimitazione e blocco 

[BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) supporta delimitazione e blocco. La delimitazione consente di impostare la capacità massima della raccolta. La delimitazione è importante in determinati scenari poiché consente di controllare la dimensione massima della raccolta in memoria, impedendo ai thread Producer di spostarsi troppo oltre i thread Consumer.

Più thread o attività possono aggiungere contemporaneamente elementi alla raccolta, e se la raccolta raggiunge la capacità massima specificata, i thread Producer si bloccano fino a quando non viene rimosso un elemento. Più Consumer possono rimuovere contemporaneamente elementi e quando la raccolta diventa vuota, i thread Consumer si bloccano fino a quando un Producer aggiunge un elemento. Un thread Producer può chiamare `CompleteAdding` per indicare che non verranno aggiunti altri elementi. I Consumer monitorano la proprietà `IsCompleted` per sapere quando la raccolta è vuota e non verranno aggiunti altri elementi. Nell'esempio seguente viene illustrato un semplice `BlockingCollection` con una capacità delimitata di 100. Un'attività Producer aggiunge elementi alla raccolta, purché una condizione esterna sia true e quindi chiama `CompleteAdding`. L'attività di tipo Consumer accetta elementi finché la proprietà `IsCompleted` è true.

```csharp
// A bounded collection. It can hold no more 
// than 100 items at once.
BlockingCollection<Data> dataItems = new BlockingCollection<Data>(100);


// A simple blocking consumer with no cancellation.
Task.Run(() => 
{
    while (!dataItems.IsCompleted)
    {

        Data data = null;
        // Blocks if number.Count == 0
        // IOE means that Take() was called on a completed collection.
        // Some other thread can call CompleteAdding after we pass the
        // IsCompleted check but before we call Take. 
        // In this example, we can simply catch the exception since the 
        // loop will break on the next iteration.
        try
        {
            data = dataItems.Take();
        }
        catch (InvalidOperationException) { }

        if (data != null)
        {
            Process(data);
        }
    }
    Console.WriteLine("\r\nNo more items to take.");
});

// A simple blocking producer with no cancellation.
Task.Run(() =>
{
    while (moreItemsToAdd)
    {
        Data data = GetData();
        // Blocks if numbers.Count == dataItems.BoundedCapacity
        dataItems.Add(data);
    }
    // Let consumer know we are done.
    dataItems.CompleteAdding();
});
```

Per un esempio completo, vedere [Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](how-to-add-and-take-items.md).

## <a name="timed-blocking-operations"></a>Operazioni di blocco temporizzate

Nelle operazioni di blocco temporizzate `TryAdd` e `TryTake` sulle raccolte delimitate il metodo tenta di aggiungere o rimuovere un elemento. Se è disponibile un elemento, questo viene posizionato nella variabile che è stata passata per riferimento e il metodo restituisce `true`. Se dopo un periodo di timeout specificato non viene recuperato alcun elemento, il metodo restituisce `false`. Il thread è quindi libero di eseguire altre operazioni utili prima di tentare nuovamente di accedere alla raccolta. Per un esempio di accesso con blocco temporizzato, vedere il secondo esempio in [Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](how-to-add-and-take-items.md).

## <a name="cancelling-add-and-take-operations"></a>Annullamento di operazioni di aggiunta e rimozione

Le operazioni di aggiunta e rimozione solitamente vengono eseguite in un ciclo. È possibile annullare un ciclo passando un `CancellationToken` al metodo `TryAdd` o `TryTake` e quindi controllando il valore della proprietà `IsCancellationRequested` del token in ogni iterazione. Se il valore è `true`, l'utente deve decidere se rispondere alla richiesta di annullamento cancellando tutte le risorse e uscendo dal ciclo. Nell'esempio seguente viene illustrato un overload di `TryAdd` che accetta un token di annullamento e il codice che viene usato:

```csharp
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );
```

## <a name="specifying-the-collection-type"></a>Specifica del tipo di raccolta

Quando si crea un oggetto `BlockingCollection<T>;`, è possibile specificare non solo la capacità delimitata ma anche il tipo di raccolta da usare. Ad esempio, è possibile specificare un oggetto [ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) per il comportamento FIFO (First In, First Out) o un oggetto [ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) per il comportamento LIFO (Last In, First Out). È possibile usare qualsiasi classe di raccolta che implementa l'interfaccia [IProducerConsumerCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.IProducerConsumerCollection-1). Il tipo di raccolta predefinito per `BlockingCollection<T>` è `ConcurrentQueue<T>`. L'esempio di codice seguente illustra come creare un `BlockingCollection<T>` di stringhe con una capacità di 1000, che usa un oggetto [ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1):

```csharp
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );
```

## <a name="ienumerable-support"></a>Supporto di IEnumerable

`BlockingCollection<T>` fornisce un metodo `GetConsumingEnumerable` che consente agli utenti di usare un'istruzione `foreach` per rimuovere gli elementi fino a quando non viene completata la raccolta, ovvero finché non è vuota e non verranno aggiunti altri elementi. Per altre informazioni, vedere [Procedura: usare ForEach per rimuovere elementi in un oggetto BlockingCollection](how-to-use-foreach-to-remove.md).

## <a name="using-many-blockingcollections-as-one"></a>Uso di più oggetti BlockingCollections come uno solo

Per gli scenari in cui un Consumer deve rimuovere elementi da più raccolte contemporaneamente, è possibile creare matrici di `BlockingCollection<T>` e usare i metodi statici, ad esempio `TakeFromAny` e `AddToAny` che eseguiranno operazioni di aggiunta o rimozione in qualsiasi raccolta nella matrice. Se una raccolta è bloccata, il metodo ne cerca immediatamente un'altra finché non ne trova una che può eseguire l'operazione. Per altre informazioni, vedere [Procedura: usare matrici di BlockingCollection in una pipeline](how-to-use-arrays-of-blockingcollections.md).

## <a name="see-also"></a>Vedere anche

[System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent)

[Raccolte e strutture di dati](../index.md)

[Raccolte thread-safe](index.md)


