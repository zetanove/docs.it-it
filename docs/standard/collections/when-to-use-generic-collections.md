---
title: Quando utilizzare raccolte generiche
description: Quando utilizzare raccolte generiche
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 971e08bd-b63f-4832-9e61-9f65cbedd352
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: bde317c165981775330e1d0d8261d355e2401bc9
ms.lasthandoff: 03/03/2017

---

# <a name="when-to-use-generic-collections"></a>Quando utilizzare raccolte generiche

L'uso di raccolte generiche è in genere consigliato perché offre l'immediato vantaggio dell'indipendenza dai tipi senza la necessità di derivare da un tipo di raccolta di base e implementare membri specifici di tipo. I tipi di raccolte generiche offrono anche prestazioni migliori rispetto ai tipi di raccolte non generiche corrispondenti (e tipi derivati dai tipi di raccolte base non generiche) quando gli elementi della raccolta sono tipi di valore, perché con i generics non è necessario il boxing degli elementi. 

È necessario usare le classi Collection generiche nello spazio dei nomi [System.Collections.Concurrent](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent) quando più thread potrebbero aggiungere o rimuovere elementi dalla raccolta contemporaneamente.

I seguenti tipi generici corrispondono ai tipi di raccolte esistenti: 

*   [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) è la classe generica che corrisponde a [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList).

*   [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e [ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) sono le classi generiche che corrispondono a [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable). 

*   [Collection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.Collection-1) è la classe generica che corrisponde a [CollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.CollectionBase). `Collection<T>` può essere usata come classe di base, ma a differenza di `CollectionBase`, non è astratta. Questo la rende più facile da usare.

*   [ReadOnlyCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.ReadOnlyCollection-1) è la classe generica che corrisponde a [ReadOnlyCollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.ReadOnlyCollectionBase). `ReadOnlyCollection<T>` non è astratta e ha un costruttore che semplifica l'esposizione di una [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) esistente come raccolta di sola lettura.

*   Le classi generiche [Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1), [ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1), [Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1), [ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) e [SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) corrispondono alle rispettive classi non generiche con gli stessi nomi.

## <a name="additional-types"></a>Tipi aggiuntivi

Diversi tipi di raccolte generiche non hanno controparti non generiche. Di seguito vengono forniti alcuni esempi: 

*   [LinkedList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1) è un elenco collegato di uso generale che specifica le operazioni di inserimento e rimozione O(1).

*   [SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) è un dizionario ordinato con operazioni di inserimento e recupero O(log n), che lo rende un'utile alternativa a [SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2). 

*   [KeyedCollection&lt;TKey, TItem&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) è un ibrido tra un elenco e un dizionario, che specifica un metodo per memorizzare oggetti contenenti le loro stesse chiavi.

*   [BlockingCollection&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.BlockingCollection-1) implementa una classe di raccolta con funzionalità di delimitazione e blocco.

*   [ConcurrentBag&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentBag-1) consente di eseguire rapidamente le operazioni di inserimento e rimozione di elementi non ordinati.

## <a name="linq-to-objects"></a>LINQ to Objects

La funzionalità LINQ to Objects consente agli sviluppatori di usare le query LINQ per accedere agli oggetti in memoria, a condizione che il tipo dell'oggetto implementi l'interfaccia [System.Collections.IEnumerable](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) o l'interfaccia [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1). Le query LINQ forniscono un modello comune per l'accesso ai dati, sono in genere più concise e leggibili dei cicli standard `foreach` e forniscono funzioni di filtro, ordinamento e raggruppamento. Le query LINQ possono inoltre migliorare le prestazioni.

## <a name="additional-functionality"></a>Funzionalità aggiuntive

Alcuni tipi generici hanno funzionalità che non si trovano nei tipi di raccolte non generiche. Ad esempio, la classe [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1), che corrisponde alla classe [ArrayList](https://docs.microsoft.com/dotnet/core/api/System.Collections.ArrayList) non generica ha una serie di metodi che accettano i delegati generici, quali il delegato [Predicate&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Predicate-1) che consente di specificare metodi per la ricerca nell'elenco e il delegato [Action&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Action-1) che rappresenta metodi che agiscono su ogni elemento dell'elenco.

La classe [List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) consente di specificare le proprie implementazioni di interfaccia [IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1) generica per l'ordinamento e la ricerca nell'elenco. Anche le classi [SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) e [SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) dispongono di questa funzionalità. Inoltre, queste classi consentono di specificare gli operatori di confronto quando viene creata la raccolta. In modo analogo, le classi [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e [KeyedCollection&lt;TKey, TItem&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) consentono di specificare operatori di confronto di uguaglianza personalizzati.

## <a name="see-also"></a>Vedere anche

[Raccolte e strutture di dati](index.md) 

[Tipi di raccolte usate comunemente](commonly-used-collection-types.md)

