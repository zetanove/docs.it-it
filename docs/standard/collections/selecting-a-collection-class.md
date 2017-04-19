---
title: Selezionare una classe Collection | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- last-in-first-out collections
- first-in-first-out collections
- collections [.NET Framework], selecting collection class
- indexed collections
- Collections classes
- grouping data in collections, selecting collection class
ms.assetid: ba049f9a-ce87-4cc4-b319-3f75c8ddac8a
caps.latest.revision: 20
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 403a78e3fc1496b91403b3c42494e34d12607b70
ms.lasthandoff: 04/18/2017

---
# <a name="selecting-a-collection-class"></a>Selezione di una classe Collection
Assicurarsi di scegliere con attenzione la classe Collection, poiché l'uso del tipo errato può limitare l'uso della raccolta. In generale, evitare di usare i tipi nello spazio dei nomi <xref:System.Collections> a meno che la destinazione specifica non sia .NET Framework versione 1.1. È preferibile usare le versioni generiche e simultanee delle raccolte per via di una maggiore indipendenza dai tipi e di altri miglioramenti.  
  
 Prendere in considerazione le domande seguenti:  
  
-   È necessario un elenco sequenziale quando l'elemento viene in genere eliminato dopo che il valore è stato recuperato?  
  
    -   Se la risposta è affermativa ed è necessario un comportamento FIFO (First In First Out), considerare l'uso della classe <xref:System.Collections.Queue> o della classe generica <xref:System.Collections.Generic.Queue%601>. Se è necessario un comportamento LIFO (Last In First Out), considerare l'uso della classe <xref:System.Collections.Stack> o della classe generica <xref:System.Collections.Generic.Stack%601>. Per un accesso sicuro da più thread, usare le versioni simultanee <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
    -   Se la risposta è negativa, è opportuno usare le altre raccolte.  
  
-   È necessario accedere agli elementi in un determinato ordine, ad esempio FIFO, LIFO o casuale?  
  
    -   La classe <xref:System.Collections.Queue> e la classe generica <xref:System.Collections.Generic.Queue%601> o <xref:System.Collections.Concurrent.ConcurrentQueue%601> consentono l'accesso FIFO. Per altre informazioni, vedere [When to Use a Thread-Safe Collection](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md) (Quando usare una raccolta thread-safe).  
  
    -   La classe <xref:System.Collections.Stack> e la classe generica <xref:System.Collections.Generic.Stack%601> o <xref:System.Collections.Concurrent.ConcurrentSTack%601> consentono l'accesso LIFO. Per altre informazioni, vedere [When to Use a Thread-Safe Collection](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md) (Quando usare una raccolta thread-safe).  
  
    -   La classe generica <xref:System.Collections.Generic.LinkedList%601> consente l'accesso sequenziale dall'inizio alla fine o viceversa.  
  
-   È necessario accedere a ciascun elemento tramite l'indice?  
  
    -   Le classi <xref:System.Collections.ArrayList> e <xref:System.Collections.Specialized.StringCollection> e la classe generica <xref:System.Collections.Generic.List%601> consentono l'accesso ai relativi elementi tramite l'indice in base zero dell'elemento.  
  
    -   Le classi <xref:System.Collections.Hashtable>, <xref:System.Collections.SortedList>, <xref:System.Collections.Specialized.ListDictionary> e <xref:System.Collections.Specialized.StringDictionary> e le classi generiche <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Generic.SortedDictionary%602> consentono l'accesso ai relativi elementi tramite la chiave dell'elemento.  
  
    -   Le classi <xref:System.Collections.Specialized.NameObjectCollectionBase> e <xref:System.Collections.Specialized.NameValueCollection> e le classi generiche <xref:System.Collections.ObjectModel.KeyedCollection%602> e <xref:System.Collections.Generic.SortedList%602> consentono l'accesso ai relativi elementi tramite l'indice in base zero o la chiave dell'elemento.  
  
