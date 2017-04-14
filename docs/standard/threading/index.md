---
title: "Managed Threading | Microsoft Docs"
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
  - "threading [.NET Framework], about threading"
  - "managed threading"
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Managed Threading
Generalmente l'obiettivo del programmatore è di sviluppare applicazioni in grado di garantire tempi di risposta veloci anche se sono in esecuzione altre attività, in computer con uno o più processori.  L'utilizzo di più thread di esecuzione è uno dei metodi più efficaci per raggiungere questo risultato e per fare uso al tempo stesso del processore tra un evento e l'altro o persino durante gli eventi.  Introducendo i concetti di base del threading, in questa sezione verrà trattato in particolar modo il threading gestito e ne verrà descritto l'utilizzo.  
  
> [!NOTE]
>  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la programmazione multithreading viene semplificata notevolmente con le classi <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> e <xref:System.Threading.Tasks.Task?displayProperty=fullName>, [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md), le nuove classi Collection simultanee nello spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName> e un nuovo modello di programmazione basato sul concetto di attività anziché di thread.  Per ulteriori informazioni, vedere [Parallel Programming](../../../docs/standard/parallel-programming/index.md).  
  
## In questa sezione  
 [Managed Threading Basics](../../../docs/standard/threading/managed-threading-basics.md)  
 Vengono forniti i cenni preliminari sul threading gestito e le indicazioni per stabilire quando utilizzare più thread.  
  
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)  
 Vengono illustrati la creazione, l'avvio, la sospensione, la ripresa e l'interruzione dei thread.  
  
 [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md)  
 Vengono illustrati i livelli di sincronizzazione, come evitare deadlock e race condition, i computer a processore unico e a più processori e altri problemi relativi al threading.  
  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)  
 Vengono descritte le classi gestite che è possibile utilizzare per sincronizzare le attività dei thread e i dati degli oggetti a cui si accede in thread diversi e viene fornita una panoramica sui thread dei pool di thread.  
  
## Riferimenti  
 <xref:System.Threading>  
 Vengono fornite le classi che consentono di utilizzare e sincronizzare i thread gestiti.  
  
 <xref:System.Collections.Concurrent>  
 Contiene classi Collection che è possibile utilizzare con più thread.  
  
 <xref:System.Threading.Tasks>  
 Contiene classi per la creazione e la pianificazione di attività di elaborazione simultanee.  
  
## Sezioni correlate  
 [Domini applicazione](../../../docs/framework/app-domains/application-domains.md)  
 Viene fornita una descrizione dei domini dell'applicazione e dell'uso da parte di Common Language Infrastructure.  
  
 [I\/O di file asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md)  
 Vengono descritti il funzionamento di base dell'I\/O asincrono e i relativi vantaggi in termini di prestazioni.  
  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 Viene fornita una descrizione generale della programmazione asincrona.  
  
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 Viene illustrato come chiamare i metodi sui thread di un pool utilizzando le funzionalità incorporate dei delegati.  
  
 [Parallel Programming](../../../docs/standard/parallel-programming/index.md)  
 Vengono descritte le librerie per la programmazione parallela, che semplificano l'utilizzo di più thread nelle applicazioni.  
  
 [Parallel LINQ \(PLINQ\)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)  
 Viene descritto un sistema per l'esecuzione di query in parallelo, per sfruttare più processori.