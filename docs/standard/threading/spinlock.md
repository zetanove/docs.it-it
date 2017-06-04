---
title: "SpinLock | Microsoft Docs"
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
  - "synchronization primitives, SpinLock"
ms.assetid: f9af93bb-7a0d-4ba5-afe8-74f48b6b6958
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# SpinLock
La struttura <xref:System.Threading.SpinLock> è una primitiva di sincronizzazione di basso livello a esclusione reciproca che ruota in attesa di acquisire un blocco.  Nei computer multicore, quando si prevedono tempi di attesa brevi e il conflitto è minimo, <xref:System.Threading.SpinLock> può risultare più efficace di altri tipi di blocchi.  È tuttavia consigliabile utilizzare <xref:System.Threading.SpinLock> soltanto quando si stabilisce, mediante profilatura, che il metodo <xref:System.Threading.Monitor?displayProperty=fullName> o i metodi <xref:System.Threading.Interlocked> rallentano in maniera significativa le prestazioni del programma.  
  
 <xref:System.Threading.SpinLock> può produrre la porzione di tempo del thread anche se non ha ancora acquisito il blocco.  Ciò serve a evitare un'inversione di priorità del thread e a consentire l'avanzamento del Garbage Collector.  Quando si utilizza un oggetto <xref:System.Threading.SpinLock>, assicurarsi che nessun thread possa contenere il blocco se non per un intervallo di tempo brevissimo e che nessun thread possa bloccarsi mentre contiene il blocco.  
  
 Poiché SpinLock è un tipo di valore, è necessario passarlo in modo esplicito per riferimento se si desidera che le due copie facciano riferimento allo stesso blocco.  
  
 Per ulteriori informazioni sull'utilizzo di questo tipo, vedere <xref:System.Threading.SpinLock?displayProperty=fullName>.  Per un esempio, vedere [How to: Use SpinLock for Low\-Level Synchronization](../../../docs/standard/threading/how-to-use-spinlock-for-low-level-synchronization.md).  
  
 <xref:System.Threading.SpinLock> supporta una modalità di *rilevamento* dei *thread* che è possibile utilizzare durante la fase di sviluppo per facilitare il rilevamento del thread che contiene il blocco in un momento specifico.  La modalità di rilevamento dei thread è molto utile per l'esecuzione del debug, ma si consiglia di disattivarla nella versione finale del programma in quanto potrebbe rallentarne le prestazioni.  Per ulteriori informazioni, vedere [How to: Enable Thread\-Tracking Mode in SpinLock](../../../docs/standard/threading/how-to-enable-thread-tracking-mode-in-spinlock.md).  
  
## Vedere anche  
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)