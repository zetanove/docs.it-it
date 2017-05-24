---
title: Tipi di raccolte comunemente utilizzate | Documenti di Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [.NET Framework], generic
- objects [.NET Framework], grouping in collections
- generics [.NET Framework], collections
- IList interface, grouping data in collections
- IDictionary interface, grouping data in collections
- grouping data in collections, generic collection types
- Collections classes
- generic collections
ms.assetid: f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55
caps.latest.revision: 29
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 1f8d938d61492b4da4b35a56fba169a12ed4787e
ms.lasthandoff: 04/18/2017

---
# <a name="commonly-used-collection-types"></a>Tipi di raccolte comunemente utilizzate
I tipi di raccolta sono le varianti comuni delle raccolte di dati, ad esempio tabelle hash, code, stack, contenitori, dizionari ed elenchi.  
  
 Le raccolte si basano sulle interfacce <xref:System.Collections.ICollection>, <xref:System.Collections.IList>, <xref:System.Collections.IDictionary> o sulle relative controparti generiche. Le interfacce <xref:System.Collections.IList> e <xref:System.Collections.IDictionary> derivano entrambe dall'interfaccia <xref:System.Collections.ICollection>; pertanto, tutte le raccolte si basano sull'interfaccia <xref:System.Collections.ICollection>, direttamente o indirettamente. Nelle raccolte che si basano sull'interfaccia <xref:System.Collections.IList> (<xref:System.Array>, <xref:System.Collections.ArrayList> o <xref:System.Collections.Generic.List%601>) o direttamente sull'interfaccia <xref:System.Collections.ICollection> (quali <xref:System.Collections.Queue>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Stack>, <xref:System.Collections.Concurrent.ConcurrentStack%601> o <xref:System.Collections.Generic.LinkedList%601>) ogni elemento contiene un solo valore. Nelle raccolte che si basano sull'interfaccia <xref:System.Collections.IDictionary> (come le classi <xref:System.Collections.Hashtable> e <xref:System.Collections.SortedList> e le classi generiche <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Generic.SortedList%602>), oppure nelle classi <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, ogni elemento contiene sia una chiave che un valore.  La classe <xref:System.Collections.ObjectModel.KeyedCollection%602> è univoca perché è un elenco di valori con le chiavi incorporate nei valori e quindi funge da elenco e da dizionario.  
  
 Le raccolte generiche rappresentano la migliore soluzione per la tipizzazione forte. Tuttavia, se il linguaggio non supporta i generics, lo spazio dei nomi <xref:System.Collections> include le raccolte di base, come <xref:System.Collections.CollectionBase>, <xref:System.Collections.ReadOnlyCollectionBase> e <xref:System.Collections.DictionaryBase>, che sono classi di base astratte che possono essere estese per creare classi di raccolte fortemente tipizzate. Quando è necessario accedere a raccolte con multithreading efficiente, usare le raccolte generiche nello spazio dei nomi <xref:System.Collections.Concurrent>.  
  
 Le raccolte possono variare a seconda di come vengono archiviati gli elementi, la modalità di ordinamento, la modalità di ricerca e confronto. La classe <xref:System.Collections.Queue> e la classe generica <xref:System.Collections.Generic.Queue%601> forniscono elenchi first-in-first-out (FIFO), mentre la classe <xref:System.Collections.Stack> e la classe generica <xref:System.Collections.Generic.Stack%601> forniscono elenchi last-in-first-out (LIFO). La classe <xref:System.Collections.SortedList> e la classe generica <xref:System.Collections.Generic.SortedList%602> forniscono versioni ordinate della classe <xref:System.Collections.Hashtable> e della classe generica <xref:System.Collections.Generic.Dictionary%602>. Gli elementi di una classe <xref:System.Collections.Hashtable> o <xref:System.Collections.Generic.Dictionary%602> sono accessibili solo tramite la chiave dell'elemento, mentre gli elementi di una classe <xref:System.Collections.SortedList> o <xref:System.Collections.ObjectModel.KeyedCollection%602> sono accessibili sia tramite la chiave sia tramite l'indice dell'elemento. Gli indici di tutte le raccolte sono in base zero, ad eccezione di <xref:System.Array>, che consente matrici non in base zero.  
  
 La funzionalità LINQ to Objects consente agli sviluppatori di usare le query LINQ per accedere agli oggetti in memoria, a condizione che il tipo dell'oggetto implementi l'interfaccia <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>. Le query LINQ forniscono un modello comune per l'accesso ai dati, sono in genere più concise e leggibili dei cicli standard `foreach` e forniscono funzioni di filtro, ordinamento e raggruppamento. Le query LINQ possono inoltre migliorare le prestazioni. Per altre informazioni, vedere [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9) e [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Raccolte e strutture di dati](../../../docs/standard/collections/index.md)|Vengono descritti i diversi tipi di raccolta disponibili in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], compresi stack, code, elenchi, matrici e dizionari.|  
|[Tipi di Collection Hashtable e Dictionary](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Vengono descritte le funzionalità dei tipi di dizionario basati su hash generici e non generici.|  
|[Tipi di raccolta ordinati](../../../docs/standard/collections/sorted-collection-types.md)|Vengono descritte le classi che forniscono funzionalità di ordinamento per elenchi e set.|  
|[Generics](../../../docs/standard/generics/index.md)|Viene descritta la funzionalità generics, compresi delegati, interfacce e raccolte generiche fornite da [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Vengono forniti collegamenti alla documentazione sulle funzionalità per i linguaggi C#, Visual Basic e Visual C++ e a tecnologie di supporto come reflection.|  
  
## <a name="reference"></a>Riferimento  
 <xref:System.Collections?displayProperty=fullName>  
  
 <xref:System.Collections.Generic?displayProperty=fullName>  
  
 <xref:System.Collections.ICollection?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>  
  
 <xref:System.Collections.IList?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.IList%601?displayProperty=fullName>  
  
 <xref:System.Collections.IDictionary?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>
