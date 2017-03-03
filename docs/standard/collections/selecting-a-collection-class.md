---
title: Selezione di una classe Collection
description: Selezione di una classe Collection
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 0a60fca7-e082-48d4-9dda-30b0d3e67ec7
translationtype: Human Translation
ms.sourcegitcommit: 763433b00ae7d01cfa0c7fa250f51d23a95f6f15
ms.openlocfilehash: d174d0cb910035340fb317521f3ad930d16853c2
ms.lasthandoff: 01/18/2017

---

# <a name="selecting-a-collection-class"></a>Selezione di una classe Collection

Assicurarsi di scegliere con attenzione la classe Collection, poiché l'uso del tipo errato può limitare l'uso della raccolta. È preferibile usare le versioni generiche e simultanee delle raccolte per via di una maggiore indipendenza dai tipi e di altri miglioramenti. In generale, evitare di usare i tipi nello spazio dei nomi System.Collections a meno che la destinazione specifica non sia .NET Framework versione 1.1. 

Prendere in considerazione le domande seguenti:

* È necessario un elenco sequenziale quando l'elemento viene in genere eliminato dopo che il valore è stato recuperato? 

    * Se la risposta è affermativa ed è necessario un comportamento FIFO (First In First Out), considerare l'uso della classe generica [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1). Se è necessario un comportamento LIFO (Last In First Out), considerare l'uso della classe generica [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1). Per un accesso sicuro da più thread, usare le versioni simultanee [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) e [System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1).
    
    * Se la risposta è negativa, è opportuno usare le altre raccolte.
    
* È necessario accedere agli elementi in un determinato ordine, ad esempio FIFO, LIFO o casuale?

    * La classe generica [System.Collections.Generic.Queue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Queue-1) o [System.Collections.Concurrent.ConcurrentQueue&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentQueue-1) offre l'accesso FIFO. Per altre informazioni, vedere [When to Use a Thread-Safe Collection](threadsafe/when-to-use-a-thread-safe-collection.md) (Quando usare una raccolta thread-safe).
    
    * La classe generica [System.Collections.Generic.Stack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Stack-1) o [System.Collections.Concurrent.ConcurrentStack&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentStack-1) offre l'accesso LIFO. Per altre informazioni, vedere [When to Use a Thread-Safe Collection](threadsafe/when-to-use-a-thread-safe-collection.md) (Quando usare una raccolta thread-safe).
    
    * La classe generica [System.Collections.Generic.LinkedList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.LinkedList-1) consente l'accesso sequenziale dall'inizio alla fine o viceversa.
    
* È necessario accedere a ciascun elemento tramite l'indice? 

    * La classe [System.Collections.Specialized.StringCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringCollection) e la classe generica [System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) consentono l'accesso ai relativi elementi tramite l'indice in base zero dell'elemento. 
    
    * Le classi [System.Collections.Specialized.ListDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.ListDictionary) e [System.Collections.Specialized.StringDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringDictionary) e le classi generiche [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) consentono l'accesso ai relativi elementi tramite la chiave dell'elemento.
    
    * Le classi [System.Collections.Specialized.NameObjectCollectionBase](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameObjectCollectionBase) e [System.Collections.Specialized.NameValueCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameValueCollection) e le classi generiche [System.Collections.ObjectModel.KeyedCollection&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2) e [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) consentono l'accesso ai relativi elementi tramite l'indice in base zero o la chiave dell'elemento.
    
* Ogni elemento contiene un valore, una combinazione di una chiave e un valore o una combinazione di una chiave e più valori? 

    * Un valore: usare una qualsiasi raccolta basata sull'interfaccia generica [System.Collections.Generic.IList&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IList-1).
    
    * Una chiave e un valore: usare una qualsiasi raccolta basata sull'interfaccia generica [System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2).
    
    * Un valore con chiave incorporata: usare la classe generica [System.Collections.ObjectModel.KeyedCollection&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.ObjectModel.KeyedCollection-2).
    
    * Una chiave e più valori: usare la classe [System.Collections.Specialized.NameValueCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.NameValueCollection).
    
* È necessario ordinare gli elementi in modo diverso da come sono stati immessi? 

    * La classe [System.Collections.Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) ordina gli elementi in base ai rispettivi codici hash.
    
    * Le classi generiche [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) e [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) ordinano gli elementi in base alla chiave, in base all'implementazione dell'interfaccia [System.Collections.IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer) e dell'interfaccia generica [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1).
    
    * La classe generica [System.Collections.Generic.List&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) offre un metodo `Sort` che accetta come parametro un'implementazione dell'interfaccia generica `IComparer<T>`.
    
* Sono necessarie raccolte che accettano solo stringhe? 

    * [StringCollection](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringCollection) (in base a [System.Collections.IList](https://docs.microsoft.com/dotnet/core/api/System.Collections.IList)) e [StringDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized.StringDictionary) (in base a [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)) sono presenti nello spazio dei nomi [System.Collections.Specialized](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized). 
    
    * È anche possibile usare una qualsiasi classe di raccolte generiche nello spazio dei nomi [System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic) come raccolte di stringhe fortemente tipizzate specificando la classe `String` per i relativi argomenti di tipo generico.
    
## <a name="linq-to-objects"></a>LINQ to Objects

LINQ to Objects consente agli sviluppatori di usare le query LINQ per accedere agli oggetti in memoria, a condizione che il tipo dell'oggetto implementi [System.Collections.IEnumerable](https://docs.microsoft.com/dotnet/core/api/System.Collections.IEnumerable) o [System.Collections.Generic.IEnumerable&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IEnumerable-1). Le query LINQ offrono un modello comune per l'accesso ai dati, sono in genere più concise e leggibili dei cicli standard e includono funzioni di filtro, ordinamento e raggruppamento. Per altre informazioni, vedere [Language Integrated Query (LINQ)](../../csharp/linq/index.md).

## <a name="see-also"></a>Vedere anche

[System.Collections](https://docs.microsoft.com/dotnet/core/api/System.Collections)

[System.Collections.Specialized](https://docs.microsoft.com/dotnet/core/api/System.Collections.Specialized)

[System.Collections.Generic](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic)

[Raccolte thread-safe](threadsafe/index.md)

