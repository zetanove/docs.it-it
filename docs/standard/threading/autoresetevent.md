---
title: "AutoResetEvent | Microsoft Docs"
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
  - "threading [.NET Framework], AutoResetEvent class"
  - "AutoResetEvent class"
ms.assetid: 6d39c48d-6b37-4a9b-8631-f2924cfd9c18
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# AutoResetEvent
La classe <xref:System.Threading.AutoResetEvent> rappresenta un evento handle di attesa locale che viene reimpostato automaticamente quando riceve un segnale, dopo il rilascio di un singolo thread in attesa.  Questa classe rappresenta una classe speciale della relativa classe base, <xref:System.Threading.EventWaitHandle>.  Vedere la documentazione di [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md) per informazioni sull'utilizzo e le caratteristiche degli eventi di reimpostazione automatica.  
  
 L'oggetto <xref:System.Threading.AutoResetEvent> viene reimpostato automaticamente dal sistema come non segnalato dopo il rilascio di un singolo thread in attesa.  Se nessun thread è in attesa, lo stato dell'oggetto evento resta segnalato.  <xref:System.Threading.AutoResetEvent> corrisponde a una chiamata `CreateEvent` Win32, in cui si specifica `false` per l'argomento `bManualReset`.  
  
 Per un esempio che utilizza <xref:System.Threading.AutoResetEvent>, vedere [Monitor](../Topic/Monitors.md).  
  
## Vedere anche  
 <xref:System.Threading.ManualResetEvent>   
 <xref:System.Threading.Monitor>   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Wait Handles](../Topic/Wait%20Handles.md)