---
title: Threading gestito | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- threading [.NET Framework], about threading
- managed threading
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
caps.latest.revision: 19
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 3d6aa14f94b4a1537b49cda17229cd073b5d8486
ms.contentlocale: it-it
ms.lasthandoff: 05/22/2017

---
# <a name="managed-threading"></a>Threading gestito
Indipendentemente dal numero di processori usati nello sviluppo per i computer, l'applicazione dovrà offrire l'interazione più reattiva possibile con l'utente, anche se sono in corso altre attività. L'uso di più thread di esecuzione è uno dei modi più efficaci per mantenere la reattività dell'applicazione con l'utente e contemporaneamente usare il processore tra un evento utente e l'altro o persino durante gli eventi. Oltre a introdurre i concetti di base del threading, questa sezione è incentrata sui concetti di threading gestito e di uso del threading gestito.  
  
> [!NOTE]
>  A partire da [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la programmazione multithreading è notevolmente semplificata con le classi <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> e <xref:System.Threading.Tasks.Task?displayProperty=fullName>, [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md), le nuove classi di raccolta simultanee nello spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName> e un nuovo modello di programmazione che si basa sul concetto di attività anziché di thread. Per altre informazioni, vedere [Programmazione parallela](../../../docs/standard/parallel-programming/index.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Nozioni di base sul threading gestito](../../../docs/standard/threading/managed-threading-basics.md)  
 Fornisce una panoramica del threading gestito e illustra quando usare più thread.  
  
 [Utilizzo di thread e threading](../../../docs/standard/threading/using-threads-and-threading.md)  
 Illustra come creare, avviare, sospendere, riprendere e interrompere i thread.  
  
 [Suggerimenti per l'utilizzo del threading gestito](../../../docs/standard/threading/managed-threading-best-practices.md)  
 Illustra i livelli di sincronizzazione, come evitare deadlock e race condition, computer a processore singolo e multiprocessore e altri problemi di threading.  
  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md) (Oggetti e funzionalità del threading)  
 Descrive le classi gestite che è possibile usare per sincronizzare le attività dei thread e i dati di oggetti accessibili su thread differenti e fornisce una panoramica dei thread del pool.  
  
## <a name="reference"></a>Riferimento  
 <xref:System.Threading>  
 Contiene classi per l'uso e la sincronizzazione dei thread gestiti.  
  
 <xref:System.Collections.Concurrent>  
 Contiene le classi di raccolta che sono sicure per l'uso con più thread.  
  
 <xref:System.Threading.Tasks>  
 Contiene classi per la creazione e la pianificazione delle attività di elaborazione simultanee.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Domini dell'applicazione](../../../docs/framework/app-domains/application-domains.md)  
 Fornisce una panoramica dei domini dell'applicazione e del loro uso da parte di Common Language Runtime.  
  
 [I/O di file asincrono](../../../docs/standard/io/asynchronous-file-i-o.md)  
 Vengono descritti il funzionamento di base dell'I/O asincrono e i relativi vantaggi in termini di prestazioni.  
  
 [Event-based Asynchronous Pattern (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md) (Modello asincrono basato su eventi)  
 Fornisce una descrizione generale della programmazione asincrona.  
  
 [Chiamata sincrona dei metodi asincroni](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 Illustra come chiamare metodi sul thread del pool usando le funzionalità predefinite dei delegati.  
  
 [Programmazione parallela](../../../docs/standard/parallel-programming/index.md)  
 Descrive le librerie per la programmazione parallela, che semplificano l'uso di più thread nelle applicazioni.  
  
 [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)  
 Descrive un sistema per l'esecuzione di query in parallelo, in modo da sfruttare più processori.
