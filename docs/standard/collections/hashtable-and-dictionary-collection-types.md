---
title: Tipi di Collection Hashtable e Dictionary
description: Tipi di Collection Hashtable e Dictionary
keywords: .NET, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 0f18fac7-fd0d-4f25-a046-1d3d51de062e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 58c87f9e86b5b97feb654e92a56f81940c201a6a
ms.lasthandoff: 03/02/2017

---

# <a name="hashtable-and-dictionary-collection-types"></a>Tipi di Collection Hashtable e Dictionary

La classe [System.Collections.Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) e le classi generiche [System.Collections.Generic.Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) e [System.Collections.Concurrent.ConcurrentDictionary<T>](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2) implementano l'interfaccia [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary). La classe generica `Dictionary<T>` implementa anche l'interfaccia generica [IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2). Ogni elemento di queste raccolte è pertanto una coppia chiave-valore.

Un oggetto `Hashtable` è costituito da bucket che contengono gli elementi della raccolta. Un bucket è un sottogruppo virtuale di elementi all'interno di `Hashtable`, che rende più semplici e veloci le operazioni di ricerca e recupero rispetto alla maggior parte delle raccolte. Ogni bucket è associato a un codice hash, generato usando una funzione hash ed basato sulla chiave dell'elemento.

La classe generica [HashSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.HashSet-1) è una raccolta non ordinata destinata a contenere elementi univoci. 

Una funzione hash è un algoritmo che restituisce un codice hash numerico basato su una chiave. La chiave è il valore di una proprietà dell'oggetto che viene archiviato. Una funzione hash deve sempre restituire lo stesso codice hash per la stessa chiave. È possibile per una funzione hash generare lo stesso codice hash per due chiavi diverse, ma una funzione hash che genera un codice hash univoco per ogni chiave univoca offre prestazioni migliori durante il recupero di elementi dalla tabella hash.

Ogni oggetto usato come elemento in un oggetto `Hashtable` deve essere in grado di generare un codice hash per se stesso tramite un'implementazione del metodo `GetHashCode`. 

Quando un oggetto viene aggiunto a `Hashtable`, viene archiviato nel bucket associato al codice hash corrispondente al codice hash dell'oggetto. Quando viene cercato un valore in `Hashtable`, viene generato il codice hash per tale valore e viene eseguita la ricerca nel bucket associato a tale codice hash.

Ad esempio, una funzione hash per una stringa potrebbe prendere i codici ASCII di ogni carattere della stringa e combinarli per generare un codice hash. La stringa "picnic" avrebbe un codice hash diverso da quello della stringa "basket", pertanto le due stringhe si troverebbero in bucket diversi. "Stressed" e "desserts" avrebbero invece lo stesso codice hash e si troverebbero nello stesso bucket.

Le classi `Dictionary<T>` e `ConcurrentDictionary<T>` hanno la stessa funzionalità della classe `Hashtable`. Un oggetto `Dictionary<T>` di un tipo specifico (diverso da `Object`) offre prestazioni migliori rispetto a un oggetto `Hashtable` per i tipi di valore, in quanto gli elementi di `Hashtable` sono di tipo `Object`. Le conversioni boxing e unboxing vengono in genere eseguite quando si archivia o si recupera un tipo di valore. La classe `ConcurrentDictionary<T>` deve essere usata quando più thread potrebbero accedere contemporaneamente alla raccolta.

## <a name="see-also"></a>Vedere anche

[Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable)

[IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)

[Dictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2)

[System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)

[System.Collections.Concurrent.ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2)

[Tipi di raccolte usate comunemente](commonly-used-collection-types.md)


