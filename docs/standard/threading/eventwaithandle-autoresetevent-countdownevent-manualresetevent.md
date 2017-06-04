---
title: "EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent | Microsoft Docs"
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
  - "wait handles"
  - "threading [.NET Framework], EventWaitHandle class"
  - "event wait handles [.NET Framework]"
ms.assetid: cd94fc34-ac15-427f-b723-a1240a4fab7d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent
Gli handle di attesa degli eventi consentono ai thread di sincronizzare le attività inviandosi segnali reciprocamente e rimanendo ciascuno in attesa dei segnali di un altro.  Questi eventi di sincronizzazione sono basati sugli handle di attesa Win32 e possono essere suddivisi in due tipi: quelli che vengono reimpostati automaticamente alla ricezione di un segnale e quelli che devono essere reimpostati manualmente.  
  
 Gli handle di attesa degli eventi sono utili in molti degli stessi scenari di sincronizzazione della classe <xref:System.Threading.Monitor>.  In genere, risultano più facili da utilizzare rispetto ai metodi <xref:System.Threading.Monitor.Wait%2A?displayProperty=fullName> e <xref:System.Threading.Monitor.Pulse%2A?displayProperty=fullName> e forniscono un controllo più efficiente della segnalazione.  Mentre i monitor sono locali al dominio applicazione, gli handle di attesa degli eventi possono essere anche utilizzati per sincronizzare le attività in più domini applicazioni o processi.  
  
## In questa sezione  
 [EventWaitHandle](../../../docs/standard/threading/eventwaithandle.md)  
 La classe <xref:System.Threading.EventWaitHandle> può rappresentare eventi di reimpostazione automatica o manuale, nonché eventi locali o eventi di sistema denominati.  
  
 [AutoResetEvent](../../../docs/standard/threading/autoresetevent.md)  
 La classe <xref:System.Threading.AutoResetEvent> deriva da <xref:System.Threading.EventWaitHandle> e rappresenta un evento locale che viene reimpostato automaticamente.  
  
 [ManualResetEvent and ManualResetEventSlim](../../../docs/standard/threading/manualresetevent-and-manualreseteventslim.md)  
 La classe <xref:System.Threading.ManualResetEvent> deriva da <xref:System.Threading.EventWaitHandle> e rappresenta un evento locale che deve essere reimpostato manualmente.  La classe <xref:System.Threading.ManualResetEventSlim> è una versione leggera e più veloce che è possibile utilizzare per gli eventi all'interno dello stesso processo.  
  
 [CountdownEvent](../../../docs/standard/threading/countdownevent.md)  
 La classe <xref:System.Threading.CountdownEvent> offre un metodo semplificato per implementare modelli di parallelismo di biforcazione e unione nel codice in cui vengono utilizzati handle di attesa.  
  
## Sezioni correlate  
 [Wait Handles](../Topic/Wait%20Handles.md)  
 La classe <xref:System.Threading.WaitHandle> è la classe di base per le classi <xref:System.Threading.EventWaitHandle>, <xref:System.Threading.Semaphore> e <xref:System.Threading.Mutex>.  Contiene metodi statici quali <xref:System.Threading.WaitHandle.SignalAndWait%2A> e <xref:System.Threading.WaitHandle.WaitAll%2A>, utili quando vengono utilizzati tutti i tipi di handle di attesa.  
  
## Vedere anche  
 <xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading.WaitHandle>   
 <xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [Managed Threading Basics](../../../docs/standard/threading/managed-threading-basics.md)