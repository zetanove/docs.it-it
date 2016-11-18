---
title: Tipi di raccolta ordinati
description: Tipi di raccolta ordinati
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: bdc9c13e-e56a-433b-a293-c92364f6e9cb
translationtype: Human Translation
ms.sourcegitcommit: 149086110d7470d97e1ab3e5969269626290b523
ms.openlocfilehash: 4359ec4c55921497f32d5891ea337a30867e4fa5

---

# <a name="sorted-collection-types"></a>Tipi di raccolta ordinati  
 
 La classe [System.Collections.SortedList](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList), la classe generica [System.Collections.Generic.SortedList&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedList-2) e la classe generica [System.Collections.Generic.SortedDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2) sono simili alla classe [Hashtable](https://docs.microsoft.com/dotnet/core/api/System.Collections.Hashtable) e alla classe generica [Dictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2) poiché implementano l'interfaccia [IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary), ma gestiscono gli elementi in ordine di chiave e non presentano la caratteristica di inserimento e recupero O(1) delle tabelle hash. Le tre classi hanno diverse funzionalità in comune:  

 *   Tutte e tre le classi implementano l'interfaccia [System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary). Le due classi generiche implementano anche l'interfaccia generica [System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2).  
 
 *   Ogni elemento è una coppia chiave/valore per scopi di enumerazione.   
  
> [!NOTE]  
> La classe non generica [SortedList](https://docs.microsoft.com/dotnet/core/api/System.Collections.SortedList) restituisce oggetti [DictionaryEntry](https://docs.microsoft.com/dotnet/core/api/System.Collections.DictionaryEntry) quando enumerata, anche se i due tipi generici restituiscono oggetti [KeyValuePair&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.KeyValuePair-2).  
   
*   Gli elementi vengono ordinati in base a un'implementazione [System.Collections.IComparer](https://docs.microsoft.com/dotnet/core/api/System.Collections.IComparer) (per `SortedList` non generico) o un'implementazione [System.Collections.Generic.IComparer&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IComparer-1) (per le due classi generiche).  
   
 *   Ogni classe specifica le proprietà che restituiscono raccolte contenenti solo chiavi o solo valori.  
   
Nella tabella seguente sono elencate alcune delle differenze tra le due classi SortedList e la classe [SortedDictionary<TKey, TValue>](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedDictionary-2).  
   
 Classe non generica `SortedList` e classe generica `SortedList<TKey, TValue>` | Classe generica `SortedDictionary<TKey, TValue>`  
 --------------------------------------------------------------------------------- | ------------------------------  
 Le proprietà che restituiscono chiavi e valori vengono indicizzate, consentendo un efficiente recupero indicizzato. | Senza recupero indicizzato.  
 Il recupero è O (log n). | Il recupero è O (log n).  
 L'inserimento e la rimozione sono in genere O(n); l'inserimento è tuttavia O(1) per i dati già presenti nel criterio di ordinamento in modo che ogni elemento venga aggiunto alla fine dell'elenco. (Ciò presuppone che non sia necessario un ridimensionamento). | Inserimento e rimozione sono O(log n).  
 Usa meno memoria di un `SortedDictionary<TKey, TValue>`. | Usa più memoria della classe non generica `SortedList` e della classe generica `SortedList<TKey, TValue>`.  
  
 Per gli elenchi ordinati o i dizionari che devono essere accessibili contemporaneamente da più thread, è possibile aggiungere logica di ordinamento per una classe che deriva da [ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2).  
  
 > [!NOTE]  
 > Per i valori che contengono le proprie chiavi (ad esempio, record dei dipendenti che contengono un numero di ID dipendente) è possibile creare una raccolta con chiave che include alcune caratteristiche di un elenco e alcune caratteristiche di un dizionario mediante la derivazione dalla classe generica [KeyedCollection&lt;TKey, TItem&gt;]().  
   
 La classe [SortedSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.SortedSet-1) presenta una struttura ad albero auto-bilanciata che mantiene i dati ordinati dopo inserimenti, eliminazioni e ricerche. Questa classe e la classe [HashSet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.HashSet-1) implementano l'interfaccia [ISet&lt;T&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.ISet-1).  
   
## <a name="see-also"></a>Vedere anche  
  
[System.Collections.IDictionary](https://docs.microsoft.com/dotnet/core/api/System.Collections.IDictionary)  
   
[System.Collections.Generic.IDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IDictionary-2)  
   
[ConcurrentDictionary&lt;TKey, TValue&gt;](https://docs.microsoft.com/dotnet/core/api/System.Collections.Concurrent.ConcurrentDictionary-2)  
 
[Tipi di raccolte usate comunemente](commonly-used-collection-types.md) 



<!--HONumber=Nov16_HO3-->


