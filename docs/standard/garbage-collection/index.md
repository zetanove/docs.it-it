---
title: "Garbage Collection | Microsoft Docs"
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
  - "memory, garbage collection"
  - "garbage collection, automatic memory management"
  - "GC [.NET Framework]"
  - "memory, allocating"
  - "common language runtime, garbage collection"
  - "garbage collector"
  - "cleanup operations"
  - "garbage collection"
  - "memory, releasing"
  - "common language runtime, automatic memory management"
  - "automatic memory management"
  - "runtime, automatic memory management"
  - "runtime, garbage collection"
  - "garbage collection, about"
ms.assetid: 22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9
caps.latest.revision: 36
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 36
---
# Garbage Collection
Il Garbage Collector di .NET Framework gestisce tutte le allocazioni e i rilasci di memoria di un'applicazione.  Ogni qualvolta si crea un nuovo oggetto, Common Language Runtime alloca memoria per l'oggetto dall'heap gestito.  Finché nell'heap gestito resta spazio di indirizzamento libero, il runtime continua ad allocare memoria per i nuovi oggetti.  La memoria, però, non è infinita.  A un certo punto, è necessario che venga eseguita una Garbage Collection al fine di liberare memoria.  Il motore di ottimizzazione del Garbage Collector individua il momento migliore per effettuare la Garbage Collection in base alle allocazioni in corso.  Quando il Garbage Collector effettua una raccolta, cerca tra gli oggetti contenuti nell'heap gestito quelli non più utilizzati dall'applicazione e compie le necessarie operazioni per reclamare la memoria da essi occupata.  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Fundamentals of Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md)|Viene descritto il funzionamento di Garbage Collection, il modo in cui gli oggetti vengono allocati nell'heap gestito e altri concetti fondamentali.|  
|[Garbage Collection and Performance](../../../docs/standard/garbage-collection/performance.md)|Vengono descritti i controlli delle prestazioni che è possibile utilizzare per diagnosticare problemi di Garbage Collection e prestazioni.|  
|[Raccolte indotte](../../../docs/standard/garbage-collection/induced.md)|Viene descritto come far sì che abbia luogo un'operazione di Garbage Collection.|  
|[Latency Modes](../../../docs/standard/garbage-collection/latency.md)|Vengono descritte le modalità che determinano l'ingerenza del Garbage Collection.|  
|[Optimization for Shared Web Hosting](../../../docs/standard/garbage-collection/optimization-for-shared-web-hosting.md)|Viene descritto come ottimizzare Garbage Collection nei server condivisi da diversi siti Web di piccole dimensioni.|  
|[Garbage Collection Notifications](../../../docs/standard/garbage-collection/notifications.md)|Viene descritto come determinare quando si sta per verificare e quando è terminata un'operazione di Garbage Collection completa.|  
|[Application Domain Resource Monitoring](../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)|Viene descritto come monitorare la CPU e l'utilizzo della memoria mediante un dominio applicazione.|  
|[Weak References](../../../docs/standard/garbage-collection/weak-references.md)|Vengono descritte le funzionalità che consentono al Garbage Collector di raccogliere un oggetto, senza tuttavia impedire all'applicazione di accedervi.|  
  
## Riferimento  
 <xref:System.GC?displayProperty=fullName>  
  
 <xref:System.GCCollectionMode?displayProperty=fullName>  
  
 <xref:System.GCNotificationStatus?displayProperty=fullName>  
  
 <xref:System.Runtime.GCLatencyMode?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName>  
  
 <xref:System.Object.Finalize%2A?displayProperty=fullName>  
  
 <xref:System.IDisposable?displayProperty=fullName>  
  
## Vedere anche  
 [Cleaning Up Unmanaged Resources](../../../docs/standard/garbage-collection/unmanaged.md)