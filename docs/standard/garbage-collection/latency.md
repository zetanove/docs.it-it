---
title: "Latency Modes | Microsoft Docs"
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
  - "garbage collection, intrusiveness"
  - "garbage collection, latency modes"
ms.assetid: 96278bb7-6eab-4612-8594-ceebfc887d81
caps.latest.revision: 41
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 41
---
# Latency Modes
Per recuperare oggetti, tramite il Garbage Collector devono essere arrestati tutti i thread in esecuzione in un'applicazione.   In alcune situazioni, ad esempio quando un'applicazione recupera dati o visualizza contenuto, un'operazione completa di Garbage Collection può verificarsi in un momento critico e può ostacolare le prestazioni.  È possibile rettificare l'ingerenza del Garbage Collector impostando la proprietà <xref:System.Runtime.GCSettings.LatencyMode%2A?displayProperty=fullName> su uno dei valori <xref:System.Runtime.GCLatencyMode?displayProperty=fullName>.  
  
 La latenza si riferisce al momento dell'intrusione del Garbage Collector nell'applicazione.  Durante i periodi di bassa latenza, il Garbage Collector è più conservativo e meno intrusivo nel recupero degli oggetti.  Tramite l'enumerazione <xref:System.Runtime.GCLatencyMode?displayProperty=fullName> vengono fornite due impostazioni a bassa latenza:  
  
-   Tramite il campo <xref:System.Runtime.GCLatencyMode> vengono eliminate le raccolte di generazione 2 ed eseguite solo le raccolte di generazione 0 e 1.  Può essere usato solo per brevi periodi di tempo.  In caso di lunghi periodi, se viene usata una quantità elevata di memoria, tramite il Garbage Collector verrà attivata una raccolta mediante la quale è possibile mettere in pausa brevemente l'applicazione e interrompere un'operazione critica rispetto al tempo.  Questa impostazione è disponibile solo per le operazioni di Garbage Collection per workstation.  
  
-   Tramite il campo <xref:System.Runtime.GCLatencyMode> vengono eliminate le raccolte di generazione 2 in primo piano ed eseguite solo le raccolte di generazione 0, 1 e di generazione 2 in background.  Può essere usato per periodi di tempo più lunghi ed è disponibile per le operazioni di Garbage Collection per workstation e per server.  Questa impostazione non può essere usata se l'operazione di [Garbage Collection in modalità simultanea](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) è disabilitata.  
  
 Durante i periodi di bassa latenza, le raccolte di generazione 2 vengono soppresse eccetto nei seguenti casi:  
  
-   Il sistema riceve una notifica di memoria insufficiente dal sistema operativo.  
  
-   Il codice dell'applicazione induce una raccolta chiamando il metodo <xref:System.GC.Collect%2A?displayProperty=fullName> e specificando 2 per il parametro `generation`.  
  
 Nella tabella seguente sono elencati gli scenari di applicazioni per usare i valori <xref:System.Runtime.GCLatencyMode>.  
  
|Modalità di latenza|Scenari di applicazione|  
|-------------------------|-----------------------------|  
|<xref:System.Runtime.GCLatencyMode>|Per applicazioni che non hanno nessuna interfaccia utente o operazioni lato server.<br /><br /> Si tratta della modalità predefinita quando l'operazione di [Garbage Collection in modalità simultanea](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) è disabilitata.|  
|<xref:System.Runtime.GCLatencyMode>|Per la maggior parte delle applicazioni che hanno una interfaccia utente.<br /><br /> Si tratta della modalità predefinita quando l'operazione di [Garbage Collection in modalità simultanea](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) è abilitata.|  
|<xref:System.Runtime.GCLatencyMode>|Per le applicazioni con operazioni a breve termine, per cui il tempo riveste un'importanza significativa, durante le quali le interruzioni del Garbage Collector potrebbero rivelarsi dannose.  Ad esempio, applicazioni di rendering delle animazioni o che hanno funzioni di acquisizione dei dati.|  
|<xref:System.Runtime.GCLatencyMode>|Per le applicazioni con operazioni per cui i tempi sono importanti per una durata contenuta, ma potenzialmente lunga, durante la quale le interruzioni del Garbage Collector potrebbero rivelarsi dannose.  Ad esempio, le applicazioni per cui sono richiesti tempi di risposta rapidi come i cambiamenti dei dati di mercato durante le ore di negoziazione.<br /><br /> Questa modalità comporta dimensioni dell'heap gestito maggiori rispetto ad altre.  Poiché non consente di comprimere l'heap gestito, è possibile avere una maggiore frammentazione.  Assicurarsi che sia disponibile memoria sufficiente.|  
  
## Linee guida per l'uso della bassa latenza  
 Quando si usa la modalità <xref:System.Runtime.GCLatencyMode>, tenere in considerazione le seguenti linee guida:  
  
-   Mantenere il periodo di tempo in bassa latenza più brevemente possibile.  
  
-   Evitare di allocare quantità di memoria elevate durante i periodi di bassa latenza.  Possono verificarsi notifiche di memoria insufficiente perché le operazioni di Garbage Collection recuperano meno oggetti.  
  
-   In modalità di bassa latenza, ridurre al minimo il numero delle allocazioni effettuate, in particolare le allocazioni su Large Object Heap e oggetti bloccati.  
  
-   Tenere presenti i thread che potrebbero essere in corso di allocazione.  Poiché l'impostazione delle proprietà <xref:System.Runtime.GCSettings.LatencyMode%2A> interessa l'intero processo, è possibile generare un'eccezione <xref:System.OutOfMemoryException> su qualsiasi thread eventualmente in corso di allocazione.  
  
-   Eseguire il wrapping del codice di bassa latenza nelle aree a esecuzione vincolata \(per altre informazioni, vedere [Constrained Execution Regions](../../../docs/framework/performance/constrained-execution-regions.md)\).  
  
-   È possibile forzare le operazioni di Garbage Collection di generazione 2 durante un periodo di bassa latenza chiamando il metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%29?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.GC?displayProperty=fullName>   
 [Raccolte indotte](../../../docs/standard/garbage-collection/induced.md)   
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)