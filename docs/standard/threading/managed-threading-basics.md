---
title: "Managed Threading Basics | Microsoft Docs"
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
  - "multiple threads"
  - "threading [.NET Framework], multiple threads"
  - "threading [.NET Framework], about threading"
  - "managed threading"
ms.assetid: b2944911-0e8f-427d-a8bb-077550618935
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Managed Threading Basics
Nei primi cinque argomenti di questa sezione verrà illustrato come stabilire quando utilizzare il threading gestito e verranno descritte alcune funzionalità di base.  Per informazioni sulle classi che forniscono funzionalità aggiuntive, vedere [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md) e [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md).  
  
 Negli altri argomenti di questa sezione verranno discussi argomenti avanzati, tra cui l'interazione del threading gestito con il sistema operativo Windows.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la libreria TPL \(Task Parallel Library\) e PLINQ forniscono le API per il parallelismo di attività e dati nei programmi a thread multipli.  Per ulteriori informazioni, vedere [Parallel Programming](../../../docs/standard/parallel-programming/index.md).  
  
## In questa sezione  
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)  
 Vengono illustrati i vantaggi e gli svantaggi di più thread e vengono delineati gli scenari in cui creare thread o utilizzare thread di pool di thread.  
  
 [Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)  
 Viene illustrato il comportamento delle eccezioni non gestite in thread per diverse versioni di .NET Framework, in particolare le situazioni in cui tali eccezioni determinano l'interruzione dell'applicazione.  
  
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)  
 Vengono descritte le strategie per la sincronizzazione di dati in classi utilizzate con più thread.  
  
 [Stati dei thread gestiti](../../../docs/standard/threading/managed-thread-states.md)  
 Vengono descritti gli stati di thread di base e viene illustrato come rilevare se un thread è in esecuzione.  
  
 [Foreground and Background Threads](../../../docs/standard/threading/foreground-and-background-threads.md)  
 Vengono illustrate le differenze tra thread in primo piano e in background.  
  
 [Managed and Unmanaged Threading in Windows](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)  
 Viene descritta la relazione tra threading gestito e non gestito, vengono elencati gli equivalenti gestiti delle API di threading di Windows e viene descritta l'interazione di apartment COM e thread gestiti.  
  
 [Thread.Suspend, Garbage Collection, and Safe Points](../../../docs/standard/threading/thread-suspend-garbage-collection-and-safe-points.md)  
 Vengono descritte la sospensione dei thread e le operazioni di Garbage Collection.  
  
 [Thread Local Storage: Thread\-Relative Static Fields and Data Slots](../../../docs/standard/threading/thread-local-storage-thread-relative-static-fields-and-data-slots.md)  
 Vengono descritti i meccanismi della memoria relativi ai thread.  
  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)  
 Viene descritto come le operazioni asincrone o sincrone a esecuzione prolungata possano essere annullate tramite un token di annullamento.  
  
## Riferimenti  
 <xref:System.Threading.Thread>  
 Viene fornita la documentazione di riferimento relativa alla classe **Thread** che rappresenta un thread gestito, indipendentemente dal fatto che provenga da codice non gestito o sia stato creato in un'applicazione gestita.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 Viene fornito un modo affidabile per implementare il multithreading insieme a oggetti dell'interfaccia utente.  
  
## Sezioni correlate  
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)  
 Viene descritta la classe gestita utilizzata per sincronizzare le attività di più thread.  
  
 [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md)  
 Vengono descritti i problemi che si riscontrano comunemente con i thread e vengono illustrate le strategie per evitarli.  
  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)  
 Vengono descritti la libreria TPL \(Task Parallel Library\) e PLINQ, che semplificano notevolmente la creazione di applicazioni di .NET Framework asincrone e a thread multipli.