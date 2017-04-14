---
title: "Thread.Suspend, Garbage Collection, and Safe Points | Microsoft Docs"
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
  - "suspending threads"
  - "safe points"
  - "threading [.NET Framework], suspending"
  - "threading [.NET Framework], garbage collection"
  - "garbage collection, threads"
ms.assetid: e8f58e17-2714-4821-802a-f8eb3b2baa62
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Thread.Suspend, Garbage Collection, and Safe Points
Quando si chiama <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> su un thread, nel sistema viene rilevato che è stata richiesta una sospensione di thread, di cui viene consentita l'esecuzione fino al raggiungimento di un punto sicuro, prima di sospendere effettivamente il thread.  Per un thread un punto sicuro è un punto nell'esecuzione in corrispondenza del quale è possibile eseguire le operazioni di Garbage Collection.  
  
 Dopo avere raggiunto un punto sicuro, il runtime garantisce che il thread sospeso non effettuerà ulteriori avanzamenti nel codice gestito.  Un thread in esecuzione all'esterno del codice gestito è sempre sicuro per le operazioni di Garbage Collection e l'esecuzione continua finché non tenta di riprendere l'esecuzione del codice gestito.  
  
> [!NOTE]
>  Per effettuare un'operazione di Garbage Collection, è necessario che vengano sospesi tutti i thread ad eccezione di quello che esegue la raccolta.  Ogni thread deve essere portato a un punto sicuro prima di poter essere sospeso.  
  
## Vedere anche  
 <xref:System.Threading.Thread>   
 <xref:System.GC>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Gestione automatica della memoria](../../../docs/standard/automatic-memory-management.md)