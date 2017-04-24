---
title: "Raccolte e strutture di dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "raggruppamento di dati in raccolte"
  - "oggetti [.NET Framework], raggruppamento in raccolte"
  - "Array (classe), raggruppamento di dati in raccolte"
  - "threading [.NET Framework], sicurezza"
  - "Classi Collection"
  - "raccolte [.NET Framework]"
ms.assetid: 60cc581f-1db5-445b-ba04-a173396bf872
caps.latest.revision: 36
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 35
---
# Raccolte e strutture di dati
Dati simili possono spesso essere gestiti in modo più efficiente quando memorizzati e modificati come una raccolta. È possibile utilizzare il <xref:System.Array?displayProperty=fullName> classe o le classi di <xref:System.Collections>, <xref:System.Collections.Generic>, <xref:System.Collections.Concurrent>, System.Collections.Immutable gli spazi dei nomi da aggiungere, rimuovere e modificare singoli elementi o un intervallo di elementi in una raccolta.  
  
 Esistono due tipi principali di raccolte: raccolte generiche e raccolte non generiche. Le raccolte generiche sono state aggiunte in.NET Framework 2.0 e sono indipendenti dai tipi in fase di compilazione. Per questo motivo, le raccolte generiche offrono in genere prestazioni migliori. Le raccolte generiche accettano un parametro di tipo quando vengono costruite e non richiedono il cast da e verso il tipo <xref:System.Object> quando si aggiungono o rimuovono elementi dalla raccolta.  Inoltre, gran parte delle raccolte generiche sono supportate nelle applicazioni [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]. Raccolte non generiche memorizzano elementi come <xref:System.Object>, richiedono il cast e molte non sono supportate per [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)] lo sviluppo di app. Tuttavia, si possono vedere raccolte non generiche nel codice precedente.  
  
 A partire dal [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], gli insiemi di <xref:System.Collections.Concurrent> dello spazio dei nomi forniscono operazioni thread-safe efficienti per accedere agli elementi della raccolta da più thread. Le classi di raccolte non modificabili nello spazio dei nomi System.Collections.Immutable ([pacchetto NuGet](https://www.nuget.org/packages/System.Collections.Immutable)) sono intrinsecamente thread-safe in quanto le operazioni su una copia della raccolta originale e della raccolta originale non può essere modificata.  
  
   
  
<a name="BKMK_Commoncollectionfeatures"></a>   
## <a name="common-collection-features"></a>Funzionalità comuni delle raccolte  
 Tutte le raccolte forniscono metodi per l'aggiunta, la rimozione o la ricerca di elementi nella raccolta. Inoltre, tutte le raccolte che implementano direttamente o indirettamente il <xref:System.Collections.ICollection> interfaccia o <xref:System.Collections.Generic.ICollection%601> interfaccia condividere queste funzionalità:  
  
-   **La possibilità di enumerare la raccolta**  
  
     Raccolte di .NET framework implementano <xref:System.Collections.IEnumerable?displayProperty=fullName> oppure <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> per abilitare la raccolta di iterazione. Un enumeratore può essere considerato come un puntatore che si sposta a qualsiasi elemento nella raccolta. Il [foreach, in](../Topic/foreach,%20in%20\(C%23%20Reference\).md) istruzione e [For Each... Istruzione successiva](../Topic/For%20Each...Next%20Statement%20\(Visual%20Basic\).md) utilizzare l'enumeratore esposto dal <xref:System.Collections.IEnumerable.GetEnumerator%2A> metodo e nascondono la complessità di gestione dell'enumeratore. Inoltre, qualsiasi raccolta che implementi <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> viene considerato un *tipo queryable* e possono essere sottoposti a query con LINQ. Le query LINQ forniscono un modello comune per l'accesso ai dati. In genere sono più concise e leggibili dei cicli `foreach` standard e forniscono funzionalità di filtro, ordinamento e raggruppamento. Le query LINQ possono inoltre migliorare le prestazioni. Per ulteriori informazioni, vedere [LINQ to Objects](../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-objects.md), [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md) e [Introduzione alle query LINQ (c#)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md).  
  
-   **La possibilità di copiare il contenuto della raccolta in una matrice**  
  
     Tutte le raccolte possono essere copiate in una matrice utilizzando la **CopyTo** metodo; tuttavia, l'ordine degli elementi nella nuova matrice si basa sulla sequenza in cui vengono restituiti dall'enumeratore. La matrice risultante è sempre unidimensionale con limite inferiore pari a zero.  
  
 Inoltre, molte classi di raccolte contengono le seguenti funzionalità:  
  
-   **Proprietà capacità e conteggio**  
  
     La capacità di una raccolta è il numero di elementi che può contenere. Il conteggio di una raccolta è il numero di elementi che contiene effettivamente. Alcune raccolte nascondono la capacità o il conteggio oppure entrambi.  
  
     La capacità della maggior parte delle raccolte si espande automaticamente quando viene raggiunta la capacità corrente. La memoria viene riallocata e gli elementi vengono copiati dalla raccolta precedente a quella nuova. Ciò riduce la quantità di codice necessario per usare la raccolta. Tuttavia, le prestazioni della raccolta possono essere influenzate negativamente. Ad esempio, per <xref:System.Collections.Generic.List%601>, se <xref:System.Collections.Generic.List%601.Count%2A> è minore di <xref:System.Collections.Generic.List%601.Capacity%2A>, aggiunta di un elemento è un'operazione o (1). Se la capacità deve essere incrementata per far posto al nuovo elemento, l'aggiunta di un elemento diventa un'operazione o (n), dove n è <xref:System.Collections.Generic.List%601.Count%2A>. Il modo migliore per evitare una riduzione delle prestazioni causata da più riallocazioni consiste nell'impostare la capacità iniziale sulla dimensione prevista della raccolta.  
  
     Un <xref:System.Collections.BitArray> è un caso speciale: la sua capacità corrisponde alla lunghezza, che equivale al conteggio.  
  
-   **Un limite inferiore coerente**  
  
     Il limite inferiore di una raccolta è l'indice del primo elemento. Tutte le raccolte indicizzate negli spazi dei nomi <xref:System.Collections> hanno un limite inferiore pari a zero, ossia possono essere indicizzate da 0. <xref:System.Array> ha un limite inferiore pari a zero per impostazione predefinita, ma può definire un limite inferiore differente durante la creazione di un'istanza del **matrice** usando <xref:System.Array.CreateInstance%2A?displayProperty=fullName>.  
  
-   **Sincronizzazione per l'accesso da più thread** (solo classi <xref:System.Collections>).  
  
     Tipi di raccolte non generiche nel <xref:System.Collections> dello spazio dei nomi forniscono una determinata thread safety con la sincronizzazione, in genere esposte attraverso il <xref:System.Collections.ICollection.SyncRoot%2A> e <xref:System.Collections.ICollection.IsSynchronized%2A> membri. Queste raccolte non sono thread-safe per impostazione predefinita. Se si richiede un accesso multithreading scalabile ed efficiente a una raccolta, usare una delle classi nello spazio dei nomi <xref:System.Collections.Concurrent> o considerare l'uso di una raccolta non modificabile. Per altre informazioni, vedere [Raccolte thread-safe](../../../docs/standard/collections/thread-safe/index.md).  
  
<a name="BKMK_Choosingacollection"></a>   
## <a name="choosing-a-collection"></a>Scelta di una raccolta  
 In generale, è necessario usare raccolte generiche. Nella tabella seguente vengono descritti alcuni scenari comuni di raccolta e le classi di raccolta che è possibile usare per gli scenari. Se si ha già familiarità con le raccolte generiche, questa tabella consente di scegliere la raccolta generica più adatta alla propria attività.  
  
|||||  
|-|-|-|-|  
|Si desidera...|Opzioni di raccolta generica|Opzioni di raccolta non generica|Opzioni di raccolta thread-safe o non modificabile|  
|Archiviare gli elementi come coppie chiave/valore per la ricerca rapida dalla chiave|<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName></TKey, TValue>|<xref:System.Collections.Hashtable><br /><br /> (Una raccolta di coppie chiave/valore che sono organizzate in base al codice hash della chiave).|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>\</TKey, TValue><br /><br /> <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=fullName>\</TKey, TValue><br /><br /> [Classe ImmutableDictionary (TKey, TValue)](../Topic/ImmutableDictionary\(TKey,%20TValue\)%20Class.md)|  
|Accedere agli elementi in base all'indice|<xref:System.Collections.Generic.List%601?displayProperty=fullName>|<xref:System.Array?displayProperty=fullName><br /><br /> <xref:System.Collections.ArrayList?displayProperty=fullName>|[Classe ImmutableList(T)](../Topic/ImmutableList\(T\)%20Class.md)<br /><br /> [Classe ImmutableArray](../Topic/ImmutableArray%20Class.md)|  
|Usare gli elementi first-in-first-out (FIFO)|<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>|<xref:System.Collections.Queue?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName><br /><br /> [Classe ImmutableQueue(T)](../Topic/ImmutableQueue\(T\)%20Class.md)|  
|Usare i dati Last-In-First-Out (LIFO)|<xref:System.Collections.Generic.Stack%601?displayProperty=fullName>|<xref:System.Collections.Stack?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName><br /><br /> [Classe ImmutableStack(T)](../Topic/ImmutableStack\(T\)%20Class.md)|  
|Accedere agli elementi in sequenza|<xref:System.Collections.Generic.LinkedList%601?displayProperty=fullName>|Nessuna raccomandazione|Nessuna raccomandazione|  
|Ricevere notifiche quando gli elementi vengono rimossi o aggiunti alla raccolta. (implementa <xref:System.ComponentModel.INotifyPropertyChanged> e <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=fullName>)|<xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=fullName>|Nessuna raccomandazione|Nessuna raccomandazione|  
|Una raccolta ordinata|<xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>\</TKey, TValue>|<xref:System.Collections.SortedList?displayProperty=fullName>|[Classe ImmutableSortedDictionary (TKey, TValue)](../Topic/ImmutableSortedDictionary\(TKey,%20TValue\)%20Class.md)<br /><br /> [Classe ImmutableSortedSet(T)](../Topic/ImmutableSortedSet\(T\)%20Class.md)|  
|Un set di funzioni matematiche|<xref:System.Collections.Generic.HashSet%601?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName>|Nessuna raccomandazione|[Classe ImmutableHashSet(T)](../Topic/ImmutableHashSet\(T\)%20Class.md)<br /><br /> [Classe ImmutableSortedSet(T)](../Topic/ImmutableSortedSet\(T\)%20Class.md)|  
  
<a name="BKMK_RelatedTopics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Selezione di una classe Collection](../../../docs/standard/collections/selecting-a-collection-class.md)|Vengono descritte le diverse raccolte e come selezionarne una per lo scenario.|  
|[Tipi di raccolte comunemente utilizzate](../../../docs/standard/collections/commonly-used-collection-types.md)|Vengono descritti i tipi di raccolta generici e non generici comunemente utilizzati, ad esempio <xref:System.Array?displayProperty=fullName>, <xref:System.Collections.Generic.List%601?displayProperty=fullName>, e <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>.\</TKey, TValue>|  
|[Quando utilizzare raccolte generiche](../../../docs/standard/collections/when-to-use-generic-collections.md)|Viene illustrato l'utilizzo di tipi di raccolta generici.|  
|[Confronti e ordinamenti all'interno delle raccolte](../../../docs/standard/collections/comparisons-and-sorts-within-collections.md)|Viene illustrato l'utilizzo di confronti di uguaglianza e ordinamento nelle raccolte.|  
|[Tipi di raccolta ordinati](../../../docs/standard/collections/sorted-collection-types.md)|Vengono descritte le caratteristiche e le prestazioni di raccolte ordinate|  
|[Tipi di Collection Hashtable e Dictionary](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Vengono descritte le funzionalità dei tipi di dizionario basati su hash generici e non generici.|  
|[Raccolte thread-safe](../../../docs/standard/collections/thread-safe/index.md)|Vengono descritti i tipi di raccolta quali <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> e <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName> che supportano l'accesso simultaneo sicuro ed efficiente da più thread.|  
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