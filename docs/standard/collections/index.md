---
title: Raccolte e strutture di dati | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- grouping data in collections
- objects [.NET Framework], grouping in collections
- Array class, grouping data in collections
- threading [.NET Framework], safety
- Collections classes
- collections [.NET Framework]
ms.assetid: 60cc581f-1db5-445b-ba04-a173396bf872
caps.latest.revision: 36
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: c50b3e328998b65ec47efe6d7457b36116813c77
ms.openlocfilehash: 27c475b8d29eb295bb3d6be24aa9ee9188f5c114
ms.lasthandoff: 04/08/2017

---
# <a name="collections-and-data-structures"></a>Raccolte e strutture di dati
Dati simili possono spesso essere gestiti in modo più efficiente quando memorizzati e modificati come una raccolta. È possibile usare la classe <xref:System.Array?displayProperty=fullName> o le classi nello spazio dei nomi <xref:System.Collections>, <xref:System.Collections.Generic>, <xref:System.Collections.Concurrent>, System.Collections.Immutable per aggiungere, rimuovere e modificare singoli elementi o un intervallo di elementi in una raccolta.  
  
 Esistono due tipi principali di raccolte: raccolte generiche e raccolte non generiche. Le raccolte generiche sono state aggiunte in.NET Framework 2.0 e sono indipendenti dai tipi in fase di compilazione. Per questo motivo, le raccolte generiche offrono in genere prestazioni migliori. Le raccolte generiche accettano un parametro di tipo quando vengono costruite e non richiedono il cast da e verso il tipo <xref:System.Object> quando si aggiungono o rimuovono elementi dalla raccolta.  Inoltre, gran parte delle raccolte generiche sono supportate nelle applicazioni [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]. Le raccolte non generiche memorizzano elementi come <xref:System.Object>, richiedono il cast e molte non sono supportate per lo sviluppo di applicazioni [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]. Tuttavia, si possono vedere raccolte non generiche nel codice precedente.  
  
 A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], le raccolte nello spazio dei nomi <xref:System.Collections.Concurrent> forniscono operazioni thread-safe efficienti per accedere agli elementi della raccolta da più thread. Le classi di raccolte non modificabili dello spazio dei nomi System.Collections.Immutable ([Pacchetto NuGet](https://www.nuget.org/packages/System.Collections.Immutable)) sono intrinsecamente thread-safe, perché le operazioni vengono eseguite su una copia della raccolta originale, che non può essere modificata.  
  
  
<a name="BKMK_Commoncollectionfeatures"></a>   
## <a name="common-collection-features"></a>Funzionalità comuni delle raccolte  
 Tutte le raccolte forniscono metodi per l'aggiunta, la rimozione o la ricerca di elementi nella raccolta. Inoltre, tutte le raccolte che implementano direttamente o indirettamente l'interfaccia <xref:System.Collections.ICollection> o <xref:System.Collections.Generic.ICollection%601> condividono le funzionalità seguenti:  
  
-   **La possibilità di enumerare la raccolta**  
  
     Le raccolte di .NET Framework implementano <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> per consentire l'iterazione attraverso la raccolta. Un enumeratore può essere considerato come un puntatore che si sposta a qualsiasi elemento nella raccolta. L'istruzione [foreach, in](~/docs/csharp/language-reference/keywords/foreach-in.md) e [For Each...Next](~/docs/visual-basic/language-reference/statements/for-each-next-statement.md) usano l'enumeratore esposto dal metodo <xref:System.Collections.IEnumerable.GetEnumerator%2A> e nascondono la complessità di gestione dell'enumeratore. Inoltre, qualsiasi raccolta che implementi <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> vene considerata un *tipo queryable* e può essere sottoposta a query con LINQ. Le query LINQ forniscono un modello comune per l'accesso ai dati. In genere sono più concise e leggibili dei cicli `foreach` standard e forniscono funzionalità di filtro, ordinamento e raggruppamento. Le query LINQ possono inoltre migliorare le prestazioni. Per altre informazioni, vedere [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9), [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md) e [Introduzione alle query LINQ (C#)](~/docs/csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
-   **La possibilità di copiare il contenuto della raccolta in una matrice**  
  
     Tutti le raccolte possono essere copiate in una matrice usando il metodo **CopyTo**. Tuttavia, l'ordine degli elementi nella nuova matrice si basa sulla sequenza in cui vengono restituiti dall'enumeratore. La matrice risultante è sempre unidimensionale con limite inferiore pari a zero.  
  
 Inoltre, molte classi di raccolte contengono le seguenti funzionalità:  
  
-   **Proprietà capacità e conteggio**  
  
     La capacità di una raccolta è il numero di elementi che può contenere. Il conteggio di una raccolta è il numero di elementi che contiene effettivamente. Alcune raccolte nascondono la capacità o il conteggio oppure entrambi.  
  
     La capacità della maggior parte delle raccolte si espande automaticamente quando viene raggiunta la capacità corrente. La memoria viene riallocata e gli elementi vengono copiati dalla raccolta precedente a quella nuova. Ciò riduce la quantità di codice necessario per usare la raccolta. Tuttavia, le prestazioni della raccolta possono essere influenzate negativamente. Ad esempio, per <xref:System.Collections.Generic.List%601>, se <xref:System.Collections.Generic.List%601.Count%2A> è minore di <xref:System.Collections.Generic.List%601.Capacity%2A>, l'aggiunta di un elemento è un'operazione O(1). Se la capacità deve essere incrementata per far posto al nuovo elemento, l'aggiunta di un elemento diventa un'operazione O(n), dove n è <xref:System.Collections.Generic.List%601.Count%2A>. Il modo migliore per evitare una riduzione delle prestazioni causata da più riallocazioni consiste nell'impostare la capacità iniziale sulla dimensione prevista della raccolta.  
  
     Un <xref:System.Collections.BitArray> è un caso speciale: la sua capacità corrisponde alla lunghezza, che equivale al conteggio.  
  
-   **Un limite inferiore coerente**  
  
     Il limite inferiore di una raccolta è l'indice del primo elemento. Tutte le raccolte indicizzate negli spazi dei nomi <xref:System.Collections> hanno un limite inferiore pari a zero, ossia possono essere indicizzate da 0. <xref:System.Array> ha un limite inferiore pari a zero per impostazione predefinita, ma è possibile definire un limite inferiore differente durante la creazione di un'istanza della classe **Array** con <xref:System.Array.CreateInstance%2A?displayProperty=fullName>.  
  
-   **Sincronizzazione per l'accesso da più thread** (solo classi <xref:System.Collections>).  
  
     I tipi di raccolta non generici nello spazio dei nomi <xref:System.Collections> forniscono la thread safety con sincronizzazione e sono in genere esposti attraverso i membri <xref:System.Collections.ICollection.SyncRoot%2A> e <xref:System.Collections.ICollection.IsSynchronized%2A>. Queste raccolte non sono thread-safe per impostazione predefinita. Se si richiede un accesso multithreading scalabile ed efficiente a una raccolta, usare una delle classi nello spazio dei nomi <xref:System.Collections.Concurrent> o considerare l'uso di una raccolta non modificabile. Per altre informazioni, vedere [Raccolte thread-safe](../../../docs/standard/collections/thread-safe/index.md).  
  
<a name="BKMK_Choosingacollection"></a>   
## <a name="choosing-a-collection"></a>Scelta di una raccolta  
 In generale, è necessario usare raccolte generiche. Nella tabella seguente vengono descritti alcuni scenari comuni di raccolta e le classi di raccolta che è possibile usare per gli scenari. Se si ha già familiarità con le raccolte generiche, questa tabella consente di scegliere la raccolta generica più adatta alla propria attività.  
<!-- todo: All code-formatted API refs in the table need to be changed into links -->  
|Si desidera...|Opzioni di raccolta generica|Opzioni di raccolta non generica|Opzioni di raccolta thread-safe o non modificabile|  
|-|-|-|-|  
|Archiviare gli elementi come coppie chiave/valore per la ricerca rapida dalla chiave|<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>|<xref:System.Collections.Hashtable><br /><br /> (Una raccolta di coppie chiave/valore che sono organizzate in base al codice hash della chiave).|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName><br /><br /> <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=fullName><br /><br /> `ImmutableDictionary(TKey, TValue) Class`|  
|Accedere agli elementi in base all'indice|<xref:System.Collections.Generic.List%601?displayProperty=fullName>|<xref:System.Array?displayProperty=fullName><br /><br /> <xref:System.Collections.ArrayList?displayProperty=fullName>|`ImmutableList(T) Class`<br /><br /> `ImmutableArray Class`|  
|Usare gli elementi first-in-first-out (FIFO)|<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>|<xref:System.Collections.Queue?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName><br /><br /> `ImmutableQueue(T) Class`|  
|Usare i dati Last-In-First-Out (LIFO)|<xref:System.Collections.Generic.Stack%601?displayProperty=fullName>|<xref:System.Collections.Stack?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName><br /><br /> `ImmutableStack(T) Class`|  
|Accedere agli elementi in sequenza|<xref:System.Collections.Generic.LinkedList%601?displayProperty=fullName>|Nessuna raccomandazione|Nessuna raccomandazione|  
|Ricevere notifiche quando gli elementi vengono rimossi o aggiunti alla raccolta. (implementa <xref:System.ComponentModel.INotifyPropertyChanged> e <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=fullName>)|<xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=fullName>|Nessuna raccomandazione|Nessuna raccomandazione|  
|Una raccolta ordinata|<xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>|<xref:System.Collections.SortedList?displayProperty=fullName>|`ImmutableSortedDictionary(TKey, TValue) Class`<br /><br /> `ImmutableSortedSet(T) Class`|  
|Un set di funzioni matematiche|<xref:System.Collections.Generic.HashSet%601?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName>|Nessuna raccomandazione|`ImmutableHashSet(T) Class`<br /><br /> `ImmutableSortedSet(T) Class`|  
  
<a name="BKMK_RelatedTopics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Selezione di una classe Collection](../../../docs/standard/collections/selecting-a-collection-class.md)|Vengono descritte le diverse raccolte e come selezionarne una per lo scenario.|  
|[Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)|Descrive i tipi di raccolta generici e non generici comunemente usati, ad esempio <xref:System.Array?displayProperty=fullName>, <xref:System.Collections.Generic.List%601?displayProperty=fullName> e <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>.|  
|[Quando utilizzare raccolte generiche](../../../docs/standard/collections/when-to-use-generic-collections.md)|Viene illustrato l'utilizzo di tipi di raccolta generici.|  
|[Confronti e ordinamenti all'interno delle raccolte](../../../docs/standard/collections/comparisons-and-sorts-within-collections.md)|Viene illustrato l'utilizzo di confronti di uguaglianza e ordinamento nelle raccolte.|  
|[Tipi di raccolta ordinati](../../../docs/standard/collections/sorted-collection-types.md)|Vengono descritte le caratteristiche e le prestazioni di raccolte ordinate|  
|[Tipi di Collection Hashtable e Dictionary](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Vengono descritte le funzionalità dei tipi di dizionario basati su hash generici e non generici.|  
|[Raccolte thread-safe](../../../docs/standard/collections/thread-safe/index.md)|Descrive i tipi di raccolta, come <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> e <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName>, che supportano l'accesso simultaneo, sicuro ed efficiente da più thread.|  
|System.Collections.Immutable|Introduce le raccolte non modificabili e fornisce collegamenti ai tipi di raccolta.|  
  
<a name="BKMK_Reference"></a>   
## <a name="reference"></a>Riferimento  
 <xref:System.Array?displayProperty=fullName>  
  
 <xref:System.Collections?displayProperty=fullName>  
  
 <xref:System.Collections.Concurrent?displayProperty=fullName>  
  
 <xref:System.Collections.Generic?displayProperty=fullName>  
  
 <xref:System.Collections.Specialized?displayProperty=fullName>  
  
 <xref:System.Linq?displayProperty=fullName>  
  
 System.Collections.Immutable
