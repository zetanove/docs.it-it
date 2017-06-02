---
title: "ManualResetEvent and ManualResetEventSlim | Microsoft Docs"
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
  - "threading [.NET Framework], ManualResetEvent class"
  - "ManualResetEvent class, about ManualResetEvent class"
ms.assetid: 465fdcf9-ba24-4d8d-a43f-d983b7cb0cc6
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# ManualResetEvent and ManualResetEventSlim
La classe <xref:System.Threading.ManualResetEvent?displayProperty=fullName> rappresenta un evento di handle di attesa locale che deve essere reimpostato manualmente dopo che è stato segnalato.  Questa classe rappresenta un caso speciale della relativa classe base, <xref:System.Threading.EventWaitHandle?displayProperty=fullName>.  Per informazioni sull'utilizzo e sulle funzionalità degli eventi di reimpostazione manuale, vedere la documentazione relativa a [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md).  
  
 Un oggetto <xref:System.Threading.ManualResetEvent> rimane segnalato finché non viene chiamato il relativo metodo <xref:System.Threading.EventWaitHandle.Reset%2A?displayProperty=fullName>.  È possibile rilasciare qualsiasi numero di thread in attesa, o thread che attendono l'evento dopo che è stato segnalato, mentre lo stato dell'oggetto è segnalato.  <xref:System.Threading.ManualResetEvent> corrisponde a una chiamata `CreateEvent` Win32, in cui si specifica `true` per l'argomento `bManualReset`.  
  
 In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], è possibile utilizzare la classe <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName> per ottenere prestazioni migliori rispetto a quando si prevedono tempi di attesa molto brevi e quando l'evento non supera un limite di processo.  <xref:System.Threading.ManualResetEventSlim> utilizza l'attesa attiva per un breve periodo mentre attende che l'evento venga segnalato.  Quando i tempi di attesa sono brevi, lo spin può risultare molto meno oneroso dell'attesa tramite handle di attesa.  Tuttavia, se l'evento non viene segnalato entro un certo periodo di tempo, <xref:System.Threading.ManualResetEventSlim> ricorre a una normale attesa dell'handle dell'evento.  
  
## Vedere anche  
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)   
 [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)   
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [Semaphore and SemaphoreSlim](../../../docs/standard/threading/semaphore-and-semaphoreslim.md)