---
title: "CLR ETW Events | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "CLR ETW events"
  - "ETW, common language runtime"
  - "ETW, CLR events"
ms.assetid: ef2b31c3-7426-43e7-9924-92339b96556d
caps.latest.revision: 45
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 45
---
# CLR ETW Events
Gli argomenti presenti in questa sezione descrivono gli eventi ETW \(Event tracing for Windows\).  Ogni evento ha una parola chiave e un livello associati, descritti nell'argomento [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).  CLR dispone di due provider per gli eventi:  
  
-   Il provider di runtime, che genera eventi in base alle parole chiave \(categorie di eventi\) abilitate.  Il GUID del provider di runtime CLR è e13c0d23\-ccbc\-4e12\-931b\-d9cc2eee27e4.  
  
-   Il provider di rundown, con utilizzi finalizzati a scopi specifici.  Il GUID del provider di rundown CLR è a669021c\-c450\-4609\-a035\-5af59af4df18.  
  
 Per ulteriori informazioni sui provider, vedere [CLR ETW Providers](../../../docs/framework/performance/clr-etw-providers.md).  
  
## In questa sezione  
 [Runtime Information Events](../../../docs/framework/performance/runtime-information-etw-events.md)  
 Acquisisce informazioni sul runtime, inclusi la SKU, il numero di versione, la modalità di attivazione del runtime, i parametri della riga di comando con i quali è stato avviato, il GUID \(se applicabile\) e altre informazioni pertinenti.  
  
 [Exception Thrown\_V1 Event](../../../docs/framework/performance/exception-thrown-v1-etw-event.md)  
 Acquisisce le informazioni sulle eccezioni generate.  
  
 [Contention Events](../../../docs/framework/performance/contention-etw-events.md)  
 Acquisisce informazioni sul conflitto relativo ai blocchi di monitoraggio o ai blocchi nativi utilizzati dal runtime.  
  
 [Thread Pool Events](../../../docs/framework/performance/thread-pool-etw-events.md)  
 Acquisisce informazioni sui pool dei thread di lavoro e sui pool dei thread di I\/O.  
  
 [Loader Events](../../../docs/framework/performance/loader-etw-events.md)  
 Acquisisce informazioni sul caricamento e lo scaricamento di domini applicazione, assembly e moduli.  
  
 [Method Events](../../../docs/framework/performance/method-etw-events.md)  
 Acquisisce informazioni sui metodi CLR per la risoluzione del simbolo.  
  
 [Garbage Collection Events](../../../docs/framework/performance/garbage-collection-etw-events.md)  
 Acquisisce informazioni che riguardano la procedura di Garbage Collection, utili nella diagnostica e nel debug.  
  
 [JIT Tracing Events](../../../docs/framework/performance/jit-tracing-etw-events.md)  
 Acquisisce informazioni sull'incorporamento Just\-In\-Time \(JIT\) e sulle chiamate tail.  
  
 [Interop Events](../../../docs/framework/performance/interop-etw-events.md)  
 Acquisisce informazioni sulla generazione dello stub e la memorizzazione nella cache di Microsoft Intermediate Language \(MSIL\).  
  
 [ARM Events](../../../docs/framework/performance/application-domain-resource-monitoring-arm-etw-events.md)  
 Acquisisce informazioni diagnostiche dettagliate sullo stato di un dominio applicazione.  
  
 [Security Events](../../../docs/framework/performance/security-etw-events.md)  
 Acquisisce informazioni sul nome sicuro e la verifica Authenticode.  
  
 [Stack Event](../../../docs/framework/performance/stack-etw-event.md)  
 Acquisisce informazioni utilizzate con gli altri eventi per generare tracce dello stack dopo che è stato generato un evento.  
  
## Vedere anche  
 [Migliorare il debug e la regolazione delle prestazioni con ETW](http://go.microsoft.com/fwlink/?LinkId=179696)   
 [Blog di prestazioni di windows](http://go.microsoft.com/fwlink/?LinkId=179509)   
 [Controlling .NET Framework Logging](../../../docs/framework/performance/controlling-logging.md)   
 [CLR ETW Providers](../../../docs/framework/performance/clr-etw-providers.md)   
 [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)   
 [ETW Events in the Common Language Runtime](../../../docs/framework/performance/etw-events-in-the-common-language-runtime.md)