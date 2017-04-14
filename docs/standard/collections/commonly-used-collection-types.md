---
title: "Tipi di raccolte comunemente utilizzate | Microsoft Docs"
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
  - "raccolte [.NET Framework], generiche"
  - "Collections (classi)"
  - "raccolte generiche"
  - "generics [.NET Framework], raccolte"
  - "raggruppamento di dati in raccolte, tipi di raccolte generiche"
  - "IDictionary (interfaccia), raggruppamento di dati in raccolte"
  - "IList (interfaccia), raggruppamento di dati in raccolte"
  - "oggetti [.NET Framework], raggruppamento in raccolte"
ms.assetid: f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55
caps.latest.revision: 29
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 29
---
# Tipi di raccolte comunemente utilizzate
I tipi di raccolta sono le varianti comuni delle raccolte di dati, ad esempio tabelle hash, code, stack, contenitori, dizionari ed elenchi.  
  
 Le raccolte si basano sull'interfaccia <xref:System.Collections.ICollection>, l'interfaccia <xref:System.Collections.IList>, l'interfaccia <xref:System.Collections.IDictionary> oppure sulle relative controparti generiche.  L'interfaccia <xref:System.Collections.IList> e l'interfaccia <xref:System.Collections.IDictionary> derivano entrambe dall'interfaccia <xref:System.Collections.ICollection>. Di conseguenza, tutte le raccolte sono basate direttamente o indirettamente sull'interfaccia <xref:System.Collections.ICollection>.  Nelle raccolte basate sull'interfaccia <xref:System.Collections.IList> \(come ad esempio <xref:System.Array>, <xref:System.Collections.ArrayList> o <xref:System.Collections.Generic.List%601>\) oppure direttamente sull'interfaccia <xref:System.Collections.ICollection> \(come ad esempio <xref:System.Collections.Queue>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Stack>, <xref:System.Collections.Concurrent.ConcurrentStack%601> o <xref:System.Collections.Generic.LinkedList%601>\), ogni elemento contiene un valore.  Nelle raccolte basate sull'interfaccia <xref:System.Collections.IDictionary> \(come ad esempio le classi <xref:System.Collections.Hashtable> e <xref:System.Collections.SortedList>, le classi generiche <xref:System.Collections.Generic.Dictionary%602> e <xref:System.Collections.Generic.SortedList%602>\), oppure sulle classi <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, ogni elemento contiene sia una chiave sia un valore.  La classe <xref:System.Collections.ObjectModel.KeyedCollection%602> è univoca perché è un elenco di valori con le chiavi incorporate nei valori e quindi funge da elenco e da dizionario.  
  
 Le raccolte generiche rappresentano la migliore soluzione per la tipizzazione forte.  Tuttavia, se il linguaggio usato non supporta i generics, lo spazio dei nomi <xref:System.Collections> include le raccolte di base, come <xref:System.Collections.CollectionBase>, <xref:System.Collections.ReadOnlyCollectionBase> e <xref:System.Collections.DictionaryBase>, che sono classi di base astratte che possono essere estese in modo da creare classi di raccolta con tipizzazione forte.  Quando è necessario accedere a raccolte con multithreading efficiente, usare le raccolte generiche nello spazio dei nomi <xref:System.Collections.Concurrent>.  
  
 Le raccolte possono variare a seconda di come vengono archiviati gli elementi, la modalità di ordinamento, la modalità di ricerca e confronto.  La classe <xref:System.Collections.Queue> e la classe generica <xref:System.Collections.Generic.Queue%601> forniscono elenchi first\-in\-first\-out, mentre la classe <xref:System.Collections.Stack> e la classe generica <xref:System.Collections.Generic.Stack%601> forniscono elenchi last\-in\-first\-out.  La classe <xref:System.Collections.SortedList> e la classe generica <xref:System.Collections.Generic.SortedList%602> rappresentano versioni ordinate della classe <xref:System.Collections.Hashtable> e della classe generica <xref:System.Collections.Generic.Dictionary%602>.  Gli elementi di una <xref:System.Collections.Hashtable> o <xref:System.Collections.Generic.Dictionary%602> sono accessibili solo con la chiave dell'elemento, ma gli elementi di una <xref:System.Collections.SortedList> o <xref:System.Collections.ObjectModel.KeyedCollection%602> sono accessibili con la chiave oppure con l'indice dell'elemento.  Gli indici di tutte le raccolte sono a base zero, ad eccezione di <xref:System.Array>, che consente matrici non a base zero.  
  
 La funzionalità LINQ to Objects consente di usare le query LINQ per accedere agli oggetti in memoria purché il tipo dell'oggetto implementi <xref:System.Collections.IEnumerable> o <xref:System.Collections.Generic.IEnumerable%601>.  Le query LINQ forniscono un modello comune per l'accesso ai dati, sono in genere più concise e leggibili dei cicli standard `foreach` e forniscono funzioni di filtro, ordinamento e raggruppamento.  Le query LINQ possono inoltre migliorare le prestazioni.  Per altre informazioni, vedere [LINQ to Objects](../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-objects.md) e [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Raccolte e strutture di dati](../../../docs/standard/collections/index.md)|Vengono descritti i diversi tipi di raccolta disponibili in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], compresi stack, code, elenchi, matrici e dizionari.|  
|[Tipi di raccolte Hashtable e Dictionary](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Vengono descritte le funzionalità dei tipi di dizionario basati su hash generici e non generici.|  
|[Tipi di raccolta ordinati](../../../docs/standard/collections/sorted-collection-types.md)|Vengono descritte le classi che forniscono funzionalità di ordinamento per elenchi e set.|  
|[Generics](../../../docs/standard/generics/index.md)|Viene descritta la funzionalità generics, compresi delegati, interfacce e raccolte generiche fornite da [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  Vengono forniti collegamenti alla documentazione sulle funzionalità per i linguaggi C\#, Visual Basic e Visual C\+\+ e a tecnologie di supporto come reflection.|  
  
## Riferimento  
 <xref:System.Collections?displayProperty=fullName>  
  
 <xref:System.Collections.Generic?displayProperty=fullName>  
  
 <xref:System.Collections.ICollection?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>  
  
 <xref:System.Collections.IList?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.IList%601?displayProperty=fullName>  
  
 <xref:System.Collections.IDictionary?displayProperty=fullName>  
  
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>