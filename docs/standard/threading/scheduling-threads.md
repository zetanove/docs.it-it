---
title: "Scheduling Threads | Microsoft Docs"
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
  - "threading [.NET Framework], scheduling"
  - "scheduling threads"
ms.assetid: 67e4a0eb-3095-4ea7-b20f-908faa476277
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# Scheduling Threads
Ad ogni thread è assegnata una priorità.  Ai thread creati all'interno di Common Language Runtime viene inizialmente assegnata la priorità **ThreadPriority.Normal**.  Quelli creati all'esterno del runtime mantengono la priorità che avevano prima di entrare nell'ambiente gestito.  È possibile ottenere o impostare la priorità di qualsiasi thread con la proprietà **Thread.Priority** .  
  
 La pianificazione dell'esecuzione dei thread viene stabilita in base alle relative priorità.  Sebbene i thread siano in esecuzione all'interno dell'ambiente di esecuzione, a tutti vengono assegnate porzioni del tempo del processore da parte del sistema operativo.  I dettagli dell'algoritmo di pianificazione utilizzato per determinare l'ordine in cui i thread vengono eseguiti varia in base al sistema operativo.  In alcuni, infatti, viene sempre pianificata per prima l'esecuzione del thread con la priorità più alta, tra quelli di cui è possibile l'esecuzione  Se più thread con la stessa priorità sono tutti disponibili, l'utilità di pianificazione scorre in ciclo i thread a quella priorità, assegnando a ciascuno di essi una porzione di tempo fissa in cui effettuare l'esecuzione.  Se un thread con una priorità più alta è disponibile, non verranno eseguiti i thread a priorità più bassa.  Quando non sono più disponibili thread eseguibili a una determinata priorità, l'utilità di pianificazione passa alla priorità più bassa successiva e pianifica l'esecuzione dei thread che hanno quella priorità.  Se diventa eseguibile un thread a priorità più alta, il thread a priorità più bassa viene interrotto e viene nuovamente consentita l'esecuzione del primo.  Nel sistema operativo possono inoltre essere regolate dinamicamente le priorità del thread man mano che l'interfaccia utente di un'applicazione viene spostata tra il primo piano e il background.  In altri sistemi operativi è possibile che si opti per l'utilizzo di un algoritmo di pianificazione differente.  
  
## Vedere anche  
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)   
 [Managed and Unmanaged Threading in Windows](../../../docs/standard/threading/managed-and-unmanaged-threading-in-windows.md)