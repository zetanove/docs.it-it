---
title: Garbage Collection | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory, garbage collection
- garbage collection, automatic memory management
- GC [.NET Framework]
- memory, allocating
- common language runtime, garbage collection
- garbage collector
- cleanup operations
- garbage collection
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- runtime, automatic memory management
- runtime, garbage collection
- garbage collection, about
ms.assetid: 22b6cb97-0c80-4eeb-a2cf-5ed7655e37f9
caps.latest.revision: 36
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 11ea4186a77a600d1645fe334ba9fd704fe728b4
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="garbage-collection"></a>Garbage Collection
Il Garbage Collector di .NET gestisce l'allocazione e il rilascio di memoria per l'applicazione. Ogni volta che si crea un nuovo oggetto, Common Language Runtime alloca memoria per l'oggetto dall'heap gestito. Lo spazio per i nuovi oggetti verrà allocato in questo modo dal runtime fino all'esaurimento dello spazio degli indirizzi nell'heap gestito. La memoria, tuttavia, non è infinita. Alla fine il Garbage Collector deve eseguire una raccolta per liberare memoria. Il modulo di ottimizzazione del Garbage Collector consente di determinare il momento migliore per l'esecuzione di una raccolta sulla base delle allocazioni in corso. Durante l'esecuzione di una raccolta, il Garbage Collector verifica la presenza di oggetti non più usati dall'applicazione nell'heap gestito ed esegue le operazioni necessarie per reclamare la relativa memoria.  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Argomenti correlati  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Principi fondamentali di Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md)|Descrive il funzionamento di Garbage Collection, la modalità di allocazione degli oggetti nell'heap gestito e altri concetti di base.|  
|[Garbage Collection e prestazioni](../../../docs/standard/garbage-collection/performance.md)|Descrive i controlli delle prestazioni è possibile usare per diagnosticare i problemi di Garbage Collection e di prestazioni.|  
|[Raccolte indotte](../../../docs/standard/garbage-collection/induced.md)|Descrive come eseguire un'operazione di Garbage Collection.|  
|[Modalità di latenza](../../../docs/standard/garbage-collection/latency.md)|Descrive i modi per determinare l'ingerenza di Garbage Collection.|  
|[Ottimizzazione per l'hosting Web condiviso](../../../docs/standard/garbage-collection/optimization-for-shared-web-hosting.md)|Descrive come ottimizzare l'operazione di Garbage Collection nei server condivisi da più siti Web di piccole dimensioni.|  
|[Notifiche di Garbage Collection](../../../docs/standard/garbage-collection/notifications.md)|Descrive come determinare quando è imminente una Garbage Collection completa e quando è stata completata.|  
|[Monitoraggio delle risorse del dominio dell'applicazione](../../../docs/standard/garbage-collection/app-domain-resource-monitoring.md)|Descrive come monitorare l'utilizzo della CPU e della memoria da un dominio dell'applicazione.|  
|[Riferimenti deboli](../../../docs/standard/garbage-collection/weak-references.md)|Descrive i riferimenti che consentono al Garbage Collector di raccogliere un oggetto, pur senza impedire all'applicazione di accedervi.|  
  
## <a name="reference"></a>Riferimento  
 <xref:System.GC?displayProperty=fullName>  
  
 <xref:System.GCCollectionMode?displayProperty=fullName>  
  
 <xref:System.GCNotificationStatus?displayProperty=fullName>  
  
 <xref:System.Runtime.GCLatencyMode?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings?displayProperty=fullName>  
  
 <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName>  
  
 <xref:System.Object.Finalize%2A?displayProperty=fullName>  
  
 <xref:System.IDisposable?displayProperty=fullName>  
  
## <a name="see-also"></a>Vedere anche  
 [Pulizia delle risorse non gestite](../../../docs/standard/garbage-collection/unmanaged.md)
