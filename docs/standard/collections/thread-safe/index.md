---
title: "Raccolte thread-safe | Microsoft Docs"
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
  - "raccolte thread-safe, panoramica"
ms.assetid: 2e7ca21f-786c-4367-96be-0cf3f3dcc6bd
caps.latest.revision: 24
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 24
---
# Raccolte thread-safe
[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] introduce lo spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName>, il quale include diverse classi di raccolte che sono thread\-safe e scalabili.  Più thread possono aggiungere o rimuovere elementi da queste raccolte in modo sicuro ed efficiente senza richiedere una sincronizzazione aggiuntiva nel codice utente.  Quando si scrive nuovo codice, utilizzare le classi di raccolte simultanee ogni qualvolta la raccolta scriverà contemporaneamente in più thread.  In caso di semplice lettura da una raccolta condivisa, è possibile utilizzare le classi nello spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>.  Si consiglia di non utilizzare le classi di raccolte 1.0 a meno che la destinazione richiesta non sia il runtime di .NET Framework 1.1 o precedente.  
  
## Sincronizzazione dei thread nelle raccolte di .NET Framework 1.0 e 2.0  
 Le raccolte introdotte in .NET Framework 1.0 sono contenute nello spazio dei nomi <xref:System.Collections?displayProperty=fullName>.  Queste raccolte, che includono gli oggetti <xref:System.Collections.ArrayList> e <xref:System.Collections.Hashtable> di uso comune, forniscono un buon grado di thread safety tramite la proprietà `Synchronized`, la quale restituisce un wrapper thread\-safe per la raccolta.  Il funzionamento del wrapper consiste nel bloccare l'intera raccolta a ogni operazione di aggiunta o rimozione.  Pertanto, ogni thread che tenta di accedere alla raccolta deve attendere il proprio turno per acquisire l'unico blocco.  Questo non è scalabile e può provocare un significativo calo delle prestazioni per le raccolte di grandi dimensioni.  La progettazione, inoltre, non è completamente protetta dalle race condition.  Per ulteriori informazioni, consultare [Sincronizzazione nelle raccolte generiche](http://go.microsoft.com/fwlink/?LinkID=161130) sul sito Web MSDN.  
  
 Le classi di raccolte introdotte in .NET Framework 2.0 sono contenute nello spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>.  Alcuni esempi sono <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.Dictionary%602> e così via.  Queste classi forniscono un'indipendenza dai tipi e prestazioni migliorate rispetto alle classi di .NET Framework 1.0.  Tuttavia, le classi di raccolte di .NET Framework 2.0 non forniscono alcuna sincronizzazione dei thread; è il codice utente a dover fornire la sincronizzazione nel momento in cui vengono aggiunti o rimossi elementi in più thread contemporaneamente.  
  
 Si consigliano le classi di raccolte simultanee in [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] in quanto forniscono non solo l'indipendenza dai tipi delle classi di raccolte di .NET Framework 2.0, ma anche una thread safety più efficiente e completa rispetto alle raccolte di [!INCLUDE[net_v10_short](../../../../includes/net-v10-short-md.md)].  
  
## Blocco con granularità fine e meccanismi senza blocco  
 Alcuni tipi di raccolte simultanee utilizzano meccanismi di sincronizzazione leggeri quali <xref:System.Threading.SpinLock>, <xref:System.Threading.SpinWait>, <xref:System.Threading.SemaphoreSlim> e <xref:System.Threading.CountdownEvent>, che rappresentano una novità di [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].  Questi tipi di sincronizzazione utilizzano in genere lo *spin intenso* per brevi periodi prima di impostare lo stato di attesa del thread su true.  Quando si prevedono tempi di attesa molto brevi, lo spin risulta di gran lunga meno dispendioso in termini di calcolo rispetto all'attesa, che implica una transizione del kernel dispendiosa.  Per le classi di raccolte che utilizzano lo spin, questa efficienza significa che più thread possono aggiungere e rimuovere elementi con una frequenza molto elevata.  Per ulteriori informazioni e un confronto tra spin e blocco, consultare [SpinLock](../../../../docs/standard/threading/spinlock.md) e [SpinWait](../../../../docs/standard/threading/spinwait.md).  
  
 Le classi <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601> non utilizzano mai i blocchi.  Al contrario, si basano su operazioni <xref:System.Threading.Interlocked> per ottenere la thread safety.  
  
> [!NOTE]
>  Poiché le classi di raccolte simultanee supportano <xref:System.Collections.ICollection>, forniscono le implementazioni per le proprietà <xref:System.Collections.ICollection.IsSynchronized%2A> e <xref:System.Collections.ICollection.SyncRoot%2A>, anche se queste proprietà sono irrilevanti.  `IsSynchronized` restituisce sempre `false` e `SyncRoot` è sempre `null` \(`Nothing` in Visual Basic\).  
  
 Nella tabella riportata di seguito sono elencati i tipi di raccolte contenuti nello spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName>.  
  
|Type|Descrizione|  
|----------|-----------------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601>|Fornisce funzionalità di delimitazione e blocco per tutti i tipi che implementano <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>.  Per ulteriori informazioni, vedere [Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602>|Implementazione thread\-safe di un dizionario di coppie chiave\-valore.|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601>|Implementazione thread\-safe di una coda FIFO \(First In First Out\).|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601>|Implementazione thread\-safe di uno stack LIFO \(Last In First Out\).|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601>|Implementazione thread\-safe di una raccolta non ordinata di elementi.|  
|<xref:System.Collections.Concurrent.IProducerConsumerCollection%601>|Interfaccia che un tipo deve implementare per essere utilizzato in un oggetto `BlockingCollection`.|  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Panoramica di BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)|Vengono descritte le funzionalità fornite dal tipo <xref:System.Collections.Concurrent.BlockingCollection%601>.|  
|[Procedura: aggiungere e rimuovere elementi da un oggetto ConcurrentDictionary](../../../../docs/standard/collections/thread-safe/how-to-add-and-remove-items.md)|Viene descritto come aggiungere e rimuovere elementi da un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602>|  
|[Procedura: Aggiungere e rimuovere singoli elementi di un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md)|Viene descritto come aggiungere e recuperare elementi da una raccolta di blocco senza utilizzare l'enumeratore di sola lettura.|  
|[Procedura: Aggiungere funzionalità di delimitazione e blocco a una raccolta](../../../../docs/standard/collections/thread-safe/how-to-add-bounding-and-blocking.md)|Viene descritto come utilizzare una classe di raccolte come meccanismo di archiviazione sottostante per una raccolta <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>.|  
|[Procedura: utilizzare ForEach per rimuovere elementi in un oggetto BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md)|Viene descritto come utilizzare `foreach`, \(`For Each` in Visual Basic\) per rimuovere tutti gli elementi in una raccolta di blocco.|  
|[Procedura: utilizzare matrici di raccolte di blocco in una pipeline](../../../../docs/standard/collections/thread-safe/how-to-use-arrays-of-blockingcollections.md)|Viene descritto come utilizzare più raccolte di blocco contemporaneamente per implementare una pipeline.|  
|[Procedura: Creare un pool di oggetti con un oggetto ConcurrentBag](../../../../docs/standard/collections/thread-safe/how-to-create-an-object-pool.md)|Viene illustrato come utilizzare un contenitore simultaneo per migliorare le prestazioni in scenari in cui è possibile riutilizzare oggetti anziché crearne continuamente di nuovi.|  
  
## Riferimento  
 <xref:System.Collections.Concurrent?displayProperty=fullName>