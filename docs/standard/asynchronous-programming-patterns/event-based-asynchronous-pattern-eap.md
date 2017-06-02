---
title: "Event-based Asynchronous Pattern (EAP) | Microsoft Docs"
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
  - "asynchronous calls"
  - "asynchronous programming, design patterns"
  - "asynchronous programming"
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# Event-based Asynchronous Pattern (EAP)
È possibile esporre funzionalità asincrone al codice client in molti modi.  Il modello asincrono basato su eventi determina l'unico modo per la presentazione del comportamento asincrono da parte delle classi.  
  
> [!NOTE]
>  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Task Parallel Library fornisce un nuovo modello di programmazione asincrona e parallela.  Per altre informazioni, vedere [Parallel Programming](../../../docs/standard/parallel-programming/index.md).  
  
## In questa sezione  
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 Descrive il modo in cui il modello asincrono basato su eventi rende disponibili i vantaggi delle applicazioni multithread, nascondendo al tempo stesso molti dei problemi complessi correlati alla progettazione multithread.  
  
 [Implementing the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)  
 Descrive il modo standardizzato di creare un pacchetto di una classe con funzionalità asincrone.  
  
 [Suggerimenti per l'implementazione del modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 Descrive i requisiti per l'esposizione di funzionalità asincrone in base al modello asincrono basato su eventi.  
  
 [Deciding When to Implement the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 Descrive come determinare quando occorre scegliere di implementare il modello asincrono basato su eventi invece del modello <xref:System.IAsyncResult>.  
  
 [Walkthrough: Implementing a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)  
 Illustra come creare un componente che implementa un modello asincrono basato su eventi.  L'implementazione è eseguita mediante classi di helper dallo spazio dei nomi <xref:System.ComponentModel?displayProperty=fullName>, in modo da assicurare che il componente funzioni correttamente con qualsiasi modello di applicazione.  
  
 [How to: Use Components That Support the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 Descrive come usare un componente che supporta il modello asincrono basato su eventi.  
  
## Riferimenti  
 <xref:System.ComponentModel.AsyncOperation>  
 Descrive la classe <xref:System.ComponentModel.AsyncOperation> e include collegamenti a tutti i membri corrispondenti.  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 Descrive la classe <xref:System.ComponentModel.AsyncOperationManager> e include collegamenti a tutti i membri corrispondenti.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 Descrive il componente <xref:System.ComponentModel.BackgroundWorker> e include collegamenti a tutti i membri corrispondenti.  
  
## Sezioni correlate  
 [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)  
 Descrive un modello di programmazione delle operazioni asincrone e parallele.  
  
 [Threading](../../../docs/standard/threading/index.md)  
 Descrive le funzionalità di multithreading nel.NET Framework.  
  
 [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)  
 Descrive le funzionalità di multithreading nei linguaggi C\# e Visual Basic.  
  
## Vedere anche  
 [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md)   
 [Eventi](../../../docs/standard/events/index.md)   
 [Multithreading in Components](../Topic/Multithreading%20in%20Components.md)   
 [Asynchronous Programming Design Patterns](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)