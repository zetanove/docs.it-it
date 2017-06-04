---
title: "How to: Enable Thread-Tracking Mode in SpinLock | Microsoft Docs"
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
  - "SpinLock, how to enable thread-tracking"
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Enable Thread-Tracking Mode in SpinLock
<xref:System.Threading.SpinLock?displayProperty=fullName> è un blocco a esclusione reciproca di basso livello utilizzabile per scenari con tempi di attesa molto brevi.  <xref:System.Threading.SpinLock> non è rientrante.  Una volta che un thread accede al blocco, deve uscirne correttamente prima di potervi accedere nuovamente.  In genere, qualsiasi tentativo di riaccedere al blocco causerebbe un deadlock, e il debug dei deadlock può risultare molto difficile.  Per facilitare lo sviluppo, <xref:System.Threading.SpinLock?displayProperty=fullName> supporta una modalità di rilevamento thread che fa in modo che venga generata un'eccezione quando un thread tenta di riaccedere a un blocco già contenuto.  Ciò consente di individuare più facilmente il punto in cui l'uscita dal blocco non è avvenuta correttamente.  La modalità di rilevamento thread può essere attivata utilizzando il costruttore <xref:System.Threading.SpinLock> che accetta un parametro di input booleano e passando un argomento `true`.  Una volta completate le fasi di sviluppo e di test, disattivare la modalità di rilevamento thread per ottenere prestazioni migliori.  
  
## Esempio  
 Nell'esempio seguente viene illustrata la modalità di rilevamento thread.  Le righe che escono correttamente dal blocco vengono impostate come commento per simulare un errore di codifica che provoca uno dei seguenti risultati:  
  
-   Se <xref:System.Threading.SpinLock> è stato creato utilizzando un argomento `true` \(`True` in Visual Basic\), viene generata un'eccezione.  
  
-   Un deadlock se <xref:System.Threading.SpinLock> è stato creato utilizzando un argomento `false` \(`False` in Visual Basic\).  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## Vedere anche  
 [SpinLock](../../../docs/standard/threading/spinlock.md)