-   Ogni elemento contiene un valore, una combinazione di una chiave e un valore o una combinazione di una chiave e più valori?  
  
    -   Un valore: usare una delle raccolte basate sull'interfaccia <xref:System.Collections.IList> o l'interfaccia generica <xref:System.Collections.Generic.IList%601>.  
  
    -   Una chiave e un valore: usare una delle raccolte basate sull'interfaccia <xref:System.Collections.IDictionary> o l'interfaccia generica <xref:System.Collections.Generic.IDictionary%602>.  
  
    -   Un valore con chiave incorporata: usare la classe generica <xref:System.Collections.ObjectModel.KeyedCollection%602>.  
  
    -   Una chiave e più valori: usare la classe <xref:System.Collections.Specialized.NameValueCollection>.  
  
-   È necessario ordinare gli elementi in modo diverso da come sono stati immessi?  
  
    -   La classe <xref:System.Collections.Hashtable> ordina gli elementi in base ai rispettivi codici hash.  
  
    -   La classe <xref:System.Collections.SortedList> e le classi generiche <xref:System.Collections.Generic.SortedDictionary%602> e <xref:System.Collections.Generic.SortedList%602> ordinano i relativi elementi in base alla chiave, facendo riferimento alle implementazioni dell'interfaccia <xref:System.Collections.IComparer> e dell'interfaccia generica <xref:System.Collections.Generic.IComparer%601>.  
  
    -   <xref:System.Collections.ArrayList> offre un metodo <xref:System.Collections.ArrayList.Sort%2A> che accetta un'implementazione <xref:System.Collections.IComparer> come parametro. La controparte generica, la classe generica <xref:System.Collections.Generic.List%601> offre un metodo <xref:System.Collections.Generic.List%601.Sort%2A> che accetta un'implementazione dell'interfaccia generica <xref:System.Collections.Generic.IComparer%601> come parametro.  
  
-   Sono necessarie le ricerche veloci e il recupero di informazioni?  
  
    -   <xref:System.Collections.Specialized.ListDictionary> è più veloce di <xref:System.Collections.Hashtable> per le raccolte dimensioni ridotte (non più di 10 elementi). La classe generica <xref:System.Collections.Generic.Dictionary%602> offre un sistema di ricerca più rapido della classe generica <xref:System.Collections.Generic.SortedDictionary%602>. L'implementazione multithread è <xref:System.Collections.Concurrent.ConcurrentDictionary%602>. <xref:System.Collections.Concurrent.ConcurrentBag%601> offre un rapido inserimento multithread per i dati non ordinati. Per altre informazioni su entrambi i tipi di multithread, vedere [Quando usare una raccolta thread-safe](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
-   Sono necessarie raccolte che accettano solo stringhe?  
  
    -   <xref:System.Collections.Specialized.StringCollection> (basata su <xref:System.Collections.IList>) e <xref:System.Collections.Specialized.StringDictionary> (basata su <xref:System.Collections.IDictionary>) sono nello spazio dei nomi <xref:System.Collections.Specialized>.  
  
    -   È anche possibile usare una qualsiasi classe di raccolte generiche nello spazio dei nomi <xref:System.Collections.Generic> come raccolte di stringhe fortemente tipizzate, specificando la classe <xref:System.String> per i relativi argomenti di tipo generico.  
  
## <a name="linq-to-objects-and-plinq"></a>LINQ to Objects e PLINQ  
 LINQ to Objects consente agli sviluppatori di usare le query LINQ per accedere agli oggetti in memoria, a condizione che il tipo dell'oggetto implementi <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>. Le query LINQ forniscono un modello comune per l'accesso ai dati, sono in genere più concise e leggibili dei cicli `foreach` standard e forniscono funzionalità di filtro, ordinamento e raggruppamento. Per altre informazioni, vedere [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9).  
  
 PLINQ fornisce un'implementazione parallela di LINQ to Objects in grado di offrire un'esecuzione più rapida delle query in molti scenari, grazie a un uso più efficiente dei computer multicore. Per altre informazioni, vedere [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections>   
 <xref:System.Collections.Specialized>   
 <xref:System.Collections.Generic>   
 [Raccolte thread-safe](../../../docs/standard/collections/thread-safe/index.md)
