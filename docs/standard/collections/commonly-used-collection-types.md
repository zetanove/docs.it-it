---
title: Tipi di raccolte comunemente utilizzate
description: Tipi di raccolte comunemente utilizzate
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 55861611-1e40-4cc2-9ec5-0b2df4ba6c0c
translationtype: Human Translation
ms.sourcegitcommit: d4e7ef84480aa9f735fb8d1ff03c9e8a61127c83
ms.openlocfilehash: 063e43b156771ba0db7c6b8ef5823330a4405c2c

---

# <a name="commonly-used-collection-types"></a>Tipi di raccolte comunemente utilizzate

I tipi di raccolta sono le varianti comuni delle raccolte di dati, ad esempio tabelle hash, code, stack, contenitori, dizionari ed elenchi.

Le raccolte si basano sull'interfaccia [`ICollection`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection), sull'interfaccia [`IList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList), sull'interfaccia [`IDictionary`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary) oppure sulle relative controparti generiche. L'interfaccia `IList` e l'interfaccia `IDictionary` derivano entrambe dall'interfaccia `ICollection`. Di conseguenza, tutte le raccolte sono basate direttamente o indirettamente sull'interfaccia `ICollection`. Nelle raccolte basate sull'interfaccia `IList`, come ad esempio [`Array`](https://docs.microsoft.com/dotnet/core/api/System.Array), [`ArrayList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList) o [`List<T>)`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1), oppure direttamente sull'interfaccia `ICollection`, ad esempio [`Queue`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Queue), [`ConcurrentQueue<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1), [`Stack`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Stack), [`ConcurrentStack<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) o [`LinkedList<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1), ogni elemento contiene solo un valore. Nelle raccolte basate sull'interfaccia `IDictionary`, come ad esempio le classi [`Hashtable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) e [`SortedList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) le classi generiche [`Dictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e [`SortedList<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2), oppure sulle classi [`ConcurrentDictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2), ogni elemento contiene sia una chiave sia un valore. La classe [`KeyedCollection<TKey, TItem>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) è univoca perché è un elenco di valori con le chiavi incorporate nei valori e quindi funge da elenco e da dizionario.

Le raccolte generiche rappresentano la migliore soluzione per la tipizzazione forte. Tuttavia, se il linguaggio usato non supporta i generics, lo spazio dei nomi [`System.Collections`](https://docs.microsoft.com/dotnet/core/api/System.Collections) include le raccolte di base, come [`CollectionBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.CollectionBase), [`ReadOnlyCollectionBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ReadOnlyCollectionBase) e [`DictionaryBase`](https://docs.microsoft.com/dotnet/core/api/System.Collections.DictionaryBase), che sono classi di base astratte che possono essere estese per creare classi di raccolta fortemente tipizzate. Quando è necessario accedere a raccolte con multithreading efficiente, usare le raccolte generiche nello spazio dei nomi [`System.Collections.Concurrent`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent).

Le raccolte possono variare a seconda di come vengono archiviati gli elementi, la modalità di ordinamento, la modalità di ricerca e confronto. La classe [`Queue`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Queue) e la classe generica [`Queue<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) offrono elenchi First In, First Out, mentre la classe [`Stack`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Stack) e la classe generica [`Stack<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) offrono elenchi Last In, First Out. La classe [`SortedList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) e la classe generica [`SortedList<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) rappresentano versioni ordinate della classe [`Hashtable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) e della classe generica [`Dictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2). Gli elementi di un oggetto `Hashtable` o `Dictionary<TKey, TValue>` sono accessibili solo con la chiave dell'elemento. Gli elementi di un oggetto `SortedList` o [`KeyedCollection<TKey, TItem>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) sono invece accessibili con la chiave oppure con l'indice dell'elemento. Gli indici di tutte le raccolte sono in base zero, ad eccezione di [`Array`](https://docs.microsoft.com/dotnet/core/api/System.Array), che consente matrici non in base zero.

La funzionalità LINQ to Objects consente di usare le query LINQ per accedere agli oggetti in memoria purché il tipo dell'oggetto implementi [`IEnumerable`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) o [`IEnumerable<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1). Le query LINQ offrono un modello comune per l'accesso ai dati oltre a funzioni di filtro, ordinamento e raggruppamento e sono in genere più concise e leggibili dei cicli foreach standard. Le query LINQ possono inoltre migliorare le prestazioni.

## <a name="related-topics"></a>Argomenti correlati

Titolo | Descrizione
----- | -----------
[`Collections and Data Structures`](index.md) | Vengono descritti i diversi tipi di raccolta disponibili in .NET Framework, compresi stack, code, elenchi, matrici e dizionari.
[`Hashtable and Dictionary Collection Types`](hashtable-and-dictionary-collection-types.md) | Vengono descritte le funzionalità dei tipi di dizionario basati su hash generici e non generici.
[`Sorted Collection Types`](sorted-collection-types.md) | Vengono descritte le caratteristiche e le prestazioni delle raccolte ordinate.

## <a name="reference"></a>Riferimento

[`System.Collections`](https://docs.microsoft.com/dotnet/core/api/System.Collections)

[`System.Collections.Generic`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic)

[`System.Collections.ICollection`](https://docs.microsoft.com/dotnet/core/api/System.Collections.ICollection)

[`System.Collections.Generic.ICollection<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.ICollection-1)

[`System.Collections.IList`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList)

[`System.Collections.Generic.IList<T>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IList-1)

[`System.Collections.IDictionary`](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)

[`System.Collections.Generic.IDictionary<TKey, TValue>`](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)

[`System.Linq`](https://docs.microsoft.com/dotnet/core/api/System.Linq)



<!--HONumber=Nov16_HO1-->


